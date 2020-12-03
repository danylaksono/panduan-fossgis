# Basisdata Spasial dengan PostGIS
Pada bagian ini akan dibahas mengenai bagaimana menggunakan PostGIS untuk melakukan analisis spasial sederhana. QGIS akan digunakan sebagai antarmuka utama untuk melakukan koneksi pada PostGIS dan menampilkan hasil analisis.

```{admonition} Catatan
Latihan ini akan menggunakan QGIS, sehingga terlebih dahulu lakukan instalasi QGIS.
Data latihan dapat diperoleh dari link berikut:

https://github.com/danylaksono/sleman-dataset/

Gunakan Github untuk melakukan clone atau unduh seluruh data sebagai zip
```


## [Pengantar PostGIS](https://postgis.net/workshops/postgis-intro/introduction.html)
Dalam implementasi GIS **generasi pertama**, semua data spasial disimpan dalam file datar dan perangkat lunak GIS khusus diperlukan untuk menafsirkan dan memanipulasi data. Sistem pengelolaan generasi pertama ini dirancang untuk memenuhi kebutuhan pengguna yang semua data yang diperlukan berada dalam domain organisasi pengguna. Mereka adalah sistem berpemilik dan mandiri yang secara khusus dibangun untuk menangani data spasial.

Sistem spasial **generasi kedua** menyimpan beberapa data dalam database relasional (biasanya "atribut" atau bagian non-spasial) tetapi masih kekurangan fleksibilitas yang diberikan dengan integrasi langsung.

*"Database spasial sejati lahir ketika orang mulai memperlakukan fitur spasial sebagai objek database kelas satu."*

Database spasial sepenuhnya mengintegrasikan data spasial dengan database relasional objek. Orientasi berubah dari GIS-centric menjadi database-centric.


![](img/2020-12-03-07-15-37.png)

Untuk memanipulasi data selama kueri, database biasa menyediakan fungsi seperti menggabungkan string, melakukan operasi hash pada string, melakukan matematika pada angka, dan mengekstraksi informasi dari tanggal. Database spasial menyediakan satu set lengkap fungsi untuk menganalisis komponen geometris, menentukan hubungan spasial, dan memanipulasi geometri. Fungsi spasial ini berfungsi sebagai blok bangunan untuk setiap proyek tata ruang.

Mayoritas dari semua fungsi spasial dapat dikelompokkan ke dalam salah satu dari lima kategori berikut:

* **Konversi**: Fungsi yang mengonversi antara geometri dan format data eksternal.
* **Manajemen**: Fungsi yang mengatur informasi tentang tabel spasial dan administrasi PostGIS.
* **Retrieval**: F  ungsi yang mengambil properti dan pengukuran Geometri.
* **Perbandingan**: Fungsi yang membandingkan dua geometri sehubungan dengan hubungan spasialnya.
* **Pembuatan data**: Fungsi yang menghasilkan geometri baru dari orang lain.
Daftar fungsi yang mungkin sangat besar, tetapi sekumpulan fungsi umum ditentukan oleh OGC SFSQL dan diimplementasikan (bersama dengan fungsi tambahan yang berguna) oleh PostGIS.

## Menggunakan QGIS sebagai antarmuka PostGIS
QGIS barangkali merupakan perangkat lunak GIS OpenSource yang paling terkenal. QGIS memiliki berbagai dukungan format data spasial, termasuk untuk koneksi terhadap basisdata PostGIS. Pada latihan ini akan digunakan QGIS untuk melakukan koneksi pada basisdata.


### Memasukkan Data pada PostGIS
Berikut adalah data yang tersedia pada link yang disebutkan di atas:
Data vector yang digunakan berupa data di daerah Kabupaten Sleman, antara lain:
    o	Data jaringan jalan (line)
    o	Data jaringan sungai (line)
    o	Data bangunan (polygon)
    o	Data titik-titik penting (point)
    o	Data batas administrasi (polygon)
    o	Data penggunaan lahan (multipolygon)
    o	Data Kawasan Rawan Bencana (KRB) BNPB 2010 (polygon)
Data berupa raster terdiri atas:
    o	Raster populasi penduduk Indonesia dengan resolusi 100 meter yang diambil dari www.worldpop.org.uk 
    o	Raster SRTM dengan resolusi 30 meter.

Untuk data vektor, kita akan gunakan QGIS untuk memasukkan data pada PostGIS:
![](img/2020-12-03-12-57-00.png)

Adapun untuk data raster, terlebih dahulu perlu mengakses mesin Docker dengan mengcopikan data pada root mesin tersebut, sebagai berikut:

```bash
docker exec -it postgrest_tut bash -c "apt-get update && apt-get install postgis"
docker cp dem.tif postgis:/
```

kemudian, gunakan raster2pgsql untuk mengkonversi raster menjadi sql:
```bash
docker exec -it postgrest_tut bash -c 'raster2pgsql -s 32749 -I -C -M dem.tif -F -t 100x100 public.rstdem  | psql -U postgres -d postgres'
```

### Latihan: Query Spasial pada data vektor

Berikut adalah beberapa latihan yang dapat dilakukan menggunakan QGIS dan PostGIS:

* Mencari titik-titik penting (POI) yang berada pada kawasan rawan bencana:
    ```sql
    select poi.id_0, poi.geom
    from poi, krb
    where  st_within(poi.geom,krb.geom) = True
    ```

    hasilnya,

    ![](img/2020-12-03-13-06-55.png)


* Buffer jalan utama sejauh 100 meter

    ```sql
    select id, name, st_buffer(geom, 100) from jalan
    where type = 'primary'
    ```

* Menampilkan jumlah bangunan pendidikan di berbah
    ```sql
    select count(id_0) as jumlah
    from poi
    where st_within(poi.geom, (
    select geom
    from kecamatan
    where kec = 'Berbah')) and fungsi = 'Pendidikan'
    ```

* Total Panjang Jalan utama di Kecamatan Berbah

    ```sql
    select sum(st_length(jalan.geom)) as total
    from jalan, kecamatan
    where jalan.type = 'primary' and st_intersects(jalan.geom,
    (select geom from kecamatan where kec = 'Berbah'))
    ```

 
* Mencari jalan yang berjarak 5 kilometer dari STIE YKPN
    ```sql
    select jalan.id, jalan.name, jalan.type 
    from jalan, poi 
    where ST_DWithin(poi.geom, jalan.geom, 5000)
    and poi.nama = 'STIE YKPN'
    ```

 
* Mencari kecamatan paling luas di Kabupaten Sleman
    ```sql
    select kec, st_area(geom) as luas
    from kecamatan 
    where st_area(geom) in 
    (
    select max(st_area(geom)) 
    from kecamatan 
    )
    ```

 
* Menampilkan ruas jalan terpanjang di Kecamatan Berbah

    ```sql
    select name, st_length(geom) as panjang
    from jalan 
    where st_length(geom) in 
    (
    select max(st_length(jalan.geom)) 
    from jalan, kecamatan 
    where st_intersects(jalan.geom, kecamatan.geom) and kec='Berbah' 
    )
    ```
    ![](img/2020-12-03-13-04-59.png)
 

* Mencari kecamatan yang dilewati oleh Jalan Kabupaten
    ```sql
    select kec 
    from kecamatan, jalan 
    where st_intersects(jalan.geom,kecamatan.geom)
    and jalan.geom in (select geom 
    from jalan 
    where name='Jln. Kabupaten')
    ```
    ![](img/2020-12-03-13-04-38.png)

* Mencari luas Hutan 
    ```sql
    select st_area(geom) as luas from gunalahan 
    where guna_lahan='HUTAN'
    ```
    ![](img/2020-12-03-13-04-23.png)
 

* Mencari jumlah bangunan di area KRB III 
    ```sql
    select st_area(geom) as luas from krb 
    where id = '3'
    ```
    ![](img/2020-12-03-13-04-11.png)
 
Untuk latihan lanjutan, coba lakukan Query berikut:
* Menampilkan jumlah titik penting yang berada di kecamatan Berbah
* Menampilkan Bangunan dengan luas lebih dari 1500 m2
* Menampilkan keliling Kecamatan Cangkringan
* Menampilkan panjang jalan kaliurang
* Menampilkan panjang total semua sungai


### Latihan: Query Spasial pada Raster
Berikut contoh analisis raster dengan PostGIS:

* Membuat tingkat kepadatan penduduk pada kecamatan Berbah
```sql
CREATE TABLE klasifikasi (rid SERIAL primary key, rast raster);
INSERT INTO klasifikasi (rast) 
with Berbah as
	 (Select geom from kecamatan where kec='Berbah'),
         klip as
	 (Select ST_Clip(rast, 1, geom, true) as rast from rstdem, berbah where st_intersects(geom,rast))
select st_reclass(rast, 1, '0-50:1, 51-100:2, 101-150:3, 151-200:4', '4BUI', 0) from klip;
SELECT AddRasterConstraints('klasifikasi'::name, 'rast'::name);
```
![](img/2020-12-03-13-11-23.png)

* Rencana Lokasi perumahan di Kecamatan Kalasan
Dibuat kondisi sebagai berikut:
-	Penggunaan lahan berupa sawah irigasi atau tegalan
-	Berada pada daerah Kecamatan Kalasan
-	Kemiringan lereng tidak lebih dari 0.1 radian
Dibuat query sebagai berikut:
```sql
CREATE TABLE perumahan (rid SERIAL primary key, rast raster);
INSERT INTO perumahan(rast)

with kalasan as
		(select geom from kecamatan where kec='Kalasan'),
	sawah as
		(select geom from gunalahan where guna_lahan='SAWAH IRIGASI' or guna_lahan='TEGALAN'),
	potong1 as
		(select  ST_Clip(rast, 1, geom, true) as rast from rstdem, kalasan where st_intersects(geom,rast)),
	lereng as
		(select ST_Slope(rast, 1, '32BF') as rast from potong1),
	kelas_lereng as
		(select st_reclass(rast, 1, '0-0.09:1', '4BUI', 0) as rast from lereng)
	
SELECT  ST_Clip(rast, 1, geom, true) from kelas_lereng, sawah where st_intersects(geom,rast);
	
SELECT AddRasterConstraints('perumahan'::name, 'rast'::name);	

```

hasilnya:

![](img/2020-12-03-13-12-33.png)

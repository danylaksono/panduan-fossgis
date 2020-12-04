# Publikasi Data Spasial dengan Geoserver

Web Map Server merupakan program komputer yang menghasilkan peta data yang direferensikan secara spasial dari
data dan informasi geografis. Aplikasi ini, sebagaimana dibahas sebelumnya, adalah antarmuka sederhana yang menyajikan data dalam format standar untuk ditampilkan pada aplikasi berbasis web. Berbagai protokol melibatkan sintaks kueri untuk memposting meminta layer yang diinginkan dan memperbesar jendela ke server, yang menghasilkan peta sebagai image dalam format standar (GIF, PNG atau format lain) atau sebagai format vektor (misalnya KML, GML). Data ini kemudian dapat dikonsumsi oleh berbagai client. Pada bagian ini akan dibahas mengenai bagaimana melakukan publikasi data spasial dengan Geoserver.

## Menghubungkan Geoserver dengan Data
Geoserver mengenali berbagai jenis data spasial. Adapun urutan untuk melakukan publikasi data pada Geoserver adalah sebagai berikut:
1. Membuat Workspace
2. Menambahkan Data Store
3. Menambahkan Layer pada Data Store
4. Mengatur Simbologi (opsional)
5. Mengatur Publikasi

Langkah tersebut dapat diikuti pada antarmuka Geoserver berikut:
![](img/2020-12-04-08-57-51.png)

Berikut adalah daftar datastore yang didukung oleh Geoserver:
![](img/2020-12-04-08-55-02.png)

### Mengunggah Shapefile
Geoserver membaca data yang disimpan pada Environment variable `GEOSERVER_DATA_DIR`, sehingga untuk melakukan ini, kita perlu mengcopy shapefile yang akan diunggah ke dalam folder tersebut. Lokasi folder ini dapat dilihat pada bagian data directory di server status:

![](img/2020-12-04-08-53-02.png)

Pada gambar di atas, folder Data Directory adalah `/opt/tomcat/apache-tomcat-9.0.40/webapps/geoserver/data`.

### Basisdata PostGIS
PostGIS dapat dihubungkan melalui antarmuka Geoserver. Berikut adalah tampilan antarmuka dan parameter koneksinya:

![](img/2020-12-04-08-55-41.png)

Sama seperti pada QGIS, koneksi ke PostGIS dari Geoserver juga menggunakan parameter seperti Host, Username, Basisdata dan Password.

### Publikasi Data melalui REST-API Geoserver
Pada remote server, seringkali kita tidak dapat menggunakan antarmuka yang memungkinkan untuk publikasi data secara langsung. Dengan demikian, interaksi pada Geoserver juga menjadi terbatas. Untuk itu, Geoserver menyediakan REST API yang dapat digunakan untuk berinteraksi dengan fungsi-fungsi Geoserver melalui antar muka API standard. API ini dapat diakses melalui http://alamatgeoserver:8080/geoserver/rest/workspaces.

Berikut adalah langkah untuk mengunggah file pada server:
1. Membuat Workspace baru dengan nama `latihan` (lewati jika Workspace sudah tersedia)
```bash
curl -v -u admin:password -XPOST -H "Content-type: text/xml"  -d "<workspace><name>latihan</name></workspace>" http://alamatgeoserver:8080/geoserver/rest/workspaces
```

2. Mengunggah file `jalan.zip` sebagai layer baru pada workspace `latihan` dengan nama datastore `jalan`

```bash
curl -v -u admin:geoserver -XPUT -H "Content-type: application/zip" --data-binary @jalan.zip http://54.254.9.31:8080/geoserver/rest/workspaces/latihan/datastores/jalan/file.shp
```


## Styling dengan SLD
Protokol WMS yang digunakan pada Geoserver memerlukan styling sebelum disajikan pada client. Format yang digunakan oleh Geoserver adalah SLD (*Style Layer Descriptor*). Antarmuka untuk pengaturan SLD adalah sebagai berikut:

![](img/2020-12-04-08-58-42.png)

SLD menggunakan format XML untuk menyimpan style. Untuk memudahkan styling, dapat digunakan QGIS untuk menyimpan simbolosasi yang diinginkan. 










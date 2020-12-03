# Basisdata Relational

Basisdata relational merupakan salah satu model basisdata pada DBMS (Database Management System). Model Relasional banyak digunakan sejak tahun 90an hingga saat ini karena berbagai kelebihannya dalam memanajemen data dalam jumlah besar. Pada bagian ini akan dibahas mengenai basisdata relasional, khususnya PostgreSQL.


## Pengantar Basisdata Relational
**Sistem Manajemen Basis Data Relasional** adalah kumpulan program dan fungsi berbasis tabel yang menyediakan antarmuka antara pengguna dan aplikasi dan basis data, memberikan cara sistematis untuk membuat, memperbarui, menghapus, mengelola, dan mengambil data. Sebagian besar sistem manajemen database relasional menggunakan bahasa pemrograman SQL untuk mengakses database dan banyak yang mengikuti properti *ACID (Atomicity, Consistency, Isolation, Durability)* dari database:
* **Atomicity**: Jika ada pernyataan dalam transaksi yang gagal, seluruh transaksi gagal dan database dibiarkan tidak berubah.
* **Consistency**: Transaksi harus memenuhi semua protokol yang ditentukan oleh sistem - tidak ada transaksi yang diselesaikan sebagian.
* **Isolation**: Tidak ada transaksi yang memiliki akses ke transaksi lain yang belum selesai. Setiap transaksi bersifat independen.
* **Durability**: Setelah transaksi dilakukan, transaksi akan tetap dilakukan melalui penggunaan log transaksi dan cadangan.

Basisdata relasional menyimpan data dalam bentuk tabel serta menyediakan cara yang efisien, intuitif, dan fleksibel untuk menyimpan dan mengakses informasi pada tabel tersebut secara terstruktur. Tabel pada basisdata relasional juga dikenal sebagai **relasi**, terdiri dari kolom yang berisi satu atau lebih kategori data, dan baris, juga dikenal sebagai rekaman tabel, berisi sekumpulan data yang ditentukan oleh kategori. 

Aplikasi DBMS (seperti PostgreSQL) mengakses data dengan menentukan **kueri**, yang menggunakan operasi seperti proyek untuk mengidentifikasi atribut, memilih *tuples*, dan menentukan relasi pada data. Model relasional untuk manajemen basis data dikembangkan oleh ilmuwan komputer IBM Edgar F. Codd pada tahun 1970.

![](img/2020-12-03-06-57-27.png)


### Pemodelan data pada basisdata Relasional
kita ambil sebuah contoh: anda ditugaskan oleh pimpinan anda untuk melakukan inventarisasi data yang diperoleh dari hasil pemetaan akibat bencana banjir di suatu daerah. Anda misalnya berurusan dengan data-data jumlah pengungsi dari masing-masing desa, kerusakan pada tiap desa, lokasi kantung-kantung pengungsian, kebutuhan tiap kepala, dan lain sebagainya. Apabila dinyatakan dalam bentuk tabel, data-data tersebut mungkin tampak seperti berikut:

### Beberapa istilah pada basisdata relasional
Sebagai review, berikut adalah beberapa istilah yang dikenal pada basisdata relasional:
* **Tabel**: Merupakan struktur penyimpanan dasar dari basis data objek relasional, terdiri dari satu atau lebih kolom (column) dan nol atau lebih baris (row).
* **Row (baris)**: Baris merupakan kombinasi dari nilai-nilai kolom dalam tabel; sebagai contoh, informasi tentang suatu departemen pada tabel Departmen. Baris seringkali disebut dengan record atau tuple.
* **Column (kolom)**: Kolom menggambarkan jenis data pada tabel; Kolom di definisikan dengan nama kolom dan tipe data beserta panjang data tertentu.
* **Field**: Field merupakan pertemuan antara baris dan kolom. Sebuah field menggambarkan satu keterangan mengenai data. Jika pada suatu field tidak terdapat data, maka field tersebut dikatakan memiliki nilai “null” atau kosong.
* **Primary key**: Primary key atau kunci utama merupakan kolom atau kumpulan kolom yang secara unik membedakan antara baris yang satu dengan lainnya; Kolom yang merupakan primary key ini tidak boleh mengandung nilai “null”, dan nilainya harus unik (berbeda antara baris satu dengan lainnya).
* **Foreign key**: Foreign key atau kunci tamu merupakan kolom atau kumpulan kolom yang mengacu ke primary key pada tabel yang sama atau tabel lain. Foreign key ini dibuat untuk memaksakan aturan-aturan relasi pada basis data. Nilai data dari foreign key harus sesuai dengan nilai data pada kolom dari tabel yang diacunya atau bernilai “null”.
* **Relasi** merupakan interaksi antara tabel yang menunjukkan hubungan antara objek-objek yang ada di dunia nyata. Relasi menyatakan hubungan antar tabel sebagai model dari dunia nyata.  



### Relasi pada basisdata relasional
Berikut adalah model relasi pada sebuah basisdata relasional:
1. **One to One (1 to 1)**
   Relasi database model ini terjadi apalabila sebuah data terdapat pada 2 buah tabel, dan hanya diperbolehkan satu data saja pada masing masing tabel (unique record), sama halnya seperti primary key, record yang ada pada model ini tidak boleh ada yang sama.
2. **One to Many (1 to n)**
   Relasi database model  ini membolehkan data yang sama pada tabel kedua, tapi hanya membolehkan data yang bersifat unique (unik) pada tabel pertama. Jadi pada model tabel kedua boleh memiliki beberapa data yang sama.
3. **Many to many (n to m)**
   Berbeda dengan kedua model diatas, relasi database model ini membolehkan beberapa data yang sama baik pada tabel pertama maupun tabel kedua. Dengan demikian tidak ada unique record di kedua tabel tersebut.

### Operasi pada basisdata relasional
Pada basisdata relasional, operasi yang dilakukan ke sebuah tabel dapat dikelompokkan menjadi empat kelompok besar. Empat operasi pembaruan dasar yang dilakukan pada model database relasional adalah **Insert, Update, Delete** dan **Select** [^footnote5]:
[^footnote5]:

* **Insert** digunakan untuk memasukkan data ke dalam relasi
* **Delete** digunakan untuk menghapus tupel dari tabel.
* **Modify** memungkinkan Anda untuk mengubah nilai dari beberapa atribut dalam tupel yang ada.
* **Select** memungkinkan Anda untuk memilih rentang data tertentu.
Setiap kali salah satu operasi ini diterapkan, batasan integritas yang ditentukan pada skema database relasional tidak boleh dilanggar.

Berikut adalah contoh dari operasi ini:

**Insert Operation**

Operasi Insert menambahkan data baru pada sebuah tabel sesuai dengan kolom yang tersedia

![](img/2020-12-03-07-21-13.png)

**Update Operation**

Pada tabel di bawah, status `CustomerName=Apple` berubah dari `inactive` menjadi `active`

![](img/2020-12-03-07-21-29.png)

**Delete Operation**
Pada operasi penghapusan, suatu kriteria diberikan melalui Query untuk 
![](img/2020-12-03-07-21-44.png)


**Select Operation**

Operasi berikut memilih Customer dengan nama "Amazon"
![](img/2020-12-03-07-22-43.png)


## Instalasi dan Pengaturan Basisdata PostgreSQL

PostgreSQL/PostGIS merupakan salah satu perangkat lunak untuk membuat basisdata yang bersifat open source. PostgreSQL/PostGIS memiliki kelebihan mampu menyimpan data spasial dalam basisdatanya. Pada bagian ini diuraikan cara membuat basisdata dengan menggunakan
PostgreSQL/PostGIS, dengan lebih dahulu membahas mengenai instalasi PostgreSQL dan PostGIS menggunakan Docker.

### Latihan: Instalasi dan Pengaturan Docker



### Latihan: Memulai Docker untuk PostGIS



## Menggunakan Query SQL pada Basisdata

### Review SQL


### Latihan: Menggunakan `psql` untuk melakukan query sederhana


### Latihan: Menggunakan pgAdmin sebagai GUI Basisdata PostgreSQL













# Pengaturan dan Administrasi Linux

Setelah memiliki sebuah sistem operasi Linux yang dapat digunakan untuk latihan dengan menggunakan WSL, pada bagian ini akan dibahas mengenai beberapa perintah dasar pada Linux. 


```{admonition} Catatan
**Ubuntu Pocket Guide** merupakan panduan yang cukup komprehensive untuk 'penggunaan Ubuntu sehari-hari'. Buku ini dapat diunduh secara gratis dari alamat: [http://www.ubuntupocketguide.com/download_main.html](http://www.ubuntupocketguide.com/download_main.html)

```

## Arsitektur Linux

Sebelum terjun langsung dalam penggunaan Linux, sebaiknya terlebih dahulu dipelajari mengenai filosofi dan arsitektur sebuah sistem operasi Linux. Pemahaman mengenai hal ini akan memudahkan dalam bekerja dengan Linux serta menghindari permasalahan pada saat bekerja dengan Linux.

### Kernel dan komponen-komponen Linux
Sebelumnya, [kernel linux](kernel) telah disebutkan beberapa kali pada panduan ini. Lisensi kernel Linux yang dikembangkan oleh Linus Torvalds sebagai rangkaian kode yang bersifat bebas dan terbuka memungkinkan pengembangan berbagai aplikasi lain di atasnya, yang kemudian melahirkan ratusan distro yang masing-masingnya adalah sebuah sistem operasi sendiri. Tetapi, apa sebenarnya yang dimaksud dengan *Linux Kernel*?

```{figure} img/2020-12-02-02-49-33.png
---
name: kernel
---
Arsitektur Sistem Operasi Linux
```

Sebuah 'kernel' dapat diartikan sebagai potongan kode yang menjadi antarmuka antara perangkat keras (*hardware*) dan berbagai aplikasi yang menggunakan perangkat tersebut. Linux Kernel yang awalnya didesain oleh Linus Torvalds sebagai sebuah sistem yang tertutup dan tidak portabel ternyata berubah menjadi kode yang dapat digunakan pada berbagai platform dengan dukungan pada berbagai perangkat keras, sehingga muncul berbagai pengembangan versi distribusi Linux yang berbeda. 

### Filosofi Linux
Di atas kernel inilah berbagai aplikasi berdiri sebagai perantara antara perangkat keras dan perangkat lunak pada sebuah sistem operasi. Filosofi Linux ini kemudian dikenal luas dengan istilah, **["Everything is a File"](https://unix.stackexchange.com/questions/225537/everything-is-a-file)**: setiap transaksi, proses, dan apapun yang terjadi pada sebuah sistem Unix sejatinya adalah '*stream of byte*' yang berdiri di atas kernel.

```{figure} img/2020-12-02-03-10-30.png
---
name: komponen
---
Komponen-komponen Linux
```

Jika Kernel digunakan untuk berkomunikasi dengan perangkat keras, maka sebuah **Shell** pada Linux berfungsi sebagai penghubung antara pengguna dan kernel. Shell dapat menerima berbagai perintah pengguna dan menerjemahkannya menjadi perintah yang dapat dipahami oleh perangkat keras. Berbagai aplikasi juga menggunakan shell untuk melakukan operasi-operasi yang diinginkan pengguna, misalnya pada antarmuka desktop. Karena setiap operasi adalah 'file', maka pengguna yang berbeda dapat melakukan operasi yang berbeda pada sebuah berkas yang sama. Pada Linux, kondisi berikut berlaku:
* Tiap program dijalankan oleh *user*/pengguna
* Tiap berkas dimiliki oleh pengguna
* Tiap pengguna memiliki identitas unik yang membedakan pengguna satu dengan yang lain

Dari uraian di atas, dapat disimpulkan bahwa beberapa karakteristik dari Linux adalah sebagai berikut [^footnote2]:

[^footnote2]: https://www.tutorialspoint.com/operating_system/os_linux.htm


* Portabel - Portabilitas berarti perangkat lunak dapat bekerja pada berbagai jenis perangkat keras dengan cara yang sama. Kernel Linux dan program aplikasi mendukung instalasi mereka pada semua jenis platform perangkat keras.
* Open Source - Kode sumber Linux tersedia secara gratis dan merupakan proyek pengembangan berbasis komunitas. Beberapa tim bekerja sama untuk meningkatkan kemampuan sistem operasi Linux dan pengembangannya terus berjalan.
* Multi-User - Linux adalah sistem multiuser yang berarti banyak pengguna dapat mengakses sumber daya sistem seperti memori / ram / program aplikasi pada saat yang bersamaan.
* Multiprogramming - Linux adalah sistem multiprogramming yang berarti banyak aplikasi dapat berjalan pada waktu yang bersamaan.
* Sistem File Hirarkis - Linux menyediakan struktur file standar di mana file sistem / file pengguna disusun dengan struktur yang sama pada berbagai distribusi Linux.
* Shell - Linux menyediakan program penerjemah khusus yang dapat digunakan untuk menjalankan perintah sistem operasi. Dapat digunakan untuk melakukan berbagai jenis operasi, memanggil program aplikasi. dll.
* Keamanan - Linux menyediakan keamanan pengguna menggunakan fitur otentikasi seperti proteksi kata sandi / akses terkontrol ke file / enkripsi data tertentu.


## Mengunakan Shell 
Shell Command merupakan antarmuka untuk melakukan berbagai operasi pada sistem operasi Linux. Meskipun saat ini berbagai Distro Linux telah dilengkapi dengan antarmuka yang sangat canggih, penggunaan Shell untuk operasi sehari-hari memiliki beberapa kelebihan:
* Perintah yang kompleks dapat dilakukan dengan mudah menggunakan Shell (coba: `cal`)
* Shell diperlukan pada saat menggunakan Linux sebagai mesin server: perintah shell jauh lebih cepat dan menggunakan bandwith lebih sedikit apabila koneksi dilakukan dengan shell
* Shell dapat diprogram (contoh: `for i in *.png do ...`)
* Penggunaan Shell memungkinkan kustomisasi, misalnya dengan menggunakan argumen untuk berbagai perintah (contoh: pipe operation) 

Pada bagian ini akan dilakukan beberapa latihan untuk mengenal perintah-perintah shell pada Linux. Perintah-perintah pada panduan ini dilakukan pada Ubuntu, sehingga penggunaan distro yang lain mungkin memerlukan penyesuaian. Meskipun sebagian besar perintah antar distro Linux yang satu dengan yang lain sama, tetapi boleh jadi ada sedikit perbedaan (sebagai contoh, Ubuntu yang berbasis Debian menggunakan Package Manager *apt*, sedangkan CentOS yang berbasis RedHat menggunakan *yum*). 

```{admonition} Catatan
**Bash Shell** adalah aplikasi Command Shell yang saat ini merupakan aplikasi standar pada hampir semua distribusi Linux, sehingga perintah pada panduan ini mengacu pada Bash Shell. Perintah-perintah pada Bash Shell dapat dilihat pada [link berikut](https://devhints.io/bash).
```

### Latihan: Perintah Dasar pada Shell

WSL2 untuk Windows 10 yang diinstall pada latihan sebelumnya memberikan antarmuka Shell pada pengguna (lihat [gambar sebelumnya](wsl2)). Latihan-latihan berikut menggunakan antarmuka *shell command* yang diberikan oleh WSL2 ini.

Berikut adalah beberapa perintah yang dapat digunakan untuk berlatih memanajemen file pada Linux:


  
|  Command	| Deskripsi |
| :--: | :--- |
| pwd |	print current working directory |
| cd |	change working directory |
| ls	| list files in working directory |
| man |	bring up manual for a command |
| exit |	log out of shell |
| clear | 	clears all output from console |
| date | 	output the system date  |
| cal | 	output a text calendar  |
| uname | 	print information about the current system |
|  |  |

Untuk latihan, buka konsol Ubuntu WSL2, kemudian ketikkan salah satu perintah di atas:

![](img/2020-12-02-04-08-05.png)

Perintah `pwd` pada gambar di atas digunakan untuk menampilkan direktori tempat shell saat ini berjalan. Keluaran dari perintah ini langsung ditampilkan pada konsol. Untuk latihan, jalankan perintah-perintah lain dan perhatikan apa yang terjadi pada konsol.

### Latihan: Operasi pada File





### Instalasi aplikasi
Ubuntu menggunakan APT (*Advanced Package Tool*) sebagai package manager untuk mengatur 

https://itsfoss.com/apt-command-guide/

## Pengaturan Pengguna dan Hak Akses
Sebagaimana disebutkan, Linux merupakan sistem operasi MultiUser dan Multiprogramming, dimana tiap berkas dimiliki oleh seorang pengguna, dan tiap pengguna memiliki hak akses tertentu. Latihan berikut akan memberikan gambaran mengenai pengaturan pengguna dan hak akses pada berkas atau direktori [^footnote3].

[^footnote3]: https://vitux.com/a-beginners-guide-to-user-management-on-ubuntu/

### Latihan: Administrasi Pengguna



### Pengaturan Grup


### Pengaturan Hak Akses 

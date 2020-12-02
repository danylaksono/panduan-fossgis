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
**Bash Shell** adalah aplikasi Command Shell yang saat ini merupakan aplikasi standar pada hampir semua distribusi Linux, sehingga perintah pada panduan ini mengacu pada Bash Shell. Perintah-perintah pada Bash Shell dapat dilihat pada [link berikut](https://devhints.io/bash) atau [link berikut](https://courses.cs.washington.edu/courses/cse391/16sp/bash.html).
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

### Latihan: Operasi pada File dan Direktori
Sebagaimana pada Windows, berkas pada Linux disusun dalam beberapa folder yang masing-masing mengatur pekerjaan tertentu. Pada Linux, struktur direktorinya adalah sebagai berikut:

![](img/2020-12-02-04-35-50.png)

Perintah pada Shell umumnya mengikuti struktur sebagai berikut: 

![](img/2020-12-02-05-10-13.png)

`Command` adalah perintah yang dipanggil pada shell. `Flags` menunjukkan opsi yang dapat dipanggil oleh command tersebut, sedangkan `argument` menyatakan variabel yang dipanggil oleh perintah tersebut.

1. Untuk berpindah antar satu direktori ke direktori lain, dapat digunakan Relative Directory, dimana struktur direktori dapat diakses secara hirarkis.

|  Command	| Deskripsi |
| :--: | :--- |
| .	| direktory saat ini |
| .. |	direktory yang berada satu tingkat di atas direktori saat ini  |
| ~	 | home directory untuk pengguna saat ini |
| /	 | root directory |
| /apt	| folder **apt** pada root|
| | |


2. Selanjutnya, perintah-perintah berikut dapat digunakan pada saat berhubungan dengan pengaturan direktori:

|  Command	| Deskripsi |
| :--: | :--- |
| ls | 	list files in working directory | 
| pwd | 	print current working directory | 
| cd | 	change working directory | 
| mkdir | 	make a new directory | 
| rmdir | 	remove the given directory (must be empty) | 
| | | 

3. Gunakan perintah `man <namaperintah>` atau `namaperintah --help` untuk menampilkan opsi apa saja yang dapat digunakan pada tiap perintah tersebut
3. Untuk latihan selanjutnya, tampilkan isi dari root folder, seperti berikut:

![](img/2020-12-02-05-08-58.png)

   
4. Selanjutnya, buatlah struktur folder berikut pada home directory Anda (pengguna aktif saat ini):

![](img/2020-12-02-05-01-36.png)

Buat folder `workspace` yang didalamnya berisi dua buah folder, masing-masing folder `latihan1` dan `latihan2`. Di dalam folder `latihan1` berisi sebuah folder lain

5. Untuk bekerja dengan file, gunakan perintah-perintah berikut:

|  Command	| Deskripsi |
| :--: | :--- |
| cp	| copy a file |
| mv	| move a file (also used to rename files)  |
| rm	| remove the given file  |
| touch	| create empty file, or change time-modified  |
| | |

Gunakan perintah di atas untuk membuat file `berkas1.txt` pada `folder_a` di dalam folder `latihan1`. Selanjutnya, lakukan perintah copy dan rename untuk menghasilkan struktur file seperti berikut:

![](img/2020-12-02-05-21-44.png)

6. Terakhir, hapus folder_b berikut semua file dan sub direktori di dalamnya. Hasil akhirnya sebagai berikut:

![](img/2020-12-02-05-29-52.png)


Dengan demikian, latihan ini menunjukkan bagaimana manajemen terhadap file dilakukan di Linux.


### Latihan: Instalasi aplikasi
Ubuntu menggunakan APT (*Advanced Package Tool*) sebagai package manager untuk mengatur seluruh aplikasi yang digunakan. Terdapat beberapa antarmuka yang berhubungan dengan Package Manager ini yang dikenal di sistem operasi berbasis Debian, seperti *apt-get, aptitude,* maupun *apt*. Latihan berikut diberikan untuk memahamkan bagaimana menggunakan *apt* untuk memanajemen aplikasi pada Linux [^footnote4].

[^footnote4]:https://itsfoss.com/apt-command-guide/


1. Melakukan *update* basisdata APT
   Pada Ubuntu dan distro berbasis Debian lainnya, aplikasi yang terinstall disimpan pada basisdata. Untuk melakukan update atau pembaruan aplikasi dari repository, gunakan perintah:

   ```bash
   sudo apt update
   ```
   keluaran perintah tersebut adalah seperti berikut:

   ![](img/2020-12-02-05-36-00.png)

   hasil dari `apt update` adalah daftar aplikasi yang dapat diperbarui. Untuk mengeksekusi pembaruan aplikasi, gunakan perintah:

   ```bash
   sudo apt upgrade
   ```

   kedua perintah di atas dapat diringkas menggunakan `&&` :

   ```bash
   sudo apt update && sudo apt upgrade
   ```

   ```{caution} 
   Upgrade adalah hak *sudoers*. Apa yang terjadi jika perintah di atas dijalankan tanpa `sudo`?
   ```



2. `apt` dapat digunakan untuk melakukan instalasi paket aplikasi. sebagai contoh, perintah berikut akan menginstall aplikasi `tree`:

   ```bash
   sudo apt install tree
   ```

   selanjutnya, perintah `tree` dapat langsung digunakan pada shell.

3. Untuk menghapus aplikasi, gunakan perintah:
   ```bash
   sudo apt purge <nama aplikasi>
   ```

   atau

   ```bash
   sudo apt remove <nama aplikasi>
   ```

   perbedaan keduanya terletak pada kedalaman penghapusan. `purge` menghapus seluruh aplikasi berikut konfigurasi yang tersimpan

4. Sebagai latihan, lakukan instalasi untuk aplikasi editing bernama `vim`. **vim** dapat digunakan untuk mengedit sebuah file yang memiliki tingkat kompleksitas tinggi.


## Pengaturan Pengguna dan Hak Akses
Sebagaimana disebutkan, Linux merupakan sistem operasi MultiUser dan Multiprogramming, dimana tiap berkas dimiliki oleh seorang pengguna, dan tiap pengguna memiliki hak akses tertentu. ***Sudoers*** merupakan kelas pengguna yang memiliki hak akses lebih tinggi (elevated) dibandingkan pengguna biasa, sehingga mampu melakukan berbagai perintah yang tidak diizinkan untuk pengguna biasa, misalnya `apt upgrade`.


```{figure} img/2020-12-02-05-41-38.png
---
name: sudo
---
sumber: https://xkcd.com/149/
```

Beberapa perintah terkait user pada Linux adalah sebagai berikut:

|  Command	| Deskripsi |
| :--: | :--- |
| whoami |	print your username|
| id	| print user id and group membership |
| users |	list logged-in users (short) |
| who	| list logged-in users (long) |
| finger |	print information about users |
| | |

### Latihan: Administrasi Pengguna

Latihan berikut akan memberikan gambaran mengenai pengaturan pengguna dan hak akses pada berkas atau direktori [^footnote3].

[^footnote3]: https://vitux.com/a-beginners-guide-to-user-management-on-ubuntu/

1. Membuat user baru
Akun pengguna baru dapat digunakan pada sebuah sistem Enterprise, dimana satu sistem operasi yang sama digunakan oleh beberapa pengguna yang berbeda. untuk menambahkan pengguna baru, gunakan perintah berikut:

```bash
sudo adduser namauser
```

Setelah user baru dibuat, kita akan diminta untuk memasukkan nama pengguna dan password, serta beberapa informasi lainnya.

2. Merubah password
Setelah membuat akun, langkah selanjutnya adalah merubah password untuk akun tersebut:

```bash
sudo passwd namauser
```

### Latihan: Pengaturan Grup


Grup dapat digunakan untuk mendefinisikan peranan yang berbeda untuk tiap pengguna, misalnya membatasi akses pada direktori tertentu serta akses untuk perintah tertentu. Untuk memasukkan pengguna pada grup, perintahnya adalah sebagai berikut:

1. Menambahkan pengguna ke grup

```bash
sudo usermod –a –G namagrup namauser
```

2. jika grup yang dimaksud adalah **sudoer**, maka perintahnya adalah sebagai berikut:

```bash
usermod -aG sudo namauser
```

3. selanjutnya, lakukan penambahan akses pengguna ini ke dalam sudoer:

```bash
sudo visudo
```

masukkan informasi nama user sebagai sudoer

```bash
namauser  ALL=(ALL) NOPASSWD:ALL
```

4. Berpindah akun (switch user)
Untuk keperluan administrasi, seringkali pengguna harus berpindah dari satu akun (non-sudoer) ke akun lain (sudoer). untuk itu, perintah berikut dapat digunakan:

```bash
 su –u userkedua
 whoami
 ``` 

untuk mengakses *superelevated user* atau root, perintah berikut dapat digunakan:

```bash
 su –u userkedua
 whoami
 ``` 

### Pengaturan Hak Akses 
Sebagaimana disebutkan sebelumnya, akses terhadap file dan perintah pada Linux dapat dibatasi untuk user tertentu. Izin (*Permission*) ini pada linux dibagi menjadi:
* owner(u) - user yang membuat file. ini dapat dirubah menggunakan perintah `chown`
* group(g) - grup yang berhubungan dengan tiap file
* others(o) - orang lain yang bukan owner maupun anggota grup yang dapat mengakses file tersebut
* 
Sebagai contoh, jika kita menggunakan perintah `ls -al` berikut:

![](img/2020-12-02-08-39-09.png)

terdapat penjelasan (`drwxr-xr-x`) mengenai status dan hak akses pada file tersebut, yaitu:
* d - menunjukka bahwa berkas tersebut adalah sebuah `directory`
* rwx - permission (izin) yang diberikan pada pemilik file untuk ***r**ead, **w**rite dan e**x**ecute*
* r-x - izin grup, pengguna dari grup `danylaksono` (kebetulan nama pengguna dan grup sama) dapat melakukan *read dan execute* pada file tersebut
* r-x - izin untuk other, atau pengguna lain


Penulisan izin tersebut juga dapat dilakukan menggunakan **notasi numerik**:
* 0: Tidak ada izin
* 1: Jalankan (x)
* 2: Tulis (w)
* 4: Baca (r))

Sekarang, bagaimana cara menghitung izin untuk pengguna dan grup dalam notasi numerik? Cukup tambahkan nilai izin untuk mendapatkan nilai pengguna, grup, dan izin lainnya masing-masing.

Sebagai contoh:
baca (4), tulis (2) dan jalankan (1) izin **rwx** diterjemahkan ke 7 (4 + 2 + 1)
baca (4) dan tulis (2) izin **rw-** diterjemahkan ke 6 (4 + 2)
tulis (2) dan jalankan (1) izin **-wx** diterjemahkan ke 3 (2 + 1), dan seterusnya.

```{warning}
Kira-kira apa pengaruh `chmod 777`?
```


Dengan menggunakan perintah `chmod`, izin suatu file dapat dirubah. perintah ini menggunakan notasi:
* tanda minus (-), yang berarti "hapus izin ini"
* tanda tambah (+), yang berarti "tambahkan izin ini"
* tanda sama dengan (=), yang berarti "ubah izin menjadi persis seperti ini".

Sebagai contoh:
```bash
chmod +x latihan.txt
```

maksudnya adalah memberi izin kepada semua pengguna untuk mengakses file tersebut. ini sama dengan `chmod a+x latihan1.txt`, dimana **a** berarti 'all'. Hal yang sama berlaku untuk grup (g) dan other (o).

Sebagai latihan untuk sesi ini, buat user kedua, kemudian rubah akses pada file latihan1.txt yang sudah dibuat sebelumnya agar user lain tidak dapat membaca file tersebut. Apa pengaruhnya apabila user pertama hendak mengakses file tersebut?






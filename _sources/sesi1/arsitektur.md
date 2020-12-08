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


* **Portabel** - Portabilitas berarti perangkat lunak dapat bekerja pada berbagai jenis perangkat keras dengan cara yang sama. Kernel Linux dan program aplikasi mendukung instalasi mereka pada semua jenis platform perangkat keras.
* **Open Source** - Kode sumber Linux tersedia secara gratis dan merupakan proyek pengembangan berbasis komunitas. Beberapa tim bekerja sama untuk meningkatkan kemampuan sistem operasi Linux dan pengembangannya terus berjalan.
* **Multi-User** - Linux adalah sistem multiuser yang berarti banyak pengguna dapat mengakses sumber daya sistem seperti memori / ram / program aplikasi pada saat yang bersamaan.
* **Multiprogramming** - Linux adalah sistem multiprogramming yang berarti banyak aplikasi dapat berjalan pada waktu yang bersamaan.
* **Sistem File Hirarkis** - Linux menyediakan struktur file standar di mana file sistem / file pengguna disusun dengan struktur yang sama pada berbagai distribusi Linux.
* **Shell** - Linux menyediakan program penerjemah khusus yang dapat digunakan untuk menjalankan perintah sistem operasi. Dapat digunakan untuk melakukan berbagai jenis operasi, memanggil program aplikasi. dll.
* **Keamanan** - Linux menyediakan keamanan pengguna menggunakan fitur otentikasi seperti proteksi password dan akses terkontrol ke file/enkripsi data tertentu.

&nbsp;  

## Mengunakan Shell 
**Shell Command** merupakan antarmuka untuk melakukan berbagai operasi pada sistem operasi Linux. Meskipun saat ini berbagai Distro Linux telah dilengkapi dengan antarmuka yang sangat canggih, penggunaan Shell untuk operasi sehari-hari memiliki beberapa kelebihan:
* Perintah yang kompleks dapat dilakukan dengan mudah menggunakan Shell (coba: `cal`)
* Shell diperlukan pada saat menggunakan Linux sebagai mesin server: perintah shell jauh lebih cepat dan menggunakan bandwith lebih sedikit apabila koneksi dilakukan dengan shell
* Shell dapat diprogram (contoh: `for i in *.png do ...`)
* Penggunaan Shell memungkinkan kustomisasi, misalnya dengan menggunakan argumen untuk berbagai perintah (contoh: *pipe operation*) 

Pada bagian ini akan dilakukan beberapa latihan untuk mengenal perintah-perintah shell pada Linux. Perintah-perintah pada panduan ini dilakukan pada Ubuntu, sehingga penggunaan distro yang lain mungkin memerlukan penyesuaian. Meskipun sebagian besar perintah antar distro Linux yang satu dengan yang lain sama, tetapi boleh jadi ada sedikit perbedaan (sebagai contoh, Ubuntu yang berbasis Debian menggunakan Package Manager *apt*, sedangkan CentOS yang berbasis RedHat menggunakan *yum*). 

```{admonition} Catatan
**Bash Shell** adalah aplikasi Command Shell yang saat ini merupakan aplikasi standar pada hampir semua distribusi Linux, sehingga perintah pada panduan ini mengacu pada Bash Shell. Perintah-perintah pada Bash Shell dapat dilihat pada [link berikut](https://devhints.io/bash) atau [link berikut](https://courses.cs.washington.edu/courses/cse391/16sp/bash.html).
```
&nbsp;  

### Latihan: Perintah Dasar pada Shell

WSL2 untuk Windows 10 yang diinstall pada latihan sebelumnya memberikan antarmuka Shell pada pengguna (lihat [gambar sebelumnya](wsl2)). Latihan-latihan berikut menggunakan antarmuka *shell command* yang diberikan oleh WSL2 ini.

Berikut adalah beberapa perintah yang dapat digunakan untuk berlatih manajemen file pada Linux:

|  Command	| Deskripsi |
| :--: | :--- |
| man |	bring up manual for a command |
| exit |	log out of shell |
| clear | 	clears all output from console |
| date | 	output the system date  |
| cal | 	output a text calendar  |
| uname | 	print information about the current system |
|<img width=100/>|<img width=500/>|

Untuk latihan, buka konsol Ubuntu WSL2, kemudian ketikkan salah satu perintah di atas:

![](img/2020-12-02-04-08-05.png)

Perintah `pwd` pada gambar di atas digunakan untuk menampilkan direktori tempat shell saat ini berjalan. Keluaran dari perintah ini langsung ditampilkan pada konsol. Untuk latihan, jalankan perintah-perintah lain dan perhatikan apa yang terjadi pada konsol.

&nbsp;  

### Latihan: Operasi pada File dan Direktori
Sebagaimana pada Windows, berkas pada Linux disusun dalam beberapa folder yang masing-masing mengatur pekerjaan tertentu. Pada Linux, struktur direktorinya adalah sebagai berikut:

![](img/2020-12-02-04-35-50.png)

Perintah pada Shell umumnya mengikuti struktur sebagai berikut: 

![](img/2020-12-02-05-10-13.png)

`Command` adalah perintah yang dipanggil pada shell. `Flags` menunjukkan opsi yang dapat dipanggil oleh command tersebut, sedangkan `Argument` menyatakan variabel yang dipanggil oleh perintah tersebut.

1. Untuk berpindah antar satu direktori ke direktori lain, dapat digunakan *Relative Directory*, dimana struktur direktori dapat diakses secara hirarkis.
   
   |  Command	| Deskripsi |
   | :--: | :--- |
   | .	| direktory saat ini |
   | .. |	direktory yang berada satu tingkat di atas direktori saat ini  |
   | ~	 | home directory untuk pengguna saat ini |
   | /	 | root directory |
   | /apt	| folder **apt** pada root|
   |<img width=100/>|<img width=300/>|

   &nbsp;  

2. Selanjutnya, perintah-perintah berikut dapat digunakan pada saat berhubungan dengan pengaturan direktori:

   |  Command	| Deskripsi |
   | :--: | :--- |
   | ls | 	tampilkan daftar berkas pada direktori saat ini | 
   | pwd | 	print working directory - cetak direktori saat ini | 
   | cd | 	change directory - berpindah ke direktori baru | 
   | mkdir | 	membuat direktori baru | 
   | rmdir | 	menghapus direktori (isi folder harus kosong) | 
   | rm | 	hapus file atau direktori (`rm -rf` untuk menghapus secara paksa) | 
   |<img width=100/>|<img width=300/>|

   &nbsp;  

3. Gunakan perintah `man <namaperintah>` atau `namaperintah --help` untuk menampilkan opsi apa saja yang dapat digunakan pada tiap perintah tersebut. Sebagai contoh berikut adalah manual page untuk perintah `ls`:
   ![](img/2020-12-07-11-00-11.png)
   &nbsp;  


4. Untuk latihan selanjutnya, tampilkan isi dari **root directory** (satu tingkat di atas `home directory`), seperti berikut:
   ![](img/2020-12-02-05-08-58.png)
   &nbsp;  

5. Selanjutnya, buatlah struktur folder berikut pada `home directory` Anda (pengguna aktif saat ini):
   ![](img/2020-12-02-05-01-36.png)

   Buat folder `workspace` yang didalamnya berisi dua buah folder, masing-masing folder `latihan1` dan `latihan2`. Di dalam folder `latihan1` berisi sebuah folder lain.

   ```{admonition} Catatan
   Berbagai perintah pada *shell* Linux sangat efektif apabila digunakan dengan baik. Perintah yang berbeda dapat dikombinasikan dan dioptimalkan untuk mempersingkat tugas-tugas yang diberikan. Sebagai contoh, beberapa perintah dapat menerima lebih dari satu argumen (misalnya, `mkdir folder1 folder2`). Penggunaan operator pada command juga dapat menyingkat operasi yang diinginkan (misalnya, `sudo apt update && sudo apt update` dengan operator `AND_IF`), operasi ekspansi dengan bracket (misalnya `cp /alamat/file.txt{,.bak}`)


   Sebagai catatan tambahan, Shell pada Linux bahkan mendukung [Regex](https://likegeeks.com/regex-tutorial-linux/)!
   ```

   &nbsp;  

6. Untuk bekerja dengan file, beberapa perintah berikut dapat digunakan:

   |  Command	| Deskripsi |
   | :--: | :--- |
   | cp	| copy a file |
   | mv	| move a file (also used to rename files)  |
   | rm	| remove the given file  |
   | touch	| create empty file, or change time-modified  |
   |<img width=100/>|<img width=300/>|

   Gunakan perintah di atas untuk membuat file `berkas1.txt` pada `folder_a` di dalam folder `latihan1`. Selanjutnya, lakukan perintah copy dan rename untuk menghasilkan struktur file seperti berikut:

   ![](img/2020-12-02-05-21-44.png)

   untuk melakukan editing pada file, kebanyakan distro Linux menyediakan shell editor bawaan, misalnya `nano`.

   &nbsp;  

7. Terakhir, hapus **folder_b** berikut semua file dan sub-direktori di dalamnya. Hasil akhirnya sebagai berikut:

   ![](img/2020-12-02-05-29-52.png)

&nbsp;  

Dengan demikian, latihan ini menunjukkan bagaimana manajemen terhadap file dilakukan di Linux. Berbagai perintah dapat digabungkan untuk memperoleh hasil yang diinginkan, misalnya membuat beberapa folder baru sekaligus atau membuat dan mengcopy berkas secara cepat.

&nbsp;  

### Latihan: Instalasi aplikasi
Ubuntu menggunakan APT (*Advanced Package Tool*) sebagai *package manager* untuk mengatur seluruh aplikasi yang digunakan. Sebuah Package manager menghubungkan antara Repository dan mesin linux yang kita gunakan. [**Repositori Linux**](https://www.linuxid.net/24289/penjelasan-lengkap-ubuntu-repository-dan-cara-menggunakan-repository/) merupakan lokasi penyimpanan tempat sistem Anda mengambil dan menginstal pembaruan dan aplikasi OS. Setiap repositori adalah kumpulan perangkat lunak yang disimpan pada server jarak jauh dan digunakan untuk menginstal dan memperbarui paket perangkat lunak pada sistem Linux.

```{figure} img/2020-12-03-02-08-32.png
---
name: apt
---
Cara kerja Package Manager pada Linux
```

Pada pemanggilan berkas yang tersimpan di repository, berlaku kondisi sebagaimana akses informasi melalui internet pada umumnya: semakin jauh secara fisik lokasi server, semakin lambat koneksi yang akan diperoleh. Untuk itu, terdapat sejumlah repository lokal untuk tiap versi distribusi Linux. Sebagai contoh, [http://repo.ugm.ac.id/](http://repo.ugm.ac.id/) berisi repository untuk beberapa distribusi Linux yang disimpan pada server UGM.

Terdapat beberapa antarmuka yang berhubungan dengan Package Manager yang dikenal di sistem operasi berbasis Debian, seperti *apt-get, aptitude,* maupun *apt*. Aplikasi antarmuka ini menghubungkan perintah dari pengguna (misalnya `sudo apt update`) dengan *package manager* (seperti APT) untuk kemudian melakukan operasi terkait dengan basisdata aplikasi pada repository.

Latihan berikut diberikan untuk memahamkan bagaimana menggunakan *apt* untuk memanajemen aplikasi pada Linux [^footnote4].

[^footnote4]:https://itsfoss.com/apt-command-guide/


1. Melakukan *update* basisdata APT
   Pada Ubuntu dan distro berbasis Debian lainnya, aplikasi yang terinstall disimpan pada basisdata. Untuk melakukan update atau pembaruan aplikasi dari repository, gunakan perintah:

   ```bash
   sudo apt update
   ```
   keluaran perintah tersebut adalah seperti berikut:

   ![](img/2020-12-02-05-36-00.png)

   Hasil dari `apt update` adalah daftar aplikasi yang dapat diperbarui. Untuk mengeksekusi pembaruan aplikasi, gunakan perintah:

   ```bash
   sudo apt upgrade
   ```

   Kedua perintah di atas dapat diringkas menggunakan `&&` :

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

&nbsp;  

3. Untuk menghapus aplikasi, gunakan perintah:
   ```bash
   sudo apt purge <nama aplikasi>
   ```

   atau

   ```bash
   sudo apt remove <nama aplikasi>
   ```

   perbedaan keduanya terletak pada kedalaman penghapusan. `purge` menghapus seluruh aplikasi berikut konfigurasi yang tersimpan, sedangkan `remove` hanya menghapus aplikasi dari daftar basisdata **APT**, tetapi meninggalkan konfigurasi dari aplikasi, sehingga apabila kelak dilakukan instalasi kembali, konfigurasi ini akan digunakan.

&nbsp;  

4. Sebagai latihan, lakukan instalasi untuk aplikasi editing bernama `vim`. **vim** dapat digunakan untuk mengedit sebuah file yang memiliki tingkat kompleksitas tinggi, dan akan membantu pada saat kita melakukan editing file, misalnya pada sebuah mesin server.


## Pengaturan Pengguna dan Hak Akses
Sebagaimana disebutkan, Linux merupakan sistem operasi MultiUser dan Multiprogramming, dimana tiap berkas dimiliki oleh seorang pengguna, dan tiap pengguna memiliki hak akses tertentu. ***Sudoers*** merupakan kelas pengguna yang memiliki hak akses lebih tinggi (*elevated*) dibandingkan pengguna biasa, sehingga mampu melakukan berbagai perintah yang tidak diizinkan untuk pengguna yang tidak termasuk dalam **grup 27 (sudo)**, misalnya `apt upgrade`.


```{figure} img/2020-12-02-05-41-38.png
---
name: sudo
---
Sumber: https://xkcd.com/149/
```

Beberapa perintah terkait user pada Linux adalah sebagai berikut:

|  Command	| Deskripsi |
| :--: | :--- |
| whoami |	print your username|
| id	| print user id and group membership |
| users |	list logged-in users (short) |
| who	| list logged-in users (long) |
| finger |	print information about users |
|<img width=100/>|<img width=500/>|

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
Grup pada Linux dapat digunakan untuk mendefinisikan peranan yang berbeda untuk tiap pengguna, misalnya membatasi akses pada direktori serta akses untuk perintah tertentu. Untuk memasukkan pengguna yang sudah dibuat pada sebuah grup, perintahnya adalah sebagai berikut:

1. Menambahkan pengguna ke grup

   ```bash
   sudo usermod –a –G namagrup namauser
   ```
   &nbsp;  
2. Jika grup yang dimaksud adalah **sudoer**, maka perintahnya adalah sebagai berikut:

   ```bash
   usermod -aG sudo namauser
   ```
   &nbsp;  

3. Selanjutnya, lakukan penambahan akses pengguna ini ke dalam *sudoer*:

   ```bash
   sudo visudo
   ```

   masukkan informasi nama user sebagai *sudoer*

   ```bash
   namauser  ALL=(ALL) NOPASSWD:ALL
   ```
   &nbsp;  
4. Berpindah akun (switch user)
   Untuk keperluan administrasi, seringkali pengguna harus berpindah dari satu akun (non-sudoer) ke akun lain (sudoer). untuk itu, perintah berikut dapat digunakan:

   ```bash
   su –u userkedua
   whoami
   ``` 

   untuk mengakses *superelevated user* atau **root**, perintah berikut dapat digunakan:

   ```bash
   sudo su
   whoami
   ``` 

Grup dapat digunakan untuk mengatur dan mengelompokkan pengguna pada satu hak akses yang sama. Selanjutnya adalah bagaimana melakukan pengaturan hak akses tersebut.



### Pengaturan Hak Akses 
Sebagaimana disebutkan sebelumnya, akses terhadap file dan perintah pada Linux dapat dibatasi untuk user tertentu. Izin (*Permission*) ini pada linux dibagi menjadi:
* **owner** (u) - user yang membuat file. ini dapat dirubah menggunakan perintah `chown`
* **group** (g) - grup yang berhubungan dengan tiap file
* **others** (o) - orang lain yang bukan owner maupun anggota grup yang dapat mengakses file tersebut ('=semua orang')
  

Sebagai contoh, jika kita menggunakan perintah `ls -al` berikut:

![](img/2020-12-02-08-39-09.png)

akan muncul keterangan (`drwxr-xr-x`) mengenai status dan hak akses pada file tersebut, yaitu:
* **d** : menunjukkan bahwa berkas tersebut adalah sebuah `directory`
* **rwx** : permission (izin) yang diberikan pada pemilik file untuk ***r**ead, **w**rite dan e**x**ecute
* **r-x** : izin *grup*, pengguna dari grup `danylaksono` (kebetulan untuk contoh di atas nama pengguna dan grup sama) dapat melakukan *read dan execute* pada file tersebut
* **r-x** : izin untuk *other*, atau pengguna lain


```{figure} img/2020-12-03-02-33-45.png
---
height: 500px
name: izin
---
Penjelasan hak akses pada Linux
```

Penulisan izin tersebut juga dapat dilakukan menggunakan **notasi numerik**:
* 0: Tidak ada izin
* 1: Jalankan (x)
* 2: Tulis (w)
* 4: Baca (r)

Sekarang, bagaimana cara menghitung izin untuk pengguna dan grup dalam notasi numerik? Cukup tambahkan nilai izin untuk mendapatkan nilai pengguna, grup, dan izin lainnya masing-masing.

Sebagai contoh:

* Izin *baca* (4), *tulis* (2) dan *jalankan* (1): izin **rwx** diterjemahkan menjadi 7 (4 + 2 + 1)
* Izin *baca* (4) dan *tulis* (2): izin **rw-** diterjemahkan menjadi 6 (4 + 2)
* Izin *tulis* (2) dan *jalankan* (1): izin **-wx** diterjemahkan menjadi 3 (2 + 1), dan seterusnya.

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

maksudnya adalah memberi izin kepada semua pengguna untuk mengakses file tersebut. Ini sama dengan `chmod a+x latihan1.txt`, dimana **a** berarti 'all'. Hal yang sama berlaku untuk *grup* (g) dan *other* (o).

Perintah lain yang berguna untuk merubah kepemilikan berkas pada Linux adalah `chown`. Format untuk perintah ini adalah:

```bash
chown user[:group] namafile
```
Perintah di atas akan merubah owner untuk file `namafile` menjadi `user` pada grup `group`. Selain file, perintah ini juga dapat digunakan untuk merubah kepemilikan sebuah folder atau direktori. Untuk kasus ini, flag `-R` berguna untuk merubah kepemilikan sebuah direktori secara rekursif, yaitu sekaligus merubah seluruh subdirektory dan berkas yang ada di dalamnya.

```bash
chown -R user[:group] direktori
```

Sebagai latihan untuk sesi ini, buat user kedua, kemudian rubah akses pada file `latihan1.txt` yang sudah dibuat sebelumnya agar user lain tidak dapat membaca file tersebut. Apa pengaruhnya apabila user pertama hendak mengakses file tersebut?


```{admonition} Catatan
Penggunaan DAC (*Discretionary Access Control*) seperti di atas akan lebih baik apabila dilengkapi dengan pengaturan ACL (*Access Control List*) atau SELinux pada distribusi seperti Centos untuk manajemen berkas pada server. 
```


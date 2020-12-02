# Linux untuk WebServer

Linux merupakan salah satu sistem operasi yang paling banyak digunakan untuk server, karena kemampuan enterprise dan biaya yang murah (bahkan gratis). Atas alasan itulah, Linux banyak dijumpai pada berbagai server, baik dalam skala besar maupun kecil.  Pada bagian ini akan dilakukan pengaturan Linux untuk webserver 


## Aplikasi Web Server
Sebuah aplikasi webserver berguna untuk mempublikasi file lokal agar dapat diakses melalui jaringan. Sebagai contoh, halaman HTML yang dibuat di komputer belum akan dapat diakses secara luas apabila tidak dipasang pada aplikasi webserver yang dapat mempublikasi data ini. 
Terdapat banyak aplikasi webserver yang tersedia dengan masing-masing bahasa yang melandasinya. berikut beberapa diantaranya:
* Apache 
* Tomcat
* Flask
* Django
* NodeJS
* Nginx
  
Apache adalah salah satu webserver berbasis PHP yang paling sering digunakan. Cara kerja Apache adalah seperti berikut:

![](img/2020-12-02-10-44-11.png)

Dengan Apache, maka berkas yang tersimpan pada komputer akan dapat dionlinekan dengan pengaturan tertentu. Pengaturan yang dimaksud meliputi pengaturan keamanan, virtual host, proxy, dan lain sebagainya.



## Menggunakan Apache

Pada latihan ini akan dilakukan instalasi dan konfigurasi Apache untuk publikasi data dalam bentuk HTML sederhana.

### Instalasi Apache 

Lakukan langkah berikut untuk melakukan instalasi Apache pada sistem Ubuntu WSL:

1. Update basisdata aplikasi di Ubuntu
   ```bash
    sudo apt update
    ```
2. Instalasi Apache2
    ```bash
    sudo apt install apache2
    ```
3. Pengaturan firewall. Firewall berfungsi untuk 'mencegat' terjadinya  transfer data antara sistem lokal dengan jaringan internet. Pengaturan ini diperlukan agar apache diizinkan untuk mengakses port yang diperlukan untuk berkomunikasi dengan dunia luar

    ```bash
    sudo ufw allow 'Apache'
    ```

    Selanjutnya periksa status `ufw` menggunakan perintah:

    ```bash
    sudo ufw status
    ```

    Apabila keluarannya seperti berikut, artinya port berhasil dibuka:

    ```
    Output
    Status: active

    To                         Action      From
    --                         ------      ----
    OpenSSH                    ALLOW       Anywhere                  
    Apache                     ALLOW       Anywhere                  
    OpenSSH (v6)               ALLOW       Anywhere (v6)             
    Apache (v6)                ALLOW       Anywhere (v6)
    ```

    
4. Jalankan Apache setelah instalasi

    ```bash
    sudo service apache2 start
    ```
    Periksa apakah Apache sudah dijalankan oleh *Service*

    ```bash
    sudo service apache2 status
    ```

    Apabila status menunjukkan 'running', artinya webserver Apache sudah berhasil dijalankan
    ![](img/2020-12-02-10-56-11.png)

5. Buka Apache pada browser pada port 80

   ![](img/2020-12-02-10-57-55.png)

   Apabila halaman Apache Ubuntu sudah terbuka, artinya instalasi Apache berhasil dengan baik    


### Konfigurasi Apache


### Membuat Website sederhana



## Tomcat sebagai Servlet Aplikasi







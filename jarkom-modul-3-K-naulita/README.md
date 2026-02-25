[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/e_s827HM)
| Name               | NRP        | Kelas |
| -----------------  | ---------- | :----: |
| Kartika Nana Naulita | 5025241021 | A     |



## Put your topology config image here!

![Foto](https://i.imgur.com/rFZ9aId.png)

## Put your GNS3 Project file here!

[GNS3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-3-K-naulita/blob/main/jarkom3.gns3project)

<br>

## Soal 1

> Setup Topo

> _Document the results of the subnet grouping that has been created._

**Answer:**

- Screenshot
  `DNS Master`  
  ![Foto](https://i.imgur.com/K65EikJ.png)
  
  `DNS Slave`  
  ![Foto](https://i.imgur.com/UMPmyEs.png)  

  `Client`  
  ![Foto](https://i.imgur.com/pHJThxU.png)  
  ![Foto](https://i.imgur.com/3lIe1OF.png)  
  ![Foto](https://i.imgur.com/WbcCw2o.png)

  `Web Server`  
  ![Foto](https://i.imgur.com/dPyxpwb.png)  
  ![Foto](https://i.imgur.com/YWRSMTq.png)  
  ![Foto](https://i.imgur.com/fNlujzv.png)

  `Reverse Proxy`  
  ![Foto](https://i.imgur.com/OsjKLR3.png)  

- Explanation

  `Konfigurasikan agar semua node mendapatkan IP Statis dengan cara menambahkan pada configuration, pembagian IP berdasarkan prefix "10.144.x.y" dengan x adalah kompleks/ subnet sesuai dengan soal dan y adalah bebas (dalam hal ini saya urutkan agar lebih mudah untuk diingat).`
  
  `Renoir (DNS Master)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.3.2
    netmask 255.255.0.0
    gateway 10.14.3.1
  ```
  
  `Verso (DNS Slave)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.3.3
    netmask 255.255.0.0
    gateway 10.14.3.1
  ```
  
  `Esquie (Client)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.5.2
    netmask 255.255.0.0
    gateway 10.14.5.1
    dns-nameserver 10.14.3.2  10.14.3.3
  ```
  
  `Monocco (Client)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.5.3
    netmask 255.255.0.0
    gateway 10.14.5.1
    dns-nameserver 10.14.3.2  10.14.3.3
  ```
  
  `Maelle (Client)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.5.4
    netmask 255.255.0.0
    gateway 10.14.5.1
    dns-nameserver 10.14.3.2  10.14.3.3
  ```
  
  `Lune (Web Server)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.2.2
    netmask 255.255.0.0
    gateway 10.14.2.1
  ```
  
  `Sciel (Web Server)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.2.3
    netmask 255.255.0.0
    gateway 10.14.2.1
  ```
  
  `Gustave (Web Server)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.2.4
    netmask 255.255.0.0
    gateway 10.14.2.1
  ```
  
  `Alicia (Reverse Proxy)`
   ```bash
  auto eth0
  iface eth0 inet static
    address 10.14.4.2
    netmask 255.255.0.0
    gateway 10.14.4.1
  ```
<br>

## Soal 2

> Buatlah konfigurasi untuk domain 
> **lune33.com** → ke IP node Lune , 
> **sciel33.com** → ke IP node Sciel ,
> **gustave33.com** → ke IP node Gustave 
> pada DNS Master Renoir. Kemudian konfigurasikan node Verso sebagai DNS Slave yang bekerja untuk DNS Master Renoir.

> _Dns Configuration , on  the DNS Master (Renoir)_
> _lune33.com → IP of node Lune ,_
> _sciel33.com → IP of node Sciel ,_
> _gustave33.com → IP of node Gustave_
> _Configure Verso as the DNS Slave that works with DNS Master Renoir._

**Answer:**

- Screenshot
  
  ![Foto](https://i.imgur.com/CTFJlIo.png)  
  ![Foto](https://i.imgur.com/WTxm1aV.png)  
  ![Foto](https://i.imgur.com/ASnFr1Z.png)

  `Hasil transfer file dari Renoir ke Verso`
  
  ![Foto](https://i.imgur.com/JQXXq4m.png)  
  `Foto yang dilampirkan hanya 3 karena bukti sukses ketika DNS Slave berhasil menggantikan DNS Master adalah ketika semuanya bisa ping sebagaimana DNS Master dijalankan (hasilnya sama).`
  
- Explanation

  `Mulai dari setting Renoir sebagai DNS Master adalah server utama yang menyimpan dan mengelola data asli (authoritative) untuk satu atau lebih domain. Lalu lakukan ini : `
  
  `nano /etc/bind/named.conf.local`
  ```bash
  zone "lune33.com" {
    type master;
    file "/etc/bind/jarkom/lune33.com";
    allow-transfer { 10.14.3.3; };  
    also-notify { 10.14.3.3; };
  };

  zone "sciel33.com" {
      type master;
      file "/etc/bind/jarkom/sciel33.com";
      allow-transfer { 10.14.3.3; };
      also-notify { 10.14.3.3; };
  };

  zone "gustave33.com" {
      type master;
      file "/etc/bind/jarkom/gustave33.com";
      allow-transfer { 10.14.3.3; };
      also-notify { 10.14.3.3; };
  };
  ```
  `Berfungsi untuk mendefinisikan tiga zona utama, yaitu lune33.com, sciel33.com, dan gustave33.com, yang masing-masing menunjuk ke file konfigurasi zona di folder /etc/bind/jarkom/. Setiap zona menggunakan tipe master, menandakan bahwa Renoir bertanggung jawab penuh sebagai pengelola utama domain-domain tersebut. Perintah allow-transfer dan also-notify dengan alamat IP 10.14.3.3 digunakan untuk memberikan izin dan notifikasi kepada Verso sebagai DNS Slave, agar Verso dapat menyalin data zona dari Renoir secara otomatis setiap kali terjadi perubahan. Dengan konfigurasi ini, Renoir menjadi pusat pengelolaan domain, sementara Verso bertugas sebagai cadangan untuk menjaga ketersediaan layanan DNS.`
  
  `Selanjutnya untuk membuat konfigurasi zona utama (master zone) untuk tiga domain, yaitu lune33.com, sciel33.com, dan gustave33.com. Setiap domain akan diarahkan ke IP node masing-masing.`

  `Langkah selanjutnya (di Renoir)  :`
  
  `Buat folder baru tempat penyimpanan file konfigurasi zona domain:`
  ```bash
  mkdir /etc/bind/jarkom
  ```

  `nano /etc/bind/jarkom/lune33.com`
  ```bash
  $TTL 604800
  @   IN  SOA lune33.com. root.lune33.com. (
          2025102401 ; Serial
          604800 ; Refresh
          86400  ; Retry
          2419200 ; Expire
          604800 ) ; Negative Cache TTL
  ;
  @   IN  NS  lune33.com.
  @   IN  A   10.14.2.2
  ```
  
  `nano /etc/bind/jarkom/sciel33.com`
  ```bash
  $TTL 604800
  @   IN  SOA sciel33.com. root.sciel33.com. (
          2025102401
          604800
          86400
          2419200
          604800 )
  ;
  @   IN  NS  sciel33.com.
  @   IN  A   10.14.2.3
  ```
  
  `nano /etc/bind/jarkom/gustave33.com`
  ```bash
  $TTL 604800
  @   IN  SOA gustave33.com. root.gustave33.com. (
          2025102401
          604800
          86400
          2419200
          604800 )
  ;
  @       IN  NS  gustave33.com.
  @       IN  A   10.14.2.4
  ```
  `Setelah semua file zona dibuat, restart service BIND agar konfigurasi diterapkan:`
  ```bash
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `Selanjutnya dilakukan konfigurasi DNS Master pada node Renoir dan DNS Slave pada node Verso. DNS Master akan mengelola tiga domain utama (lune33.com, sciel33.com, gustave33.com) dan melakukan delegasi subdomain expedition.gustave33.com ke DNS Slave.`
  
  `Buat folder baru untuk menyimpan file konfigurasi zona domain:`
  ```bash
  mkdir /etc/bind/jarkom
  ```
  
  `Konfigurasi zona di /etc/bind/named.conf.local:`
  ```bash
   zone "lune33.com" {
      type slave;
      masters { 10.14.3.2; }; 
      file "/var/lib/bind/lune33.com";
  };
  
  zone "sciel33.com" {
      type slave;
      masters { 10.14.3.2; };
      file "/var/lib/bind/sciel33.com";
  };
  
  zone "gustave33.com" {
      type slave;
      masters { 10.14.3.2; };
      file "/var/lib/bind/gustave33.com";
  };
  ```
  `Kemudian lakukan ini untuk transfer file dari DNS Master: `
  ```bash
  ls -l /var/lib/bind
  ```  
  
  `Restart service BIND:`
  ```bash  
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```
  
  `Testing dilakukan dengan cara membuka setiap client dan melakukan konfigurasi pada client untuk memastikan DNS Master (Renoir) dan DNS Slave (Verso) berfungsi dengan baik. Dengan mengedit file /etc/resolv.conf, client diarahkan untuk menggunakan Verso (10.14.3.2) sebagai DNS utama dan Renoir (10.14.3.3) sebagai cadangan. Setelah itu, dilakukan pengujian menggunakan perintah ping ke domain lune33.com, sciel33.com, dan gustave33.com untuk memastikan domain dapat diresolusikan dengan benar oleh DNS server.`

  `nano /etc/resolv.conf`
  ```bash
  nameserver 10.14.3.3
  nameserver 10.14.3.2
  ```

  `Testing : (matikan prosess di Renoir sehingga hanya Verso yang menyala, dengan cara pkill named di Renoir)`
  ```bash
  ping lune33.com
  ping sciel33.com
  ping gustave33.com
  ```
  
## Soal 3

> Tambahkan subdomain alias berupa exp.lune33.com yang mengarah ke alamat lune33.com dan exp.sciel33.com yang mengarah ke alamat sciel33.com (HINT: CNAME). Selain itu, tambahkan konfigurasi untuk melakukan reverse DNS lookup untuk domain gustave33.com

> _Subdomain Configuration,_ 
> _Add alias subdomains (HINT: CNAME)._
> _exp.lune33.com → alias to lune33.com_
> _exp.sciel33.com → alias to sciel33.com_
> _Also, configure reverse DNS lookup for the domain gustave33.com._

**Answer:**

- Screenshot
  
  ![Foto](https://i.imgur.com/q5c7Ax3.png)
  ![Foto](https://i.imgur.com/LONf722.png)
  ![Foto](https://i.imgur.com/WE5VQHy.png)

  `Foto yang dilampirkan hanya 3 karena bukti sukses ketika DNS Slave berhasil menggantikan DNS Master adalah ketika semuanya bisa ping sebagaimana DNS Master dijalankan (hasilnya sama).`

- Explanation

  `Pada tahap ini dilakukan penambahan konfigurasi untuk subdomain dan reverse DNS. Subdomain "exp" ditambahkan sebagai alias (CNAME) pada domain utama lune33.com dan sciel33.com agar dapat diakses melalui nama pendek. Selain itu, dilakukan juga konfigurasi delegasi subdomain expedition.gustave33.com pada DNS Slave (Verso) yang telah didefinisikan sebelumnya di DNS Master. Sebagai pelengkap, dibuat zona reverse untuk gustave33.com agar IP address dapat di-resolve kembali menjadi nama domain. Edit file zona lune33.com dan sciel33.com pada Renoir untuk menambahkan subdomain exp.`

  `nano /etc/bind/jarkom/lune33.com `
  ```bash
  $TTL 604800
  @   IN  SOA lune33.com. root.lune33.com. (
          2025102402 ; Serial
          604800 ; Refresh
          86400  ; Retry
          2419200 ; Expire
          604800 ) ; Negative Cache TTL
  ;
  @   IN  NS  lune33.com.
  @   IN  A   10.14.2.2
  exp IN  CNAME lune33.com.
  ```

  `nano /etc/bind/jarkom/sciel33.com`
  ```bash
  $TTL 604800
  @   IN  SOA sciel33.com. root.sciel33.com. (
          2025102402
          604800
          86400
          2419200
          604800 )
  ;
  @   IN  NS  sciel33.com.
  @   IN  A   10.14.2.3
  exp IN  CNAME sciel33.com.
  ```
  `Restart service BIND di Renoir agar perubahan diterapkan:`
  ```bash
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `Edit file zona domain utama gustave33.com agar subdomain expedition didelegasikan ke DNS Slave Verso.`
  
  `nano /etc/bind/jarkom/gustave33.com`
  ```bash
  $TTL 604800
  @   IN  SOA gustave33.com. root.gustave33.com. (
          2025102402
          604800
          86400
          2419200
          604800 )
  ;
  @       IN  NS  gustave33.com.
  @       IN  A   10.14.2.4
  expedition  IN  NS  verso.gustave33.com.  
  verso       IN  A   10.14.3.2
  <br>
  ```
  
  `Karena subdomain expedition.gustave33.com telah didelegasikan dari Renoir, maka perlu dibuat file zona di DNS Slave (Verso). Artinya, pengelolaan DNS untuk subdomain expedition.gustave33.com akan diserahkan sepenuhnya kepada Verso. Delegasi ini dilakukan agar jika subdomain memerlukan konfigurasi tambahan, pengelolaannya dapat dilakukan di DNS Slave tanpa mengubah konfigurasi di DNS Master.`
  
  `nano /etc/bind/jarkom/expedition.gustave33.com`
  ```bash
  $TTL 604800
  @       IN      SOA     expedition.gustave33.com. root.expedition.gustave33.com. (
                          2025102101 ; Serial
                          604800     ; Refresh
                          86400      ; Retry
                          2419200    ; Expire
                          604800 )   ; Negative Cache TTL
  ;
  @       IN      NS      expedition.gustave33.com.
  @       IN      A       10.14.2.3  
  ```

  `Untuk memungkinkan resolusi IP ke nama domain (reverse lookup), buat file zona reverse 2.14.10.in-addr.arpa.`
  
  `nano /etc/bind/jarkom/2.14.10.in-addr.arpa`
  ```bash
  $TTL 604800
  @       IN      SOA     gustave33.com. root.gustave33.com. (
                          2025102102 ; Serial
                          604800     ; Refresh
                          86400      ; Retry
                          2419200    ; Expire
                          604800 )   ; Negative Cache TTL
  ;
  @       IN      NS      gustave33.com.
  4       IN      PTR     gustave33.com.
  ```

   `Restart service BIND di Verso agar perubahan diterapkan:`
  ```bash
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `Testing : (pada client)`
  ```bash
  ping exp.lune33.com
  ping exp.sciel33.com
  ping expedition.gustave33.com
  ```
<br>

## Soal 4

> Buatlah subdomain berupa expedition.gustave33.com dan delegasikan subdomain tersebut dari Renoir ke Verso dengan alamat IP tujuan adalah node Gustave. Kemudian, matikan Renoir dan coba lakukan ping ke semua domain dan subdomain yang telah dikonfigurasikan pada nomor 2, 3, dan 4.

> _Create a subdomain expedition.gustave33.com and delegate it from Renoir to Verso, with the target IP being node Gustave.Then, turn off Renoir and try pinging all domains and subdomains configured in tasks 2, 3, and 4 to verify delegation works correctly._

**Answer:**

- Screenshot
  
  ![Foto](https://i.imgur.com/CTFJlIo.png)  
  ![Foto](https://i.imgur.com/WTxm1aV.png)  
  ![Foto](https://i.imgur.com/ASnFr1Z.png)
  ![Foto](https://i.imgur.com/q5c7Ax3.png)
  ![Foto](https://i.imgur.com/LONf722.png)
  ![Foto](https://i.imgur.com/WE5VQHy.png)
  ![Foto](https://i.imgur.com/1vZZasu.png)
  ![Foto](https://i.imgur.com/Ynumkn6.png)
  ![Foto](https://i.imgur.com/tMjVUji.png)

- Explanation

  `Tahap ini bertujuan untuk memastikan bahwa konfigurasi DNS Slave (Verso) dapat berfungsi menggantikan DNS Master (Renoir) ketika DNS Master sedang tidak aktif. Dengan kata lain, layanan DNS tetap berjalan dan seluruh domain maupun subdomain masih dapat diakses walaupun Renoir dimatikan. Selanjutnya, lakukan pengujian awal untuk memastikan semua domain masih dapat diakses saat DNS Master aktif.`

`Setelah pengujian awal berhasil, matikan layanan BIND pada DNS Master (Renoir) untuk mensimulasikan kondisi server utama down.`  
```bash
pkill named
```
`Kemudian, ulangi pengujian yang sama dari sisi client. Jika konfigurasi DNS Slave telah benar, seluruh domain dan subdomain tetap dapat di-resolve dan diping tanpa kendala walaupun Renoir sudah dimatikan. Hal ini menunjukkan bahwa DNS Slave (Verso) berhasil mengambil alih peran sebagai penyedia layanan DNS sementara DNS Master tidak aktif.`  

`Testing : (pada client)`
  ```bash
  ping lune33.com
  ping sciel33.com
  ping gustave33.com
  ping exp.lune33.com
  ping exp.sciel33.com
  ping expedition.gustave33.com
  ```
<br>

## Soal 5

> Konfigurasi node Lune, Sciel, dan Gustave agar berfungsi sebagai web server Nginx yang akan menyajikan halaman profil, dimana halaman profil akan berbeda untuk setiap node. Dari folder berikut, gunakan profile_lune.html untuk menyajikan halaman profil di node Lune, profile_sciel.html untuk menyajikan halaman profil di node Sciel, dan profile_gustave.html untuk menyajikan halaman profil di node Gustave. Konfigurasikan Nginx di setiap node untuk menyimpan custom access log ke file /tmp/access.log dan error log ke file /tmp/error.log. 

> _Configure Lune, Sciel, and Gustave as Nginx web servers serving profile pages, where each node has a unique profile page:_
> _- Use profile_lune.html for Lune_
> _- Use profile_sciel.html for Sciel_
> _- Use profile_gustave.html for Gustave_
> _In each web server, Configure Nginx to store custom logs:_
> _- Access log: /tmp/access.log_
> _- Error log: /tmp/error.log_

**Answer:**

- Screenshot
  
  ![Foto](https://i.imgur.com/FpXgDde.png)
  ![Foto](https://i.imgur.com/qUnUghp.png)
  ![Foto](https://i.imgur.com/erZVa2e.png)

  `Hasil Log`
  
  ![Foto](https://i.imgur.com/CoyfFk4.png)
  ![Foto](https://i.imgur.com/OVKU8ON.png)
  ![Foto](https://i.imgur.com/0jPYIJB.png)
  
- Explanation

  `Membuat direktori yang akan digunakan untuk menyimpan file HTML (halaman profil) dari setiap server. Lakukan di setiap node (Lune, Sciel, dan Gustave)`
  `mkdir /var/www/html`

  `Membuat konfigurasi server Nginx untuk domain lune33.com, agar mengarah ke file profile_lune.html yang sudah dibuat.`
  
  `nano /var/www/html/profile_lune.html`
  ```bash
  <!DOCTYPE html>
  <html lang="en">
  <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lune</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      color: #fff;
      background: linear-gradient(270deg, #0a043c, #4a0c25, #7b1b0c, #f9a826);
      background-size: 800% 800%;
      animation: bgShift 20s ease infinite;
    }
    @keyframes bgShift {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }
    .container {
      max-width: 700px;
      margin: 4rem auto;
      background: rgba(255, 255, 255, 0.08);
      border-radius: 16px;
      padding: 2.5rem;
      box-shadow: 0 4px 20px rgba(0,0,0,0.5);
      backdrop-filter: blur(6px);
    }
    h1 {
      text-align: center;
      color: #00e5ff;
      text-shadow: 0 0 10px #00e5ff;
    }
    h2 {
      color: #ffd166;
      margin-top: 1.5rem;
    }
    p, li { line-height: 1.6; }
    ul { list-style: none; padding-left: 0; }
    li::before { content: "▹ "; color: #00e5ff; }
    footer { text-align: center; font-size: 0.85rem; color: #ccc; margin-top: 2rem; }
  </style>
  </head>
  <body>
    <div class="container">
      <h1>Lune</h1>
      <p><i>“When one falls, we continue.”</i></p>
  
      <h2>Core Expertise</h2>
      <ul>
        <li>Analysis of Ancient Technologies</li>
        <li>Equipment Calibration & Field Maintenance</li>
        <li>Defense System Deployment</li>
        <li>Data Collection & Anomaly Detection</li>
      </ul>
  
      <h2>Profile Summary</h2>
      <p>Lune is the mind behind the expedition’s technology. 
         Her understanding of ancient mechanisms and magical artifacts 
         is key to decoding the Paintress’ secrets and keeping the team operational.</p>
    </div>
  
    <footer>© 2025 Expedition 33 — For Those Who Come After</footer>
  </body>
  </html>
  ```

  `Membuat konfigurasi server Nginx untuk domain lune33.com, agar mengarah ke file profile_lune.html yang sudah dibuat.`
  
  `nano /etc/nginx/sites-available/lune`
  ```bash
  server {
    listen 80;
    server_name lune33.com;

    root /var/www/html;
    index profile_lune.html;

    access_log /tmp/access.log;
    error_log /tmp/error.log;

    location / {
        try_files /profile_lune.html =404;
    }
  }
  ```

  `ln -s mengaktifkan konfigurasi dengan membuat symbolic link ke folder sites-enabled. touch membuat file log untuk mencatat error dan akses. Dan chmod 666 memberi izin agar log bisa dibaca dan ditulis oleh semua user.`
  ```bash
  ln -s /etc/nginx/sites-available/lune /etc/nginx/sites-enabled/
  touch /tmp/access.log /tmp/error.log
  chmod 666 /tmp/access.log /tmp/error.log
  ```

  `Lakukan hal yang sama untuk Sciel dan Gustave, mulai dari membuat folder html dahulu baru kemudian isi kode .html dan buat log-nya.`
  
  `SCIEL`
  
  `Mengatur virtual host Nginx untuk domain sciel33.com, dengan root ke /var/www/html dan halaman utama profile_sciel.html.`
  `nano /var/www/html/profile_sciel.html`
  ```bash
  <!DOCTYPE html>
  <html lang="en">
  <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sciel</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      color: #fff;
      background: linear-gradient(270deg, #0a043c, #4a0c25, #7b1b0c, #f9a826);
      background-size: 800% 800%;
      animation: bgShift 20s ease infinite;
    }
    @keyframes bgShift {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }
    .container {
      max-width: 700px;
      margin: 4rem auto;
      background: rgba(255, 255, 255, 0.08);
      border-radius: 16px;
      padding: 2.5rem;
      box-shadow: 0 4px 20px rgba(0,0,0,0.5);
      backdrop-filter: blur(6px);
    }
    h1 {
      text-align: center;
      color: #00e5ff;
      text-shadow: 0 0 10px #00e5ff;
    }
    h2 {
      color: #ffd166;
      margin-top: 1.5rem;
    }
    p, li { line-height: 1.6; }
    ul { list-style: none; padding-left: 0; }
    li::before { content: "▹ "; color: #00e5ff; }
    footer { text-align: center; font-size: 0.85rem; color: #ccc; margin-top: 2rem; }
  </style>
  </head>
  <body>
    <div class="container">
      <h1>Sciel</h1>
      <p><i>“Tomorrow comes.”</i></p>
  
      <h2>Core Expertise</h2>
      <ul>
        <li>Stealth and Infiltration Tactics</li>
        <li>Long-Range Surveillance</li>
        <li>Navigation and Terrain Mapping</li>
        <li>Rapid Response & Target Acquisition</li>
      </ul>
  
      <h2>Profile Summary</h2>
      <p>Sciel serves as the eyes and ears of Expedition 33. 
         Agile and perceptive, he scouts ahead, tracks enemy movement, 
         and secures safe passage before every major confrontation.</p>
    </div>
  
    <footer>© 2025 Expedition 33 — For Those Who Come After</footer>
  </body>
  </html>
  ```
  `nano /etc/nginx/sites-available/sciel`
  ```bash
    server {
        listen 80;
        server_name sciel33.com;
    
        root /var/www/html;
        index profile_sciel.html;
    
        access_log /tmp/access.log;
        error_log /tmp/error.log;
    
        location / {
            try_files $uri $uri/ =404;
        }
    }
  ```
  
  ```bash
  ln -s /etc/nginx/sites-available/sciel /etc/nginx/sites-enabled/
  ```
  ```bash
  touch /tmp/access.log /tmp/error.log
  chmod 666 /tmp/access.log /tmp/error.log
  ```

  `GUSTAVE`
  `nano /var/www/html/profile_gustave.html`
  ```bash
  <!DOCTYPE html>
  <html lang="en">
  <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gustave</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      color: #fff;
      background: linear-gradient(270deg, #0a043c, #4a0c25, #7b1b0c, #f9a826);
      background-size: 800% 800%;
      animation: bgShift 20s ease infinite;
    }
    @keyframes bgShift {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }
    .container {
      max-width: 700px;
      margin: 4rem auto;
      background: rgba(255, 255, 255, 0.08);
      border-radius: 16px;
      padding: 2.5rem;
      box-shadow: 0 4px 20px rgba(0,0,0,0.5);
      backdrop-filter: blur(6px);
    }
    h1 {
      text-align: center;
      color: #00e5ff;
      text-shadow: 0 0 10px #00e5ff;
    }
    h2 {
      color: #ffd166;
      margin-top: 1.5rem;
    }
    p, li {
      line-height: 1.6;
    }
    ul {
      list-style: none;
      padding-left: 0;
    }
    li::before {
      content: "▹ ";
      color: #00e5ff;
    }
    footer {
      text-align: center;
      font-size: 0.85rem;
      color: #ccc;
      margin-top: 2rem;
    }
  </style>
  </head>
  <body>
    <div class="container">
      <h1>Gustave</h1>
      <p><i>“For those who come after. Right?”</i></p>
  
      <h2>Core Expertise</h2>
      <ul>
        <li>Tactical Combat Planning</li>
        <li>Frontline Leadership & Morale Management</li>
        <li>Heavy Weapon Proficiency</li>
        <li>Risk Assessment & Survival Techniques</li>
      </ul>
  
      <h2>Profile Summary</h2>
      <p>Gustave is a battle-hardened veteran and the backbone of Expedition 33. 
         With experience from countless missions, he oversees every tactical decision 
         made in the war against the Paintress.</p>
    </div>
  
    <footer>© 2025 Expedition 33 — For Those Who Come After</footer>
  </body>
  </html>
  ```
  
  `nano /etc/nginx/sites-available/gustave`
  ```bash
  server {
    listen 80;
    server_name gustave33.com;

    root /var/www/html;
    index profile_gustave.html;

    access_log /tmp/access.log;
    error_log /tmp/error.log;

    location / {
        try_files $uri $uri/ =404;
    }
    }
  ```
   ```bash
  ln -s /etc/nginx/sites-available/gustave /etc/nginx/sites-enabled/
  ```
  ```bash
  touch /tmp/access.log /tmp/error.log
  chmod 666 /tmp/access.log /tmp/error.log
  ```

  `Pada setiap node (Lune, Sciel, dan Gustave), tambahkan hosts sehingga ketika di curl, client memahami bahwa link tersebut mengarah ke IP mana/ memetakan nama domain ke IP address masing-masing server agar dapat diakses langsung tanpa DNS eksternal.`
  `nano /etc/hosts`
  ```bash
  10.14.2.2 lune33.com
  10.14.2.3 sciel33.com
  10.14.2.4 gustave33.com
  ```

  `Restart :`
  ```bash
  pkill nginx
  nginx
  service nginx status
  ```

  `Testing : (Pada client untuk menguji apakah setiap domain menampilkan halaman profil yang sesuai dengan konfigurasi Nginx.)`
  ```bash
  curl lune33.com 
  curl sciel33.com
  curl gustave33.com
  ```

  `Testing : (Pada Node Lune, Sciel, dan Gustave untuk melihat catatan aktivitas (akses dan error) untuk memastikan bahwa setiap request dari client tercatat dengan benar di log server.)`
  ```bash
  cat /tmp/error.log
  cat /tmp/access.log
  ```
<br>

## Soal 6

> Setelah website berhasil dideploy pada masing-masing node web server dan halaman dapat menampilkan profil yang sesuai,  buatlah custom access log ke file /tmp/access.log di masing-masing node web server menggunakan format log tertentu seperti di bawah:
> - Tanggal dan waktu akses dalam format standar log.
> - Nama node yang sedang diakses.
> - Alamat IP klien yang mengakses website.
> - Metode HTTP dan URI yang diakses oleh klien.
> - Status respons HTTP yang diberikan oleh server.
> - Jumlah byte yang dikirimkan dalam respons.
> - Waktu yang dihabiskan oleh server untuk menangani permintaan.
> - Contoh format log yang sesuai:
>   [01/Oct/2024:11:30:45 +0000] Jarkom Node Lune Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds

> _After successfully deploying each website and verifying the correct profile page is displayed, create a custom access log in /tmp/access.log on each web server using the following format:_
> _- Date and time of access (standard log format)_
> _- Name of the node being accessed_
> _- IP address of the client accessing the website_
> _- HTTP method and URI accessed by the client_
> _- HTTP response status code_
> _- Number of bytes sent in the response_
> _- Time taken by the server to process the request_
> _- Example Log Format:_
> _[01/Oct/2024:11:30:45 +0000] Jarkom Node Lune Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds_

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/Lq770fX.png)
  ![Foto](https://i.imgur.com/8vC57dt.png)
  ![Foto](https://i.imgur.com/76jiTAN.png)

- Explanation

  `Edit pada "nano /etc/nginx/sites-available/ ... (untuk sedtiap node" sehingga bisa custom log sesuai dengan permintaan soal. Sehingga menjadi sebagai berikut :`
  
  `nano /etc/nginx/sites-available/lune`
  ```bash
  log_format custom_lune '[$time_local] Jarkom Node Lune Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';

  server {
      listen 80;
      server_name lune33.com;

    root /var/www/html;
    index profile_lune.html;

    access_log /tmp/access.log custom_lune;
    error_log /tmp/error.log;

    location / {
        try_files $uri $uri/ =404;
    }
  }
  ```

  `nano /etc/nginx/sites-available/sciel`
  ```bash
  log_format custom_sciel '[$time_local] Jarkom Node Sciel Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
  
  server {
      listen 80;
      server_name sciel33.com;
  
      root /var/www/html;
      index profile_sciel.html;
  
      access_log /tmp/access.log custom_sciel;
      error_log /tmp/error.log;
  
      location / {
          try_files $uri $uri/ =404;
      }
  }
  ```
  
  `nano /etc/nginx/sites-available/gustave`
  ```bash
  log_format custom_gustave '[$time_local] Jarkom Node Gustave Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
  
  server {
      listen 80;
      server_name gustave33.com;
  
      root /var/www/html;
      index profile_gustave.html;
  
      access_log /tmp/access.log custom_gustave;
      error_log /tmp/error.log;
  
      location / {
          try_files $uri $uri/ =404;
      }
  }
  ```
  
    `Kemudian restart kembali dengan cara:`
    ```bash
    pkill nginx
    nginx
    service nginx status
    ```
  
    `Testing : (Pada Node Lune, Sciel, dan Gustave untuk melihat catatan aktivitas akses dari tiap client untuk memastikan bahwa setiap request dari client tercatat dengan benar di log server.)`
    ```bash
    cat /tmp/access.log
    ```
<br>

## Soal 7

> Gustave merupakan web server yang tidak disarankan untuk dilihat oleh publik. Maka dari itu, ubahlah konfigurasi nginx sehingga halaman profil Gustave menjadi hanya bisa di akses melalui port 8080 dan 8888.

> _The Gustave web server should not be publicly accessible.
Modify the Nginx configuration so that Gustave’s profile page can only be accessed through ports 8080 and 8888._

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/Dw0nLv0.png)
  ![Foto](https://i.imgur.com/vp0cUys.png)
  ![Foto](https://i.imgur.com/aRrrMlL.png)
  ![Foto](https://i.imgur.com/vp0cUys.png)
  ![Foto](https://i.imgur.com/Gdi458M.png)

- Explanation
  `Edit lagi pada bagian nano /etc/nginx/sites-available/gustave pada node Gustave menjadi seperti di bawah ini (tambahkan listen)`
  ```bash
  log_format custom_gustave '[$time_local] Jarkom Node Gustave Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';

  server {
      listen 8080;
      listen 8888;
      server_name gustave33.com;
  
      root /var/www/html;
      index profile_gustave.html;
  
      access_log /tmp/access.log custom_gustave;
      error_log /tmp/error.log;
  
      location / {
          try_files $uri $uri/ =404;
      }
  }
  ```
  
  `Konfigurasi di atas membuat halaman profil Gustave hanya dapat diakses melalui port 8080 dan 8888, sesuai dengan permintaan soal yang menyebutkan bahwa web server Gustave tidak disarankan untuk diakses publik (port 80).
Dengan listen 8080; dan listen 8888;, Nginx hanya akan melayani permintaan pada dua port tersebut, sedangkan akses ke port default (80) tidak akan menampilkan halaman profil.`

  `Kemudian restart kembali dengan cara:`
  ```bash
  pkill nginx
  nginx
  service nginx status
  ```
  
  `Testing : (pada client)`
  ```bash
  curl http://gustave33.com:8080
  curl http://gustave33.com:8888
  curl http://gustave33.com:8000 (gagal)
  ```


<br>

## Soal 8

> Untuk mempermudah program ekspedisi, maka node Lune, Sciel, Gustave sepakat untuk membuat halaman informasi dengan konten yang sama. Maka dari itu, buatlah lagi 1 server block di dalam konfigurasi nginx yang akan menyajikan file HTML ini. Namun, mereka ingin menyajikan halaman informasi tersebut di port yang berbeda-beda, yaitu Lune menggunakan port 8000, Sciel menggunakan port 8100, dan Gustave menggunakan port 8200.

> _To simplify coordination for the expedition program, Lune, Sciel, and Gustave agree to create a shared information page with the same content. Add one more server block in each node’s Nginx configuration that serves this HTML file 
Each node should serve the information page on a different port:_
> _- Lune → port 8000_
> _- Sciel → port 8100_
> _- Gustave → port 8200_

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/DMPJIdB.png)
  ![Foto](https://i.imgur.com/dlScVsG.png)
  ![Foto](https://i.imgur.com/6uKJtF7.png)
  ![Foto](https://i.imgur.com/dlScVsG.png)
  ![Foto](https://i.imgur.com/NjSWVsn.png)
  ![Foto](https://i.imgur.com/dlScVsG.png)

- Explanation

  `Buat file HTML di semua node, kemudian isi dengan konten di bawah ini:`

  `nano /var/www/html/info.html`
  ```bash
  <!DOCTYPE html>
  <html lang="en">
  <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Expedition 33 — Mission Brief</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      color: #fff;
      background: linear-gradient(270deg, #0a043c, #4a0c25, #7b1b0c, #f9a826);
      background-size: 800% 800%;
      animation: bgShift 20s ease infinite;
    }
    @keyframes bgShift {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }
    header {
      text-align: center;
      padding: 3rem 1rem 1rem;
    }
    header h1 {
      font-size: 2.8rem;
      color: #00e5ff;
      letter-spacing: 1px;
      text-shadow: 0 0 10px #00e5ff;
    }
    header p {
      font-size: 1rem;
      color: #b5eaff;
      margin-top: 0.3rem;
    }
    .container {
      max-width: 700px;
      margin: 2rem auto 3rem;
      background: rgba(255, 255, 255, 0.08);
      border-radius: 16px;
      padding: 2rem 2.5rem;
      box-shadow: 0 4px 20px rgba(0,0,0,0.4);
      backdrop-filter: blur(6px);
    }
    h2 {
      color: #00e5ff;
      margin-top: 1.5rem;
    }
    p, li {
      line-height: 1.6;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      margin: 0.4rem 0;
    }
    strong {
      color: #ffd166;
    }
    .motto {
      text-align: center;
      margin-top: 1.5rem;
      font-style: italic;
      color: #ccc;
      opacity: 0.9;
    }
    footer {
      text-align: center;
      font-size: 0.9rem;
      color: #ddd;
      padding: 1rem;
      background: rgba(0,0,0,0.4);
    }
  </style>
  </head>
  <body>
  <header>
    <h1>Expedition 33</h1>
    <p>Mission Log #E33-00</p>
  </header>
  
  <div class="container">
    <h2>Mission Brief</h2>
    <p>Expedition 33 is a digital exploration led by <strong>Lune</strong>, <strong>Sciel</strong>, and <strong>Gustave</strong>.  
       Together, they traverse the unknown layers of the Paintress system — seeking order within chaos.</p>
  
    <h2>Active Nodes</h2>
    <ul>
      <li><strong>Lune</strong> — “When one falls, we continue.”</li>
      <li><strong>Sciel</strong> — “Tomorrow comes.”</li>
      <li><strong>Gustave</strong> — “For those who come after. Right?”</li>
    </ul>
  
    <h2>Ports</h2>
    <ul>
      <li>Lune: Port <strong>8000</strong></li>
      <li>Sciel: Port <strong>8100</strong></li>
      <li>Gustave: Port <strong>8200</strong></li>
    </ul>
  
    <div class="motto">
      “Despite the odds, Expedition 33 marches forward.”
    </div>
  </div>
  
  <footer>
    © 2025 Expedition 33 — For Those Who Come After
  </footer>
  </body>
  </html>
  ```

  `Penjelasan kode di bawah ini :listen 8000: port berbeda dari profil (80), agar bisa diakses secara terpisah. index info.html: file yang akan ditampilkan sebagai halaman informasi. Log akses dan error dipisah (info_access.log, info_error.log), supaya mudah dianalisis hanya untuk halaman info. try_files /info.html =404;: memastikan selalu menampilkan info.html di root, jika tidak ada maka 404. Fungsinya: menampilkan halaman informasi yang identik di semua node (Lune, Sciel, Gustave) tapi di port berbeda (Lune 8000, Sciel 8100, Gustave 8200). Selanjutnya, untuk di setiap node, tambahkan kode di bawah ini pada bagian bawah kode sebelumnya sehingga menjadi sebagai berikut : `


  `LUNE : nano /etc/nginx/sites-available/lune`
  ```bash
    log_format custom_lune '[$time_local] Jarkom Node Lune Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
  
  server {
      listen 80;
      server_name lune33.com;
  
      root /var/www/html;
      index profile_lune.html;
  
      access_log /tmp/access.log custom_lune;
      error_log /tmp/error.log;
  
      location / {
          try_files $uri $uri/ =404;
      }
  }
  
    server {
      listen 8000;
      server_name lune33.com;
  
      root /var/www/html;
      index info.html;
  
      access_log /tmp/info_access.log;
      error_log /tmp/info_error.log;
  
      location / {
          try_files /info.html =404;
      }
    }
  ```

  `SCIEL : nano /etc/nginx/sites-available/sciel`
  ```bash
    log_format custom_sciel '[$time_local] Jarkom Node Sciel Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
  
    server {
        listen 80;
        server_name sciel33.com;
  
      root /var/www/html;
      index profile_sciel.html;
  
      access_log /tmp/access.log custom_sciel;
      error_log /tmp/error.log;
  
      location / {
          try_files $uri $uri/ =404;
      }
    }
  
    server {
      listen 8100;
      server_name sciel33.com;
  
      root /var/www/html;
      index info.html;
  
      access_log /tmp/info_access.log custom_sciel;
      error_log /tmp/info_error.log;
  
      location / {
          try_files /info.html =404;
      }
    }
  ```

  `GUSTAVE : nano /etc/nginx/sites-available/gustave`
  ```bash
  log_format custom_gustave '[$time_local] Jarkom Node Gustave Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';

  server {
      listen 8080;
      listen 8888;
      server_name gustave33.com;
  
      root /var/www/html;
      index profile_gustave.html;
  
      access_log /tmp/access.log custom_gustave;
      error_log /tmp/error.log;
  
      location / {
          try_files $uri $uri/ =404;
      }
  }
  
  server {
    listen 8200;
    server_name gustave33.com;

    root /var/www/html;
    index info.html;

    access_log /tmp/info_access.log custom_gustave;
    error_log /tmp/info_error.log;

    location / {
        try_files /info.html =404;
    }
  }
  ```

  `Kemudian restart kembali dengan cara:`
  ```bash
  pkill nginx
  nginx
  service nginx status
  ```

  `Testing : (di semua client)`
  ```bash
  curl http://lune33.com:8000
  curl http://sciel33.com:8100
  curl http://gustave33.com:8200
  ```
  
<br>

## Soal 9

> Untuk mempermudah akses ke profil tiap anggota ekspedisi, buatlah 1 domain lagi yaitu "expeditioners.com" yang akan mengarah ke Alicia. Lalu, untuk mencegah overload dari salah satu web server, konfigurasikan reverse proxy Alicia agar bisa forward request ke server yang sesuai berdasarkan URL profile yang diminta oleh klien dengan ketentuan sebagai berikut:
> -  Request untuk “expeditioners.com/profil_lune” harus dialihkan ke halaman profil web server Lune.
> -  Request untuk “expeditioners.com/profil_sciel” harus dialihkan ke halaman profil web server Sciel.
> -  Request untuk “expeditioners.com/profil_gustave” harus dialihkan ke halaman profil web server Gustave.
> Jika terdapat request ke URL selain profil yang ditentukan, reverse proxy akan mengalihkan ke halaman informasi pada web server Lune.

> _To make it easier to access each member’s profile, create a new domain “expeditioners.com” that points to Alicia. "
Configure Alicia’s reverse proxy (Nginx) to forward requests to the correct web server based on the requested URL, with the following rules:_
> _- Request URL expeditioners.com/profil_lune, Forward To Lune’s profile page_
> _- Request URL expeditioners.com/profil_sciel, Forward To Sciel’s profile page_
> _- Request URL expeditioners.com/profil_gustave, Forward To Gustave’s profile page_
> _- Any other URL, Forward To Lune’s information page_

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/aPJWXXf.png)
  ![Foto](https://i.imgur.com/wcUL6Bn.png)
  ![Foto](https://i.imgur.com/gRoVm3w.png)
  ![Foto](https://i.imgur.com/kx9oQ3D.png)
  ![Foto](https://i.imgur.com/oTbBulk.png)
  ![Foto](https://i.imgur.com/EmskIym.png)
  ![Foto](https://i.imgur.com/JYW1ghi.png)
  ![Foto](https://i.imgur.com/jMZFWPN.png)
  ![Foto](https://i.imgur.com/USDmtxb.png)
  ![Foto](https://i.imgur.com/GV5WQtv.png)

- Explanation

  `Untuk itu, digunakan reverse proxy pada server Alicia. Konfigurasi Nginx di Alicia dibuat agar request yang masuk ke URL tertentu dialihkan ke web server yang sesuai: request ke /profil_lune diteruskan ke server Lune, request ke /profil_sciel diteruskan ke server Sciel, dan request ke /profil_gustave diteruskan ke server Gustave. Semua request selain URL profil yang ditentukan akan diarahkan ke halaman informasi pada server Lune. Pada konfigurasi ini juga digunakan proxy_set_header Host agar header host dikirim sesuai server target, sehingga Nginx pada server tujuan menampilkan halaman yang benar. Log akses dan error dicatat secara terpisah pada /tmp/expeditioners_access.log dan /tmp/expeditioners_error.log untuk memudahkan analisis.`

`Selain itu, domain expeditioners.com harus dapat di-resolve melalui DNS. Oleh karena itu, pada server Renoir dibuat konfigurasi zona master di BIND, di mana domain ini diarahkan ke IP Alicia (10.14.4.2) dengan tambahan CNAME untuk subdomain www. Konfigurasi ini mencakup SOA record, NS record, dan A record agar domain dapat dikenali di jaringan. Setelah konfigurasi DNS diperbarui, layanan BIND dihentikan sementara dan dijalankan kembali agar perubahan berlaku.`

  `ALICIA`
  
  `nano /etc/nginx/sites-available/expeditioners`
  ```bash
  server {
    listen 80;
    server_name expeditioners.com www.expeditioners.com;

    access_log /tmp/expeditioners_access.log;
    error_log /tmp/expeditioners_error.log;

    location /profil_lune {
        proxy_pass http://10.14.2.2/;      
        proxy_set_header Host lune33.com;
    }

    location /profil_sciel {
        proxy_pass http://10.14.2.3/;     
        proxy_set_header Host sciel33.com;
    }

    location /profil_gustave {
        proxy_pass http://10.14.2.4/profile_gustave.html;     
        proxy_set_header Host gustave33.com;
    }

    location / {
        proxy_pass http://10.14.2.2:8000;  
        proxy_set_header Host lune33.com;
    }
}
  ```

  ```bash
  ln -s /etc/nginx/sites-available/expeditioners /etc/nginx/sites-enabled/
  ```

  `Kemudian restart kembali dengan cara:`
  ```bash
  pkill nginx
  nginx
  service nginx status
  ```

  `RENOIR`
  
  `nano /etc/bind/named.conf.local (tambahkan di bawah kode sebelumnya)`
  ```bash
  zone "expeditioners.com" {
      type master;
      file "/etc/bind/jarkom/expeditioners.com";
      allow-transfer { 10.14.3.3; };      
      also-notify { 10.14.3.3; };  
  };
  ```
  
  `nano /etc/bind/jarkom/expeditioners.com`
  ```bash
  $TTL 604800
  @       IN      SOA     expeditioners.com. root.expeditioners.com. (
                          2025102801 ; Serial
                          604800     ; Refresh
                          86400      ; Retry
                          2419200    ; Expire
                          604800 )   ; Negative Cache TTL
  ;
  
  @       IN      NS      expeditioners.com.
  @       IN      A       10.14.4.2        
  www     IN      CNAME   expeditioners.com.
  ```

  `Kemudian restart kembali :`
  ```bash
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `VERSO`
  `pkill named dahulu sebelum Renoir diubah, kemudian setelah Renoir di restart kembali baru Verso dinyalakan ulang dengan restart kembali.`

<br>

## Soal 10

> Untuk mendistribusikan traffic halaman informasi, atur Reverse Proxy Alicia agar dapat membagi pekerjaan kepada web server Lune, Sciel, dan Gustave secara optimal menggunakan algoritma Round-robin. Pastikan target pembagian load merupakan halaman informasi, bukan halaman profil masing-masing web server.

> _To distribute traffic for the information page, configure the reverse proxy (Alicia) to use Round-robin load balancing between the three web servers: Lune, Sciel, and Gustave.
Ensure that only the information page is included in the load-balancing configuration - not the profile pages._

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/phdiS14.png)
  ![Foto](https://i.imgur.com/BEWcDNH.png)
  ![Foto](https://i.imgur.com/6KYI22Y.png)

- Explanation

  `Cukup tambahkan upstream di Alicia untuk mendistribusikan request halaman informasi (info.html) ke tiga server menggunakan algoritma Round-robin. Sehingga menjadi sebagai berikut : `
  
  `nano /etc/nginx/sites-available/expeditioners`
  ```bash
  upstream info_backend {
    server 10.14.2.2:8000;   
    server 10.14.2.3:8100;
    server 10.14.2.4:8200;   
  }
  
  server {
      listen 80;
      server_name expeditioners.com www.expeditioners.com;

    access_log /tmp/expeditioners_access.log;
    error_log /tmp/expeditioners_error.log;

    location /profil_lune {
        proxy_pass http://10.14.2.2/;
        proxy_set_header Host lune33.com;
    }

    location /profil_sciel {
        proxy_pass http://10.14.2.3/;
        proxy_set_header Host sciel33.com;
    }

    location /profil_gustave {
        proxy_pass http://10.14.2.4/profile_gustave.html;;
        proxy_set_header Host gustave33.com;
    }

    location / {
        proxy_pass http://info_backend/;
        proxy_set_header Host $host;
    }
    }
  ```
  
  `Kemudian restart kembali :`
    ```bash
    pkill nginx
    nginx
    service nginx status
    ```

  `Kemudian, untuk bisa mengecek apakah setiap kali pemanggilan info bisa bergantian yang mengirimkan, tambahkan kode berikut pada setiap info.html di setiap node.`
  ```bash
  LUNE
  <html><body><h1>Halo dari Lune</h1></body></html>
  
  SCIEL
  <html><body><h1>Halo dari Sciel</h1></body></html>
  
  GUSTAVE
  <html><body><h1>Halo dari Gustave</h1></body></html>
  ```

  `Kemudian restart kembali :`
    ```bash
    pkill nginx
    nginx
    service nginx status
    ```

  `Testing :`
  ```bash
  curl expeditioners.com/
  ```

<br>
  
## Problems
Terjadi perbedaan antara modul dan PPT yang digunakan pada case 3 dan 4 sehingga cukup membuat bingung sebenarnya mana yang bisa diikuti, khususnya pada soal yang topologinya tidak memakai NAT tetapi di modul tiba-tiba diminta apt-get update yang tidak mungkin berjalan. Sekaligus karena timelinenya yang cukup aneh, saya mengerjakan praktikum sebelum case 3 dan 4 sehingga makin kesulitan karena tidak memiliki pondasi.

## Revisions (if any)

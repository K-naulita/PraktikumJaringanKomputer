[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/1niUih_B)
# Daftar Anggota

| Name                  | NRP        | Kelas |
|-----------------------|------------|:------:|
| Kartika Nana Naulita  | 5025241021 |    A  |


## Put your topology config image here!
![Foto](https://i.imgur.com/zLYAdvo.png)
![Foto](https://i.imgur.com/QIqFhYG.png)  
![Foto](https://i.imgur.com/mRZZ8rm.png)  
![Foto](https://i.imgur.com/5X8zoPS.png)  
![Foto](https://i.imgur.com/cDaEVy0.png)  
![Foto](https://i.imgur.com/pkjBXeQ.png)  
![Foto](https://i.imgur.com/QAxdz4w.png)  
![Foto](https://i.imgur.com/jUWxvYP.png)  
![Foto](https://i.imgur.com/crGwzfR.png)  
![Foto](https://i.imgur.com/9pepcAW.png)  
![Foto](https://i.imgur.com/ug9BlCT.png)  
![Foto](https://i.imgur.com/St8Fxzq.png)  
![Foto](https://i.imgur.com/nc4SnUN.png)  


## Put your GNS3 Project file here!

[Project](./JARKOOO.gns3project)

<br>

## Soal 1

> Dokumentasikan hasil pengelompokan subnet yang telah dibuat.

> _Document the results of the subnet grouping that has been created._

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/fQzhChA.png)

- Explanation  
  **Kompleks 1 (Jalanan Kiri)**  
  - eth0 BlackPanther: 10.14.1.1/24  
  - eth1 IronMan: 10.14.1.2/24  
  
  **Kompleks 2 (Jalanan Kanan)**  
  - eth2 IronMan: 10.14.2.1/24  
  - eth0 BlackWidow: 10.14.2.2/24  
  
  **Kompleks 3**  
  - eth1 BlackPanther: 10.14.3.1/24  
  - CaptainAmerica: 10.14.3.2/24  
  - Falcon: 10.14.3.20 – 10.14.3.25/24  
  
  **Kompleks 4**  
  - eth2 BlackPanther: 10.14.4.1/24  
  - WinterSoldier: 10.14.4.2/24  
  - Hawkeye: 10.14.4.30 – 10.14.4.35/24  
  
  **Kompleks 5**  
  - eth2 BlackWidow: 10.14.5.1/24  
  - ScarletWitch dan Thor : 10.14.5.40 – 10.14.5.45/24 dan 10.14.5.100 – 10.14.5.105/24  
  
  **Kompleks 6**  
  - eth1 BlackWidow: 10.14.6.1/24  
  - eth0 Vision: 10.14.6.3/24  
  - Hulk: 10.14.6.50 – 10.14.6.55/24  
  
  **Kompleks 7**  
  - eth1 Vision: 10.14.7.1/24  
  - SpiderMan dan DoctorStrange: 10.14.7.60 – 10.14.7.65/24 dan 10.14.7.110 – 10.14.7.115/24  
  
<br>

## Soal 2

> Lakukan konfigurasi routing agar setiap node dapat saling berkomunikasi. Pastikan setiap router dapat mengirimkan paket ke jaringan lain melalui tabel routing yang sesuai. Sertakan bukti bahwa Falcon bisa melakukan ping ke SpiderMan, DoctorStrange, dan ScarletWitch.

> _Configure routing so that each node can communicate with each other. Ensure each router can forward packets to other networks through the appropriate routing table. Include proof that Falcon can ping SpiderMan, Doctor Strange, and ScarletWitch._

**Answer:**

- Screenshot  
  ![Foto](https://i.imgur.com/9NlLPI8.png)  
  ![Foto](https://i.imgur.com/reuNMqv.png)  

- Explanation
  
    `Pertama, mulai dari **IronMan**, pastikan bahwa internet telah tersambung dari NAT1. Kemudian atur configurationnya dengan code ini. Hal ini digunakan untuk mendaftarkan ip eth0, eth1, eth2 agar tidak berubah-ubah ketika di stop. Kemudian routing ditambahkan agar IronMan dapat meneruskan paket ke subnet lain (Kompleks 3–7) melalui gateway yang sesuai. Default route diarahkan ke 192.168.122.1 agar seluruh jaringan bisa mengakses internet. Kemudian buka console, jalankan "iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE" dan "echo "nameserver 8.8.8.8" > /etc/resolv.conf" dan "echo "nameserver 1.1.1.1" >> /etc/resolv.conf" agar sistem menggunakan server DNS Google (8.8.8.8) dan Cloudflare (1.1.1.1) untuk melakukan resolusi nama domain menjadi alamat IP. Dengan konfigurasi ini, komputer tidak hanya bisa mengakses tujuan menggunakan IP langsung (misalnya ping 8.8.8.8), tetapi juga bisa mengakses menggunakan nama domain (misalnya ping google.com) karena domain tersebut akan diterjemahkan otomatis ke IP oleh server DNS yang ditentukan.`  
    ![Foto](https://i.imgur.com/gWeVPQi.png)
    
  `Selanjutnya, ke BlackPanther. Atur configuration seperti di bawah ini. Interface lo sebagai loopback untuk komunikasi internal, kemudian menetapkan IP statis pada tiga interface utama yaitu eth0 (10.14.1.1/24) yang terhubung ke Kompleks 1, eth1 (10.14.3.1/24) yang menghubungkan ke Kompleks 3, serta eth2 (10.14.4.1/24) yang menghubungkan ke Kompleks 4. Pengaturan ini memastikan BlackPanther dapat berfungsi sebagai penghubung antar jaringan di kompleks-kompleks tersebut. Selanjutnya jalankan "echo "nameserver 8.8.8.8" > /etc/resolv.conf" dan "echo "nameserver 1.1.1.1" >> /etc/resolv.conf" agar sistem menggunakan server DNS Google (8.8.8.8) dan Cloudflare (1.1.1.1) untuk melakukan resolusi nama domain menjadi alamat IP.`
    
    ![Foto](https://i.imgur.com/VaxRZvI.png)  
  
  `Kemudian atur configurasi di CaptainAmerica seperti kode di bawah ini. Selanjutnya jalankan "apt-get update", kemudian "apt-get install isc-dhcp-server". Selanjutnya edit configurasi dhcp menggunakan "nano isc-dhcp-server" dan isi dengan code di bawah (setelah gambar). Tujuannya sebagai DHCP server, pembagian alamat IP dinamis untuk setiap kompleks. Semua subnet menggunakan DNS Google (8.8.8.8) dan Cloudflare (1.1.1.1) agar client dapat melakukan resolusi domain. Terakhir simpan (CTRL+x - CTRL+O), jalankan  "echo "nameserver 8.8.8.8" > /etc/resolv.conf" dan "echo "nameserver 1.1.1.1" >> /etc/resolv.conf" agar sistem menggunakan server DNS Google (8.8.8.8) dan Cloudflare (1.1.1.1) untuk melakukan resolusi nama domain menjadi alamat IP. serta jalankan service isc-dhcp-server restart dan service isc-dhcp-server status.`
   ![Foto](https://i.imgur.com/mRZZ8rm.png)
   ```bash
   # Falcon
  subnet 10.14.3.0 netmask 255.255.255.0 {
      range 10.14.3.20 10.14.3.25;
      option routers 10.14.3.1;
      option domain-name-servers 8.8.8.8, 1.1.1.1;
  }
  
  # Hawkey
  subnet 10.14.4.0 netmask 255.255.255.0 {
      range 10.14.4.30 10.14.4.35;
      option routers 10.14.4.1;
      option domain-name-servers 8.8.8.8, 1.1.1.1;
  }
  
  # ScarletWitch 
  subnet 10.14.5.0 netmask 255.255.255.0 {
      range 10.14.5.40 10.14.5.45;
      range 10.14.5.100 10.14.5.105;   
      option routers 10.14.5.1;
      option domain-name-servers 8.8.8.8, 1.1.1.1;
      default-lease-time 120;
  }
  
  # Hulk
  subnet 10.14.6.0 netmask 255.255.255.0 {
      range 10.14.6.50 10.14.6.55;
      option routers 10.14.6.1;
      option domain-name-servers 8.8.8.8, 1.1.1.1;
  }
  
  # SpiderMan dan Doctor
  subnet 10.14.7.0 netmask 255.255.255.0 {
      range 10.14.7.60 10.14.7.65;
      range 10.14.7.110 10.14.7.115;
      option routers 10.14.7.1;
      option domain-name-servers 8.8.8.8, 1.1.1.1;
  }
   ```

  `Kembali ke BlackPanther, setting sebagai relay. Jalankan pada console, yaitu "apt-get update", "apt-get install isc-dhcp-relay -y" dan "service isc-dhcp-relay start". Ketika "apt-get install isc-dhcp-relay -y", akan muncul pertanyaan mengenai server mana yang akan terhubung, isi dengan 10.14.3.2 (IP CaptainAmerica), selanjutnya akan muncul interfaces yang digunakan adalah eth0 eth1 eth2. Kemudian, jalankan "nano /etc/sysctl.conf" dan hapus # di depan net.ipv4.ip_forward=1, fungsinya untuk mengaktifkan ip forwarding. Kemudian, jalankan "echo "nameserver 8.8.8.8" > /etc/resolv.conf" dan "echo "nameserver 1.1.1.1" >> /etc/resolv.conf" agar sistem menggunakan server DNS Google (8.8.8.8) dan Cloudflare (1.1.1.1) untuk melakukan resolusi nama domain menjadi alamat IP. Terakhir, jalankan service isc-dhcp-relay restart. `

  `Selanjutnya lakukan hal yang sama untuk semua relay (BlackWidow dan Vision) dan ubah configurasinya jadi sebagai berikut :`
  ![Foto](https://i.imgur.com/5X8zoPS.png)  
  ![Foto](https://i.imgur.com/cDaEVy0.png)
  
  `Setelah itu, ubah configurasi semua client (Falcon, Hawkey, Thor, ScarletWitch, Hulk, SpiderMan, dan DoctorStrange) sehingga bagian : `
  
  `auto eth0`
  `iface eth0 inet dhcp`

  `bisa aktif. Menunjukkan bahwa melalui eth0, tiap client siap menerima ip secara DHCP. Lihat configurasi di bagian atas.`
  `Gunakan "ping <ip destination>" Untuk testing. Pertama cek ip tiap client menggunakan open console. Dari Falcon ke SpiderMan berarti "ping 10.14.7.61", ke DoctorStrange "ping 10.14.7.60", dan ke ScarletWitch "ping 10.14.5.41". Ip tiap client bisa diketahui dengan membuka console tiap client.`

<br>

## Soal 3

> Lakukan konfigurasi agar semua node dapat terhubung ke internet. Sertakan hasil uji coba dengan melakukan ping ke google.com dari node Falcon, CaptainAmerica, SpiderMan, dan Thor.

> _Configure all nodes to connect to the internet. Include test results by pinging google.com from the Falcon, CaptainAmerica, SpiderMan, and Thor nodes._

**Answer:**

- Screenshot  
  ![Foto](https://i.imgur.com/7ZSczOi.png)
  ![Foto](https://i.imgur.com/hZDLVie.png)
  ![Foto](https://i.imgur.com/wMslzyv.png)
  ![Foto](https://i.imgur.com/dVLLYxc.png)
  ![Foto](https://i.imgur.com/vys4XkX.png)
  
- Explanation
  
  `Pertama pastikan internet sudah bisa terhubung, gunakan "iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE" pada configuration network di IronMan. Berfungsi untuk mengaktifkan Network Address Translation (NAT) pada tabel nat, tepatnya di chain POSTROUTING (tahap setelah paket siap keluar dari router). Aturan ini membuat semua paket yang keluar melalui interface eth0 diubah source IP-nya menjadi IP milik eth0 itu sendiri. Dengan begitu, seluruh client yang berada di jaringan internal bisa menggunakan satu alamat IP publik dari router untuk mengakses internet. Alasan aturan iptables MASQUERADE dipasang di IronMan adalah karena IronMan berperan sebagai gateway utama yang menghubungkan seluruh jaringan internal (Kompleks 1–7) dengan jaringan luar atau internet melalui interface eth0.`
  
  `Selanjutnya untuk setiap router dan server, lakukan "echo "nameserver 8.8.8.8" > /etc/resolv.conf" dan "echo "nameserver 1.1.1.1" >> /etc/resolv.conf" digunakan untuk mengatur DNS resolver sistem agar menggunakan Google DNS (8.8.8.8) dan Cloudflare DNS (1.1.1.1). Dengan konfigurasi ini, komputer bisa menerjemahkan nama domain (misalnya google.com) menjadi alamat IP yang valid di internet. Tanpa pengaturan ini, sistem hanya bisa mengakses tujuan menggunakan IP langsung, tetapi tidak bisa mengakses menggunakan nama domain karena proses resolusi nama tidak berjalan. Terakhir, gunakan "ping google.com" untuk melakukan testing tiap client, jika muncul jumlah bytes pengiriman packet, maka ping dikatakan berhasil.`

<br>

## Soal 4

> Berikan Falcon alamat IP dalam rentang [Prefix IP].3.20 - [Prefix IP].3.25
> <br> </br>
> Berikan Hawkeye alamat IP dalam rentang [Prefix IP].4.30 - [Prefix IP].4.35
> <br> </br>
> Berikan Hulk alamat IP dalam rentang [Prefix IP].6.50 - [Prefix IP].6.55

<br>

> _Give Falcon an IP address in the range [IP Prefix].3.20 - [IP Prefix].4.35_
> <br> </br>
> _Give Hawkeye an IP address in the range [IP Prefix].4.30 - [IP Prefix].4.35_
> <br> </br>
> _Give Hulk an IP address in the range [IP Prefix].6.50 - [IP Prefix].6.55_

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/Y3hZp0x.png)
  ![Foto](https://i.imgur.com/j4ZVHG1.png)
  ![Foto](https://i.imgur.com/BoEVq4J.png) 

- Explanation

  `Berdasarkan konfigurasi DHCP yang saya buat di CaptainAmerica sebagai server, setiap client akan mendapatkan alamat IP sesuai dengan subnet tempatnya berada. Untuk Falcon, saya menyediakan alokasi pada subnet 10.14.3.0/24 dengan range IP 10.14.3.20 – 10.14.3.25 serta router 10.14.3.1, sehingga Falcon hanya akan menerima alamat IP dalam rentang tersebut. Sedangkan untuk Hawkey, diatur pada subnet 10.14.4.0/24 dengan range IP 10.14.4.30 – 10.14.4.35 dengan router 10.14.4.1. Dengan konfigurasi ini, pembagian alamat IP untuk Falcon dan Hawkey sudah sesuai dengan ketentuan yang diminta dan dikelola otomatis oleh server DHCP.`

<br>

## Soal 5

> Berikan ScarletWitch dan Thor alamat IP dalam rentang [Prefix IP].5.40 - [Prefix IP].5.45 dan [Prefix IP].5.100 - [Prefix IP].5.105

> _Give ScarletWitch and Thor IP addresses in the range [IP Prefix].5.40 - [IP Prefix].5.45 and [IP Prefix].5.100 - [IP Prefix].5.105_

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/YbkZBks.png)
  ![Foto](https://i.imgur.com/qC7jpAO.png) 

- Explanation

  `Berdasarkan konfigurasi DHCP pada CaptainAmerica, untuk subnet 10.14.5.0/24 saya memberikan dua alokasi rentang IP yaitu 10.14.5.40 – 10.14.5.45 dan 10.14.5.100 – 10.14.5.105 dengan gateway 10.14.5.1. Rentang pertama diperuntukkan bagi Thor, sedangkan rentang kedua untuk ScarletWitch, sehingga pembagian alamat IP diatur otomatis oleh server sesuai blok yang tersedia. Dalam pengujian, Thor mendapatkan IP 10.14.5.40 sebagai alamat pertama yang tersedia dalam rentangnya, sedangkan ScarletWitch mendapat 10.14.5.41 yang merupakan alokasi berikutnya dari DHCP server. Hal ini terjadi karena mekanisme DHCP akan memberikan alamat IP secara berurutan (sequential) dari range yang telah ditentukan, sehingga Thor dan ScarletWitch menempati urutan awal dari subnet yang telah dikonfigurasi.`

<br>

## Soal 6

> Berikan SpiderMan dan DoctorStrange alamat IP dalam rentang [Prefix IP].7.60 - [Prefix IP].7.65  dan [Prefix IP].7.110 - [Prefix IP].7.115

> _Give SpiderMan and DoctorStrange IP addresses in the ranges [IP Prefix].7.60 - [IP Prefix].7.65 and [IP Prefix].7.110 - [IP Prefix].7.115_

**Answer:**

- Screenshot

 ![Foto](https://i.imgur.com/z3REUdR.png) 
 ![Foto](https://i.imgur.com/Fg58kAN.png) 

- Explanation

  `Untuk konfigurasi pada subnet 10.14.7.0/24, saya menetapkan dua rentang alokasi IP, yaitu 10.14.7.60 – 10.14.7.65 dan 10.14.7.110 – 10.14.7.115, dengan gateway 10.14.7.1. Rentang pertama digunakan untuk SpiderMan, sementara rentang kedua diperuntukkan bagi DoctorStrange. Dengan pengaturan ini, DHCP server di CaptainAmerica akan otomatis memberikan alamat IP kepada SpiderMan dan DoctorStrange sesuai dengan blok yang telah ditentukan. Sama seperti pada kasus Thor dan ScarletWitch, pembagian IP dilakukan secara berurutan oleh server; SpiderMan akan menerima alamat dari rentang awal (misalnya 10.14.7.60), sedangkan DoctorStrange akan mendapatkan alamat dari rentang berikutnya (misalnya 10.14.7.110). Mekanisme ini memastikan setiap client hanya memperoleh IP dari pool yang sudah dikhususkan untuk mereka, sehingga manajemen jaringan lebih teratur.`

<br>

## Soal 7

> Tetapkan waktu peminjaman alamat IP pada DHCP server untuk client yang terhubung melalui Switch 2 selama 5 menit (Default), dan untuk client melalui Switch 5 selama 10 menit (Default). Tetapkan juga batas waktu peminjaman maksimal selama 2 jam.
> <br> </br>
> Tetapkan waktu peminjaman alamat IP pada DHCP server untuk client yang terhubung melalui Switch 1 dan Switch 3 selama 2 menit (Default). Tetapkan juga batas waktu peminjaman maksimal selama 100 menit.

<br>

> _Set the IP address lease period on the DHCP server for clients connected through Switch 2 to 5 minutes (default), and for clients connected through Switch 5 to 10 minutes (default). Also, set the maximum lease period to 2 hours._
> <br> </br>
> _Set the IP address lease time on the DHCP server for clients connected via Switch 1 and Switch 3 to 2 minutes (default). Also set the maximum lease time limit to 100 minutes._

**Answer:**

- Screenshot  
  `Switch 2 (Hawkey)`  
  ![Foto](https://i.imgur.com/uGEIJPc.png)   
  ![Foto](https://i.imgur.com/yPVs7Ih.png)
  
  `Switch 5 (SpiderMan dan DoctorStrange`  
  ![Foto](https://i.imgur.com/gYKuRWr.png)
  ![Foto](https://i.imgur.com/h2aju0A.png)
  ![Foto](https://i.imgur.com/uO91jxm.png)
  
  `Switch 1 (Falcon)`  
  ![Foto](https://i.imgur.com/uGEIJPc.png)  
  ![Foto](https://i.imgur.com/9QFTNed.png)
  
  `Switch 3 (Thor dan ScarletWitch)`  
  ![Foto](https://i.imgur.com/BfpXhfe.png) 
  ![Foto](https://i.imgur.com/f7rx5J6.png)
  ![Foto](https://i.imgur.com/kBNCkV0.png)  

- Explanation

  `Ubah /etc/dhcp/dhcpd.conf pada server CaptainAMerica, tambahkan default-lease time dan max-lease-time sesuai yang diminta soal. Default time menggunakan detik, sehingga untuk setiap swith :  `  
   `Switch 2 -> default : 300 dan max : 7200`  
   `Switch 5 -> default : 600 dan max : 7200`    
   `Switch 1 -> default : 120 dan max : 6000`  
   `Switch 3 -> default : 120 dan max : 6000`  
  `Kemudian simpan (CTRL+x - CTRL+O) dan jalankan service isc-dhcp-server restart dan service isc-dhcp-server status. Cek kembali tiap client (stop dan start dahulu) untuk melihat berapa IP yang didapatkan sekaligus lease timenya. Seharusnya berada di antara default sampai max time.`

<br>

## Soal 8

> Ubah konfigurasi DHCP Server agar Hawkeye, Thor, dan SpiderMan mendapatkan IP statis dengan [Prefix IP].x.5, namun masih menggunakan DHCP.

> _Change the DHCP Server configuration so that Hawkeye, Thor, and SpiderMan get static IPs with [Prefix IP].x.5, but still use DHCP._

**Answer:**

- Screenshot

  ![Foto](https://i.imgur.com/oaeQOsX.png)
  ![Foto](https://i.imgur.com/zKGpz24.png)
  ![Foto](https://i.imgur.com/U6DFBGx.png)
  ![Foto](https://i.imgur.com/h5nUnCf.png) 

- Explanation

  `Dengan mengubah konfigurasi bagian /etc/dhcp/dhcpd.conf pada server yaitu CaptainAmerica. Tambahkan code di atas pada bagian paling bawah, kemudian simpan (CTRL+x - CTRL+O) dan jalankan service isc-dhcp-server restart dan service isc-dhcp-server status. Code di atas terdiri atas hardware thernet yang berisi MAC ip dari tiap client (buka console client lalu "ip link show eth0" dn fixed-addres adalah ip baru yang diinginkan untuk bisa diberikan pada client. Lalu untuk mengecek, stop dan start client Hawkey, thor, serta SpiderMan. Ubah juga pengaturan config client, tambahkan "hwaddress ether 'MAC ip' dibagian paling bawwah kemudian simpan. Terakhir, restart client lalu open console dan akan terlihat ip mereka yang sudah terganti tetapi masih diberi oleh server (DHCP).`

<br>

## Soal 9

> Buatlah konfigurasi DHCP Failover dengan WinterSoldier sebagai DHCP server backup untuk CaptainAmerica.

> _Create a DHCP Failover configuration with WinterSoldier as the backup DHCP server for CaptainAmerica._

**Answer:**

- Screenshot    
  `CaptainAmerica`   
  ![Foto](https://i.imgur.com/0XCADug.png)
  
  `WinterSoldier`  
  ![Foto](https://i.imgur.com/wHyPdJW.png)
  ![Foto](https://i.imgur.com/Jaf1SFz.png)

  `Next code (sama baik CaptainAmerica maupun WinterSoldier)`  
  ![Foto](https://i.imgur.com/neZuq5X.png)
  ![Foto](https://i.imgur.com/uTLgbDX.png)
  ![Foto](https://i.imgur.com/BejidqQ.png)
  ![Foto](https://i.imgur.com/EXOTss0.png)
  ![Foto](https://i.imgur.com/mMCAMIy.png)
  ![Foto](https://i.imgur.com/oaeQOsX.png)

  `Hasil`
    
  ![Foto](https://i.imgur.com/9rtF6Jd.png)  
  ![Foto](https://i.imgur.com/UrwApHW.png)  
  ![Foto](https://i.imgur.com/Zp9HfwM.png)  
  ![Foto](https://i.imgur.com/kBNCkV0.png)
  ![Foto](https://i.imgur.com/7WaDulA.png)  
  ![Foto](https://i.imgur.com/0MTy6ug.png)  
  ![Foto](https://i.imgur.com/GNJaX8c.png)  

- Explanation

  `Mengubah bagian /etc/dhcp/dhcpd.conf baik pada primary maupun secondary server. Pertama, ubah di primary dengan code yang dilampirkan di atas. Tambahkan function "Failover peer" yang berisi informasi apakah server ini primary atau secondary, kemudian ip server tersebut, ip server pasangannya (server lain yang terkait, kalau primary berarti isi peer address dengan ip server secondary dan sebaliknya). Lalu ada, port TCP yang dipakai (template, 647-primary, 847-secondary). Max-response delay emmbatasi kapan max detik sebelum dianggap gagal dan Max-unacked updates berarti jumlah update informasi lease yang boleh pending sebelum dianggap gagal. MCLT (Maximum Client Lead Time) berarti waktu pemberian lease yang diberikan pada secondary, ketika primary down. Terakhir, cukup tambahkan bracket "pool" untuk tiap subnet untuk menunjukkan pembagian ip menggunakan function failover peer. Selanjutnya simpan (CTRL+x - CTRL+O) dan jalankan service isc-dhcp-server restart dan service isc-dhcp-server status.`

  `Selanjutnya setting dahulu server primary, lakukan configurasi yang sama dengan primary, cukup ganti ip address (statis) dan gateway yang sesuai (karena kompleks 4, atur dengan 4.x dan pastikan gatewaynya ewat ip BlackPanther yang di kompleks 4 yaitu 4.1. Selanjutnya lakukan setting server seperti apt-get update, apt-get install isc-dhcp-server, dan edit konfigurasi pada /etc/default/isc-dhcp-server (isi INTERFACESv4="eth0 eth1 eth2" agar bisa mendengarkan dari berbagai interfaces. Terakhir, service isc-dhcp-server restart dan service isc-dhcp-server status.`

  `Ubah configurasi /etc/default/isc-dhcp-relay dan tambahkan IP server secondary (10.14.4.2) pada SERVERS. Untuk testing, matikan primary server (isc-dhcp-server stop) dan cek tiap client apakah berhasil dapat ip dari server secndary semua (from 10.14.4.2).`

<br>

## Soal 10

> Buatlah konfigurasi agar CaptainAmerica dan WinterSoldier berjalan dengan mode Load Balancing.

> _Create a configuration so that CaptainAmerica and WinterSoldier run in Load Balancing mode._

**Answer:**

- Screenshot
  `CaptainAmerica`    
   ![Foto](https://i.imgur.com/0XCADug.png)

  `WinterSoldier`  
  ![Foto](https://i.imgur.com/Jaf1SFz.png)

  `Next code (sama baik CaptainAmerica maupun WinterSoldier)`  
  ![Foto](https://i.imgur.com/neZuq5X.png)
  ![Foto](https://i.imgur.com/uTLgbDX.png)
  ![Foto](https://i.imgur.com/BejidqQ.png)
  ![Foto](https://i.imgur.com/EXOTss0.png)
  ![Foto](https://i.imgur.com/mMCAMIy.png)
  ![Foto](https://i.imgur.com/oaeQOsX.png)  

  `CaptainAmerica`  
  ![Foto](https://i.imgur.com/bK02B9j.png)  
  ![Foto](https://i.imgur.com/2yKfeW2.png)  
  ![Foto](https://i.imgur.com/YNqdiPR.png)  
    
  `WinterSoldier`   
  ![Foto](https://i.imgur.com/xWZFaFT.png)  
  ![Foto](https://i.imgur.com/5YxTqy7.png)  
  ![Foto](https://i.imgur.com/0jQO9vP.png)  
  ![Foto](https://i.imgur.com/lBbk8vU.png)  
- Explanation

  `Pada /etc/dhcp/dhcpd.conf yaitu pada bracket failoverver peer, harus ada "split 128" agar bisa terjadi Load Balancing yaitu pembagian assignment lease dari server primary dan secondary secara 50:50. Split 128 berarti membagi setengah range (0-127) untuk primary dan sisanya (128-255) untuk secondary. Di mana nilai split di DHCP Failover sendiri di rentang 0-255. Untuk testing, jalankan service isc-dhcp-server start untuk kedua server dan cek ip tiap client. Hasilnya dari 7 client, 3 assignment lease dari CaptainAmerica (lihat from 10.14.3.2) dan 4 assignment lease dari WinterSoldier (from 10.14.4.2).`

<br>
  
## Problems
Saya terus salah paham karena harus mengikuti runtutan soal. Sehingga sejak awal dengan niat untuk testing, client saya atur memiliki ip statis padahal jika mengikuti soal 4, 5, dan 6 hasilnya bisa lebih cepat. Selain itu, saya tidak tahu mengapa antara IronMan dan NAT1 awalnya tidak bisa terhubung internetnya. Sehingga untuk melakukan apt-get-update di semua relay dan server tidak bisa dilakukan.

## Revisions (if any)

[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/aRvIU2lf)
| Name                   | NRP        | Kelas |
| ---------------------- | ---------- | :----:|
| Kartika Nana Naulita   | 5025241021 | A     |



## Put your topology config image here!

![Img](https://i.imgur.com/F5A7O7C.png)  

`Router`

![img](https://i.imgur.com/cValpo5.png)
![img](https://i.imgur.com/OtKnQMa.png)
![img](https://i.imgur.com/46gvssH.png)
![img](https://i.imgur.com/yv1VWYD.png)
![img](https://i.imgur.com/A0hCzAs.png)

`DHCP Server`

![img](https://i.imgur.com/e4gDein.png)
![img](https://i.imgur.com/Zoz53P2.png)

`DNS`

![img](https://i.imgur.com/hZ3Mi0p.png)
![img](https://i.imgur.com/wBdqkKb.png)

`Reverse Proxy`

![img](https://i.imgur.com/AfNmDNW.png)

`Web Server`

![img](https://i.imgur.com/DBx5hDl.png)
![img](https://i.imgur.com/SSMlm3A.png)

`Client`

![img](https://i.imgur.com/ApFb8BC.png)
![img](https://i.imgur.com/QblrYGE.png)
![img](https://i.imgur.com/UyHXCAe.png)

## Put your GNS3 Project file here!

[FP Jarkom](https://github.com/Praktikum-NETICS-2025/jarkom-modul-final-K-naulita/blob/main/FP%20Jarkom.gns3project)

<br>

## Soal 1

> Menggunakan metode VLSM, buatlah pembagian subnet untuk masing-masing gedung dengan cara yang seefisien mungkin!

> _Using the VLSM method, create subnets for each building as efficiently as possible!_

**Answer:**

- Screenshot

  ![Subnetting](https://github.com/user-attachments/assets/98c3e438-d7a0-4f3c-aa4e-fda1d5c6fcac)

  ![Subnetting (1)](https://github.com/user-attachments/assets/d0571588-2653-4031-aab1-46a25c4dc4f6)


- Explanation

  `Pembagian subnet dilakukan menggunakan metode VLSM (Variable Length Subnet Mask) dengan prefix utama 10.14.0.0/16, di mana ukuran subnet ditentukan berdasarkan kebutuhan host masing-masing gedung agar penggunaan alamat IP максимально efisien. Subnet dialokasikan mulai dari kebutuhan terbesar (A1 dan A2) ke yang lebih kecil untuk mencegah fragmentasi alamat dan memudahkan agregasi routing. Zona dengan kebutuhan host besar menggunakan prefix kecil (/19 dan /21), sedangkan jaringan lokal dan antar-router menggunakan prefix lebih besar hingga /30 untuk koneksi point-to-point. Gateway setiap subnet ditempatkan pada alamat host pertama untuk konsistensi desain dan kemudahan konfigurasi routing statis. Pembagian ini selaras dengan topologi jaringan pada gambar, mendukung routing hierarkis melalui Smith-Morra, Fianchetto, Lucena, Zwischenzug, dan Zugzwang, serta memungkinkan integrasi DHCP relay dan NAT dengan efisien.`

| Zona | Kebutuhan Host | Host Alokasi | Subnet            | Netmask            | Gateway (Router)         | Node / Peran Utama                                  | IP Address Penting (Fixed/Test)                  | Range IP Usable                    |
|------|----------------|--------------|-------------------|--------------------|--------------------------|-----------------------------------------------------|--------------------------------------------------|-----------------------------------|
| A1   | 5002           | 8190         | 10.14.0.0/19      | 255.255.224.0      | Smith-Morra (eth2)       | Client Group 3, Blackmar-Diemer (DHCP)                     | 10.14.0.1 (Smith-Morra), 10.14.0.10 (Black-Diemer)   | 10.14.0.1 – 10.14.31.254           |
| A2   | 1253           | 2046         | 10.14.32.0/21     | 255.255.248.0      | Smith-Morra (eth3)       | Stafford, Budapest (DHCP), Client Group 1 & 2             | 10.14.32.1 (Smith-Morra), 10.14.32.10 (Budapest)      | 10.14.32.1 – 10.14.39.254          |
| A3   | 202            | 254          | 10.14.40.0/24     | 255.255.255.0      | Zugzwang (eth1)          | Slav, Webserver-Group-2                             | 10.14.40.1 (Zugzwang), 10.14.40.3 (Slave Fixed)        | 10.14.40.1 – 10.14.40.254          |
| A4   | 102            | 126          | 10.14.41.0/25     | 255.255.255.128    | Zugzwang (eth3)          | Sicilian, Webserver-Group-1                         | 10.14.41.1 (Zugzwang), 10.14.41.5 (Sicilian Fixed)     | 10.14.41.1 – 10.14.41.126          |
| A5   | 53             | 62           | 10.14.41.128/26   | 255.255.255.192    | Lucena (eth1)            | Ponziani (DHCP Master), RuyLopez (DHCP Slave)       | 10.14.41.129 (Lucena), 10.14.41.130 (Ponziani), 10.14.41.131 (RuyLopez)       | 10.14.41.129 – 10.14.41.190        |
| A6   | 13             | 14           | 10.14.41.192/28   | 255.255.255.240    | Zugzwang (eth2)          | Caro-Kann, Alekhine, DNS Group-1                     | 10.14.41.193 (Zugzwang), 10.14.41.194 (Caro-Kann), 10.14.41.195 (Alekhine)       | 10.14.41.193 – 10.14.41.206        |
| A7   | 3              | 6            | 10.14.41.208/29   | 255.255.255.248    | Lucena (eth0)            | Switch-Pusat (Router Interconnect), Fianchetto, Zwsichenzug | 10.14.41.209 (Lucena), 10.14.41.210 (Fianchetto), 10.14.41.211 (Zwsichenzug)    | 10.14.41.209 – 10.14.41.214        |
| A8   | 3              | 6            | 10.14.41.216/29   | 255.255.255.248    | Zwischenzug (eth1)       | Petrov (Reverse Proxy)                | 10.14.41.217 (Zwischenzug), 10.14.41.218 (Petrov)                         | 10.14.41.217 – 10.14.41.222        |
| A9   | 2              | 2            | 10.14.41.224/30   | 255.255.255.252    | Fianchetto / Smith-Morra | Link Point-to-Point Router                         | 10.14.41.225 (Fianchetto), 10.14.41.226 (Smith-Morra)                      | 10.14.41.225 – 10.14.41.226        |


<br>

## Soal 2

> Konfigurasi semua router agar bisa terhubung ke semua jaringan. Gunakan static routing dan uji dengan melakukan ping dari **Budapest** ke **Alekhine** dan dari **Ponziani** ke **Sicilian**!

> _Configure all routers to connect to all networks. Use static routing and perform testing by pinging from **Budapest** to **Alekhine** and from **Ponziani** to **Sicilian**!_

**Answer:**

- Screenshot

  ![img](https://i.imgur.com/UEjfZQY.png)
  <img width="649" height="247" alt="Screenshot 2025-12-04 113108" src="https://github.com/user-attachments/assets/5fe4286c-1ddf-4178-9198-156aa72d732f" />

  

- Explanation

  `Pada tahap ini, seluruh router seperti Smith-Morra, Fianchetto, Lucena, Zwischenzug, dan Zugzwang dikonfigurasi agar dapat saling terhubung ke semua subnet dalam topologi.
Routing dilakukan menggunakan static routing, sehingga setiap router secara eksplisit mengetahui jalur menuju setiap jaringan lain.`

  `Konfigurasi ini memastikan bahwa: Budapest (A1) dapat menjangkau Alekhine (A6) melalui jalur Budapest → Smith-Morra → Fianchetto → Zugzwang → Alekhine; Ponziani (A5) dapat mengakses Sicilian (A4) melalui jalur Ponziani → Lucena → Zwischenzug → Zugzwang → Sicilian. Semua router juga mengaktifkan IP forwarding agar dapat meneruskan paket antar interface.`

  `Smith-Morra`
  ```
  auto eth0
  iface eth0 inet dhcp
  
  auto eth1
  iface eth1 inet static
      address 10.14.41.226
      netmask 255.255.255.252
  
  auto eth2
  iface eth2 inet static
      address 10.14.0.1
      netmask 255.255.224.0
  
  auto eth3
  iface eth3 inet static
      address 10.14.32.1
      netmask 255.255.248.0
  
  up ip route add 10.14.40.0/24 via 10.14.41.225 dev eth1
  up ip route add 10.14.41.0/25 via 10.14.41.225 dev eth1
  up ip route add 10.14.41.128/26 via 10.14.41.225 dev eth1
  up ip route add 10.14.41.192/28 via 10.14.41.225 dev eth1
  up ip route add 10.14.41.208/29 via 10.14.41.225 dev eth1
  up ip route add 10.14.41.216/29 via 10.14.41.225 dev eth1
  ```
  
  `Lalu lakukan :`
  ```
  apt update
  apt install iptables
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE 
  echo 1 > /proc/sys/net/ipv4/ip_forward
  ```
  
  `Fianchetto`
  ```
  auto eth0
  iface eth0 inet static
      address 10.14.41.210
      netmask 255.255.255.248
  
  auto eth1
  iface eth1 inet static
      address 10.14.41.225
      netmask 255.255.255.252
  
  up ip route add 0.0.0.0/0 via 10.14.41.226 dev eth1
  up ip route add 10.14.0.0/19 via 10.14.41.226 dev eth1
  up ip route add 10.14.32.0/21 via 10.14.41.226 dev eth1
  up ip route add 10.14.40.0/24 via 10.14.41.211 dev eth0
  up ip route add 10.14.41.0/25 via 10.14.41.211 dev eth0
  up ip route add 10.14.41.128/26 via 10.14.41.209 dev eth0
  up ip route add 10.14.41.192/28 via 10.14.41.211 dev eth0
  up ip route add 10.14.41.216/29 via 10.14.41.211 dev eth0
  ```

  `Lucena`
  ```
  auto eth0
  iface eth0 inet static
      address 10.14.41.209
      netmask 255.255.255.248
  
  auto eth1
  iface eth1 inet static
      address 10.14.41.129
      netmask 255.255.255.192
  
  up ip route add 0.0.0.0/0 via 10.14.41.210 dev eth0
  up ip route add 10.14.0.0/19 via 10.14.41.210 dev eth0
  up ip route add 10.14.32.0/21 via 10.14.41.210 dev eth0
  up ip route add 10.14.40.0/24 via 10.14.41.211 dev eth0
  up ip route add 10.14.41.0/25 via 10.14.41.211 dev eth0
  up ip route add 10.14.41.192/28 via 10.14.41.211 dev eth0
  up ip route add 10.14.41.216/29 via 10.14.41.212 dev eth0
  up ip route add 10.14.41.224/30 via 10.14.41.210 dev eth0
  ```

  `Zwischenzug`
  ```
  auto eth0
  iface eth0 inet static
      address 10.14.41.211
      netmask 255.255.255.248
  
  auto eth1
  iface eth1 inet static
      address 10.14.41.217
      netmask 255.255.255.248
  
  up ip route add 0.0.0.0/0 via 10.14.41.210 dev eth0
  up ip route add 10.14.0.0/19 via 10.14.41.210 dev eth0
  up ip route add 10.14.32.0/21 via 10.14.41.210 dev eth0
  up ip route add 10.14.41.224/30 via 10.14.41.210 dev eth0
  up ip route add 10.14.41.128/26 via 10.14.41.209 dev eth0
  up ip route add 10.14.40.0/24 via 10.14.41.219 dev eth1
  up ip route add 10.14.41.0/25 via 10.14.41.219 dev eth1
  up ip route add 10.14.41.192/28 via 10.14.41.219 dev eth1
  ```

  `Zugzwang`
  ```
  auto eth0
  iface eth0 inet static
      address 10.14.41.219
      netmask 255.255.255.248
  
  auto eth1
  iface eth1 inet static
      address 10.14.40.1
      netmask 255.255.255.0
  
  auto eth2
  iface eth2 inet static
      address 10.14.41.193
      netmask 255.255.255.240
  
  auto eth3
  iface eth3 inet static
      address 10.14.41.1
      netmask 255.255.255.128
  
  up ip route add 0.0.0.0/0 via 10.14.41.217 dev eth0
  up ip route add 10.14.0.0/19 via 10.14.41.217 dev eth0
  up ip route add 10.14.32.0/21 via 10.14.41.217 dev eth0
  up ip route add 10.14.41.128/26 via 10.14.41.217 dev eth0
  up ip route add 10.14.41.208/29 via 10.14.41.217 dev eth0
  up ip route add 10.14.41.224/30 via 10.14.41.217 dev eth0
  ```

  `Karena soal meminta agar ping dilakukan dari dan ke client yang IPnya DHCP, maka perlu dilakukan setting DHCP yang lebih detail dijelaskan pada nomor 3 (menyalakan DHCP Master, SLave, dan Relay). Setelah berhasil mendapatkan IP DHCP, baru testing dengan ping.`

  `Testing`
  ```
  #BUDAPEST KE ALEKHINE :
  ping 10.14.41.195
  #PONZIANI KE SILICIAN :
  ping 10.14.40.10
  ```
  
<br>

## Soal 3

> Berikan seluruh client (**Blackmar-Diemer, Budapest,** dan **Stafford**) IP secara dinamis dari DHCP. Range IP dibebaskan, namun tunjukkan bahwa mereka mendapatkan IP secara dinamis!

> _Assign all clients (**Blackmar-Diemer, Budapest,** and **Stafford**) dynamic IP addresses via DHCP. You may use any IP range you would like, but prove that they receive IP addresses dynamically!_

**Answer:**

- Screenshot

  <img width="714" height="287" alt="Screenshot 2025-12-03 223224" src="https://github.com/user-attachments/assets/f4889c32-f94c-4e24-b5fa-94939bd92af3" />
  <img width="721" height="266" alt="Screenshot 2025-12-03 223113" src="https://github.com/user-attachments/assets/2a5a73bb-b754-4c62-ab24-345090d77859" />
  <img width="715" height="260" alt="Screenshot 2025-12-03 223126" src="https://github.com/user-attachments/assets/2de78e90-77cc-4226-b4f3-f8e67c41cd7f" />


- Explanation

  `Untuk memberikan IP secara dinamis kepada Blackmar-Diemer (A?), Budapest (A1), dan Stafford (A2), digunakan server DHCP yang berada pada Ponziani. Karena lokasi subnet mereka berjauhan, diperlukan DHCP Relay (isc-dhcp-relay) pada setiap router yang dilewati agar permintaan DHCP dapat diteruskan ke server.`

  `Dalam konfigurasi, setiap subnet klien memiliki: Router (default gateway), Range IP dinamis, DNS server, dan Failover (redundant) dengan Ruylopez. Hasil pengujian menunjukkan bahwa ketiga client mendapatkan IP secara otomatis melalui DHCP.`

  `Setting DHCP Master : Ponziani`
  ```
  echo "nameserver 8.8.8.8" > /etc/resolv.conf
  apt-get update
  apt-get install isc-dhcp-server
  ```
  
  `nano /etc/default/isc-dhcp-server`
  ```
  Isi pada ipv4 : eth0
  ```
  
  `nano /etc/dhcp/dhcpd.conf`
  ```
  ddns-update-style none;
  authoritative;
  
  failover peer "dhcp-failover" {
      primary;                              
      address 10.14.41.130;               
      port 519;                            
      peer address 10.14.41.131;            
      peer port 520;                        
      max-response-delay 60;
      max-unacked-updates 10;
      mclt 3600;                            
      split 128;                            
      load balance max seconds 3;
  }
  
  # Subnet A5 (lokal PONZIANI & RuyLopez)
  subnet 10.14.41.128 netmask 255.255.255.192 {
      option routers 10.14.41.129;
      option broadcast-address 10.14.41.191;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.41.140 10.14.41.190;
      }
  }
  
  # Subnet A1 (BUDAPEST via relay)
  subnet 10.14.0.0 netmask 255.255.224.0 {
      option routers 10.14.0.1;
      option broadcast-address 10.14.31.255;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.0.10 10.14.31.250;
      }
  }
  
  # Subnet A2 (STAFFORD via relay)
  subnet 10.14.32.0 netmask 255.255.248.0 {
      option routers 10.14.32.1;
      option broadcast-address 10.14.39.255;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.32.10 10.14.39.250;
      }
  }
  
  # Subnet A3 (SLAV via relay)
  subnet 10.14.40.0 netmask 255.255.255.0 {
      option routers 10.14.40.1;
      option broadcast-address 10.14.40.255;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.40.10 10.14.40.250;
      }
  }
  
  # Subnet A4 (SICILIAN via relay)
  subnet 10.14.41.0 netmask 255.255.255.128 {
      option routers 10.14.41.1;
      option broadcast-address 10.14.41.127;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.41.10 10.14.41.120;
      }
  }
  
  subnet 10.14.41.208 netmask 255.255.255.248 {}
  subnet 10.14.41.224 netmask 255.255.255.252 {}
  subnet 10.14.41.192 netmask 255.255.255.240 {}
  subnet 10.14.41.216 netmask 255.255.255.248 {}

  ```

  `Setting DHCP Slave : Ruy-Lopez`

  ```
  ddns-update-style none;
  authoritative;
  
  failover peer "dhcp-failover" {
      secondary;                            
      address 10.14.41.131;                 
      port 520;                            
      peer address 10.14.41.130;           
      peer port 519;                       
      max-response-delay 60;
      max-unacked-updates 10;
      load balance max seconds 3;
  }
  
  # Subnet A5 
  subnet 10.14.41.128 netmask 255.255.255.192 {
      option routers 10.14.41.129;
      option broadcast-address 10.14.41.191;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.41.140 10.14.41.190;
      }
  }
  
  # Subnet A1 
  subnet 10.14.0.0 netmask 255.255.224.0 {
      option routers 10.14.0.1;
      option broadcast-address 10.14.31.255;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.0.10 10.14.31.250;
      }
  }
  
  # Subnet A2 
  subnet 10.14.32.0 netmask 255.255.248.0 {
      option routers 10.14.32.1;
      option broadcast-address 10.14.39.255;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.32.10 10.14.39.250;
      }
  }
  
  subnet 10.14.40.0 netmask 255.255.255.0 {
      option routers 10.14.40.1;
      option broadcast-address 10.14.40.255;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.40.10 10.14.40.250;
      }
  }
  
  # Subnet A4 
  subnet 10.14.41.0 netmask 255.255.255.128 {
      option routers 10.14.41.1;
      option broadcast-address 10.14.41.127;
      option domain-name-servers 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      
      pool {
          failover peer "dhcp-failover";
          range 10.14.41.10 10.14.41.120;
      }
  }
  
  # Subnet relay 
  subnet 10.14.41.208 netmask 255.255.255.248 {}
  subnet 10.14.41.224 netmask 255.255.255.252 {}
  subnet 10.14.41.192 netmask 255.255.255.240 {}
  subnet 10.14.41.216 netmask 255.255.255.248 {}
  ```

  `Restart DHCP Server`
  ```
  service isc-dhcp-server restart
  ```

  `Selanjutnya, jadikan semua router menjadi relay`
  ```
  echo 1 > /proc/sys/net/ipv4/ip_forward
  echo "nameserver 8.8.8.8" > /etc/resolv.conf
  apt-get update
  apt-get install isc-dhcp-relay -y
  service isc-dhcp-relay start
  ```
  
  `nano /etc/default/isc-dhcp-relay`
  ```
  SERVICE : 10.14.41.130 10.14.41.131
  #interface menyesuaikan
  ```

  `Restart Relay`
  ```
  service isc-dhcp-relay restart
  ```

  `Testing :`
  
  `Buka console semua client terkait`

  `Untuk memastikan DHCP Master dan Slave bekerja sesuai tugasnya, matikan Master (service isc-dhcp-relay stop) dan jalankan Slave. Client harus tetap dapat ip`

<br>

## Soal 4

> Berikan web server **Slav** dan **Sicilian** IP address yang tetap/fixed dari DHCP. 

> _Assign **Slav** and **Sicilian** web servers fixed IP addresses via DHCP._

**Answer:**

- Screenshot

  <img width="650" height="179" alt="Screenshot 2025-12-04 112751" src="https://github.com/user-attachments/assets/46f9d78a-6d0b-47d3-8dbe-8ffc684a1ad4" />
  <img width="645" height="179" alt="Screenshot 2025-12-04 112912" src="https://github.com/user-attachments/assets/147cf5d1-390b-4541-8cfd-f1a408d0d40f" />


- Explanation

  `Langkah pertama adalah mendapatkan MAC address masing-masing mesin Slav dan Sicilian, yaitu dengan menjalankan perintah ip link show eth0 pada keduanya. MAC address inilah yang dijadikan acuan oleh DHCP server. Setelah MAC diperoleh, kita menambahkan section host pada file konfigurasi DHCP server (/etc/dhcp/dhcpd.conf). Pada bagian ini kita mendefinisikan nama host, MAC address, dan IP statis yang dialokasikan. Dengan konfigurasi ini, Slav akan selalu mendapat IP 10.14.40.5 dan Sicilian akan selalu mendapat IP 10.14.41.3 setiap kali meminta kepada DHCP server. Selain itu, pada sisi klien kita juga menambahkan konfigurasi hwaddress ether <mac> pada interface masing-masing untuk memastikan alamat MAC yang digunakan sesuai dengan DHCP reservation yang sudah dibuat.`

  `Pada Ponziani dan RuyLOpez : nano /etc/dhcp/dhcpd.conf`
  ```
  host Slav {
      hardware ethernet 02:42:be:b3:3f:00;
      fixed-address 10.14.40.3;
  }
  
  # DHCP Reservation untuk Web Server Sicilian
  host Sicilian {
      hardware ethernet 02:42:47:1e:4c:00;
      fixed-address 10.14.41.5;
  }
  ```

  `Config Client`
  ```
  #Slav
  hwaddress ether 02:42:be:b3:3f:00
  #Sicilian
  hwaddress ether 02:42:47:1e:4c:00
  ```
  
<br>

## Soal 5

> Buatlah konfigurasi untuk domain:  
**parkov.com** → IP Node **Slav**  
**paskarov.com** → IP Node **Sicilian** 
Pada **DNS Master Caro-Kann.** Tambahkan juga subdomain www untuk kedua domain tersebut.

> _Configure the domains:  
**parkov.com** → **Slav** Node IP  
**paskarov.com** → **Sicilian** Node IP  
On the **Caro-Kann DNS Master,** then add the www subdomain for both domains._

**Answer:**

- Screenshot

  <img width="635" height="437" alt="Screenshot 2025-12-04 120216" src="https://github.com/user-attachments/assets/0308aea1-3146-449a-a67f-370322f96922" />
  <img width="647" height="393" alt="Screenshot 2025-12-04 120342" src="https://github.com/user-attachments/assets/c64f3fb4-e56c-4516-b12a-86fafb80332e" />


- Explanation

  `Pada server Caro-Kann, dilakukan konfigurasi DNS Master menggunakan Bind9 untuk melayani dua domain, yaitu parkov.com yang mengarah ke node Slav, serta paskarov.com yang mengarah ke node Sicilian. Setelah instalasi Bind9, dibuat direktori khusus untuk menyimpan file zone dan ditambahkan dua konfigurasi zone baru pada named.conf.local. Masing-masing domain dibuatkan file zone berisi SOA, NS record, A record, serta subdomain www yang mengarah ke alamat IP server masing-masing. Setelah konfigurasi selesai, dilakukan pengecekan file zone dan restart service Bind untuk memastikan DNS berjalan dengan benar. Pada sisi client seperti Alekhine, resolver diarahkan ke IP DNS Master Caro-Kann agar domain dapat di-resolve. Dengan konfigurasi ini, domain dan subdomain dapat diakses menggunakan ping atau perintah DNS lainnya.`

  `Di Caro-Kann`
  ```
  echo "nameserver 8.8.8.8" > /etc/resolv.conf
  apt-get update
  apt-get install bind9 -y

  mkdir -p /etc/bind/jarkom
  ```

  `Tambahkan zone di /etc/bind/named.conf.local`
  ```
  zone "parkov.com" {
    type master;
    file "/etc/bind/jarkom/parkov.com";
  };
  
  zone "paskarov.com" {
      type master;
      file "/etc/bind/jarkom/paskarov.com";
  };
  ```
  `nano /etc/bind/jarkom/parkov.com`
  ```
  $TTL 604800
  @   IN  SOA parkov.com. root.parkov.com. (
          2025120403
          604800
          86400
          2419200
          604800 )
  ;
  @       IN  NS  parkov.com.
  @       IN  A   10.14.40.3
  www     IN  A   10.14.40.3
  ```
  `nano /etc/bind/jarkom/paskarov.com`
  ```
  $TTL 604800
  @   IN  SOA paskarov.com. root.paskarov.com. (
          2025120403
          604800
          86400
          2419200
          604800 )
  ;
  @       IN  NS  paskarov.com.
  @       IN  A   10.14.41.5
  www     IN  A   10.14.41.5
  ```
  `Restart Bind`
  ```
  named-checkzone parkov.com /etc/bind/jarkom/parkov.com
  named-checkzone paskarov.com /etc/bind/jarkom/paskarov.com
  named-checkconf
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `Set DNS resolver di client`
  ```
  echo "nameserver 10.14.41.194" > /etc/resolv.conf
  ```

  `Testing`
  ```
  ping parkov.com
  ping www.parkov.com
  ping paskarov.com
  ping www.paskarov.com
  ```
  

<br>

## Soal 6

> Konfigurasikan juga **Alekhine** sebagai **DNS Slave** yang bekerja untuk membantu **Caro-Kann.** Lakukan pengujian dengan **mematikan Caro-Kann** lalu coba ping ke domain dan subdomain tersebut (pilih salah satu saja).

> _Configure **Alekhine** as a **DNS Slave** to assist **Caro-Kann**. Perform testing by **disabling Caro-Kann** and then pinging the domain and subdomain (choose only one)._

**Answer:**

- Screenshot
 
 <img width="659" height="366" alt="Screenshot 2025-12-04 121138" src="https://github.com/user-attachments/assets/8e5fb870-edb1-4b63-adef-b4fa2de963b4" />
 <img width="654" height="290" alt="Screenshot 2025-12-04 121212" src="https://github.com/user-attachments/assets/97a47c6e-b436-4362-bc83-348650007837" />


- Explanation

  `Pada tahap ini, server Alekhine dikonfigurasi sebagai DNS Slave untuk membantu Caro-Kann sebagai DNS Master. Konfigurasi dilakukan dengan menambahkan izin transfer zone dan mekanisme notifikasi perubahan pada sisi master, sehingga setiap pembaruan zone akan dikirim ke slave. Pada Alekhine, setiap domain didefinisikan sebagai zone bertipe slave dengan sumber master dari Caro-Kann. Setelah Bind9 direstart, Alekhine otomatis mengunduh file zone ke direktori /var/lib/bind, memastikan redundansi DNS tersedia. Untuk pengujian, resolver client diarahkan ke Alekhine lalu dilakukan ping ke domain dan subdomain. Setelah itu, DNS Master dimatikan untuk memastikan Slave tetap dapat memberikan resolusi domain. Jika domain tetap dapat di-resolve setelah master mati, maka konfigurasi DNS Slave berjalan dengan benar.`

  `Di Caro-Kann perbarui isi: nano /etc/bind/named.conf.local`
  ```
  zone "parkov.com" {
    type master;
    file "/etc/bind/jarkom/parkov.com";
    allow-transfer { 10.14.41.195; };     
    also-notify { 10.14.41.195; };
  };
  
  zone "paskarov.com" {
      type master;
      file "/etc/bind/jarkom/paskarov.com";
      allow-transfer { 10.14.41.195; };
      also-notify { 10.14.41.195; };
  };
  ```
  `Restart`
  ```
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `Di Alekhine : nano /etc/bind/named.conf.local`
  ```
  zone "parkov.com" {
    type slave;
    masters { 10.14.41.194; };    
    file "/var/lib/bind/parkov.com";
  };
  
  zone "paskarov.com" {
      type slave;
      masters { 10.14.41.194; };
      file "/var/lib/bind/paskarov.com";
  };
  ```
  `Restart`
  ```
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  
  #Cek apakah berhasil download file
  ls -l /var/lib/bind/
  ```

  `Testing : Ping sebelum dan sesudah Master dimatikan`
  ```
  echo "nameserver 10.14.41.195" > /etc/resolv.conf

  ping parkov.com
  ping www.parkov.com
  ping paskarov.com
  ping www.paskarov.com

  #Matikan DNS master
  pkill named
  ```
  

<br>

## Soal 7

> Konfigurasikan **Sicilian** agar berfungsi sebagai **web server nginx** yang akan menyajikan [halaman berikut](https://drive.google.com/file/d/1eX0ZjRKprx8T34XFAssrpc7ZE1j6Jv0j/view). Konfigurasikan juga agar **Sicilian** bisa menyimpan custom access log ke file **/tmp/access.log** dan error log ke file **/tmp/error.log.**

> _Configure **Sicilian** to function as an **nginx web server**that will serve [this page](https://drive.google.com/file/d/1eX0ZjRKprx8T34XFAssrpc7ZE1j6Jv0j/view). Also, configure **Sicilian** to save custom access logs to **/tmp/access.log** and error logs to **/tmp/error.log.**_

**Answer:**

- Screenshot

  <img width="650" height="620" alt="Screenshot 2025-12-04 123502" src="https://github.com/user-attachments/assets/265bb5a6-2df6-4cfe-b4d0-bc1c9ae9b822" />
  <img width="659" height="80" alt="Screenshot 2025-12-04 123544" src="https://github.com/user-attachments/assets/bb8ded1c-2ec8-4097-95bc-c040b38d4db3" />


- Explanation

  `Pada node Sicilian, dilakukan instalasi dan konfigurasi Nginx untuk menyajikan halaman web statis bernama sicilian.html. Direktori web disiapkan pada /var/www/html, dan file konfigurasi virtual host dibuat agar domain sicilian.com dapat diakses melalui port 80. Selain itu, Nginx dikonfigurasi untuk menyimpan akses log ke /tmp/access.log dan error log ke /tmp/error.log sebagai lokasi khusus untuk keperluan monitoring. Domain sicilian.com kemudian ditambahkan ke file /etc/hosts pada sisi client agar dapat di-resolve tanpa DNS. Setelah Nginx direstart, halaman dapat diuji menggunakan browser atau curl, serta log dapat dilihat langsung dari file yang telah dibuat. Konfigurasi ini memastikan Sicilian berfungsi penuh sebagai web server yang melayani domain custom dengan logging terpisah.`

 `Di Sicilian`
   ```
   echo "nameserver 8.8.8.8" > /etc/resolv.conf
   apt-get update
   apt-get install nginx -y
  
   mkdir -p /var/www/html
   ```
  
  `nano /var/www/html/sicilian.html : isi dengan file google drive`
  
  `nano /etc/nginx/sites-available/sicilian`
  ```
  server {
      listen 80;
      server_name sicilian.com 10.14.41.5;
  
      root /var/www/html;
      index sicilian.html;
  
      access_log /tmp/access.log;
      error_log /tmp/error.log;
  
      location / {
          try_files /sicilian.html =404;
      }
  }
  ```
  `Aktifkan konfigurasi`
  ```
  ln -s /etc/nginx/sites-available/sicilian /etc/nginx/sites-enabled/
  ```
  
  `Buat Log Access dan Log`
  ```
  touch /tmp/access.log /tmp/error.log
  chmod 666 /tmp/access.log /tmp/error.log
  ```
  
  `Ke Client : nano /etc/hosts`
  ```
  10.14.41.5 sicilian.com
  ```

  `Install Nginx di Client`
  ```
   echo "nameserver 8.8.8.8" > /etc/resolv.conf
   apt-get update
   apt-get install nginx -y
  ```

  `Restart Nginx di Client dan Sicilian`
  ```
  pkill nginx
  nginx
  service nginx status
  ```

  `Testing : `
  ```
  curl sicilian.com

  #Test log di Sicilian:
  cat /tmp/access.log
  cat /tmp/error.log
  ```


<br>

## Soal 8

> Buatlah custom access log ke file **/tmp/access.log.** Untuk keperluan logging, gunakan format log seperti di bawah:
> - Tanggal dan waktu akses dalam format standar log.
> - Nama node yang sedang diakses.
> - Alamat IP klien yang mengakses website.
> - Metode HTTP dan URI yang diakses oleh klien.
> - Status respons HTTP yang diberikan oleh server.
> - Jumlah byte yang dikirimkan dalam respons.
> - Waktu yang dihabiskan oleh server untuk menangani permintaan.> 
> - Contoh format log yang sesuai:  
[01/Oct/2024:11:30:45 +0000] Jarkom Node Sicilian Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds

> _Webserver: Create a custom access log to the file **/tmp/access.log.** For logging purposes, use the log format shown below:_
> - _The date and time of access in standard log format._
> - _The name of the node being accessed._
> - _The IP address of the client accessing the website._
> - _The HTTP method and URI accessed by the client._
> - _The HTTP response status returned by the server._
> - _The number of bytes sent in the response._
> - _The time spent by the server processing the request._
> - _Example of appropriate log format:  
[01/Oct/2024:11:30:45 +0000] Jarkom Node Sicilian Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds_

**Answer:**

- Screenshot

  <img width="669" height="203" alt="Screenshot 2025-12-04 124031" src="https://github.com/user-attachments/assets/c153a4a1-767f-45c5-8ae3-240533ba6d41" />


- Explanation

  `Pada node Sicilian, dilakukan konfigurasi custom access log untuk mencatat seluruh aktivitas akses HTTP dengan format yang telah ditentukan. Format log yang digunakan berisi informasi waktu akses, nama node, alamat IP client, metode dan URI permintaan, status response, jumlah byte yang dikirim, serta waktu proses request. Format tersebut didefinisikan dalam block http pada konfigurasi utama Nginx, lalu diaktifkan pada virtual host domain sicilian.com. Log dicatat pada file /tmp/access.log, sementara error log diarahkan ke /tmp/error.log. Setelah konfigurasi diterapkan dan Nginx direstart, setiap akses menuju Sicilian akan menghasilkan entri log sesuai format custom yang ditetapkan. Pengujian dapat dilakukan menggunakan curl atau browser, lalu isi log dapat diverifikasi langsung melalui terminal.`
  
   `Di Sicilian tambahkan: nano /etc/nginx/nginx.conf`
  ```
  log_format custom_sicilian '[$time_local] Jarkom Node Sicilian Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
  ```
  
  `nano /etc/nginx/sites-available/sicilian`
  ```
  server {
    listen 80;
    server_name sicilian.com 10.14.41.5;

    root /var/www/html;
    index sicilian.html;

    access_log /tmp/access.log custom_sicilian;
    error_log /tmp/error.log;

    location / {
        try_files /sicilian.html =404;
    }
  }
  ```
  `Restart Nginx`
  ```
  nginx -t
  pkill nginx
  nginx
  ```

  `Testing :`
  ```
  curl sicilian.com

  cat /tmp/access.log
  
  #Hapus log
  > /tmp/access.log
  ```

<br>

## Soal 9

> Konfigurasikan juga **Slav** agar berfungsi sebagai **web server nginx** yang menyajikan [halaman berikut](https://drive.google.com/file/d/1h8ik1Zcubntp0dvHt9NHYqSZLSTG6FuZ/view) dan **hanya** bisa diakses melalui port **8000** dan **8888.**

> _Configure **Slav** to function as an **nginx web server** that serves [this page](https://drive.google.com/file/d/1h8ik1Zcubntp0dvHt9NHYqSZLSTG6FuZ/view?usp=drive_link) and is **only** accessible via ports **8000** and **8888.**_

**Answer:**

- Screenshot

  <img width="655" height="634" alt="Screenshot 2025-12-04 125540" src="https://github.com/user-attachments/assets/e0bc5fb4-2498-45f5-a4b5-1f1e114c2da1" />
  <img width="651" height="629" alt="Screenshot 2025-12-04 125604" src="https://github.com/user-attachments/assets/cd43d7ef-c8d8-478f-8828-52b5ec72a313" />
  <img width="649" height="141" alt="Screenshot 2025-12-04 125631" src="https://github.com/user-attachments/assets/18cb732e-b3c7-4e73-97de-6fed3e85c6ff" />


- Explanation

  `Node Slav dikonfigurasi sebagai web server Nginx yang hanya melayani akses melalui port 8000 dan 8888. Untuk membatasi akses, dibuat dua blok server: satu blok pada port 80 yang mengembalikan respons 403 sehingga akses langsung ditolak, dan blok lain pada port 8000 serta 8888 yang menampilkan halaman slav.html sebagai konten utama. Selain itu, ditambahkan pula custom access log menggunakan format custom_slav untuk mencatat aktivitas klien yang mengakses server, termasuk informasi waktu, IP klien, metode HTTP, status respon, jumlah byte yang dikirim, serta waktu pemrosesan. Setelah konfigurasi diaktifkan dan Nginx direstart, Slav hanya dapat diakses melalui kedua port yang telah ditentukan, sementara akses ke port 80 diblokir sesuai kebutuhan.`
  
  `Di Slav :`
  ```
  echo "nameserver 8.8.8.8" > /etc/resolv.conf
  apt-get update
  apt-get install nginx -y
  ```

  `nano /var/www/html/slav.html : isi dengan file google drive`

  `nano /etc/nginx/sites-available/slav`
  ```
  server {
    listen 80;
    server_name slav.com;
    return 403 "Access to Slav web server is restricted.\n";
  }
  
  server {
      listen 8000;
      listen 8888;
      server_name slav.com;
  
      root /var/www/html;
      index slav.html;
  
      access_log /tmp/access.log custom_slav;
      error_log /tmp/error.log;
  
      location / {
          try_files /slav.html =404;
      }
  }
  ```
  `nano /etc/nginx/nginx.conf`
  ```
  log_format custom_slav '[$time_local] Jarkom Node Slav Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
  ```

  ```
  ln -s /etc/nginx/sites-available/slav /etc/nginx/sites-enabled/
  touch /tmp/access.log /tmp/error.log
  chmod 666 /tmp/access.log /tmp/error.log
  ```

  `Restart Nginx`
  ```
  nginx -t
  pkill nginx
  nginx
  ```

  `Testing : Budapest`
  ```
  nano /etc/host
  10.14.40.3 slav.com

  #Berhasil
  curl slav.com:8000
  curl slav.com:8888

  #Gagal
  curl slav.com 
  ```
  
  
<br>

## Soal 10

> Untuk memudahkan akses, buatlah satu domain lagi dengan nama **openings.com** yang mengarah ke **Petrov.** Lalu, konfigurasikan juga **Petrov** sebagai **Reverse Proxy** yang akan melakukan forward request ke server yang sesuai berdasarkan URL profile yang diminta oleh klien dengan ketentuan sebagai berikut:
> - Request untuk “openings.com/**sicilian**” harus dialihkan ke web server **Sicilian.**
> - Request untuk “openings.com/**slav**” harus dialihkan ke web server **Slav.**

> _To facilitate access, create another domain with the name **openings.com** that points to **Petrov.** Then, configure **Petrov** as a **Reverse Proxy** that will forward requests to the appropriate server based on the profile URL requested by the client with the following conditions:_
> - _Requests for “openings.com/**sicilian**” must be forwarded to web server **Sicilian.**_
> - _Request for “openings.com/**slav**” must be forwarded to web server **Slav.**_

**Answer:**

- Screenshot

  <img width="650" height="692" alt="Screenshot 2025-12-04 224541" src="https://github.com/user-attachments/assets/3030cf90-1c4d-4d35-8cd2-cb9513e37eac" />
  <img width="656" height="690" alt="Screenshot 2025-12-04 224558" src="https://github.com/user-attachments/assets/b0ada484-d152-468b-be70-7727f8aa6ed0" />

  <img width="651" height="692" alt="Screenshot 2025-12-04 224628" src="https://github.com/user-attachments/assets/0f39d1fc-5d8c-4575-9583-776f05913c7f" />
  <img width="649" height="687" alt="Screenshot 2025-12-04 224648" src="https://github.com/user-attachments/assets/d2a0cf9d-0ac3-4792-b2ab-96b1dd7431b2" />

  <img width="652" height="251" alt="Screenshot 2025-12-04 224709" src="https://github.com/user-attachments/assets/55363ca6-c0f5-47c0-a8be-370f87c0d8e3" />

- Explanation

  `Domain openings.com ditambahkan pada DNS Master (Caro-Kann) dan diarahkan ke node Petrov. Petrov kemudian dikonfigurasi sebagai Reverse Proxy menggunakan Nginx, sehingga setiap request ke openings.com akan diteruskan ke server lain berdasarkan path URL. Jika klien mengakses openings.com/sicilian, permintaan akan diteruskan ke web server Sicilian. Jika klien mengakses openings.com/slav, permintaan akan dialihkan ke server Slav yang berjalan pada port 8000. Permintaan selain kedua jalur tersebut secara otomatis menghasilkan HTTP 404 sesuai aturan yang ditentukan. Konfigurasi ini memungkinkan Petrov berfungsi sebagai gateway terpusat untuk beberapa layanan web yang berada pada server berbeda di dalam jaringan.`

  `Di Caro-Kann tambahkan : nano /etc/bind/named.conf.local`
  ```
  zone "openings.com" {
    type master;
    file "/etc/bind/jarkom/openings.com";
    allow-transfer { 10.14.41.195; };
    also-notify { 10.14.41.195; };
  }
  ```
  `nano /etc/bind/jarkom/openings.com`
  ```
  $TTL 604800
  @       IN  SOA openings.com. root.openings.com. (
              2025110301
              604800
              86400
              2419200
              604800 )
  
  @       IN  NS  openings.com.
  @       IN  A   10.14.41.218
  www     IN  CNAME openings.com.
  ```
  `Restart Bind`
  ```
  pkill named
  /usr/sbin/named -c /etc/bind/named.conf
  ```

  `Di Petrov : nano /etc/nginx/sites-available/openings`
  ```
  server {
    listen 80;
    server_name openings.com www.openings.com;

    access_log /tmp/openings_access.log;
    error_log  /tmp/openings_error.log;

    location /sicilian {
        proxy_pass http://10.14.41.5:80;
        proxy_set_header Host sicilian.com;
    }

    location /slav {
        proxy_pass http://10.14.40.3:8000;
        proxy_set_header Host slav.com;
    }

    location / {
        return 404;
    }
  }
  ```

  `Aktifkan site`
  ```
  ln -s /etc/nginx/sites-available/openings /etc/nginx/sites-enabled/
  nginx -t
  service nginx restart
  ```

  `Testing : `
  ```
  #Output: halaman dari server Sicilian
  curl openings.com/sicilian
  
  #Output: halaman dari server Slav (port 8000)
  curl openings.com/slav

  #Output: 404 Not Found
  curl openings.com/random
  ```

  
<br>

## Soal 11

> Tambahkan juga konfigurasi agar request untuk “openings.com/**random**” akan mengalihkan request ke webserver **Sicilian** dan **Slav** dengan algoritma _round-robin_.

> _Additionally, configure requests for "openings.com/**random**" to be redirected to the **Sicilian** and **Slav** web servers using a round-robin algorithm._

**Answer:**

- Screenshot
  <img width="939" height="933" alt="Screenshot 2025-12-04 233304" src="https://github.com/user-attachments/assets/97518246-b1f4-4b96-bf56-088b444d96ab" />
  <img width="725" height="915" alt="Screenshot 2025-12-04 233321" src="https://github.com/user-attachments/assets/ba80abe5-4f02-4935-9833-c28d8bc63d57" />

  <img width="892" height="916" alt="Screenshot 2025-12-04 233630" src="https://github.com/user-attachments/assets/8a434130-c81a-4cfd-847b-b4b5e835fd82" />
  <img width="879" height="934" alt="Screenshot 2025-12-04 233620" src="https://github.com/user-attachments/assets/f10726f8-544b-4012-b060-db0c920f1c96" />


- Explanation

  `Pada konfigurasi ini, server Petrov berfungsi sebagai reverse proxy untuk domain openings.com, yang bertugas meneruskan request klien ke server backend yang sesuai. Untuk dua endpoint utama, yaitu /sicilian dan /slav, proxy diarahkan secara statis ke web server Sicilian dan Slav berdasarkan URL yang diminta. Selain itu, ditambahkan fitur load balancing round-robin untuk endpoint /random, sehingga setiap request secara bergantian diteruskan ke kedua backend tersebut (Sicilian dan Slav). Untuk mewujudkan ini, dibuat dua blok upstream bernama backend_sicilian dan backend_slav yang masing-masing menyimpan alamat IP web server tujuan. Kemudian, direktif split_clients digunakan untuk membagi request berdasarkan kombinasi $remote_addr dan $request_id, sehingga menghasilkan pembagian trafik 50:50 antara “sicilian” dan “slav”. Hasil pembagian ini disimpan dalam variabel $backend_pool.`

  `Agar nama upstream yang digunakan dinamis, dibuat dua map: map $backend_pool $backend_upstream memilih upstream yang tepat (backend_sicilian atau backend_slav) dan map $backend_pool $backend_host menentukan Host header yang sesuai. Pada blok location /random, request diteruskan ke upstream dinamis menggunakan proxy_pass http://$backend_upstream/;. Selain itu, ditambahkan header X-Backend-Pool dan X-Backend-Host agar mudah mengetahui backend mana yang menangani request tersebut ketika debugging. Secara keseluruhan, implementasi ini memungkinkan Petrov melakukan reverse proxy statis untuk endpoint tertentu, sekaligus round-robin load balancing untuk trafik acak ke /random.`

  `Di Petrov : nano /etc/nginx/sites-available/openings`
  ```
    upstream backend_sicilian {
      server 10.14.41.5:80;
  }
  
  upstream backend_slav {
      server 10.14.40.3:8000;
  }
  
  # Split traffic 50:50 untuk round-robin berbasis IP + request ID
  split_clients "${remote_addr}${request_id}" $backend_pool {
      50% sicilian;
      50% slav;
  }
  
  # Tentukan upstream mana yang dipilih
  map $backend_pool $backend_upstream {
      sicilian backend_sicilian;
      slav     backend_slav;
  }
  
  # Tentukan host header yang dipakai
  map $backend_pool $backend_host {
      sicilian sicilian.com;
      slav     slav.com;
  }
  
  server {
      listen 80;
      server_name openings.com www.openings.com;
  
      access_log /tmp/openings_access.log;
      error_log  /tmp/openings_error.log;
  
      # Forward ke Sicilian
      location /sicilian {
          proxy_pass http://10.14.41.5:80/;     
          proxy_set_header Host sicilian.com;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      }
  
      # Forward ke Slav
      location /slav {
          proxy_pass http://10.14.40.3:8000/;      
          proxy_set_header Host slav.com;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      }
  
      # Round-robin load balancing untuk /random
      location /random {
          proxy_pass http://$backend_upstream/;
          proxy_set_header Host $backend_host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  
          add_header X-Backend-Pool $backend_pool always;
          add_header X-Backend-Host $backend_host always;
      }
  
      # Default selain aturan di atas → 404
      location / {
          return 404;
      }
  }
  ```
  `Restart Nginx`
  ```
  pkill nginx
  nginx
  ```

  `Testing :`
  ```
  curl openings.com/random
  curl openings.com/random
  curl openings.com/random
  curl openings.com/random
  ```

<br>

## Soal 12

> Anatoly Parkov berencana untuk melakukan ekspansi secara besar-besaran. Maka dari itu, hapus seluruh konfigurasi Static Routing dan ubah agar seluruh router menggunakan Dynamic Routing. Gunakan protokol RIP!

> _Anatoly Parkov plans to perform a great expansion. Therefore, remove all Static Routing configurations and configure all routers to use Dynamic Routing. Use the RIP protocol!_

**Answer:**

- Screenshot

  <img width="692" height="661" alt="Screenshot 2025-12-05 085525" src="https://github.com/user-attachments/assets/782a584d-d6f9-491d-8a81-9092ef804190" />
  <img width="759" height="202" alt="Screenshot 2025-12-05 085701" src="https://github.com/user-attachments/assets/c6471bbd-545e-4cee-8093-cbc50a990cbb" />
  <img width="852" height="221" alt="Screenshot 2025-12-05 085617" src="https://github.com/user-attachments/assets/b78f8a51-35c0-408c-b99b-bae31f4f3ca4" />
  <img width="791" height="217" alt="Screenshot 2025-12-05 085601" src="https://github.com/user-attachments/assets/272cec0c-4233-41fe-bdd9-7ca5e1da581a" />
  <img width="815" height="222" alt="Screenshot 2025-12-05 085638" src="https://github.com/user-attachments/assets/d6511dc7-1cda-43ad-bb73-74297ae31795" />
  <img width="751" height="225" alt="Screenshot 2025-12-05 085627" src="https://github.com/user-attachments/assets/48c5c6cc-f09c-4217-853f-1f385ba1384e" />

`Budapest ke Alekhine`

<img width="623" height="289" alt="Screenshot 2025-12-05 085746" src="https://github.com/user-attachments/assets/4b857a0f-e58a-4512-8018-d4b4eb7361be" />

`Ponziani ke Sicilian`

<img width="591" height="135" alt="Screenshot 2025-12-05 090019" src="https://github.com/user-attachments/assets/44fec1bf-ee6b-4ee2-bafd-9cffe202a013" />


- Explanation

  `Pada tahap ini, seluruh router dalam topologi Anatoly Parkov diubah dari sebelumnya menggunakan static routing menjadi dynamic routing dengan protokol RIP (Routing Information Protocol). RIP dipilih karena sederhana, kompatibel dengan banyak perangkat, dan cocok untuk topologi multi-subnet seperti jaringan Parkov. Setiap router akan membagikan rute-rute miliknya kepada router lain secara otomatis, sehingga administrator tidak perlu lagi membuat puluhan static route manual. Konfigurasi RIP di setiap router dilakukan menggunakan FRRouting (FRR). Prosesnya diawali dengan menjalankan daemon zebra, ripd, dan mgmtd agar router dapat mengelola tabel routing dan mendistribusikan rute RIP. Setelah masuk ke konsol vtysh, router diatur menggunakan mode konfigurasi.`

  `Router pertama yang disiapkan adalah Smith-Morra, router besar yang menghubungkan banyak subnet seperti Subnet A1, Subnet A2, dan link antar-router menuju Fianchetto. Smith-Morra mengaktifkan RIP versi 2, lalu menspesifikasikan jaringan yang akan diiklankan melalui perintah network. Karena subnet A1 dan A2 adalah jaringan untuk klien, interface menuju klien dijadikan passive-interface sehingga tidak mengirimkan broadcast RIP ke klien. Perintah redistribute connected menjamin bahwa seluruh jaringan langsung terhubung (connected networks) ikut diinformasikan melalui RIP.`

  `Router kedua, Fianchetto, menjadi penghubung antara Smith-Morra dan router di area pusat (Lucena, Zwischenzug, Zugzwang). Ia hanya mengiklankan dua network: link menuju Smith-Morra, dan subnet pusat 10.14.41.208/29. Karena dua interface tersebut adalah link antar-router, tidak ada interface yang dijadikan passive. Router ketiga, Lucena, menghubungkan jaringan pusat dengan Subnet A5. Interface yang mengarah ke klien Ponziani dan Ruylopez dijadikan passive agar broadcast RIP tidak dikirim ke host. Sisanya tetap aktif dan membagikan rute ke router lain. Router Zwischenzug dan Zugzwang pun dikonfigurasi dengan prinsip yang sama. Zwischenzug menjadi router transit antara subnet pusat dan subnet D (jaringan menuju Zugzwang). Sementara Zugzwang adalah router dengan banyak client-subnet (A3, A4, A6). Semua interface menuju client dibuat passive, sedangkan interface antar-router tetap aktif untuk mengirim dan menerima update routing.`

  `Dengan konfigurasi tersebut, setiap router akan saling bertukar informasi rute secara otomatis. Hasilnya dapat dilihat saat menjalankan perintah show ip rip, di mana rute-rute dari router lain muncul dengan kode R, lengkap dengan next-hop dan metric hop-count. Sementara rute lokal ditandai dengan C (connected).`

  `Smith-Morra`
  ```
  cd /usr/lib/frr
  ./zebra -d
  ./ripd -d
  ./mgmtd -d
  vtysh
  
  configure terminal
  
  router rip
    version 2
    network 10.14.0.0/19
    network 10.14.32.0/21
    network 10.14.41.224/30
    passive-interface eth2
    passive-interface eth3
    redistribute connected
  exit
  exit
  ```

  `Fianchetto`
  ```
  cd /usr/lib/frr
  ./zebra -d
  ./ripd -d
  ./mgmtd -d
  vtysh
  
  configure terminal
  
  router rip
    version 2
    network 10.14.41.208/29
    network 10.14.41.224/30
    redistribute connected
  exit
  exit
  ```

  `Lucena`
  ```
  cd /usr/lib/frr
  ./zebra -d
  ./ripd -d
  ./mgmtd -d
  vtysh
  
  configure terminal
  
  router rip
    version 2
    network 10.14.41.208/29
    network 10.14.41.128/26
    passive-interface eth1
    redistribute connected
  exit
  exit
  ```

  `Zwischenzug`
  ```
  cd /usr/lib/frr
  ./zebra -d
  ./ripd -d
  ./mgmtd -d
  vtysh
  
  configure terminal
  
  router rip
    version 2
    network 10.14.41.208/29
    network 10.14.41.216/29
    redistribute connected
  exit
  exit
  ```

  `Zugzwang`
  ```
  cd /usr/lib/frr
  ./zebra -d
  ./ripd -d
  ./mgmtd -d
  vtysh
  
  configure terminal
  
  router rip
    version 2
    network 10.14.41.216/29
    network 10.14.40.0/24
    network 10.14.41.192/28
    network 10.14.41.0/25
    passive-interface eth1
    passive-interface eth2
    passive-interface eth3
    redistribute connected
  exit
  exit
  ```

  `Cek Routing Table`
  ```
  show ip rip
  ```

  `Restart Relay`
  ```
  service isc-dhcp-relay restart
  ```
  
  `Testing (Dari Budapest): Pastikan IP forwarding hidup`
  ```
  echo 1 > /proc/sys/net/ipv4/ip_forward
  ping 10.14.40.3       # Slav
  ping 10.14.41.5       # Sicilian
  ping 10.14.41.130     # Ponziani
  ping 8.8.8.8 -c 3     # Internet
  ```

<br>

## Soal 13

> Untuk meningkatkan keamanan, konfigurasikan firewall **Smith-Morra** untuk melakukan pembatasan koneksi SSH ke server DNS. Drop semua packet SSH yang berasal dari seluruh client yang memiliki tujuan ke **Caro-Kann** atau **Alekhine.**

> _To increase security, configure the **Smith-Morra** firewall to restrict SSH connections to the **DNS server.** Drop all SSH packets from all clients destined for **Caro-Kann** or **Alekhine.**_

**Answer:**

- Screenshot

  `Dari Client, SSH ditolak`
  
  <img width="565" height="390" alt="Screenshot 2025-12-05 092519" src="https://github.com/user-attachments/assets/82cd25f8-4937-47aa-b107-0acd82e855a7" />
  <img width="883" height="359" alt="Screenshot 2025-12-05 092827" src="https://github.com/user-attachments/assets/9e65496b-31e5-485c-afe3-babc11b0a987" />

  `Dari Router, SSH masih bisa`
  
  <img width="628" height="63" alt="Screenshot 2025-12-05 093641" src="https://github.com/user-attachments/assets/56d4bc49-c6a7-4b86-bae2-e78bef3b92d4" />


- Explanation

  `Untuk meningkatkan keamanan infrastruktur jaringan, Smith-Morra yang berperan sebagai firewall utama perlu membatasi akses SSH dari seluruh subnet klien menuju server DNS di Subnet A6, yaitu Caro-Kann (10.14.41.194) dan Alekhine (10.14.41.195). Akses SSH dianggap sensitif karena memberikan kemampuan administratif penuh, sehingga penting untuk memastikan bahwa hanya perangkat tertentu yang berhak melakukan login ke kedua server tersebut. Implementasi firewall dilakukan menggunakan iptables pada chain FORWARD, karena Smith-Morra meneruskan trafik antar subnet dan bukan menjalankan koneksi lokal.`

  `Aturan firewall dikonfigurasi untuk mendeteksi trafik TCP pada port tujuan 22 (SSH) dari seluruh subnet klien: A1, A2, A3, A4, dan A5. Untuk setiap subnet, dibuat dua aturan DROP : satu untuk Caro-Kann dan satu lagi untuk Alekhine. Dengan demikian, semua percobaan SSH dari klien mana pun akan diblokir sebelum mencapai kedua server. Seluruh aturan ini tidak memblokir ping (ICMP), DNS Query, HTTP, atau port lainnya, karena pembatasan hanya berlaku pada port 22. Pengguna masih dapat melakukan nslookup, koneksi TCP port 53, atau servis lain yang tidak berbahaya.`

  `Untuk memastikan firewall berfungsi, dilakukan beberapa pengujian seperti mencoba SSH yang harus gagal (timeout/connection refused), melakukan ping yang harus berhasil, serta pengecekan counter iptables untuk melihat packet yang di-drop. Dengan konfigurasi ini, segmen DNS tetap aman dari akses ilegal tanpa mengganggu fungsi operasional jaringan lainnya.`

  `Smith-Morra`
  ```
  iptables -A FORWARD -s 10.14.0.0/19 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.0.0/19 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.32.0/21 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.32.0/21 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.40.0/24 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.40.0/24 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.0/25 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.0/25 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.128/26 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.128/26 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  ```

  `Testing Client :`
  ```
  #Gagal
  ssh root@10.14.41.194
  ssh root@10.14.41.195

  #Berhasil
  ping 10.14.41.194
  ping 10.14.41.195
  nslookup google.com 10.14.41.194
  nc -zv 10.14.41.194 53
  ```

<br>

## Soal 14

> Nampaknya, web server juga manusia sehingga hanya ingin bekerja di hari kerja. Maka dari itu, semua client hanya bisa mengakses **Sicilian** dan **Slav** pada hari Senin-Jumat pada pukul 09:00-17:00.

> _Apparently, web servers are humans too, so they only want to work on weekdays. Therefore, all clients can only access **Sicilian** and **Slav** on Monday through Friday, 9:00 AM to 5:00 PM._

**Answer:**

- Screenshot

  `Berhasil`
  
  <img width="885" height="712" alt="Screenshot 2025-12-05 093914" src="https://github.com/user-attachments/assets/8e662983-edb3-4f3e-a41c-70d8086d1244" />
  <img width="910" height="770" alt="Screenshot 2025-12-05 094826" src="https://github.com/user-attachments/assets/21ebfd69-dd29-410e-b4d3-f79f4ddcd57f" />
  <img width="904" height="741" alt="Screenshot 2025-12-05 095049" src="https://github.com/user-attachments/assets/44c651eb-c0c7-4c94-8f42-8c94a2510b7f" />

  `Gagal`

  <img width="821" height="60" alt="Screenshot 2025-12-05 094417" src="https://github.com/user-attachments/assets/8a5ec9a2-167f-4b51-adfa-6b5312b0b19a" />
  <img width="632" height="60" alt="Screenshot 2025-12-05 093947" src="https://github.com/user-attachments/assets/936c916d-d61e-4b5a-a65b-962f044e8f30" />


- Explanation

  `Pada konfigurasi ini, firewall Smith-Morra digunakan untuk membatasi akses seluruh client ke dua web server, yaitu Sicilian (10.14.41.5) dan Slav (10.14.40.3). Aturan yang diterapkan adalah: web server hanya boleh diakses pada hari kerja (Senin–Jumat) dan hanya pada pukul 09:00–17:00. Untuk mencapai hal tersebut, modul iptables time digunakan untuk mendeteksi waktu dan hari saat paket tiba. Semua trafik HTTP (port 80) maupun HTTPS (port 443) yang mengarah ke Sicilian dan Slav akan di-DROP apabila dikirim di luar jam kerja, termasuk malam hari, pagi sebelum jam 9, dan seluruh hari Sabtu serta Minggu. Karena Slav memiliki beberapa layanan tambahan, port 8000 dan 8888 juga diberlakukan aturan yang sama. Dengan konfigurasi ini, web server tetap dapat diakses sepenuhnya selama hari kerja dan jam operasional yang ditentukan, namun otomatis diblokir di luar waktu tersebut tanpa mengganggu layanan lain di sistem.`

  `Smith-Morra`
  ```
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --weekdays Sat,Sun -j DROP
  
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --weekdays Sat,Sun -j DROP
  
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --weekdays Sat,Sun -j DROP
  
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --weekdays Sat,Sun -j DROP
  ```

  `Testing (Client) :`
  ```
  # Set waktu ke jam 10:00 (dalam jam kerja) = BERHASIL 
  date -s "2025-12-09 10:00:00" 
  
  # Set waktu ke jam 18:00 (di luar jam kerja) = GAGAL
  date -s "2025-12-09 18:00:00"
  
  # Dari Budapest (10.14.0.2) 
  curl http://10.14.41.5 
  curl http://10.14.40.3:8000
  curl http://10.14.40.3:8888
  ```
  
<br>

## Soal 15

> Terakhir, Gerry Paskarov berpesan untuk selalu melakukan logging, sehingga konfigurasikan fitur logging untuk melakukan log terhadap seluruh paket yang di-DROP pada firewall **Smith-Morra.**
> _Finally, Gerry Paskarov advises to always perform logging, so configure a logging feature to log all packets dropped on the **Smith-Morra** firewall._

**Answer:**

- Screenshot

  <img width="920" height="764" alt="Screenshot 2025-12-05 103702" src="https://github.com/user-attachments/assets/62ff5d2b-479f-4a57-ad7e-804c59e54be5" />
  <img width="872" height="308" alt="Screenshot 2025-12-05 103712" src="https://github.com/user-attachments/assets/26df49d1-a4f3-48f3-8baf-055165feccd2" />


- Explanation

  `Pada konfigurasi firewall Smith-Morra, setiap paket yang di-DROP harus dicatat (di-log) agar administrator dapat memantau seluruh aktivitas yang ditolak oleh firewall. Karena aturan nomor 13 dan 14 sebelumnya hanya melakukan DROP tanpa LOG, maka aturan tersebut harus diulang kembali dengan menambahkan rule logging. Sebelum menambahkan aturan baru, dilakukan iptables -F untuk menghapus seluruh aturan lama sehingga tidak terjadi duplikasi dan firewall hanya menjalankan aturan versi terbaru yang sudah dilengkapi fitur LOG.`

  `Seluruh subnet (A1–A5) diberikan aturan untuk mencegah akses SSH (port 22) menuju server Caro-Kann (10.14.41.194) dan Alekhine (10.14.41.195). Untuk setiap rule DROP, ditambahkan rule LOG yang muncul tepat sebelum rule DROP. Hal ini memastikan setiap paket SSH yang ditolak akan tercatat di log, dengan prefix berbeda untuk Caro-Kann (SSH-DROP-CK:) dan Alekhine (SSH-DROP-AL:) sehingga memudahkan troubleshooting.`

  `Selain itu, server Sicilian (10.14.41.5) dan Slav (10.14.40.3) memiliki pembatasan akses berbasis waktu. Pada hari Sabtu–Minggu (weekend) serta pada weekday sebelum pukul 09:00 dan setelah pukul 17:00, seluruh akses HTTP/HTTPS (dan port tambahan pada Slav: 8000 & 8888) harus diblokir. Untuk itu, setiap aturan DROP kembali ditambahkan rule LOG dengan prefix berbeda (WEB-DROP-SIC: dan WEB-DROP-SLAV:). Dengan demikian, administrator bisa melihat kapan dan port mana yang diblokir berdasarkan waktu.Dengan konfigurasi ini, seluruh permintaan yang ditolak—baik dari aturan SSH antar subnet maupun aturan berbasis waktu untuk server web—tercatat secara lengkap. Administrator dapat mengeceknya melalui iptables -L -v -n`

  `Smith-Morra`
  ```
  iptables -F

  iptables -A FORWARD -s 10.14.0.0/19 -d 10.14.41.194 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-CK: "
  iptables -A FORWARD -s 10.14.0.0/19 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.0.0/19 -d 10.14.41.195 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-AL: "
  iptables -A FORWARD -s 10.14.0.0/19 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.32.0/21 -d 10.14.41.194 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-CK: "
  iptables -A FORWARD -s 10.14.32.0/21 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.32.0/21 -d 10.14.41.195 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-AL: "
  iptables -A FORWARD -s 10.14.32.0/21 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.40.0/24 -d 10.14.41.194 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-CK: "
  iptables -A FORWARD -s 10.14.40.0/24 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.40.0/24 -d 10.14.41.195 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-AL: "
  iptables -A FORWARD -s 10.14.40.0/24 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.0/25 -d 10.14.41.194 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-CK: "
  iptables -A FORWARD -s 10.14.41.0/25 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.0/25 -d 10.14.41.195 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-AL: "
  iptables -A FORWARD -s 10.14.41.0/25 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.128/26 -d 10.14.41.194 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-CK: "
  iptables -A FORWARD -s 10.14.41.128/26 -d 10.14.41.194 -p tcp --dport 22 -j DROP
  iptables -A FORWARD -s 10.14.41.128/26 -d 10.14.41.195 -p tcp --dport 22 -j LOG --log-prefix "SSH-DROP-AL: "
  iptables -A FORWARD -s 10.14.41.128/26 -d 10.14.41.195 -p tcp --dport 22 -j DROP
  
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80 -m time --weekdays Sat,Sun -j LOG --log-prefix "WEB-DROP-SIC: "
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --weekdays Sat,Sun -j LOG --log-prefix "WEB-DROP-SIC: "
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80  -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SIC: "
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80  -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SIC: "
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80  -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SIC: "
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 80  -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SIC: "
  iptables -A FORWARD -d 10.14.41.5 -p tcp --dport 443 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80 -m time --weekdays Sat,Sun -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --weekdays Sat,Sun -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --weekdays Sat,Sun -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --weekdays Sat,Sun -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --weekdays Sat,Sun -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80  -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80  -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --timestart 00:00 --timestop 08:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80  -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 80  -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 443 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8000 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j LOG --log-prefix "WEB-DROP-SLAV: "
  iptables -A FORWARD -d 10.14.40.3 -p tcp --dport 8888 -m time --timestart 17:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j DROP
  ```
  
  `Testing : `
  ```
  # Dari Budapest
  ssh root@10.14.41.194
  ssh root@10.14.41.195
  
  date -s “2025-12-09 18:00:00”
  curl http://10.14.41.5
  curl http://10.14.40.3:8000

  #Di Smith-Morra (cek log)
  iptables -L -v -n 
  ```
  
<br>
  
## Problems
   GNS saya selalu bermasalah, entah project tiba-tiba hilang, ke blokir internetnya ketika akses lewat chrome, dan lain-lain. 
   
## Revisions (if any)

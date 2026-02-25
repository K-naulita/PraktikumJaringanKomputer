[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/DGhYuEuO)
| Name                   | NRP          | Class |
|------------------------|--------------|:-------:|
| Kartika Nana Naulita   |  5025241021  |   A   |

## Task 1

- Flag
 `JARKOM25{Ja0G_Bbbb4ng3t_S1_GFW5A1YGDD5TX15LOZMQXZHJU4MYVG0xl0vel17g5nzao2e06tz2x785twbb0_7ce0700eac0a16ee8cc8cff1ae813291}`

> a. Berapa banyak packet yang terekam pada file pcapng?

> _a. How many packets are recorded in the pcapng file?_

**Answer:** `9596`

- Filter expression

  `-`

- Explanation

  `Menggunakan capture filter properties yang ada di bagian pojok kiri bawah tampilan wireshark. Terlihat bahwa pada Statistics tertera Packets yang tercapture ada 9596.`

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/XcDg0NY.png)
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/XCfCuil.png)

<br>
<br>

> b. Ada berapa jenis protocol (total) yang terekam pada traffic?

> _b. How many types of protocol (totals) are recorded in the traffic?_

**Answer:** `12`

- Filter expression

  `-`

- Explanation

  `Menggunakan tab Statistics kemudian ke Protocol Hierarchy untuk bisa melihat jenis protocol yang tertera. Ada 12 protocol yaitu Frame, Linux cooked-mode capture, Internet Protocol Version 4 (IPv4), Transmission Control Protocol (TCP), Virtual Network Computing (VNC), Thrift Protocol, Telnet, Signaling Compression (SIGCOMP), Hypertext Transfer Protocol (HTTP), JavaScript Object Notation (JSON), HiPerConTracer Trace Service, dan Data`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/9PYxI2V.png)
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/XCfCuil.png)

<br>
<br>

> c. Ada berapa jenis protocol berbasis TCP yang terekam pada traffic?

> _c. How many types of TCP-based applications protocol are recorded in the traffic?_

**Answer:** `8`

- Filter expression

  `-`

- Explanation

  `Sama seperti soal b, tetap menggunakan Protocol Hierarchy dan terlihat bahwa di bawah TCP terdapat sub-sub protocol TCP yang totalnya 8, yaitu Virtual Network Computing (VNC), Thrift Protocol, Telnet, Signaling Compression (SIGCOMP), Hypertext Transfer Protocol (HTTP), JavaScript Object Notation (JSON), HiPerConTracer Trace Service, serta Data`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/9PYxI2V.png)
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/XCfCuil.png)

  <br>
  <br>

> d. Ada berapa banyak packet dengan protokol TCP murni yang terekam pada traffic (tanpa data)?

> _d. How many packets with pure TCP protocol are recorded in the traffic (without data)?_

**Answer:** `3223`

- Filter expression

  `-`

- Explanation

  `Sama seperti soal b dan c yaitu menggunakan Protocol Hierarchy, di mana tertera bahwa total packets TCP adalah 9596. Jika yang ditanyakan adalah jumlah TCP murni (tanpa sub-protokol) dan tanpa data, maka tinggal dilakukan perhitungan    :`  
   `TCP - (VNC + Thrift + Telnet + SIGCOMP + HTTP + HiPerConTracer Trace Service + Data) ->`  
   `9596 - (3417 + 6 + 294 + 2 + 64 + 2 + 2558) = 3223`

- Output result  
  **Wireshark**  
  ![Alt Text](https://i.imgur.com/9PYxI2V.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/XCfCuil.png)

## Task 2

- Flag

`JARKOM25{N1c3_0ne_b4nggg_VYLEOWGDWRyuMM13yvggbtioiohtvwczhpldbc3r4t0ps38371870759672263420_b84b634d4af4a4fb1f2660a876242d60}`

> a. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag [ACK]?

> _a. How many packets succeed that are pure TCP based and have [ACK] flag?_

**Answer:** `3209`

- Filter expression

  `tcp.flags.ack == 1 && !tcp.analysis.flags`

- Explanation

  `Filter package digunakan untuk mencari yang memiliki flag ACK, maka gunakan tcp.flags.ack == 1. Selanjutnya gunakan filter untuk memastikan bahwa packetnya berhasil dengan memakai !tcp.analysis.flags. Selanjutnya buka Statistics lalu ke Protocol Hierarhy, lihat bagian TCP pada kolom End Packets untuk melihat berapa jumlah packet di mana protokol tersebut merupakan layer paling atas (murni TCP) yang sesuai dengan filter package yang telah diisikan.`

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/VdVW14N.png)  
  
  **Terminal**
  ![Alt Text](https://i.imgur.com/IEUu2cb.png)

  <br>
  <br>

> b. Berapa banyak packet berhasil yang berbasis murni TCP yang hanya memiliki flag [ACK]?

> _b. How many packets succeed that are pure TCP based and have only [ACK] flag?_

**Answer:** `3172`

- Filter expression

  `tcp.len == 0 && !tcp.analysis.flags && tcp.flags.ack == 1 && tcp.flags.syn == 0 && tcp.flags.fin == 0 && tcp.flags.reset == 0 && tcp.flags.push == 0 && tcp.flags.urg == 0`

- Explanation

  `Berdasarkan soal, maka cari yang murni tcp (seperti soal a) dengan filter package "tcp.len == 0". Lalu packet harus berhasil, tanpa keraguan, gunakan "!tcp.analysis.flags". Lalu hanya punya flag ACK, maka pastikan "tcp.flag.ack == 1", tetapi flag lain di nol-kan.`

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/zw7mzrY.png)  
  
  **Terminal**
  ![Alt Text](https://i.imgur.com/IEUu2cb.png)

  <br>
  <br>

> c. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag selain hanya [ACK]?

> _c. How many packets succeed that are pure TCP based and contain flags other than just [ACK] flag?_

**Answer:** `49`

- Filter expression

  `!tcp.flags == 0x10 && !tcp.analysis.flags`

- Explanation

  `Sama seperti soal a, gunakan !tcp.flags == 0x10 untuk memfilter selain TCP (0x10 merupakan kode hexadesimal TCP) lalu pastikan packetnya berhasil dengan tidak ada tcp.analysis.flags. Selanjutnya buka tab Statistics, kemudian klik Protocol Hierarchy, lihat bagian TCP di kolom End Packets.` 

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/KF69SAm.png)  
  
  **Terminal**
  ![Alt Text](https://i.imgur.com/IEUu2cb.png)

  <br>
  <br>

## Task 3

- Flag

`JARKOM25{W0w_Y0uU_h4V33e_d0n3_444_90od_j0bB_R9HS1g0dl1k341zc2qkggpvvlswaxnravl_2dee8d0a2ef37acf434ed0b7ac39014e}`

> a. Pada port berapa client telnet terbuka?

> _a. In what port is the telnet client open?_

**Answer:** `54184`

- Filter expression

  `tcp.dstport == 23`

- Explanation

  `Pada soal, ditanyakan port untuk telnet sisi client terbuka, maka filter package dengan "tcp.dstport == 23" karena yang dicari adalah packet tcp yang port destinationnya 23. Di mana 23 adalah port milik telnet. Ketika di serach, cari file yang hanya melakukan SYN ketika TCP-3 Way Handshake (dari Client -> Server). Bisa dilihat bahwa Source Port = 54184 berarti port client dan Destination Port = 23 yang menuju ke server telnet.`

- Output result  
  **Wireshark**
  ![Alt Text](https://i.imgur.com/wqEis2w.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/FyAET3d.png)

  <br>
  <br>

> b. Berapa byte file response yang dikirim dari server?

> _b. How many bytes of the response files are sent from the server?_

**Answer:** `1449`

- Filter expression

  `tcp.srcport == 23`

- Explanation

  `File response yang dikirim dari server (telnet), berarti kita mencari package yang source port == 23, sehingga filter package "tcp.srcport == 23". Selanjutnya, cari package yang melakukan [SYN, ACK] pada TCP 3-Way Handshake, yaitu ketika server mengirimkan kembali ke client. Kemudian klik kanan dan pilih Follow TCP Stream. Di bagian pojok kiri bawah terdapat jumlah bytes yang dikirimkan, pilih yang 172.16.16.102:23 (23 = server)-> 172.16.16.101:54184 (54184 = client). Tertera jumlahnya 1449 bytes. `

- Output result  

  **Wireshark**
  ![Alt Text](https://i.imgur.com/Ht2IoP6.png) 
  ![Alt Text](https://i.imgur.com/qAK7JGj.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/FyAET3d.png)

  <br>
  <br>

> c. Apa username yang digunakan client telnet untuk berhubungan dengan server?

> _c. What telnet client's username is used to connect with the server?_

**Answer:** `jovyan`

- Filter expression

  `-`

- Explanation

  `Sama seperti soal b, yang digunakan adalah Follow Stream TCP dari package yang sama. Cari sesuatu yang terkait dengan usernam dan password. Di bagian paling atas adanya login dan password, asumsi bahwa logi = username yang berarti setelah kata login adalah username client yaitu jovyan.`

- Output result  

  **Wireshark**
  ![Alt Text](https://i.imgur.com/Ht2IoP6.png)
  ![Alt Text](https://i.imgur.com/sntBo2U.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/FyAET3d.png)

  <br>
  <br>

> d. Apa password client telnet?

> _d. What is the telnet client's password?_

**Answer:** `123`

- Filter expression

  `-`

- Explanation

  `Sama seperti soal b dan c, tetap menggunakan Follow TCP Stream dan cari kata password. Di bagian atas tertera password tepat di bawah login yang diasumsikan sebagai username, maka tepat setelah kata password adalah password client yaitu 123.`

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/Ht2IoP6.png)
  ![Alt Text](https://i.imgur.com/HzXWKIM.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/FyAET3d.png)

  <br>
  <br>


## Task 4

- Flag

  `JARKOM25{G04t __ a4n4liz333er_NOYEUBQKGY1VN24ZZ
ZJKfr0ggfv9csy3bnoqsr6r3ys1051591209_30ee778f2ae347a99de00358ffedc54e}`

> a. Apa perintah pertama yang ditulis client pada koneksi telnet?

> _a. What is the first command that client wrote on telnet connection?_

**Answer:** `echo`

- Filter expression

  `tcp.srcport == 23`

- Explanation

  `Menggunakan Follow TCP Stream, ubah bagian pojok kiri bawah untuk melihal apa saja yang dikirimkan client ke server. Hal yang dapat diperhatikan adalah setelah mengisi password (123), terdapat echo, yaitu sebagai perintah pertama yang dikirimkan ke server. `

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/Ht2IoP6.png)
  ![Alt Text](https://i.imgur.com/BYpCB9w.png)  
  
  **Terminal**
  ![Alt Text](https://i.imgur.com/KVPLa40.png)

  <br>
  <br>

> b. Apa nama file .txt di server (ditulis bersama ekstensinya)?

> _b. What is the name of .txt file on the server (write with the extension)?_

**Answer:** `test.txt`

- Filter expression

  `tcp.srcport == 23`  
  `ctrl+f untuk mencari .txt`

- Explanation

  `Masih tetap menggunakan Follow TCP Stream di package yang sama seperti soal sebelumnya, ubah bagian pojok kiri bawah agar terlihat yang hanya dari server. Kemudian ctrl+f atau klik Find di bagian bawah untuk mencari di manna file .txt. File yang muncul adalah test.txt.`

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/Ht2IoP6.png)
  ![Alt Text](https://i.imgur.com/GrnzwBs.png)  
  
  **Terminal**
  ![Alt Text](https://i.imgur.com/KVPLa40.png)

  <br>
  <br>

> c. Apa kata pertama dari frasa yang dimasukkan client ke dalam file sebelumnya?

> _c. What is the first word that the client inserted into the previous file?_

**Answer:** `Jarkom`

- Filter expression

  `tcp.srcport == 23`

- Explanation

  `Masih sama seperti soal sebelumnya yang menggunakan Follow TCP Stream dari package yang sama. Seperti soal a, filternya ubah agar yang ditampilkan hanya dari client saja. Kemudian "dimasukkan ke dalam file sebelumnya" berarti input atau menggunakan "echo", gunakan ctrl+f atau langsung cari kalimat setelah echo yaitu "Jarkom gampang", frasa pertamanya adalah "Jarkom".`

- Output result

  **Wireshark**
  ![Alt Text](https://i.imgur.com/Ht2IoP6.png)
  ![Alt Text](https://i.imgur.com/BYpCB9w.png)  
  
  **Terminal**
  ![Alt Text](https://i.imgur.com/KVPLa40.png)

  <br>
  <br>

## Task 5

- Flag

`JARKOM25{n4il0ng_m1lk_dr4g000n_Q401E7K087U7A5HR2DCTW63F0061H5cr0chhv00z02q759c961jo2mb439_37f7dc86a15a51f18ead4b27473b1a10}`

> a. Berapa banyak packet berbasis HTTP yang terekam pada file pcapng?

> _a. How many HTTP packets are recorded in the pcapng file?_

**Answer:** `298`

- Filter expression

  `http`

- Explanation

  `Gunakan tab Statistics, kemudian pilih HTTP, lalu pilih Packet Counter. Pada bagian paling atas tertera total HTTP Packets adalah 298. Cara lainnya juga bisa menggunakan filter package dengan "http" kemudian lihat bagian bawah kanan terdapat tulisan displayed : 298.`

- Output result

  **Wireshark**   
  ![Alt Text](https://i.imgur.com/ULKQiJQ.png) 
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/QOyPLPr.png)

  <br>
  <br>

> b. Ada berapa HTTP packet yang berupa response?

> _b. How many response HTTP packets are recorded in the traffic?_

**Answer:** `149`

- Filter expression

  `http.response`

- Explanation

  `Sama seperti soal sebelumnya, bisa pakai HTTP Packet Counter yang mana langsung terlihat HTTP Response Packets totalnya 149. Cara lain, filter package dengan "http.response" dan lihat berapa jumlah displayed di bagian kanan bawah.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/Bz7xpJL.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/QOyPLPr.png)

  <br>
  <br>

> c. Ada berapa paket berbasis HTTP yang berhasil?

> _c. How many HTTP packets that succeed?_

**Answer:** `296`

- Filter expression

  `-`

- Explanation

  `Sama seperti soal sebelumnya, masih di HTTP Packet Counter, lihat bagian 2xx: Success yang tertera adalah 148, kemudian ada sub di dalamnya yaitu 200 OK yang isinya juga 148. Maka jumlahkan 148 + 148 = 296.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/ohGJqLu.png) 
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/QOyPLPr.png)

  <br>
  <br>

> d. Apa alamat IP dari client HTTP yang tersambung lokal dengan mesin lain?

> _d. What is the client HTTP IP Address in connection with other local machine?_

**Answer:** `172.16.16.101`

- Filter expression

  `tcp.dstport == 80 && tcp.flags.syn == 1`

- Explanation

  `Filter package dengan "tcp.dstport == 80" untuk mengecek mana package yang destination portnya mengarah ke HTTP (port = 80). Selanjutnya pastikan keduanya terhubung dengan mengecek flagsnya, pastikan [SYN] karena dalam 3-Way Handshake ketika SYN (tanpa ACK) pertama kali adalah ketika client terhubung ke server, dalam hal ini HTTP. Selanjutnya lihat IP Source yang merupakan milik client, yaitu 172.16.16.101`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/vQ4VAIE.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/QOyPLPr.png)

  <br>
  <br>

## Task 6 

- Flag

`JARKOM25{br0mb44rdin0u_Cr0ccc0c0c0cdi1l10l_1804742591awaesa7lpobrpkvmsh1n0buEW6UK7XJ2WNB2VP_38a7b2f3000ac597d2acb1f37e071423}`

> a. Apakah kamu menemukan fake flag? Tuliskan seluruhnya!

> _a. Did you find the fake flag? Write it whole!_

**Answer:** `FakeFlag{JarkomGampang}`

- Filter expression

  `-`
  `ctrl+f(string) -> flag`

- Explanation

  `Saya mengasumsikan mungkin ada package yang bernama flag atau sejenisnya. Search dilakukan dengan ctrl+f yang telah diganti ke string kemudian cari "flag" dan ketemu satu package yang mengandung flag.txt. Kemudian klik kanan package tersebut, klik Follow TCP Stream dan ada string aneh yaitu "FakeFlag{JarkomGampang}".`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/udO5dO1.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/FTIbzqE.png)

  <br>
  <br>

> b. Tuliskan username dan password yang tertulis! (format username:password)

> _b. Write the written username and password! (format username:password)_

**Answer:** `Rey:123`

- Filter expression

  `http`
  `ctrl+f (string) -> pass`

- Explanation

  `Login akun pasti berkaitan dengan http, kemudian filter package dengan "http". Untuk memudahkan karena tidak bisa menebak dalam bentuk bagaimana tulisan username dan password, gunakan ctrl+f yang telah diganti ke string lalu ketik "pass" dan ketika muncul suatu package, klik kanan, lalu Follow TCP Stream dan tertera nama (Rey) yang diasumsikan sebagai username, serta bawahnya (123) adalah password.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/m3MaTPh.png)
  ![Alt Text](https://i.imgur.com/Vdpan3f.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/FTIbzqE.png)

  <br>
  <br>

## Task 7

- Flag
  `JARKOM25{tr4l4lel0_tr1lil1_vv9rngc5h4k3b0s0sIC01MVL7S3A3CQN_e20db4bb5c36bda5402ff12dff75c0cc}`

> Apa nama gambar yang direquest oleh client? (tulis dengan ekstensinya)

> _What is the image that is being requested by the client? (write with its extension)_

**Answer:** `donalbebek.jpg`

- Filter expression

  `http.request atau http.request.uri matches ".(jpg|jpeg|png|gif)$"`
  `ctrl+f(string) -> .jpg`

- Explanation

  `Cari dengan filter package bahwa yang dicari adalah request client ke http. Cara sederhananya adalah cari "http.request", lalu gabungkan dengan filter string ".jpg", ".jpeg", "png", "gif" yang merupakan jenis ekstensi yang dipakai untuk gambar. Cara lain adalah langsung "http.request.uri matches ".(jpg|jpeg|png|gif)$""`.

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/x6yl9AM.png)
  ![Alt Text](https://i.imgur.com/qGJHSmY.png)
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/L2BJRC4.png)

  <br>
  <br>

## Task 8

- Flag

  `JARKOM25{y0u_4r3_s0_G00d_1n_F0r3nsic_GL3S2S60UTKGWYG1JRZLPC
SYMDTJXAx45y4n6phurqxs0g2391fk420pyaa9_5c1d406835dc20114f0f5da2c632740d}`

> a. Berapa banyak packet berbasis FTP yang terekam pada file pcapng? (with the data)

> _a. How many FTP packets are recorded in the pcapng file? (with the data)_

**Answer:** `81`

- Filter expression

  `ftp || ftp-data`

- Explanation

  `Untuk mencari tahu jumlah ftp, filter package dengan "ftp". Kemudian karena ada penjelasan bahwa tambahkan dengan data, maka ubah filter package jadi "ftp || ftp-data" untuk melihat jumlah keduanya. Lihat bagian kanan bawah terdapat jumlah package yang sesuai (displayed = 81).`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/eAbrDDh.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/jH8QBE9.png)

  <br>
  <br>

> b. Apa username dan password client di koneksi FTP? (tulis dalam format username:password)

> _b. What is the client's username and password in FTP connection? (write in following format username:password)_

**Answer:** `rey:password123lingangu`

- Filter expression

  `-`
  `ctrl+f(string) -> "pass" dan "user"`

- Explanation

  `Saya menggunakan ctrl+f(string) pertama kali untuk memperkirakan bentuk username dan passwordnya bagaimana. Saya tidak menggunakan filter package karena bagaimanapun filter package kalau tidak tau kata kunci persisnya juga tidak akan bisa ketemu. Tetapi jika perkiraan kata kuncinya benar, bisa menggunakan filter package.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/QhzyB64.png)
  ![Alt Text](https://i.imgur.com/BfMSiuv.png)
  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/jH8QBE9.png)

  <br>
  <br>

> c. What is the client's command for showing server directory that was sent on request packet?

> _c. Apa command client untuk melihat direktori server yang dikirimkan dalam request packet?_

**Answer:** `LIST`

- Filter expression

  `ftp.request.command == "LIST" || ftp.request.command == "NLST"`

- Explanation

  `Biasanya command yang digunakan client untuk melihat direktori adalah antara LIST (menampilkan daftar file/direktori beserta detail) atau NLST (hanya menampilkan file/direktori saja). Setelah filter package, hanya ada command LIST, berarti yang digunakan client adalah LIST. Dapat dipastikan juga dengan mengecek isinya menggunakan Follow TCP Stream.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/LRtnRl2.png)
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/jH8QBE9.png)

  <br>
  <br>

## Task 9

- Flag

  `JARKOM25{j4rk000000mmm_g4mpp4444n9999999_05624527678i41L4hz01lr65jog321k0ncol5VXJ9HNN1LD0R5F_a3408edf53110965d8fc8557d5718e9f}`

> a. Apa alamat IP dari FTP server?

> _a. What is the FTP server IP Address?_

**Answer:** `172.16.16.101`

- Filter expression

  `tcp.port == 21 && tcp.flags.syn == 1 && tcp.flags.ack == 1 `

- Explanation

  `Cara mencari IP dari server adalah ketika server mengirim data ke client saat 3-Way Handshake, berarti ketika [SYN-ACK]. Maka filter package yang merupakan ftp (tcp.port = 21) yang statusnya SYN dan ACK. Lihat IP sourcenya yaitu 172.16.16.101. Hal ini juga sesuai dengan Source Port yang menunjukkan port FTP dan Destination Portnya ke client.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/FQ60Q9R.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/INhyAUJ.png)

  <br>
  <br>

> b. Berapa banyak file yang ada dalam direktori FTP server?

> _b. How many files are there inside the FTP server directory?_

**Answer:** `7`

- Filter expression

  `ftp-data`

- Explanation

  `Filter package dengan "ftp-data" untuk bisa melihat mana package yang mengandung data dan dikirim lewat FTP. Setelah itu terlihat bahwa ada 10 package yang terdisplay (lihat kanan bawah). Kurangi dengan package yang berisi command LIST karena bukan file data, berarti 10 - 3 = 7 file.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/Ff0XAaf.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/INhyAUJ.png)

  <br>
  <br>

> c. Apa nama dari file yang digunakan dalam page.html? (tulis lengkap namanya beserta ekstensinya dan dipisahkan dengan koma ',')

> _c. What are the filenames used in the page.html? (write the filebames with their extensions and separate them with comma ',')_

**Answer:** `pokijan.jpg,research_center.jpg`

- Filter expression

  `ftp-data`

- Explanation

  `Filter package dengan "ftp-data" untuk bisa melihat mana package yang mengandung data dan dikirim lewat FTP. Setelah di search, ada package yang bernama page.html, kemudian klik kanan dan Follow TCP Stream untuk melihat isinya. Di dalamnya terdapat nama file foto yaitu pokijan.jpg dan research_center.jpg.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/DQUmBKo.png) 
  ![Alt Text](https://i.imgur.com/M5SCcQc.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/INhyAUJ.png)

  <br>
  <br>

## Task 10

- Flag

  `JARKOM25{f1nisssshs55s5s533s_l1n333ee333E3_20101542472910525spcvsa9345215123123NASG2PBGLZVCK6E_a55608284856e94f8ca259381f7f7514}`

> a. Apa nama file yang mengandung string terencode?

> _a. What is the filename that contains encoded string?_

**Answer:** `secret.txt`

- Filter expression

  `ftp-data`

- Explanation

  `Saya memperkirakan bahwa string yang belum didecode berada di file .txt sehingga saya menggunakan filter package "ftp-data" untuk melihat mana saja package yang mengandung data. Setelah di search, hanya ada 2 file .txt yaitu secret.txt dan secret1.txt. Dengan asumsi bahwa file utama adalah secret.txt dan secret.txt adalah salinan (alasannya di soal b), maka dapat dipastikan string aneh tersebut ada di file secret.txt. Kemudian klik kanan package tersebut dan Follow TCP Stream untuk melihat isinya.`

- Output result
 
  **Wireshark**  
  ![Alt Text](https://i.imgur.com/mH40lfI.png) 
  ![Alt Text](https://i.imgur.com/27g6KGz.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/qHvE1AI.png)

  <br>
  <br>

> b. Apa nama file hasil copy file sebelumnya?

> _b. What is the filename of the previous file copy?_

**Answer:** `secret1.txt`

- Filter expression

  `ftp atau ftp.response`

- Explanation

  `Setelah mengerjakan soal a, saya memperkirakan bahwa file secret1.txt merupakan salinan dari file secret.txt yang dapat dicek dengan melihat isinya yang sama. Kemudian filter package dengan ftp atau ftp.response guna mencari package yang berisi aktivitas client, yaitu ketika client request LIST untuk melihat isi direktori dan mengklik file di dalamnya. Buka package tersebut dengan Follow TCP Stream dan terdapat RETR secret.txt yaitu client mengunduh file secret.txt (retrieve), kemudian MDTM secret.txt yaitu saat client cek timestamp terakhir kali pengeditan secret.txt (modification time), terakhir STOR secret1.txt yaitu saat client upload file baru bernama secret1.txt (store). Yang mana isinya persis sama dengan file secret.txt, maka jelas secret1.txt adalah salinan dari secret.txt.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/waMWAkB.png)
  ![Alt Text](https://i.imgur.com/0RQDVi5.png)
  ![Alt Text](https://i.imgur.com/RiYhX6h.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/qHvE1AI.png)

  <br>
  <br>

> c. What is the decoded string from the previous file?

> _c. Apa decoded string dari file tersebut?_

**Answer:** `Pada suatu hari Rey bertemu dengan Nailong the Milk Dragon. Ketika bertemu, Rey mengajarkan Nailong apa itu Jaringan Komputer. Nailong pun senang karena ternyata Jaringan Komputer itu gampang.`

- Filter expression

  `ftp-data`

- Explanation

  `Sama seperti soal a, gunakan filter ftp-data untuk mencari mana package yang mengandung data. Klik kanan package secret.txt lalu Follow TCP Stream. Saya menggunakan https://www.base64decode.org/ untuk decode string aneh tersebut dan muncullah kata-kata seperti di atas.`

- Output result

  **Wireshark**  
  ![Alt Text](https://i.imgur.com/27g6KGz.png) 
  ![Alt Text](https://i.imgur.com/T0AGujh.png)  
  
  **Terminal**  
  ![Alt Text](https://i.imgur.com/qHvE1AI.png)

  <br>
  <br>

## Summary
Praktikum modul 1 mencakup Wireshark dan Crimping. Untuk Modul wireshark sendiri yang diuji adalah lebih ke mencari angka sesuai soal terkait dengam penggunaan filter package, displayed, filter string, protocol hierarchy, dan semacamnya. Digunakan pula netcat untuk menghubungkan ke server dalam pengumpulan jawaban. Sedangkan untuk crimpin, fokusnya adalah memasang kabel UTP dengan RJ-45 sebagai konektornya. 
## Problems
Tidak ada masalah tertentu, hanya kesulitan di soal nomor 2 dan 3 dan cukup membuang waktu lama memecahkan soal nomor 2. Tetapi pada akhirnya nomor 2 selesai meskipun nomor 3 akhirnya tidak sempat terselesaikan.

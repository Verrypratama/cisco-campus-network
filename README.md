# Perancangan Topologi Jaringan Kampus Multi-Fakultas

## Ringkasan Proyek
Proyek ini merupakan simulasi infrastruktur jaringan LAN untuk area kampus bertingkat/multi-fakultas menggunakan Cisco Packet Tracer. Perancangan ini menerapkan teknik Variable Length Subnet Masking (VLSM) untuk pengalamatan IP yang efisien, penamaan segmen fakultas yang terstruktur, koneksi point-to-point antarruter, serta isolasi segmen server kampus.

## Arsitektur Jaringan
![Topologi Jaringan Kampus](Gambar%20Topologi.PNG)

### Fitur Utama Jaringan
* Segmentasi Multi-Fakultas: Pemisahan subnet untuk Fakultas Ekonomi, Fakultas Hukum, Fakultas Teknik, Fakultas Sastra, dan segmen Server Kampus.
* Efisiensi Pengalamatan IP (VLSM): Pembagian alokasi IP menggunakan subnet /26, /27, /28, dan /30 dari blok IP dasar 182.26.51.0.
* Routing Antarruter: Komunikasi antar-ruter fakultas menggunakan koneksi Point-to-Point (P2P) berbasis subnet /30.
* Isolasi Server: Server diletakkan di segmen tersendiri agar seluruh lalu lintas akses data melewati ruter utama terlebih dahulu.

## Skema Pengalamatan IP dan Subnetting

* Subnet Fakultas Ekonomi
  * Network ID: 182.26.51.0
  * Subnet Mask: 255.255.255.192 (/26)
  * Rentang IP usable: 182.26.51.1 – 182.26.51.62
  * Default Gateway: 182.26.51.1

* Subnet Fakultas Hukum
  * Network ID: 182.26.51.96
  * Subnet Mask: 255.255.255.224 (/27)
  * Rentang IP usable: 182.26.51.97 – 182.26.51.126
  * Default Gateway: 182.26.51.97

* Subnet Fakultas Teknik
  * Network ID: 182.26.51.64
  * Subnet Mask: 255.255.255.224 (/27)
  * Rentang IP usable: 182.26.51.65 – 182.26.51.94
  * Default Gateway: 182.26.51.65

* Subnet Fakultas Sastra
  * Network ID: 182.26.51.128
  * Subnet Mask: 255.255.255.240 (/28)
  * Rentang IP usable: 182.26.51.129 – 182.26.51.142
  * Default Gateway: 182.26.51.129

* Subnet Server
  * Network ID: 182.26.51.144
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 182.26.51.145 – 182.26.51.146
  * Default Gateway: 182.26.51.145

* Subnet 1 (P2P Ruter Ekonomi – Hukum)
  * Network ID: 182.26.51.148
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 182.26.51.149 – 182.26.51.150
  * Default Gateway: Tidak ada

* Subnet 2 (P2P Ruter Hukum – Server)
  * Network ID: 182.26.51.152
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 182.26.51.153 – 182.26.51.154
  * Default Gateway: Tidak ada

* Subnet 3 (P2P Ruter Server – Sastra)
  * Network ID: 182.26.51.156
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 182.26.51.157 – 182.26.51.158
  * Default Gateway: Tidak ada

* Subnet 4 (P2P Ruter Ekonomi – Teknik)
  * Network ID: 182.26.51.160
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 182.26.51.161 – 182.26.51.162
  * Default Gateway: Tidak ada

## Penamaan Perangkat Standar

* Router0 (Packet Tracer)
  * Nama Standar: R-EKONOMI-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Fakultas Ekonomi

* Router1 (Packet Tracer)
  * Nama Standar: R-HUKUM-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Fakultas Hukum

* Router2 (Packet Tracer)
  * Nama Standar: R-TEKNIK-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Fakultas Teknik

* Router3 (Packet Tracer)
  * Nama Standar: R-CORE-SERVER
  * Tipe: Cisco Router
  * Peran: Ruter Pusat / Segmen Server

* Router4 (Packet Tracer)
  * Nama Standar: R-SASTRA-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Fakultas Sastra

* Server0 (Packet Tracer)
  * Nama Standar: SRV-CAMPUS-01
  * Tipe: Dedicated Server
  * Peran: Server Pusat Kampus

## Langkah-Langkah Pengerjaan

### 1. Perencanaan Subnetting (VLSM)
Saya menghitung kebutuhan alamat IP berdasarkan kapasitas tiap fakultas:
* Fakultas Ekonomi: subnet /26 (kapasitas hingga 62 host).
* Fakultas Hukum: subnet /27 (kapasitas hingga 30 host).
* Fakultas Teknik: subnet /27 (kapasitas hingga 30 host).
* Fakultas Sastra: subnet /28 (kapasitas hingga 14 host).
* Segmen Server: subnet /30 (2 host usable).
* Jalur koneksi antar-ruter (Subnet 1–4): subnet /30 (2 host usable per alur).

### 2. Penyusunan Topologi dan Perkabelan
* Menambahkan 5 ruter dan switch di tiap area fakultas.
* Menghubungkan PC/Laptop ke switch masing-masing fakultas menggunakan kabel Straight-Through.
* Menghubungkan ruter antar-fakultas dan ke ruter server menggunakan kabel Serial / Ethernet sesuai desain.

### 3. Konfigurasi Alamat IP
* Mengisi IP statis, subnet mask, dan default gateway pada perangkat PC dan Laptop.
* Memasang alamat IP pada seluruh interface ruter.

### 4. Pengaturan Routing
* Mengkonfigurasi routing antar-ruter agar seluruh segmen fakultas dapat saling berkomunikasi dan mengakses server kampus.

### 5. Pengujian dan Verifikasi
* Melakukan uji konektivitas ICMP ping antar-PC beda fakultas.
* Menguji aksesibilitas PC ke server kampus.
* Memeriksa jalur data menggunakan perintah tracert / traceroute.

## Cara Menjalankan File Simulasi
1. Clone repositori ini ke komputer lokal:
   ```bash
   git clone [https://github.com/Verrypratama/cisco-campus-network.git](https://github.com/Verrypratama/cisco-campus-network.git)

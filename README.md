# TUGAS NAT - IP MASQUERADING
## Oleh:
- Kadek Nesya Kurnia Dewi (05311840000009)
- Rindi Kartika Sari (05311840000013)
- Desya Ananda Puspita Dewi (05311840000046)
  
## Teori Singkat
**IP Masquerade** adalah proses dimana 1 (satu) komputer bertindak sebagai _gateway IP_ untuk jaringan. Semua komputer di jaringan mengirim paket IP mereka melalui _gateway_, kemudian _gateway_ akan mengganti _Source IP Address_ dengan _gateway IP_. Lalu, meneruskannya ke internet. 

## Topologi yang Digunakan

![topologi masquerade](https://user-images.githubusercontent.com/49342639/103990767-51a2dd80-51c4-11eb-84f8-e57f10a670f1.jpg)

**Penjelasan Topologi**:

Untuk mengimplementasikan **IP Masquerade** ini, maka kami menyediakan **1 Router** dan **1 Server**. Media yang kami gunakan untuk mengkonfigurasi router dan server ini adalah **Ubuntu Live Server 20.04 (Virtual Machine)**.

Perlu diperhatikan pula terkait dengan adapter yang digunakan oleh Router dan Server tersebut, yakni:
- **Router** menggunakan adapter **enp0s3** agar terhubung dengan **_Cloud_** (Internet).
- **Router** menggunakan adapter **enp0s8** agar terhubung dengan **Server**.
- **Server** menggunakan adapter **enp0s3** agar terhubung dengan **Router**.

### Pembagian IP Address
_IP Address_ yang diberikan kepada Router dan Server adalah sebagai berikut:

| Adapter | IP Address             |
| :---:  | :---:           |
| **enp0s3** (Router-Cloud)     | DHCP (10.0.2.15/24)     |
| **enp0s8** (Router-Server)     | 192.168.1.1/24  |
| **enp0s3** (Server-Router)     | 192.168.1.2/24  | 

## Demontrasi
### Tahap Persiapan
1. Menyiapkan **Server** dan **Router** pada _virtual machine_ **Ubuntu Live Server 20.04**.
   
    a. Pembuatan **Server** dengan melakukan penginstallan **Ubuntu Live Server 20.04** pada VirtualBox dengan:
     - nama sistem operasi yaitu **server**
  
      ![2](https://user-images.githubusercontent.com/49342639/103995471-1e178180-51cb-11eb-95ae-467928bfa3d5.jpg)

     - _memory size_ sebesar **4096 MB**
     
      ![3](https://user-images.githubusercontent.com/49342639/103995566-3be4e680-51cb-11eb-9743-b9c3e82a12ef.jpg)

     -  _file size_ sebesar **10.00 GB**
  
      ![7](https://user-images.githubusercontent.com/49342639/103995904-abf36c80-51cb-11eb-8d04-49e8ee45b075.jpg)

     -  _hard disk file type_ yakni **VDI VirtualBox Disk Image)**
    
      ![5](https://user-images.githubusercontent.com/49342639/103995817-90886180-51cb-11eb-897d-f999b2c9bd95.jpg)

     -  _storage on physical hardisk_ diatur pada **Dynamically allocated**
    
      ![6](https://user-images.githubusercontent.com/49342639/103995944-bca3e280-51cb-11eb-818b-c0feccf325c5.jpg)

     -  memasukkan ISO Ubuntu Live Server 20.04 pada pilihan **Setting**
    
      ![1](https://user-images.githubusercontent.com/49342639/103996035-dba27480-51cb-11eb-8136-147735704de6.jpg)

  
    b. Pembuatan **Router** dengan melakukan _clone_ dari **Server** yang telah dibuat:
    - _Clone_ **Server** untuk **Router** dengan _Full Clone_ dan tunggu hingga proses  _cloning_ selesai
  
     ![clone1](https://user-images.githubusercontent.com/49342639/103996243-22906a00-51cc-11eb-9932-a63eab7387a9.jpg)

     ![clone2](https://user-images.githubusercontent.com/49342639/103996252-24f2c400-51cc-11eb-817b-0489ec0e92f3.JPG)

     ![clone3](https://user-images.githubusercontent.com/49342639/103996254-2623f100-51cc-11eb-81e7-197ef3830cb9.jpg)

     ![clone4](https://user-images.githubusercontent.com/49342639/103996257-26bc8780-51cc-11eb-95a2-b75ec973220c.JPG)

2. Memulai untuk menjalankan **router** dan mengatur _IP Address_ untuk **Router** pada file ```etc/netplan/00-installer-config.yaml```:
   
   ![net-router](https://user-images.githubusercontent.com/49342639/103997602-e52cdc00-51cd-11eb-8222-817b9c2afa60.JPG)

   **Keterangan**:
   - Adapter ```enp0s3``` yang digunakan oleh **Router** agar terhubung dengan **_Cloud_**(Internet) menggunakan DHCP ```dhcp4: true```
   - Sedangkan, adapter ```enp0s8``` yang digunakan oleh **Router** agar terhubung dengan **Server** menggunakan _Static IP_ yaitu ```addresses: [192.168.1.1/24]```. Dikarenakan menggunakan _Static IP_, maka fungsi DHCP dimatikan pada adapter **enp0s8** ini ```dhcp4:false```

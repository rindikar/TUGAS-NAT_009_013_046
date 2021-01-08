# TUGAS NAT - IP MASQUERADING
## Oleh:
- Kadek Nesya Kurnia Dewi (05311840000009)
- Rindi Kartika Sari (05311840000013)
- Desya Ananda Puspita Dewi (05311840000046)
  
## Teori Singkat
**IP Masquerade** adalah teknik menyembunyikan seluruh ruang _Private IP Address_ di belakang 1 (satu) _IP Address_ di ruang alamat lain (biasanya _Public IP Address_).

**IP Masquerade** menggunakan teknik _many-to-one translation_, dimana teknik ini memungkinkan banyak _Private IP Address_ untuk berbagai 1 (satu) _IP Address_ internet secara bersamaan.

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

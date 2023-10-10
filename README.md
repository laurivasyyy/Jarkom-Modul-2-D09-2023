# **Lapres Praktikum Jarkom Modul 2 Kelompok D-09**
## **Nama Kelompok**
|**Nama**|**NRP**|
|--------|-------|
|Laurivasya Gadhing Syahafidh|5025211136|
|Dafarel Fatih Wirayudha     |5025211120|

## **Daftar Soal**
1. [Soal 1](#Soal-1)
2. [Soal 2](#Soal-2)
3. [Soal 3](#Soal-3)
4. [Soal 4](#Soal-4)
5. [Soal 5](#Soal-5)
6. [Soal 6](#Soal-6)
7. [Soal 7](#Soal-7)
8. [Soal 8](#Soal-8)
9. [Soal 9](#Soal-9)
10. [Soal 10](#Soal-10)
11. [Soal 11](#Soal-11)
12. [Soal 12](#Soal-12)
13. [Soal 13](#Soal-13)
14. [Soal 14](#Soal-14)
15. [Soal 15](#Soal-15)
16. [Soal 16](#Soal-16)
17. [Soal 17](#Soal-17)
18. [Soal 18](#Soal-18)
19. [Soal 19](#Soal-19)
20. [Soal 20](#Soal-20)

### Soal-1
> Yudhistira akan digunakan sebagai DNS Master, >Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut

**Solusi :**

![topologi](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/cd2550ae557469d89f7412a888c4241be227e325/assets/topologi.png)

1. Click tombol `Add Blank Project`, lalu beri nama project. Jika project sudah diberi nama, maka click tombol `Add Project`.
2. Click tombol `Add Node` pada menu bar bagian atas dan pilih `ubuntu-1`, lalu drag kedalam page.
3. Click kanan `ubuntu-1` dan pilih command `Change Hostname` menjadi `Pandudewanata`.
4. Click kanan `Pandudewanata` dan pilih command `Change Symbol` menjadi seperti gambar diatas.
5. Lakukanlah langkah 2 dan langkah 3 untuk `Nakula`,`Sadewa`, `Yudhistira`, `Werkudara`, `Prabukusuma`, `Abimanyu`, `Wisanggeni` sehingga menjadi seperti gambar diatas.
6. Lalu, lakukanlah langkah 2 hingga langkah 4 untuk `Arjuna` sebagai `loadbalancer`.
7. Jika sudah, click tombol `Add Node`.Lalu, drag `NAT1` dan 3 `Ethernet switch` ke dalam page.
8. Click tombol `Add Link` pada menu bar bagian atas dan tambahkan link seperti gambar diatas.
9. Setelah melakukan langkah-langkah diatas, kita akan setting network pada masing-masing node. Click kanan pada node lalu click `Configure` dan scroll hingga menemukan command `Edit Network Configuration`. Kita bisa menghapus semua settingsnya dan menggantinya dengan settingan berikut :
* **Pandudewanata**
``` auto eth0
 iface eth0 inet dhcp

 auto eth1
 iface eth1 inet static
 address 10.26.1.1
 netmask 255.255.255.0

 auto eth2
 iface eth2 inet static
 address 10.26.2.1
 netmask 255.255.255.0

 auto eth3
 iface eth3 inet static
 address 10.26.3.1
 netmask 255.255.255.0 
 ```

 * **Nakula**
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.1.2
 netmask 255.255.255.0
 gateway 10.26.1.1
 ```

 * **Sadewa** 
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.1.3
 netmask 255.255.255.0
 gateway 10.26.1.1
```

* **Yudhistira**
```
 auto eth0
 iface eth0 inet static
 address 10.26.2.2
 netmask 255.255.255.0
 gateway 10.26.2.1
 ```

 * **Werkudara**
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.2.3
 netmask 255.255.255.0
 gateway 10.26.2.1
 ```

 * **Prabukusuma**
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.3.2
 netmask 255.255.255.0
 gateway 10.26.3.1
 ```

 * **Abimanyu**
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.3.3
 netmask 255.255.255.0
 gateway 10.26.3.1
 ```

 * **Wisanggeni**
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.3.4
 netmask 255.255.255.0
 gateway 10.26.3.1
 ```

 * **Arjuna**
 ```
 auto eth0
 iface eth0 inet static
 address 10.26.3.5
 netmask 255.255.255.0
 gateway 10.26.3.1
 ```
10. Restart semua node
11. Cek semua node ubuntu apakah sudah memiliki ip yang sesuai dengan settingan dengan command `ip a`. Berikut adalah contoh untuk node Pandudewanata dengan Prefix IP 10.26, yang sudah disesuaikan dengan Prefix IP kelompok masing-masing.
 ![ip-a](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/e077a293c2a17e1fefa9aebf2008480735239b74/assets/Screenshot%202023-10-10%20at%2022.20.43.png)
12. Ketikkan
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.26.0.0/16
```
pada router `Pandudewanata` 
Keterangan:
* `iptables` : iptables merupakan suatu tools dalam sistem operasi Linux yang berfungsi sebagai filter terhadap lalu lintas data. Dengan iptables inilah kita akan mengatur semua lalu lintas dalam komputer, baik yang masuk, keluar, maupun yang sekadar melewati komputer kita. Untuk penjelasan lebih lanjut nanti akan dibahas pada Modul 5.
* `NAT` (Network Address Translation): Suatu metode penafsiran alamat jaringan yang digunakan untuk menghubungkan lebih dari satu komputer ke jaringan internet dengan menggunakan satu alamat IP.
* `Masquerade`: Digunakan untuk menyamarkan paket, misal mengganti alamat pengirim dengan alamat router.
* `-s` (Source Address): Spesifikasi pada source. Address bisa berupa nama jaringan, nama host, atau alamat IP.
13. Ketikkan command `cat /etc/resolv.conf` di Pandudewanata
  ```
  nameserver 192.168.122.1
  ```
14. Lalu, ketikkan command ini di node ubuntu yang lain `echo nameserver 192.168.122.1 > /etc/resolv.conf`
15. Semua node sekarang seharusnya sudah bisa melakukan `ping google.com`, yang artinya adalah sudah tersambung ke internet



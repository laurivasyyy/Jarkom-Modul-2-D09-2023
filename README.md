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
 address 10.61.1.1
 netmask 255.255.255.0

 auto eth2
 iface eth2 inet static
 address 10.61.2.1
 netmask 255.255.255.0

 auto eth3
 iface eth3 inet static
 address 10.61.3.1
 netmask 255.255.255.0 
 ```

 * **Nakula**
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.1.2
 netmask 255.255.255.0
 gateway 10.61.1.1
 ```

 * **Sadewa** 
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.1.3
 netmask 255.255.255.0
 gateway 10.61.1.1
```

* **Yudhistira**
```
 auto eth0
 iface eth0 inet static
 address 10.61.2.2
 netmask 255.255.255.0
 gateway 10.61.2.1
 ```

 * **Werkudara**
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.2.3
 netmask 255.255.255.0
 gateway 10.61.2.1
 ```

 * **Prabukusuma**
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.3.2
 netmask 255.255.255.0
 gateway 10.61.3.1
 ```

 * **Abimanyu**
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.3.3
 netmask 255.255.255.0
 gateway 10.61.3.1
 ```

 * **Wisanggeni**
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.3.4
 netmask 255.255.255.0
 gateway 10.61.3.1
 ```

 * **Arjuna**
 ```
 auto eth0
 iface eth0 inet static
 address 10.61.3.5
 netmask 255.255.255.0
 gateway 10.61.3.1
 ```



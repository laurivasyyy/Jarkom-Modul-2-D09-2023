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

## Soal-1
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

## Soal 2 
> Buatlah website utama dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

### Script
**Yudhistira**
```
zone "arjuna.d09.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.d09.com";
        allow-transfer { 10.26.3.5; }; // IP Arjuna
};' > /etc/bind9/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/arjuna.d09.com

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.d09.com. root.arjuna.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.d09.com.
@       IN      A       10.26.2.2     ; IP Yudhistira
www     IN      CNAME   arjuna.d09.com.' > /etc/bind/jarkom/arjuna.d09.com

service bind9 restart
```

**Arjuna**

Setup nameserver terlebih dahulu yang diarahkan ke `IP Node yudhistira`
```
ping arjuna.d09.com -c 5
ping www.arjuna.d09.com -c 5
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%202.png)


## Soal 3
> Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

### Script

**Yudhistira**
```
zone "arjuna.d09.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.d09.com";
        allow-transfer { 10.26.3.5; }; // IP Arjuna
};

zone "abimanyu.d09.com" {
        type master;
        file "/etc/bind/jarkom/abimanyu.d09.com";
        allow-transfer { 10.26.3.5; }; // IP Arjuna
};' > /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.d09.com

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d09.com. root.abimanyu.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.d09.com.
@       IN      A       10.26.2.2     ; IP Yudhistira
www     IN      CNAME   abimanyu.a09.com.' > /etc/bind/jarkom/abimanyu.d09.com

service bind9 restart
```

**Abimanyu**

Jangan lupa untuk setup nameserver terlebih dahulu yang diarahkan ke `IP Node yudhistira`
```
ping abimanyu.d09.com -c 5
ping www.abimanyu.d09.com -c 5
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%203.png)

## Soal 4
> Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

### Script

**Yudhistira**

Tambahkan ``parikesit IN    A       10.26.3.3     ; IP Abimanyu' > /etc/bind/jarkom/abimanyu.d09.com`` saja pada DNS Master.

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d09.com. root.abimanyu.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.d09.com.
@       IN      A       10.26.2.2     ; IP Yudhistira
www     IN      CNAME   abimanyu.a09.com.
parikesit IN    A       10.26.3.3     ; IP Abimanyu' > /etc/bind/jarkom/abimanyu.d09.com

service bind9 restart
```

**Abimanyu**
```
ping parikesit.abimanyu.d09.com -c 5
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%204.png)

## Soal 5
> Buat juga reverse domain untuk domain utama.

### Script
Untuk melakukan reverse domain, kita perlu untuk mengetahui `IP` dari `Abimanyu`. `IP Abimanyu` kelompok kami adalah `10.26.3.3`, maka kita perlu mengubahnya menjadi `3.3.26.10`

**Yudhistira**
```
zone "3.26.10.in-addr.arpa" {
        type master;
        file "/etc/bind/jarkom/3.26.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/3.26.10.in-addr.arpa

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d09.com. root.abimanyu.d09.com. (
                        2003101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.26.10.in-addr.arpa.   IN      NS      abimanyu.d09.com.
3                       IN      PTR     abimanyu.d09.com.
5                       IN      PTR     arjuna.d09.com.' > /etc/bind/jarkom/3.26.10.in-addr.arpa

service bind9 restart
```

**Nakula/Sadewa**
Jangan lupa untuk mengembalikan `nameserver` ke DNS Master
```
host -t PTR 10.26.3.3
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%205.png)

## Soal 6
> Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

### Script
**Yudhistira**
```
zone "arjuna.d09.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.d09.com";
        allow-transfer { 10.26.2.2; }; // IP Werkudara
};

zone "abimanyu.d09.com" {
        type master;
        notify yes;
        also-notify { 10.26.2.3; }; // IP Werkudara
        allow-transfer { 10.26.2.3; }; // IP Werkudara
        file "/etc/bind/jarkom/abimanyu.d09.com";
};

zone "3.26.10.in-addr.arpa" {
        type master;
        file "/etc/bind/jarkom/3.26.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

// lalu stop bind9, untuk melakukan testing slave

service bind9 restart
service bind9 stop
```

**Werkudara (DNS Slave)**
```
zone "abimanyu.d09.com" {
    type slave;
    masters {10.26.2.2; }; // IP Yudhistira
    file "/var/lib/bind/abimanyu.d09.com";
};

service bind9 restart
```

**Abimanyu**
```
ping abimanyu.d09.com -c 5
ping www.abimanyu.d09.com -c 5
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%206.png)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%206.2.png)

## Soal 7
> Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda

### Script
**Yudhistira**
```;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d09.com. root.abimanyu.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.d09.com.
@       IN      A       10.26.2.2     ; IP Yudhistira
www     IN      CNAME   abimanyu.a09.com.
parikesit IN    A       10.26.3.3     ; IP Abimanyu
ns1     IN      A       10.26.2.3     ; IP Werkudara
baratayuda IN   NS      ns1

echo "options {
    directory \"/var/cache/bind\";

    // If there is a firewall between you and nameservers you want
    // to talk to, you may need to fix the firewall to allow multiple
    // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

    // If your ISP provided one or more IP addresses for stable
    // nameservers, you probably want to use them as forwarders.
    // Uncomment the following block, and insert the addresses replacing
    // the all-0's placeholder.

    // forwarders {
    //      0.0.0.0;
    // };

    //========================================================================
    // If BIND logs error messages about the root key being expired,
    // you will need to update your keys.  See https://www.isc.org/bind-keys
    //========================================================================
    //dnssec-validation auto;

    allow-query { any; };
    auth-nxdomain no;
    listen-on-v6 { any; };
};" > /etc/bind/named.conf.options

service bind9 restart
```

**Werkudara**
```
zone "baratayuda.abimanyu.d09.com" {
        type master;
        file "/etc/bind/baratayuda/baratayuda.abimanyu.d09.com";
};' >> /etc/bind/named.conf.local

mkdir /etc/bind/baratayuda

cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.d09.com

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.d09.com. root.baratayuda.abimanyu.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.d09.com.
@       IN      A       10.26.3.3     ; IP Abimanyu
www     IN      CNAME   baratayuda.abimanyu.d09.com.' > /etc/bind/baratayuda/baratayuda.abimanyu.d09.com

echo "options {
    directory \"/var/cache/bind\";

    // If there is a firewall between you and nameservers you want
    // to talk to, you may need to fix the firewall to allow multiple
    // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

    // If your ISP provided one or more IP addresses for stable
    // nameservers, you probably want to use them as forwarders.
    // Uncomment the following block, and insert the addresses replacing
    // the all-0's placeholder.

    // forwarders {
    //      0.0.0.0;
    // };

    //========================================================================
    // If BIND logs error messages about the root key being expired,
    // you will need to update your keys.  See https://www.isc.org/bind-keys
    //========================================================================
    //dnssec-validation auto;

    allow-query { any; };
    auth-nxdomain no;
    listen-on-v6 { any; };
};" > /etc/bind/named.conf.options

service bind9 restart
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%207.png)

## Soal 8
> Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.

```
rjp             IN      A       10.26.3.3     ; IP Abimanyu
www.rjp         IN      CNAME   rjp.baratayuda.abimanyu.d9.com.
```

### Script
**Werkudara**
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.d09.com. root.baratayuda.abimanyu.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      baratayuda.abimanyu.d09.com.
@               IN      A       10.26.3.3     ; IP Abimanyu
www             IN      CNAME   baratayuda.abimanyu.a09.com.
rjp             IN      A       10.26.3.3     ; IP Abimanyu
www.rjp         IN      CNAME   rjp.baratayuda.abimanyu.d09.com.' > /etc/bind/baratayuda/baratayuda.abimanyu.d09.com

service bind9 restart
```

## Soal 9
> Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker

Sebelum mengerjakan perlu untuk melakukan setup terlebih dahulu. 

- **Nginx Config**
  ```
  apt install nginx php php-fpm -y
  ```
- **Apache2 Config**
  ```
  apt-get update
  apt-get install dnsutils -y
  apt-get install lynx -y
  apt-get install nginx -y
  service nginx start
  apt-get install apache2 -y
  apt-get install libapache2-mod-php7.0 -y
  service apache2 start
  apt-get install wget -y
  apt-get install unzip -y
  apt-get install php -y
  echo -e "\n\nPHP Version:"
  php -v
  ```

### Script
**Arjuna (Load Balancing)**

```
upstream backend {
  server 10.26.3.2; # IP Prabukusuma
  server 10.26.3.3; # IP Abimanyu
  server 10.26.3.4; # IP Wisanggeni
}

server {
  listen 80;
  server_name arjuna.d09.com www.arjuna.d09.com;

  location / {
    proxy_pass http://backend;
  }
}
' > /etc/nginx/sites-available/jarkom
```

lakukan `symlink` dengan menjalankan perintah berikut

```
ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled/jarkom
```

agar port tidak bertabrakan dengan `default` yang ada saat kita melakukan installasi pada `nginx`, maka kita harus menghapus file `default` tersebut

```
rm /etc/nginx/sites-enabled/default
```

lalu restart 
```
service nginx restart
```

**PrabuKusuma, Abimanyu,, Wisanggeni**

Jalankan perintah `shell` berikut pada masing-masing `worker`
```
service php7.0-fpm start

echo 'server {
        listen 80;

        root /var/www/jarkom;
        index index.php index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled/jarkom

rm /etc/nginx/sites-enabled/default

service nginx restart
```

**Client (Sadewa / Nakula)**
lakukan test berikut
```
lynx http://10.26.3.2
lynx http://10.26.3.3
lynx http://10.26.3.4
lynx http://10.26.3.5
lynx http://arjuna.d09.com
```

### Result
![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%209.1.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%209.2.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%209.3.JPG)

## Soal 10
> Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh (Prabakusuma:8001, Abimanyu:8002, Wisanggeni:8003)

Karena telah berhasil melakukan deployment pada nomor. Maka kita hanya perlu mengubah masing-masing port pada worker menuju port yang telah ditentukan yaitu `Prabakusuma:8001, Abimanyu:8002, Wisanggeni:8003`. Kita juga perlu mengubah port `load-balancing` dengan menambahkan `:800X` pada masing-masing server

### Script

**Arjuna (Load Balancing)**
```
upstream backend {
  server 10.26.3.2:8001; # IP PrabuKusuma
  server 10.26.3.3:8002; # IP Abimanyu
  server 10.26.3.4:8003; # IP Wisanggeni
}
```
**PrabuKusuma, Abimanyu, Wisanggeni**
```
server {
        listen 800X;

        root /var/www/jarkom;
        index index.php index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}' > /etc/nginx/sites-available/jarkom
```
### Result
**Load Balancing**

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2010.1.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2010.2.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2010.3.JPG)

## Soal 11
> Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy

### Script
**Yudhistira**
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d09.com. root.abimanyu.d09.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.d09.com.
@       IN      A       10.26.3.3     ; IP Abimanyu
www     IN      CNAME   abimanyu.a09.com.
parikesit IN    A       10.26.3.3     ; IP Abimanyu
ns1     IN      A       10.26.2.2     ; IP Werkudara
baratayuda IN   NS      ns1' > /etc/bind/jarkom/abimanyu.d09.com

service bind9 restart
```

**Abimanyu**
```
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/abimanyu.d09.com.conf

rm /etc/apache2/sites-available/000-default.conf

echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.d09

  ServerName abimanyu.d09.com
  ServerAlias www.abimanyu.d09.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.d09.com.conf

a2ensite abimanyu.d09.com.conf

service apache2 restart
```

**Client (Nakula)**
```
lynx abimanyu.d09.com
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2011.JPG)

## Soal 12
> Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.

```
<Directory /var/www/abimanyu.d09/index.php/home>
  Options +Indexes
</Directory>

Alias "/home" "/var/www/abimanyu.d09/index.php/home"
```

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.d09
  ServerName abimanyu.d09.com
  ServerAlias www.abimanyu.d09.com

  <Directory /var/www/abimanyu.d09/index.php/home>
          Options +Indexes
  </Directory>

  Alias "/home" "/var/www/abimanyu.d09/index.php/home"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.d09.com.conf

service apache2 restart
```

**Client (Nakula)**
```
lynx abimanyu.d09.com/home
curl abimanyu.d09.com/home
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2012.JPG)

## Soal 13
> Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.d09
  ServerName parikesit.abimanyu.d09.com
  ServerAlias www.parikesit.abimanyu.d09.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.d09.com.conf

a2ensite parikesit.abimanyu.d09.com.conf

service apache2 restart
```

**Client (Nakula)**
```
lynx parikesit.abimanyu.d09.com
curl parikesit.abimanyu.d09.com
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2013.JPG)

## Soal 14
> Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden)
### Script
**Abimanyu**
```
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.d09
  ServerName parikesit.abimanyu.d09.com
  ServerAlias www.parikesit.abimanyu.d09.com

  <Directory /var/www/parikesit.abimanyu.d09/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.d09/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.d09/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.d09/secret"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.d09.com.conf

service apache2 restart
```

**Client (Nakula)**
```
lynx parikesit.abimanyu.d09.com/public
lynx parikesit.abimanyu.d09.com/secret
```

### Result

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2014.2.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2014.JPG)

## Soal 15
> Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.d09
  ServerName parikesit.abimanyu.d09.com
  ServerAlias www.parikesit.abimanyu.d09.com

  <Directory /var/www/parikesit.abimanyu.d09/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.d09/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.d09/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.d09/secret"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.d09.com.conf

service apache2 restart
```

**Client (Nakula)**
```
lynx parikesit.abimanyu.d09.com/testerror
lynx parikesit.abimanyu.d09.com/secret
```

### Result
![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2015.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2015.2.JPG)

## Soal 16
> Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.yyy.com/public/js menjadi www.parikesit.abimanyu.yyy.com/js 

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.d09
  ServerName parikesit.abimanyu.d09.com
  ServerAlias www.parikesit.abimanyu.d09.com

  <Directory /var/www/parikesit.abimanyu.d09/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.d09/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.d09/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.d09/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.d09/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.d09.com.conf
```

**Client (Nakula)**
```
lynx parikesit.abimanyu.d09.com/js
```

## Soal 17
> Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.yyy.com hanya dapat diakses melalui port 14000 dan 14400.

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.d09
  ServerName rjp.baratayuda.abimanyu.d09.com
  ServerAlias www.rjp.baratayuda.abimanyu.d09.com

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.d09.com.conf

echo -e '# If you just change the port or add more ports here, you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default.conf

Listen 80
Listen 14000
Listen 14400

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet' > /etc/apache2/ports.conf

a2ensite rjp.baratayuda.abimanyu.d09.com.conf

service apache2 restart
```

**Client (Sadewa)**
```
lynx rjp.baratayuda.abimanyu.d09.com:14000
lynx rjp.baratayuda.abimanyu.d09.com:14400
```

### Result
**Port 14000 atau 14400**
![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2018.JPG)

**Port yang tidak sesuai**
![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2017.3.JPG)

## Soal 18
> Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.d09
  ServerName rjp.baratayuda.abimanyu.d09.com
  ServerAlias www.rjp.baratayuda.abimanyu.d09.com

  <Directory /var/www/rjp.baratayuda.abimanyu.d09>
          AuthType Basic
          AuthName "Restricted Content"
          AuthUserFile /etc/apache2/.htpasswd
          Require valid-user
  </Directory>

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.d09.com.conf

a2ensite rjp.baratayuda.abimanyu.d09.com.conf

service apache2 restart
```

Tambahkan autentikasi dengan menggunakan command `htpasswd`. Lalu untuk `-c` itu adalah `created` dan `-b` yang merupakan `bcrypt` agar password yang kita isi akan dilakukan hash terlebih dahulu sebelum disimpan.
```
htpasswd -c -b /etc/apache2/.htpasswd Wayang baratayudad09
```

**Client (Sadewa)**
```
lynx rjp.baratayuda.abimanyu.d09.com:14000
lynx rjp.baratayuda.abimanyu.d09.com:14400
```

### Result
![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2018.JPG)

![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomo%2018.2.JPG)


## Soal 19
> Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)

### Script
**Abimanyu**
```
echo -e '<VirtualHost *:80>
    ServerAdmin webmaster@abimanyu.d09.com
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    Redirect / http://www.abimanyu.d09.com/
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf
```

Config test
```
apache2ctl configtest
service apache2 restart
```

**Client (Nakula)**
```
lynx 10.26.3.3
```

### Result
![image](https://github.com/laurivasyyy/Jarkom-Modul-2-D09-2023/blob/fe64f19fb4dd47cbea0cf8ea069d7d2c25c40cf7/assets/nomor%2012.JPG)


## Soal 20
> Karena website www.parikesit.abimanyu.yyy.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.

### Script
**Abimanyu**

```
a2enmod rewrite
```

```
'RewriteEngine On
RewriteCond %{REQUEST_URI} ^/public/images/(.*)(abimanyu)(.*\.(png|jpg))
RewriteCond %{REQUEST_URI} !/public/images/abimanyu.png
RewriteRule abimanyu http://parikesit.abimanyu.d09.com/public/images/abimanyu.png$1 [L,R=301]' > /var/www/parikesit.abimanyu.d09/.htaccess
```

``````
'<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.d09

  ServerName parikesit.abimanyu.d09.com
  ServerAlias www.parikesit.abimanyu.d09.com

  <Directory /var/www/parikesit.abimanyu.d09/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.d09/secret>
          Options -Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.d09>
          Options +FollowSymLinks -Multiviews
          AllowOverride All
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.d09/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.d09/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.d09/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.d09.com.conf

service apache2 restart
```

**Client (Nakula)**
```
lynx parikesit.abimanyu.d09.com/public/images/not-abimanyu.png
lynx parikesit.abimanyu.d09.com/public/images/abimanyu-student.jpg
lynx parikesit.abimanyu.d09.com/public/images/abimanyu.png
lynx parikesit.abimanyu.d09.com/public/images/notabimanyujustmuseum.177013
```

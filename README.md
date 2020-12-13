# Jarkom_Modul4_Lapres_C03

- Brananda Denta WP - 05111840000143
- R. Dafa Berlian Denmar - 05111840000149

## Outline

+ [VLSM](#VLSM)
+ [CIDR](#CIDR)

## VLSM

### Langkah Pengerjaan

- Membuat pengelompokkan subnet dengan metode VLSM

![VLSMSub](/img/VLSMSub.png)

- Membuat Tree dari hasil subnetting

![VLSMTree](/img/VLSMTree.png)

- Berikut adalah tabel total ip yang sudah kami hitung

![totalip](/img/totalip.jpg)

- Berikut adalah daftar pembagian NID

![NID](/img/NID.jpg)

- Berikut adalah tabel routing dari setiap router

![routingvlsm](/img/routingvlsm.jpg)

## CIDR
### Langkah Pengerjaan

- Membuat pengelompokkan subnet dengan metode CIDR. Berikut adalah hasil akhirnya:

![CIDRSub](/img/CIDRSub.jpg)

- Membuat Tree dari hasil subnetting

![CIDRTree](/img/CIDRTree.png)

- Berikut adalah daftar detail informasi setiap subnet terkecil (A)

![](/img/tabelCIDR.png)


- Membuat file `topologi.sh` lalu jalankan `bash topologi.sh`
  
```sh
# Switch

uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch7 > /dev/null < /dev/null &
uml_switch -unix switch11 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &
uml_switch -unix switch16 > /dev/null < /dev/null &
uml_switch -unix switch17 > /dev/null < /dev/null &
uml_switch -unix switch18 > /dev/null < /dev/null &
uml_switch -unix switch19 > /dev/null < /dev/null &
uml_switch -unix switch21 > /dev/null < /dev/null &
uml_switch -unix switch20 > /dev/null < /dev/null &
uml_switch -unix switch22 > /dev/null < /dev/null &
uml_switch -unix switch25 > /dev/null < /dev/null &


# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.17 eth1=daemon,,,switch1 eth2=daemon,,,switch2 eth3=daemon,,,switch7 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch19 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3 eth1=daemon,,,switch15 eth2=daemon,,,switch16 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch7 eth1=daemon,,,switch11 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch11 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &


# Server

xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Klien 1
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &

```

- Pada setiap ***router***, ubah file `/etc/sysctl.conf` dengan menghilangkan comment pada `net.ipv4.ip_forward=1`
- Pada setiap router, jalankan perintah `sysctl -p`
- Pada setiap UML, tambahkan konfigurasi seperti berikut ini pada file `/etc/network/interfaces`.

### Surabaya

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.76.18
netmask 255.255.255.252
gateway 10.151.76.17

#ke sampang
auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

#ke A12 (pasuruan)
auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

#ke batu (a10)
auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

#ke mojokerto
auto eth4
iface eth4 inet static
address 10.151.77.38
netmask 255.255.255.252
```

### Pasuruan

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

#ke A11 (probo)
auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

#ke A6 (SIDOARJO)
auto eth2
iface eth2 inet static
address 192.168.160.0
netmask 255.255.252.0
```

### Probolinggo

```sh
auto lo
iface lo inet loopback

# ke pasuruan
auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252
gateway 192.168.144.1

# ke a4
auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.255.128

# ke a3
auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0
```

### Sidoarjo

```sh
auto lo
iface lo inet loopback

#a6
auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateway 192.168.160.1
```

### Bondowoso

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.128
gateway 192.168.136.1
```

### Jember

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.132.2
netmask 255.255.248.0
gateway 192.168.128.1
```

### Banyuwangi

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1
```

### Malang

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.34
netmask 255.255.255.252
gateway 10.151.77.33
```

### Mojokerto

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.38
netmask 255.255.255.252
gateway 10.151.77.37
```

### Sampang

```sh
auto lo
iface lo inet loopback

#ke sby (a13)
auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1
```

### Madiun

```sh
auto lo
iface lo inet loopback

#ke batu
auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

#ke A5 (bojo)
auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240
```

### Batu

```sh
auto lo
iface lo inet loopback

#ke sby
auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

# a7 ke kediri
auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

# a8 ke nganjuk
auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

# ke a9
auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0
```

### Nganjuk

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1
```

### Kediri

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.255.252
gateway 192.168.8.1

auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.151.77.33
netmask 255.255.255.252
```

### Blitar

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateway 192.168.4.1

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.252.0
```

### Lumajang

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.3
netmask 255.255.255.0
gateway 192.168.4.1
```

### Tulungagung

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateway 192.168.0.1
```

### Bojonegoro

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1
```

### Jombang

```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1
```

- Jalankan `service networking restart` pada semua UML
- Tambahkan routing pada UML Surabaya, Pasuruan, Batu, dan Kediri dengan membuat file `route.sh` pada setiap UML diatas. Berikut adalah isi dari file `route.sh`

### Surabaya

```sh
#kanan
route add -net 192.168.144.0 netmask 255.255.255.252 gw 192.168.192.2 #a11
route add -net 192.168.160.0 netmask 255.255.252.0 gw 192.168.192.2 #a6
route add -net 192.168.136.0 netmask 255.255.255.128 gw 192.168.192.2 #a4
route add -net 192.168.128.0 netmask 255.255.248.0 gw 192.168.192.2 #a3

#A9
route add -net 192.168.16.0 netmask 255.255.254.0 gw 192.168.32.2
#A5
route add -net 192.168.18.0 netmask 255.255.255.240 gw 192.168.32.2
#A8
route add -net 192.168.20.0 netmask 255.255.252.0 gw 192.168.32.2
#A7
route add -net 192.168.8.0 netmask 255.255.255.252 gw 192.168.32.2
#A2
route add -net 192.168.4.0 netmask 255.255.255.0 gw 192.168.32.2
#A1
route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.32.2
#MALANG
route add -net 10.151.77.32 netmask 255.255.255.252 gw 192.168.32.2
```

### Pasuruan

```sh
route add -net 192.168.128.0 netmask 255.255.248.0 gw 192.168.144.2 #a3
route add -net 192.168.136.0 netmask 255.255.255.128 gw 192.168.144.2 #a4
```

### Batu

```sh
#kiri
route add -net 192.168.18.0 netmask 255.255.255.240 gw 192.168.16.2

#bawah
route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.8.2 #a1
route add -net 192.168.4.0 netmask 255.255.255.0 gw 192.168.8.2 #a2
route add -net 10.151.77.32 netmask 255.255.255.252 gw 192.168.8.2 #malang
```

### Kediri

```sh
route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.4.2
```

- Jalankan `bash route.sh` pada semua UML diatas
- Jalankan `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.168.0.0/16` pada router Surabaya agar dapat terhubung dengan internet
- Lakukan tes dengan melakukan ping dari berbagai UML

#### ping its.ac.id dari TULUNGAGUNG

![1](/img/1.jpg)

#### ping its.ac.id dari BANYUWANGI

![2](/img/2.jpg)

#### ping its.ac.id dari SIDOARJO

![3](/img/3.jpg)

#### ping its.ac.id dari PROBOLINGGO

![4](/img/4.jpg)

#### ping its.ac.id dari LUMAJANG

![5](/img/6.jpg)

#### ping its.ac.id dari BOJONEGORO

![6](/img/5.jpg)

#### ping dari MALANG ke MOJOKERTO

![7](/img/7.jpg)

#### ping dari MALANG ke BANYUWANGI

![8](/img/8.jpg)

#### ping dari MOJOKERTO ke BOJONEGORO

![9](/img/9.jpg)

#### ping dari PROBOLINGGO ke MOJOKERTO

![10](/img/10.jpg)

#### ping dari KEDIRI ke PROBOLINGGO

![11](/img/11.jpg)

#### ping dari PROBOLINGGO ke JOMBANG

![12](/img/12.jpg)

#### ping dari LUMAJANG ke JOMBANG

![13](/img/13.jpg)

#### ping dari TULUNGAGUNG ke JEMBER

![14](/img/14.jpg)

#### ping dari NGANJUK ke BONDOWOSO

![15](/img/15.jpg)

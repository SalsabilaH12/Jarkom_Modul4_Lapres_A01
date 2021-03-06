#  Lapres Modul 4 Jarkom 2020

**Oleh Kelompok A01 :**
- Wisnu (05111740000170)
- Salsabila Harlen (05111840000127)

## VLSM
- Menentukan Subnet
![Alt Text](/img/Subnet.png)

- Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan melakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.
![Alt Text](/img/vlsm.png)

- Menghitung pembagian IP berdasarkan NID dan netmask tersebut menggunakan tree
- Melakukan subnetting dengan menggunakan pohon tersebut untuk pembagian IP sesuai dengan kebutuhan masing-masing subnet yang ada.
![Alt Text](/img/treevlsm.png)

- Dari pohon dari pohon tersebut akan mendapat pembagian IP sebagai berikut.
![Alt Text](/img/hasilsubnetting.png)

## CIDR
- Menentukan Subnet
![Alt Text](/img/Subnet.png)

- Melakukan penggabungan subnet sampai menjadi sebuah subnet besar yang mencakup 1 topologi.
![Alt Text](/img/Fixtopologi.png)

- Menghitung pembagian IP dengan pohon berdasarkan penggabungan subnet yang telah dilakukan.
![Alt Text](/img/CIDR.png)

- Berdasarkan penghitungan, maka didapatkan pembagian IP sebagai berikut.
![Alt Text](/img/hasilcidr.png)

- Lalu membuat nano topologi.sh
 
**Topologi UML**

```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &
uml_switch -unix switch16 > /dev/null < /dev/null &
uml_switch -unix switch17 > /dev/null < /dev/null &
uml_switch -unix switch18 > /dev/null < /dev/null &
uml_switch -unix switch19 > /dev/null < /dev/null &
uml_switch -unix switch20 > /dev/null < /dev/null &
uml_switch -unix switch21 > /dev/null < /dev/null &
uml_switch -unix switch22 > /dev/null < /dev/null &
uml_switch -unix switch25 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.72.9 eth1=daemon,,,switch1 eth2=daemon,,,switch2 eth3=daemon,,,switch4 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch19 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3 eth1=daemon,,,switch15 eth2=daemon,,,switch16 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch4 eth1=daemon,,,switch5 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch5 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Klien
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &

```

- Melakukan setting file dengan /etc/network/interfaces untuk setiap UML

**Interface UML**

Surabaya (Router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.72.8.10
netmask 255.255.255.252
gateway 10.151.72.9

auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 10.151.73.17
netmask 255.255.255.252

```

Pasuruan (Router) 
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.160.1
netmask 255.255.252.0

```

Probolinggo (Router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252
gateway 192.168.144.1

auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.255.128

auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0

```

Batu (Router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0

```

Kediri (Router)
```
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
address 10.151.73.21
netmask 255.255.255.252

```

Madiun (Router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240

```

Blitar (Router)
```
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

Mojokerto (Server)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.73.18
netmask 255.255.255.252
gateway 10.151.73.17

```

Malang (Server)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.73.22
netmask 255.255.255.252
gateway 10.151.73.21
```

Sampang (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1

```

Sidoarjo (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateway 192.168.160.1

```

Jember (klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1
```

Banyuwangi (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.3
netmask 255.255.248.0
gateway 192.168.128.1
```

Bondowoso (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.128
gateway 192.168.136.1
```

Jombang (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.3
netmask 255.255.254.0
gateway 192.168.16.1
```

Bonjonegoro (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1
```

Nganjuk (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1
```

Lumajang (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.3
netmask 255.255.255.0
gateway 192.168.4.1
```

Tulungagung (Klien)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateway 192.168.0.1
```

- Melakukan Routing

**Routing**
```
Surabaya : D1, D2, Malang
Pasuruan : B2, Default
Probolinggo : Default
Batu : A12, B1, Malang, Default
Madiun : Default
Kediri : A11, Mojokerto, Default
Blitar : Default
```

- Membuat file nano route.sh

**Routing di Surabaya**
```
route add -net 192.168.128.0 netmask 255.255.192.0 gw 192.168.192.2
route add -net 192.168.0.0 netmask 255.255.224.0 gw 192.168.32.2
route add -net 10.151.73.20 netmask 255.255.255.252 gw 192.168.32.2
```

**Routing di Pasuruan**
```
route add -net 192.168.128.0 netmask 255.255.240.0 gw 192.168.144.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.192.1
```
**Routing di Probolinggo**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.144.1
```

**Routing di Batu**
```
route add -net 192.168.18.0 netmask 255.255.255.240 gw 192.168.16.2
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.8.2
route add -net 10.151.73.20 netmask 255.255.255.252 gw 192.168.8.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw  192.168.32.1
```

**Routing di Madiun**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw  192.168.16.1
```

**Routing di Kediri**
```
route add -net 192.168.0.0 netmask 255.255.252.0 gw  192.168.4.2
route add -net 10.151.73.16 netmask 255.255.255.252 gw 192.168.8.1
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.8.1
```


**Routing di Blitar**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.4.1
```

- Untuk menjalankannya, menggunakan perintah source route.sh


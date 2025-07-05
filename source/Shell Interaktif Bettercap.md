# Bab 6 - Shell Interaktif Bettercap

## A. Menjalankan Shell Interaktif

```
sudo bettercap -iface <nama_interface>
```

Setelah itu akan masuk ke shell interaktif:

```
bettercap v2.33.0 (built for linux amd64 with go1.22.6) [type 'help' for a list of commands]

192.168.1.0/24 > 192.168.1.11  » [17:08:48] [sys.log] [inf] gateway monitor started ...
192.168.1.0/24 > 192.168.1.11  »
```

Keterangan output:
- Menjalankan `Bettercap` versi : `v2.33.0` (built for `linux amd64` with `go1.22.6`)
- `192.168.1.0/24` : Terhubung ke jaringan
- `192.168.1.1` : IP attacker (kamu)

## B. Perintah Dasar di Shell Bettercap

| Perintah | Fungsi |
|:--:|:--:|
| `help` | Menampilkan bantuan umum dan semua perintah |
| `help [modul]` | Bantuan spesifik untuk satu modul (misalnya: `help arp.spoof`) |
| `active` | Menampilkan **modul-modul** yang sedang **aktif** |
| `get *` | Menampilkan semua **variabel** yang bisa kamu **ubah** (`set`) |
| `set [nama] [nilai]` | Mengatur **nilai** dari sebuah **variabel** (contoh: `set arp.spoof.targets`) |
| `! [perintah_shell]` | Menjalankan perintah `shell Linux` dari dalam `Bettercap` |
| `include [file.cap]` | Menjalankan file **caplet** |
| `quit` | Keluar dari `Bettercap` |

## C. Modul- Modul Tersedia

Berikut adalah modul-modul Bettercap yang ditampilkan di output kamu, dan fungsinya:

| Modul	| Fungsi |
|:--:|:--:|
| `any.proxy` | Proxy untuk protokol selain **HTTP/HTTPS**. Bisa digunakan untuk protokol **non-standar**. |
| `api.rest` | Mengaktifkan **REST API** `Bettercap`. Berguna untuk **remote control** `Bettercap` dari aplikasi lain. |
| `arp.spoof` | Melakukan [ARP Poisoning](https://www.rackh.com/arp-spoofing-adalah/) untuk [Man-in-the-Middle](https://cyberhub.id/pengetahuan-dasar/apa-itu-mitm) (MITM). Modul paling umum dipakai. |
| `ble.recon` | Melakukan scanning perangkat [Bluetooth Low Energy](https://rexus.id/blogs/berita/apa-itu-bluetooth-ble-apa-bedanya-dengan-bluetooth-biasa?srsltid=AfmBOorZI3IRH0HYE8l4SdpEJ0Ub3YLPjfmX0eruKEUQXUm9KOQx-3D-) (BLE) di sekitar. |
| `c2` | Modul **Command** dan **Control** untuk mengelola **agent** pada **serangan yang terdistribusi** (seperti [Red Team op](https://www.ibm.com/id-id/think/topics/red-teaming)). |
| `caplets` | **Mengelola** dan **menjalankan caplet script** (.cap), yaitu **automation script** `Bettercap`. |
| `dhcp6.spoof` | [DHCPv6 spoofing](https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/dhcpv6-spoofing): mengirimkan jawaban [DHCP](https://www.rumahweb.com/journal/dhcp-adalah/) palsu pada jaringan [IPv6](https://id.wikipedia.org/wiki/IPv6). |
| `dns.spoof` | Memalsukan respon [DNS](https://www.ibm.com/id-id/think/topics/dns). Dapat digunakan untuk redirect **domain** ke **IP attacker** ([phishing](https://id.wikipedia.org/wiki/Pengelabuan)). |
| `events.stream` | Mencatat semua **event** secara **real-time**. Modul ini aktif secara default. |
| `gps` | Mengambil data **lokasi** jika sistem punya akses **GPS** (misalnya [Raspberry Pi](https://www.raspberrypi.com/) + [GPS dongle](https://en.wikipedia.org/wiki/Global_Positioning_System)). |
| `graph` | Menyimpan hasil [recon](https://www.cyberacademy.id/blog/mengenal-fase-peretasan-reconnaissance-) atau [sniffing](https://cyberhub.id/pengetahuan-dasar/apa-itu-sniffing) ke file `.dot` untuk dianalisis dalam bentuk **graph jaringan**. |
| `hid` | Melakukan serangan emulasi [HID](https://en.wikipedia.org/wiki/Human_interface_device) (Human Interface Device), seperti **emulasi keyboard** ([Rubber Ducky style](https://shop.hak5.org/products/usb-rubber-ducky)). |
| `http.proxy` | Menjadi **proxy HTTP**. Bisa **sniff**, **log**, atau **memanipulasi lalu lintas HTTP**. |
| `http.server` | Menyediakan **server HTTP** sederhana (misal untuk **hosting payload** atau **halaman phishing**). |
| `https.proxy` | Menjadi **MITM** untuk [HTTPS](https://id.wikipedia.org/wiki/HTTPS). Sertifikat palsu akan digunakan untuk intercept [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security)/[SSL](https://en.wikipedia.org/wiki/SSL). |
| `https.server` | Menyediakan **server HTTPS lokal** (dengan **sertifikat palsu**), untuk kombinasi serangan tertentu. |
| `mac.changer` | Mengganti **MAC address interface** untuk **penyamaran** atau **bypass filtering**. |
| `mdns.server` | **Multicast DNS server palsu**. Dapat digunakan untuk **trik-trik penipuan** pada **jaringan lokal**. |
| `mysql.server` | Jalankan **server [MySQL](https://www.mysql.com/) palsu**. Bisa digunakan untuk [honeypot](https://id.wikipedia.org/wiki/Madukala) atau **mengelabui client**. |
| `ndp.spoof` | Seperti `arp.spoof`, tetapi khusus untuk jaringan **IPv6** (Neighbor Discovery Protocol spoofing). |
| `net.probe` | Melakukan [probing](https://kupastuntasprobing.wordpress.com/2015/06/23/kupas-tuntas-probing/) ke semua **host** di **jaringan** (melalui [ARP](https://www.dewaweb.com/blog/pengertian-arp/)) untuk mendeteksi **device aktif**. |
| `net.recon` | **Passive/active scan** untuk mengidentifikasi **layanan** yang berjalan di **host** (port scan ringan). |
| `net.sniff` | **Sniff** (menyadap) paket dari **jaringan**. Bisa menangkap **password**, **cookie**, dan **data sensitif**. |
| `packet.proxy` | Modul proxy untuk paket mentah (raw packet manipulation). Eksperimental dan advance. |
| `syn.scan` | Modul untuk [port scanning](https://id.wikipedia.org/wiki/Pemindaian_port) cepat berbasis [TCP SYN](https://id.wikipedia.org/wiki/SYN_flood) (mirip `nmap -sS`). |
| `tcp.proxy`	| [MITM proxy](https://mitmproxy.org/) untuk protokol berbasis [TCP](https://id.wikipedia.org/wiki/Protokol_Kendali_Transmisi) ([FTP](https://id.wikipedia.org/wiki/Protokol_Transfer_Berkas), [IMAP](https://id.wikipedia.org/wiki/Internet_Message_Access_Protocol), **dll**). Bisa **sniff** dan **modifikasi**. |
| `ticker` | Menjalankan **perintah** secara **otomatis** setiap **beberapa detik**. Cocok untuk **monitoring berkala**. |
| `ui` | Mengaktifkan antarmuka pengguna berbasis **web** (jika tersedia, versi [GUI](https://id.wikipedia.org/wiki/Antarmuka_pengguna_grafis)). |
| `update` | Modul internal untuk melakukan **update** `bettercap` dan **semua caplets** dari [GitHub](https://github.com/bettercap/bettercap). |
| `wifi` | Modul utama [Wi-Fi](https://id.wikipedia.org/wiki/Wi-Fi): scanning [SSID](https://id.wikipedia.org/wiki/Service_set_identifier), [client](https://id.wikipedia.org/wiki/Kelayan_(komputer)), [deauth](https://en.wikipedia.org/wiki/Wi-Fi_deauthentication_attack), [beacon spam](https://capibarazero.com/docs/sbc_linux/wifi/beacon_spam/), dan [Evil Twin](https://www.asdf.id/evil-twin-attack-adalah/). |
| `wol` | Mengirim [Wake-on-LAN magic packet](https://wiki.wireshark.org/WakeOnLAN) ke **perangkat** untuk **menyalakannya secara remote**. |

## D. Contoh Aktivasi Modul

### 1. MITM + Sniff:

```
set arp.spoof.targets 192.168.1.10
arp.spoof on
net.sniff on
```

### 2. Sniff dan HTTP Proxy:

```
set net.sniff.verbose true
net.sniff on
http.proxy on
```

### 3. DNS Spoof:

```
set dns.spoof.domains <nama_domain>
set dns.spoof.address <ip_address_target>
dns.spoof on
```

## E. Tips Tambahan
- Gunakan `help [modul]` untuk lihat **parameter** yang bisa **diset**.
- Gunakan `get *` untuk melihat semua **variabel aktif**.
- **Modul bisa diaktifkan bersamaan**: `arp.spoof on, net.sniff on`, **dll**.

# Sejarah Bettercap

## 1. Awal Mula (2015)

[Bettercap](https://www.bettercap.org/) pertama kali dirilis oleh [Simone Margaritelli](https://github.com/evilsocket) (evilsocket) pada tahun **2015**. Tool ini dibuat sebagai pengganti modern untuk tool klasik [Ettercap](https://www.ettercap-project.org/), yang saat itu dianggap:
- Sudah **usang** dan **tidak aktif dikembangkan**
- Kurang modular
- Terlalu **lambat** dan **berat**
- Sulit dikustomisasi

> **Tujuan awal Bettercap**: Menyediakan **framework MITM (Man-in-the-Middle) modern**, **cepat**, **modular**, dan **fleksibel** untuk **jaringan lokal**.

## 2. Bettercap v1 (Ruby-based)

- Ditulis dalam bahasa [Ruby](https://id.wikipedia.org/wiki/Ruby_(bahasa_pemrograman)).
- Fokus pada [MITM](https://cyberhub.id/pengetahuan-dasar/apa-itu-mitm) di **jaringan lokal**, seperti:
  - [ARP spoofing](https://www.rackh.com/arp-spoofing-adalah/)
  - [DNS spoofing](https://www.asdf.id/dns-spoofing-cara-kerja-dan-pencegahannya/)
  - [HTTP injection](https://en.wikipedia.org/wiki/HTTP_header_injection)
  - [Sniffing password](https://cyberhub.id/pengetahuan-dasar/apa-itu-sniffing)

> **Kelemahan**: **Ruby** bukan bahasa yang **efisien** untuk **performa tinggi**, dan **dependensi** sering **bermasalah** di berbagai **OS**.

## 3. Revolusi Bettercap v2 (2018)

Pada awal tahun **2018**, **Simone** menulis ulang `Bettercap` versi **2** sepenuhnya dari **nol** dengan bahasa [Go](https://id.wikipedia.org/wiki/Go_(bahasa_pemrograman)) (Golang).

Versi ini menjadi lompatan besar karena:
- Lebih **cepat** dan **ringan** (native binary)
- **Portabel**: tidak tergantung pada **interpreter** seperti **Ruby/Python**
- **Modular**: **sistem modul** terpisah (**net.sniff**, **net.recon**, **arp.spoof**, **dll**.)
- **Scriptable**: dengan fitur **Caplets** (mirip [Bash script](https://www.codepolitan.com/blog/apa-itu-bash-script-pengertian-fungsi-dan-contoh-penggunaannya/))

> `Bettercap` versi **2** menjadi andalan utama untuk **pentester** dan **red teamer** karena sangat **powerful** dan **fleksibel**.

## 4. Penambahan Fitur Wireless (2019–2020)
- Dukungan untuk **serangan Wi-Fi**: [scanning SSID](https://digitalsolusigrup.co.id/ssid-adalah), [deauth attack](http://onnocenter.or.id/wiki/index.php/Kali_Linux:_WiFi_Deauth_Attack), [PMKID capture](https://www.nccgroup.com/us/research-blog/pmkid-attacks-debunking-the-80211r-myth/).
- Dukungan [Bluetooth Low Energy](https://alatuji.co.id/mengenal-teknologi-bluetooth-low-energy-ble-pada-data-logger/) (BLE): **scan**, **eksploitasi device BLE**.
- Modul **2.4GHz HID** (mousejacking) untuk **injeksi script** via [dongle wireless](https://rexus.id/blogs/tips/dongle).

## 5. Bettercap v2.x Terus Berkembang (2021–2025)
- Modul **CAN-bus** untuk **eksploitasi kendaraan modern**.
- **REST API** + **Web UI** untuk **kontrol jarak jauh**.
- Perbaikan terus-menerus dari komunitas dan pengguna aktif.
- Digunakan di banyak **lab pentest**, **pelatihan red team**, hingga **operasi cyber resmi**.

## 6. Status Saat Ini (2025)
`Bettercap` tetap menjadi salah satu tool **MITM** paling **powerful** yang tersedia saat ini.

Komunitas masih aktif dan proyek ini:
- **Open-source** di **GitHub**: [https://github.com/bettercap/bettercap](https://github.com/bettercap/bettercap)
- Didukung penuh oleh **penulis** dan **banyak kontributor**.

## Kesimpulan Sejarah

| Tahun	| Peristiwa Utama |
|:--:|:--:|
| 2015 | Rilis awal menggunakan bahasa **Ruby**, alternatif **Ettercap** |
| 2018 | `Bettercap` versi **2** menggunakan **Go**, **performa tinggi** dan **modular** |
| 2019+ | **Fitur Wi-Fi**, **BLE**, **HID**, **caplets**, **proxy** |
| 2022+ | Dukungan **CAN-bus**, **REST API**, **web UI** |
| 2025 | Versi stabil dan sangat digunakan oleh **pentester** dan **red team** |

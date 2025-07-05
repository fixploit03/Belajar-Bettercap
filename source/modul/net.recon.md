# Modul `net.recon` di Bettercap

## A. Pengertian Singkat

Modul `net.recon` digunakan untuk **mendeteksi host baru di jaringan lokal secara otomatis**. Cara kerjanya adalah dengan **membaca ARP cache secara berkala untuk mengetahui perangkat baru yang muncul di jaringan**.

Modul ini sangat berguna saat kamu ingin:
- Melakukan [enumerasi](https://ilmubersama.com/2021/04/14/enumeration/) **perangkat** yang terhubung ke **jaringan**.
- Mengetahui siapa saja yang **aktif** di **jaringan lokal**.
- Menyiapkan **target** untuk serangan seperti [ARP Spoofing](https://www.rackh.com/arp-spoofing-adalah/) atau [MITM](https://www.ibm.com/id-id/think/topics/man-in-the-middle).

## B. Perintah Dasar

| Perintah | Fungsi |
|:--:|:--:|
| `net.recon on` | Mengaktifkan proses deteksi **host** di **jaringan**. |
| `net.recon off` | Menonaktifkan proses tersebut. |
| `net.clear` | Menghapus **seluruh data host** yang telah **dikumpulkan**. |
| `net.show` | Menampilkan **daftar host yang terdeteksi** (tersimpan di cache). |
| `net.show ADDRESS1,ADDRESS2` | Menampilkan **informasi detail** berdasarkan **IP/MAC** tertentu. |
| `net.show.meta ADDRESS1,ADDRESS2` | Menampilkan **metadata** tambahan dari **IP/MAC** tertentu. |


## C. Parameter Tambahan

| Parameter | Fungsi | Default |
|:--:|:--:|:--:|
| `net.show.filter` | Gunakan **regex** untuk **memfilter output** `net.show`. | (kosong) |
| `net.show.limit` | Jumlah **maksimum host** yang **ditampilkan**. `0 = tanpa batas`. | `0` |
| `net.show.meta` | Jika `true`, `net.show` akan otomatis tampilkan **metadata lengkap**. | `false` |
| `net.show.sort` | Atur **urutan data** berdasarkan **ip, mac, seen, sent, rcvd** (dengan arah `asc/desc`). | `ip asc` |

## D. Contoh Penggunaan

### 1. Menyalakan Monitoring Host

```
net.recon on
```

### 2. Mematikan Monitoring

```
net.recon off
```

### 3. Melihat Semua Host Terdeteksi

```
net.show
```

### 4. Melihat Metadata dari IP Tertentu

```
net.show.meta 192.168.1.20
```

### 5. Menghapus Data Host yang Sudah Terdeteksi

```
net.clear
```

### 6. Filter Host berdasarkan IP Range

```
set net.show.filter 192.168.1.*
net.show
```

### 7. Sortir Berdasarkan Paket Terkirim

```
set net.show.sort sent desc
net.show
```

# E. Kegunaan Modul `net.recon`

| Kegunaan | Penjelasan |
|:--:|:--:|
| **Enumerasi Host** | Menemukan **perangkat aktif** di **jaringan** tanpa **scanning agresif**. |
| [Passive Recon](http://onnocenter.or.id/wiki/index.php/Passive_dan_Active_Reconnaissance)	| Tidak terlalu **mencolok** di **jaringan** dibanding **port scan**.  |
| **Persiapan Serangan** | Menentukan **target** untuk [ARP spoof](https://www.rackh.com/arp-spoofing-adalah/), [sniffing](https://cyberhub.id/pengetahuan-dasar/apa-itu-sniffing), atau [exploitasi](https://id.wikipedia.org/wiki/Eksploitasi). |
| **Monitoring Aktivitas** | Melihat **host baru** yang **tiba-tiba muncul** (indikasi **serangan** atau **perangkat asing**). |


## F. Catatan Penting
- Modul ini bersifat [pasif](https://kbbi.web.id/pasif), tidak mengirim **paket** untuk **probing**, hanya membaca [ARP cache](https://en.wikipedia.org/wiki/ARP_cache).
- Tidak semua **perangkat** langsung muncul, hanya yang pernah **berkomunikasi** di **jaringan** (kecuali digabung dengan **scanning aktif**).
- Lebih efektif jika digabung dengan **modul lain** seperti `arp.spoof`, `net.sniff`, atau `syn.scan`.

## G. Kesimpulan

Modul `net.recon` sangat **ideal** untuk **pemantauan jaringan pasif** dan **deteksi host aktif dengan efisien**. Cocok digunakan saat **pengumpulan informasi awal** (initial recon) sebelum **eksploitasi** atau **penyadapan** dilakukan.

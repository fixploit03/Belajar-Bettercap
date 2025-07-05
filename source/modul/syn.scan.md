# Modul `syn.scan` di Bettercap

## A. Pengertian Singkat

Modul `syn.scan` adalah fitur [Bettercap](https://www.bettercap.org/) yang berfungsi untuk melakukan [SYN port scanning](https://nmap.org/book/synscan.html), yaitu metode **scanning cepat** untuk mendeteksi **port terbuka** (open ports) pada **target IP**. Teknik ini dikenal juga dengan nama **half-open scanning** karena tidak menyelesaikan [full TCP handshake](https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/).

## B. Perintah Dasar

| Perintah | Fungsi |
|:--:|:--:|
| `syn.scan IP-RANGE START-PORT END-POR`T | Melakukan **scanning** terhadap **IP** atau **rentang IP** dan **port**. |
| `syn.scan stop` | Menghentikan **proses scanning saat ini**. |
| `syn.scan.progress` | Menampilkan **progress** dari **scanning yang sedang berjalan**. |

Contoh:

```
syn.scan 192.168.1.1 20 100
```

Melakukan **SYN scan** ke `192.168.1.1` dari **port** `20` sampai `100`.

## C. Parameter Tambahan

| Parameter | Deskripsi | Default |
|:--:|:--:|:--:|
| `syn.scan.show-progress-every` | Menentukan **jeda waktu** (dalam detik) untuk **menampilkan progress scanning**. | `1 detik` |

Contoh mengatur **progress** setiap `3 detik`:

```
set syn.scan.show-progress-every 3
```

## D. Cara Kerja SYN Scan (Half-open Scan)
- `Bettercap` mengirim **SYN packet** ke **port target**.
- Jika **port terbuka**, target membalas dengan `SYN-ACK`.
- `Bettercap` tidak melanjutkan **koneksi** (tidak mengirim `ACK`), sehingga **handshake tidak lengkap**.
- Hal ini membuat **scanning** lebih **cepat** dan **sulit dideteksi** dibanding [full connect scan](https://nmap.org/book/scan-methods-connect-scan.html).

## E. Contoh Penggunaan

### 1. Scan Port Web

```
syn.scan 192.168.1.10 80 443
```

### 2. Scan Banyak IP

```
syn.scan 192.168.1.1-100 20 100
```

### 3. Tampilkan Progress Tiap 5 Detik

```
set syn.scan.show-progress-every 5
syn.scan 192.168.1.20 1 1000
```

## F. Kegunaan Praktis

| Tujuan | Penjelasan |
|:--:|:--:|
| **Enumerasi layanan** | Menemukan **port terbuka** pada **target** sebelum **eksploitasi**. |
| **Deteksi sistem aktif** | Mengetahui **host mana saja yang aktif** berdasarkan respon `SYN`. |
| **Uji IDS/Firewall** | Melihat apakah ada **deteksi terhadap SYN scan** (beberapa [IDS](https://id.wikipedia.org/wiki/Sistem_deteksi_intrusi) mendeteksi metode ini). |

## G. Catatan Penting
- Tidak semua **port terbuka** akan menjawab dengan `SYN-ACK`, bisa diblokir **firewall**.
- Beberapa **sistem** memiliki **rate-limit** atau **protection** terhadap **scanning**.
- Gunakan hanya di **jaringan yang legal untuk diuji** (misalnya **lab** atau **dengan izin**).

## H. Kesimpulan

Modul `syn.scan` sangat berguna untuk melakukan **port scanning cepat** dan **efisien** menggunakan metode `SYN scan`. Dengan kemampuan untuk memilih **IP range** dan **port range**, modul ini cocok untuk tahap awal dalam proses [pentesting](http://onnocenter.or.id/wiki/index.php/Simulasi_Penetration_Testing_Lengkap) atau **network auditing**.

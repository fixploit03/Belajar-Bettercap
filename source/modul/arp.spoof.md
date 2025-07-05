# Modul `any.spoof` di Bettercap

## A. Pengertian Singkat

Modul `arp.spoof` di [Bettercap](https://www.bettercap.org/) digunakan untuk melakukan [ARP Spoofing](https://www.rackh.com/arp-spoofing-adalah/), yaitu teknik manipulasi **ARP** (Address Resolution Protocol) di **jaringan lokal**. Dengan teknik ini, **attacker** dapat berpura-pura menjadi **gateway** atau **host lain**, sehingga lalu lintas korban dapat dialihkan dan dianalisis ([Man-in-the-Middle](https://www.ibm.com/id-id/think/topics/man-in-the-middle) / MITM).

## B. Perintah Dasar

| Perintah	| Fungsi |
|:--:|:--:|
| `arp.spoof on` | Mengaktifkan **ARP Spoofing**. |
| `arp.spoof off` | Menonaktifkan **ARP Spoofing**. |
| `arp.ban on` | Menjalankan **spoofing** dalam mode **ban** (memutus koneksi target). |
| `arp.ban off` |	Menonaktifkan mode **ban**. |

## C. Parameter Konfigurasi

| Parameter	| Deskripsi | Nilai Default |
|:--:|:--:|:--:|
| `arp.spoof.fullduplex` | Jika **diaktifkan**, maka **gateway** dan **target akan diserang**. Jika **tidak**, hanya **target yang diserang**. Wajib `true` jika **router** punya **proteksi [ARP](https://id.wikipedia.org/wiki/Protokol_Resolusi_Alamat)**. | `false` |
| `arp.spoof.internal` | Jika `true`, **spoofing** juga dilakukan pada koneksi antar **host lokal**. Jika `false`, hanya koneksi ke **luar jaringan** yang diserang. | `false` |
| `arp.spoof.skip_restore` | Jika `true`, **ARP cache** target tidak akan **dikembalikan ke semula** saat `arp.spoof` dimatikan. | `false` |
| `arp.spoof.targets` | Daftar **IP**, **MAC**, atau **rentang target yang ingin diserang** (pisahkan dengan **koma**).	| `<seluruh subnet>` |
| `arp.spoof.whitelist` | Daftar **IP** atau **MAC** yang **tidak akan diserang** (diabaikan). | (kosong) |

## D. Contoh Penggunaan

### 1. Target Satu IP

Spoof hanya **1 korban**:

```
set arp.spoof.targets 192.168.1.20
arp.spoof on
```

### 2. Full Duplex Spoofing

Agar bisa **intercept dua arah** (**target** <--> **router**):

```
set arp.spoof.fullduplex true
arp.spoof on
```

### 3. Mode Ban (Putus Koneksi)

Untuk memutus **koneksi internet korban**:

```
set arp.spoof.targets 192.168.1.20
arp.ban on
```

### 4. Spoof Semua Koneksi Lokal

Spoof koneksi antar **host** dalam **LAN**:

```
set arp.spoof.internal true
arp.spoof on
```

## E. Cara Kerja
- `Bettercap` mengirim **ARP reply palsu** ke **target**, mengatakan bahwa **attacker** adalah **gateway**.
- **Target** percaya dan mulai mengirim **lalu lintasnya** ke **attacker**.
- Jika **fullduplex aktif**, **gateway** juga diserang supaya **lalu lintas** balik juga lewat **attacker**.
- **Attacker** dapat **menganalisis**, **memodifikasi**, atau **meneruskan paket ke tujuan asli**.

## F. Kegunaan Praktis

| Kegunaan	| Penjelasan |
|:--:|:--:|
| **Sniffing data sensitif** | Menyadap **kredensial**, **cookie**, **dll**. |
| **MITM penuh dua arah** | Untuk **manipulasi traffic dua arah**. |
| **Denial of Service** | Menggunakan `arp.ban` untuk **memblokir koneksi korban**. |
| **Target selektif** | Bisa pilih **korban spesifik**, tidak menyerang **semua host**. |

## G. Catatan Keamanan dan Etika
- **ARP spoofing** termasuk teknik berbahaya bila digunakan di jaringan **publik** tanpa **izin**.
- Gunakan hanya untuk **pentest legal**, di **lab sendiri**, atau dengan **izin tertulis**.
- Banyak sistem modern (terutama **gateway** dan **switch managed**) sudah memiliki proteksi **ARP spoofing**.

## H. Kesimpulan

Modul `arp.spoof` di `Bettercap` sangat **powerful** untuk melakukan **Man-in-the-Middle** berbasis **ARP**. Kamu bisa menggunakannya untuk **sniffing**, **manipulasi trafik**, maupun **testing proteksi ARP di jaringan**.

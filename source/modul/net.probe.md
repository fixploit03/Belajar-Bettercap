# Modul `net.probe` di Bettercap

## A. Pengertian Singkat

Modul `net.probe` digunakan untuk **menemukan host aktif di jaringan dengan cara mengirim paket [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol) dummy ke setiap kemungkinan IP dalam [subnet](https://id.wikipedia.org/wiki/Subnetwork)**. Berbeda dengan `net.recon` yang **pasif**, `net.probe` adalah metode **aktif** dan **lebih agresif**.

## B. Perintah Dasar

| Perintah	| Fungsi |
|:--:|:--:|
| `net.probe on` | Mengaktifkan **probing aktif** untuk mendeteksi **host**. |
| `net.probe off` | Menonaktifkan proses **probing**. |


## C. Parameter Konfigurasi

| Parameter | Fungsi | Default |
|:--:|:--:|:--:|
| `net.probe.mdns` | Mengaktifkan **probe [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS)** (Multicast DNS). | `true` |
| `net.probe.nbns` | Mengaktifkan **probe [NetBIOS Name Service](https://id.wikipedia.org/wiki/NetBIOS)**. | `true` |
| `net.probe.upnp` | Mengaktifkan probe **[UPnP](https://learn.microsoft.com/id-id/windows/win32/upnp/overview-of-universal-plug-and-play)** (Universal Plug and Play).	| `true` |
| `net.probe.wsd` | Mengaktifkan **probe [WSD](https://en.wikipedia.org/wiki/WS-Discovery)** (Web Services Discovery). | `true` |
| `net.probe.throttle` | **Waktu jeda **(dalam milidetik) antara **pengiriman paket probe**. **Nilai lebih besar** = l**ebih lambat**. | `10` |


## D. Contoh Penggunaan

### 1. Mulai Probing Default

```
net.probe on
```

### 2. Hentikan Probing

```
net.probe off
```

### 3. Nonaktifkan NBNS dan UPNP

```
set net.probe.nbns false
set net.probe.upnp false
net.probe on
```

### 4. Percepat atau Perlambat Probe

```
set net.probe.throttle 50   # throttle 50ms antar paket
```

## E. Perbedaan dengan `net.recon`

| Fitur	| net.recon | net.probe |
|:--:|:--:|:--:|
| **Teknik** | Pasif (membaca [ARP cache](https://en.wikipedia.org/wiki/ARP_cache)) | Aktif (mengirim paket **UDP**) |
| **Kecepatan deteksi** | Lambat | Cepat |
| **Risiko terdeteksi** | Rendah | Sedang - Tinggi |
| **Efektivitas** | Hanya **host** yang **aktif komunikasi** | Bisa deteksi **lebih banyak host** |

## F. Kegunaan Modul `net.probe`

| Kegunaan | Penjelasan |
|:--:|:--:|
| **Deteksi perangkat baru** | Menemukan **host** yang **tidak aktif** secara **ARP**, tetapi merespons **UDP**. |
| **Enumerasi layanan jaringan** | Melalui protokol **mDNS**, **NBNS**, **UPnP**, dan **WSD**. |
| **Persiapan audit jaringan** | Sebagai langkah awal untuk mengetahui jumlah **host aktif**. |

## G. Catatan Penting
- Penggunaan `net.probe` bisa memicu deteksi oleh [IDS](https://id.wikipedia.org/wiki/Sistem_deteksi_intrusi)/[IPS](https://phintraco.com/intrusion-prevention-system/), karena tekniknya bersifat **aktif**.
- Proses **probing** akan menghasilkan **lalu lintas tambahan** di **jaringan**.
- Gunakan di jaringan **lab** atau dengan **izin tertulis**.

## H. Kesimpulan

Modul `net.probe` sangat cocok untuk melakukan **host discovery aktif** menggunakan berbagai teknik **broadcast** dan **UDP dummy packet**. Sangat efektif untuk **menemukan perangkat yang tidak aktif di ARP cache**, serta untuk **pemetaan awal jaringan**.

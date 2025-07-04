# Kegunaan dan Fungsi Bettercap dalam Penetration Testing

[Bettercap](https://www.bettercap.org/) adalah **framework serangan jaringan** yang sangat **powerful** dan **modular**, digunakan oleh para **penetration tester** untuk **mengeksploitasi kelemahan komunikasi jaringan** dan **mengumpulkan informasi sensitif**. `Bettercap` mendukung berbagai **skenario serangan** dalam **uji penetrasi**, terutama pada fase [reconnaissance](https://widyasecurity.com/2025/06/03/apa-itu-reconnaissance-dalam-tahapan-penetration-testing/), [exploitation](https://widyasecurity.com/2024/01/09/apa-itu-exploit-penjelasan-jenis-dan-pencegahannya/), dan [post-exploitation](https://www.proweb.co.id/articles/penetration-testing/post-exploitation.html).

## 1. Reconnaissance (Pengintaian)

`Bettercap` bisa digunakan untuk **memetakan jaringan** dan **mengidentifikasi target potensial**:
- `net.probe` : Menemukan **semua perangkat aktif** di **jaringan**.
- `net.recon` : Melakukan **fingerprinting perangkat** (**MAC vendor**, **OS**, **IP**).
- `net.show` : Menampilkan **perangkat** yang telah **ditemukan**.

> **Tujuan**: Mengumpulkan **intelijen** tentang **struktur jaringan** dan **siapa yang aktif**.

## 2. Man-in-the-Middle (MITM)

`Bettercap` sangat terkenal karena kemampuannya melakukan [MITM](https://cyberhub.id/pengetahuan-dasar/apa-itu-mitm) secara **efisien**, misalnya:
- `arp.spoof` : Menyerang **ARP** untuk memposisikan diri di tengah **komunikasi**.
- `dns.spoof` : Mengarahkan request **DNS** ke **domain palsu** (**phishing**, **malware**).
- `http.proxy`, `https.proxy` : **Mencegat** dan **memodifikasi** lalu lintas **HTTP/HTTPS**.

> **Tujuan**: Menyadap **kredensial**, **cookie**, **session token**, dan bahkan **menyisipkan payload berbahaya**.

## 3. Sniffing dan Data Capture

`Bettercap` bisa memantau lalu lintas **jaringan** secara **real-time**:
- `net.sniff` : Menangkap **paket data**, **form login**, **URL**, **kredensial**.
- `net.sniff.verbose true` : Tampilkan **payload** secara **langsung** di **layar**.

> **Tujuan**: Mengambil **username**, **password**, **token**, bahkan **API key yang tidak terenkripsi**.

## 4. Injection dan Manipulasi

`Bettercap` bisa memodifikasi **paket data** saat **transit**:
- `net.inject` : Menyisipkan **JavaScript**, **iframe**, **redirect** ke halaman [phishing](https://id.wikipedia.org/wiki/Pengelabuan).
- `http.proxy.script` : Jalankan **script kustom** untuk memodifikasi **response** dari **server**.

> **Tujuan**: Melakukan serangan [XSS aktif](https://id.wikipedia.org/wiki/Skripting_lintas_situs), **phishing**, atau **redirect pengguna**.

## 5. Wireless Attacks (Wi-Fi)

`Bettercap` mendukung berbagai **serangan nirkabel**, seperti:
- `wifi.recon` : Deteksi **SSID**, **perangkat terhubung**.
- `wifi.deauth` : Mengirim paket **deauthentication** (putuskan koneksi client).
- `wifi.ap` : Membuat **access point palsu** ([Evil Twin](https://www.asdf.id/evil-twin-attack-adalah/)).
- `wifi.assoc` : Memonitor **perangkat** yang mencoba **terhubung**.

> **Tujuan**: Melakukan **Evil Twin Attack**, **captive portal palsu**, dan [sniffing login di jaringan palsu](https://cyberhub.id/pengetahuan-dasar/apa-itu-sniffing).

## 6. Modular, Extensible, dan Otomatisasi

`Bettercap` mendukung **scripting** dan bisa **menjalankan skenario otomatis** melalui file `.cap script`.

Contoh:

```
bettercap -caplet my_attack.cap
```

## Kesimpulan: Kenapa Bettercap Sangat Berguna dalam Pentest?

| Fungsi | Penjelasan |
|:--:|:--:|
| **MITM** serangan **efisien** | Modul **ARP spoof**, **DNS spoof**, **Proxy HTTPS** |
| Observasi **real-time**	| Tangkap **login form**, **cookie**, **API key**, dan **kredensial lain** |
| Manipulasi **paket aktif** | Inject **script XSS**, **redirect**, **payload malware** |
| Serangan **Wi-Fi**	| [Deauth](https://en.wikipedia.org/wiki/Wi-Fi_deauthentication_attack), [beacon flood](https://tkj.smkdarmasiswasidoarjo.sch.id/2024/08/22/beacon-flood-ancaman-dan-perlindungan-dalam-jaringan-wi-fi/), **Evil Twin**, [captive portal](https://www.internetcepat.id/captive-portal-adalah/) |
| **Modular** dan **otomatis** | Bisa **discript**, cocok untuk **lab**, [CTF](https://www.dicoding.com/blog/capture-the-flag-cara-seru-belajar-cyber-security/), dan [operasi Red Team](https://www.ibm.com/id-id/think/topics/red-teaming) |


# Modul `any.proxy` di Bettercap

## A. Pengertian Singkat

Modul `any.proxy` adalah fitur [Bettercap](https://www.bettercap.org/) yang memungkinkan **redirect** (pengalihan) paket dari satu **alamat/port** ke **proxy kustom** yang kamu atur. Fitur ini sangat berguna untuk **melakukan intersepsi lalu lintas jaringan yang tidak spesifik ke protokol HTTP** atau **HTTPS** saja, melainkan bisa untuk **protokol apa pun**, tergantung kebutuhanmu.

## B. Perintah Dasar

| Perintah | Fungsi 
|:--:|:--:|
| `any.proxy on` | Mengaktifkan **proxy redirection kustom**. |
| `any.proxy off` | Menonaktifkan **proxy redirection kustom**. |

## C. Parameter Konfigurasi

Berikut adalah **parameter** yang dapat kamu sesuaikan sebelum atau saat menjalankan modul `any.proxy`:

| Parameter | Deskripsi | Nilai Default |
|:--:|:--:|:--:|
| `any.proxy.dst_address`	| Alamat tujuan tempat proxy berjalan. | `<alamat interface>` |
| `any.proxy.dst_port` | Port tujuan tempat proxy mendengarkan.	| `8080` |
| `any.proxy.iface` | Interface yang digunakan untuk melakukan redirect. | `<interface aktif>` |
| `any.proxy.protocol` | Protokol yang digunakan ([TCP](https://id.wikipedia.org/wiki/Protokol_Kendali_Transmisi)/[UDP](https://id.wikipedia.org/wiki/Protokol_Datagram_Pengguna)).	| `TCP` |
| `any.proxy.src_address` | Alamat sumber dari mana trafik akan diintersepsi. Jika kosong, semua alamat akan diproses. | (kosong) |
| `any.proxy.src_port` | **Port** atau **rentang port sumber** yang ingin dialihkan ke **proxy**. **Bisa satu**, **banyak** (dipisah koma), atau **range** (misalnya `80,443,8000-8100`). | `80` |

## D. Contoh Penggunaan

Misalkan kamu ingin **mengalihkan semua trafik** dari port **80** dan **443** ke **proxy lokal** yang berjalan di port `8080`:

```
set any.proxy.src_port 80,443
set any.proxy.dst_port 8080
any.proxy on
```

Jika kamu ingin hanya menangkap trafik dari **IP tertentu saja**:

```
set any.proxy.src_address 192.168.1.20
any.proxy on
```

## E. Kegunaan Praktis

| Kasus |	Penjelasan| 
|:--:|:--:|
| **Intercept dan analisis trafik non-HTTP** | Bisa digunakan untuk mengalihkan **trafik aplikasi custom** yang menggunakan port **TCP tertentu**. |
| **MITM tingkat lanjut** | Dapat digunakan untuk **memanipulasi data** secara **real-time** dari **port mana pun**, termasuk **login**, **API**, dan **lainnya**. |
| **Integrasi dengan proxy eksternal** | Bisa dialihkan ke **proxy eksternal** seperti [mitmproxy](https://mitmproxy.org/), [Burp Suite](https://portswigger.net/burp), atau **proxy buatan sendiri**. |

## F. Catatan Penting
- **Proxy** harus sudah **berjalan** di `dst_address:dst_port` sebelum modul `any.proxy on` **diaktifkan**.
- Pastikan [IP Forwarding](https://tkj.smkdarmasiswasidoarjo.sch.id/2024/09/27/memahami-ip-forwarding-konsep-dan-penerapannya/) dan **iptables rules** mendukung **redirection** (`Bettercap` menangani sebagian besar ini secara otomatis).
- Modul `any.proxy` bisa berkonflik dengan modul lain yang juga menggunakan **intercept** atau **redirection** (seperti `http.proxy` atau `net.sniff`), jadi pastikan kamu mengatur urutan aktivasi modul dengan benar.

## F. Kesimpulan

Modul `any.proxy` di `Bettercap` adalah modul powerful untuk melakukan **redirect lalu lintas jaringan** ke **proxy manapun dengan fleksibilitas tinggi**. Dengan konfigurasi yang tepat, kamu bisa menggunakannya untuk **debugging aplikasi**, **testing keamanan**, atau **eksperimen rekayasa lalu lintas jaringan**.

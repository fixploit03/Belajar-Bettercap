# Bab 4 - Instalasi Bettercap

## A. Linux (Debian/Ubuntu Based)

### Persyaratan:
- `build-essential`
- `libpcap-dev`
- `libusb-1.0-0-dev`
- `libnetfilter-queue-dev`

### Langkah Instalasi

Berikut ini adalah langkah-langkah instalasi `Bettercap` di sistem operasi [Linux](https://www.linux.org/) yang berbasis [Debian](https://www.debian.org/)/[Ubuntu](https://ubuntu.com/):

### 1. Kali

```
# Update repositori
sudo apt update

# Instal langsung Bettercap dari repositori
sudo apt install bettercap

# Verifikasi instalasi
bettercap -version

# Set capabilities agar bisa jalan tanpa sudo untuk beberapa fungsi
sudo setcap cap_net_raw,cap_net_admin=eip /usr/bin/bettercap

# Download dan install web UI
sudo bettercap -eval "caplets.update; ui.update; q"
```

- **Kelebihan**: Super mudah, cepat
- **Kekurangan**: Versi mungkin tidak terbaru

### 2. Ubuntu

Ada **4** cara install `bettercap` di **Ubuntu**. Ini ranking dari yang paling **mudah** sampai yang paling **advanced**:

#### 1. Melalui APT Package Manager (Paling Mudah)

```
# Update repositori
sudo apt-get update

# Instal langsung Bettercap dari repositori
sudo apt-get install bettercap

# Verifikasi instalasi
bettercap -version

# Set capabilities agar bisa jalan tanpa sudo untuk beberapa fungsi
sudo setcap cap_net_raw,cap_net_admin=eip /usr/bin/bettercap

# Download dan install web UI
sudo bettercap -eval "caplets.update; ui.update; q"
```

- **Kelebihan**: Super mudah, cepat
- **Kekurangan**: Versi mungkin tidak terbaru

#### 2. Melalui Snap Package (Mudah & Terbaru)

```
# Instal Bettercap via snap
sudo snap install bettercap

# Verifikasi instalasi
bettercap -version

# Download dan install web UI
sudo bettercap -eval "caplets.update; ui.update; q"
```

- **Kelebihan**: Mudah, versi lebih terbaru
- **Kekurangan**: Butuh [snapd](https://www.newbienote.com/2022/11/apa-itu-snap.html)

#### 3. Melalui Go Install (Recommended)

```
# Update repositori
sudo apt update

# Instal dependensi
sudo apt install -y golang-go git libpcap-dev

# Set GOPATH jika belum ada
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$PATH

# Instal Bettercap langsung dari source
go install github.com/bettercap/bettercap@latest

# Pastikan binary bettercap sudah terpasang
ls ~/go/bin/bettercap

# Copy ke system path
sudo cp ~/go/bin/bettercap /usr/local/bin/

# Verifikasi instalasi
bettercap -version

# Set capabilities agar bisa jalan tanpa sudo
sudo setcap cap_net_raw,cap_net_admin=eip /usr/local/bin/bettercap

# Download dan install web UI & caplets
sudo bettercap -eval "caplets.update; ui.update; q"
```

- **Kelebihan**: Selalu versi terbaru, mudah update
- **Kekurangan**: Butuh **Go environment**

#### 4. Melalui Compile dari Source (Advanced)

```
# Update repositori
sudo apt update

# Instal dependensi
sudo apt install -y golang-go git build-essential libpcap-dev libusb-1.0-0-dev libnetfilter-queue-dev

# Clone repositori Bettercap
git clone https://github.com/bettercap/bettercap.git
cd bettercap

# Build dan instal Bettercap
make build
sudo make install

# Verifikasi instalasi
bettercap -version

# Set capabilities agar bisa jalan tanpa sudo untuk beberapa fungsi
sudo setcap cap_net_raw,cap_net_admin=eip /usr/local/bin/bettercap

# Download dan install web UI
sudo bettercap -eval "caplets.update; ui.update; q"
```

- **Kelebihan**: Full control, bisa custom compile
- **Kekurangan**: Paling ribet

## B. Androind (Termux)

### Persyaratan:
- Device harus **ROOT** (tidak bisa tanpa root)
- Instal [Termux](https://termux.dev/en/) dari [F-Droid](https://f-droid.org/en/) (bukan Google Play Store)

### Langkah Instalasi

Berikut ini adalah langkah-langkah instalasi `Bettercap` di sistem operasi [Android](https://www.android.com/) (Termux):

#### 1. Setup Repositori

```
# Instal repositori root
pkg install root-repo

# Instal dependensi
pkg install golang git libpcap libusb
```

#### 2. Fix Golang Bug (Wajib!)

```
# Masuk ke root
sudo su

# Remount filesystem
mount -o rw,remount /

# Buat direktori yang dibutuhkan
mkdir -p /home/builder/.termux-build/_cache/18-arm-21-v2/bin/

# Buat symlink untuk pkg-config
ln -s `which pkg-config` /home/builder/.termux-build/_cache/18-arm-21-v2/bin/arm-linux-androideabi-pkg-config

# Exit dari root
exit
```

#### 3. Instal Bettercap

```
# Metode 1: Melalui Go Install (Recommended)
go install github.com/bettercap/bettercap@latest

# Metode 2: Compile dari Source
git clone https://github.com/bettercap/bettercap.git
cd bettercap
go build -o bettercap .
```

#### 4. Verifikasi Instalasi

```
# Tes instalasi
~/go/bin/bettercap -version

# Atau jika compile manual
./bettercap -version
```

## C. Docker

### Persyaratan:

- [Docker versi 17.05+](https://www.docker.com/) (untuk multi-stage build)
- **Linux** host dengan akses **network**

### Langkah Instalasi

Berikut ini adalah langkah-langkah instalasi `Bettercap` menggunakan **Docker**:

#### 1. Pull Docker Image

```
# Download image terbaru
docker pull bettercap/bettercap
```

#### 2. Penggunaan Dasar

```
# Jalankan dengan menu help
docker run -it --privileged --net=host bettercap/bettercap -h

# Jalankan dengan mode interaktif
docker run -it --privileged --net=host bettercap/bettercap

# Jalankan dengan interface spesifik
docker run -it --privileged --net=host bettercap/bettercap -iface eth0
```

### Penjelasan Opsi Docker

| Opsi | Fungsi |
|:--:|:--:|
| `-it` | **Interactive** + **TTY** (bisa ketik **command**) |
| `--privileged` | Akses penuh ke **system resources** | 
| `--net=host` | Pakai **network host** (akses langsung ke **interfaces**) |

####

### D. Dokumetasi Resmi instalasi Bettercap

Untuk informasi instalasi Bettercap lebih lengkapnya lagi ada di dokumetasi resmi Bettercap-nya: [https://www.bettercap.org/installation/](https://www.bettercap.org/installation/)

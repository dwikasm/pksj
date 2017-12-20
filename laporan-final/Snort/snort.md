Laporan PKSJ Snort

### Dasar Teori 

Snort adalah sebuah software yang berguna untuk mengamati aktivitas dalam suatu jaringan komputer. 
Snort dapat digunakan sebagai suatu Network Intrusion Detection System (NIDS) yang berskala ringan (lightweight).
Komponen – komponen Snort IDS (Intrusion Detection System) meliputi :

-Rule Snort : database yang berisi pola – pola serangan berupa signature jenis -jenis serangan. Rule snort harus selalu 
terupdate secara rutin agar ketika ada suatu teknik serangan yang baru, serangan tersebut dapat terdeteksi.
-Snort Engine : program yang berjalan sebagai daemon proses yang selalu bekerja untuk membaca paket data dan 
kemudian membadingkan dengan Rule Snort.
-Alert : catatan serangan pada deteksi penyusupan. 
Jika Snort engine mendeteksi paket data yang lewat sebagai sebuah serangan, maka snort engine akam mengirimkan alert 
berupa log file. Kemudian alert tersebut akan tersimpan di dalam database.


### Instalasi

Requirements:
```
Mac OS 10.2.3
Homebrew sudah di install , Homebrew dapat di instal dengan:
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```
Untuk Menginstall Snort dalam macOS cukup mudah hanya membutuhkan Homebrew yang sudah terinstall kemudian ketikan command
```
brew install snort
```
dari situ secara otomatis brew menginstall semua dependency yang diperlukan untuk menjalankan snort
![asd](snortinstal.png)


### Konfigurasi

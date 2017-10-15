# Perancangan Keamanan Sistem dan Jaringan

## Tugas 1

### Pendahuluan
Isi pendahuluan

### Dasar Teori
penjelasan OS dan semua tools yang digunakan
os : ubuntu server dan ubuntu desktop
tools : openssh, hydra, ncrack

### Uji Penetrasi
* Langkah instalasi ubuntu server
  1. Buka VirtualBox, pilih New 
  2. Masukkan konfigurasi virtual machine lalu create
  3. Klik kanan virtual machine yang dibuat, pilih setting
  4. Pilih bagian network, tambahkan adapter 2 dengan opsi host-only adapter
  5. Pilih bagian storage, klik bagian disk image, pilih choose virtual optical disk lalu masukkan lokasi iso ubuntu server, ok
  6. Run virtual machine tadi lalu install ubuntu server seperti biasanya
  7. Karena kita membutuh ip untuk ssh, tambahkan ip address di /etc/network/interfaces
  
* Langkah instalasi OS untuk penetrasi (Ubuntu Desktop)
  1. Buka VirtualBox, pilih New 
  2. Masukkan konfigurasi virtual machine lalu create
  3. Klik kanan virtual machine yang dibuat, pilih setting
  4. Pilih bagian network, tambahkan adapter 2 dengan opsi host-only adapter
  5. Pilih bagian storage, klik bagian disk image, pilih choose virtual optical disk lalu masukkan lokasi iso ubuntu desktop, ok
  6. Run virtual machine tadi lalu install ubuntu desktop seperti biasanya
  
* Langkah instalasi SSH Server
  1. Pada ubuntu server dan ubuntu desktop : sudo apt-get install openssh-server
  
* Langkah uji penetrasi dengan SSH brute force tools

  **Hydra**
    1. sudo apt-get install hydra hydra-gtk
    2. Untuk memakainya : hydra -l ubuntu -x 6:6:a 192.168.26.102 ssh -V
    
  **Ncrack**
    1. wget http://nmap.org/ncrack/dist/ncrack-0.4ALPHA.tar.gz
    2. sudo apt-get install build-essential checkinstall libssl-dev  libssh-dev
    3. tar xvfz ncrack-0.4ALPHA.tar.gz
    4. cd ncrack-0.4ALPHA/ 
    5. ./configure
    6. make
    7. sudo make install
    8. Untuk memakainya ncrack -p 22 --user ubuntu -P pass.txt 192.168.56.102

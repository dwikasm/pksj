## Lesson 7 : Automate SQL Injection with SqlMap 

Pada lesson ini diberikan contoh - contoh script sqlmap yang dapat digunakan tidak hanya untuk melakukan sql injection dalam mendapatkan data - data penting pada aplikasi web tapi juga dalam pengumpulan informasi terkait database suatu website. 

NOTE
----

* ip website dvwa : 10.151.34.215
* ip backtack 	: 10.151.34.174

| **Langkah 1: Mendapatkan Referer dan Cookie** |
| :--- |

1. Pada browser Firefox backtrack buka Tools > Addson  

2. Aktifkan Tool Temper Data 

* ![](/lesson5/8.png)

3. Buka halaman login dvwa

* ![](/lesson5/9.png)

4. Jalankan Temper Data, buka menu Tool > Temper Data . setelah terbuka klik Start Temper

* ![](/lesson5/10.png)

| **Langkah 2: Menggunakan SqlMap untuk mendapatkan DB dan User yang aktif** |
| :--- |

1. Lakukan login pada dvwa, saat muncul pop up hapus tanda centang pada continue tempering, klik Submit

* ![](/lesson5/15.png)

2. Setelah login buka Temper Data

3. Klik data POST yang muncul paling atas, kemudian pilih POSTDATA pada Request Header lalu copy 

* ![](/lesson5/11.png)

| **Langkah 3: Menggunakan SqlMap untuk mendapatkan Username dan Password Database Management** |
| :--- |

1. Unduh file crack_web_form.pl pada link berikut
	* http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson5/cwf.tar.gz

2. Buka `/pentest/password/cwf/`

3. Extract cwf.tar.gz dengan command `tar xovfz cwf.tar.gz`

4. Ubah permission `chmod 700 crack_web_form.pl`

* ![](/lesson5/12.png)

| **Langkah 4: Menggunakan SqlMap untuk mendapatkan Daftar DB yang ada** |
| :--- |

1. Jalankan command crack_web_form.pl pada direktori `/pentest/passwords/cwf`

2. `./crack_web_form.pl -U admin -P password.txt -http "http://10.151.34.215/dvwa/login.php" -data "username=USERNAME&password=PASSWORD&Login=Login" -M "Login failed"`

* ![](/lesson5/13.png)
      
3. Perhatikan hasil crack yang telah dilakukan, untuk menampilkan hasil percobaan crack yang success jalankan command di bawah:
     
4. `grep Successful crack_output.txt`

* ![](/lesson5/14.PNG)

| **Langkah 5: Menggunakan SqlMap untuk mendapatkan Table dan Content dari DB tertentu** |
| :--- |


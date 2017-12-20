## Lesson 5 : Using Temper Data with crack_web_form.pl

Pada lesson ini dijelaskan tentang penggunaan temper data dalam mendapatkan data2 yang dikirim ke website khususnya POSTDATA yang nantinya akan digunakan untuk cracking pada form yang ada pada web dvwa.

NOTE
----

* ip website dvwa : 10.151.34.215
* ip backtack 	: 10.151.34.174

| **Langkah 1: Konfigurasi Temper Data** |
| :--- |

1. Pada browser Firefox backtrack buka Tools > Addson  

2. Aktifkan Tool Temper Data 

* ![](/lesson5/8.png)

3. Buka halaman login dvwa

* ![](/lesson5/9.png)

4. Jalankan Temper Data, buka menu Tool > Temper Data . setelah terbuka klik Start Temper

* ![](/lesson5/10.png)

| **Langkah 2: Dapatkan POSTDATA** |
| :--- |

1. Lakukan login pada dvwa, saat muncul pop up hapus tanda centang pada continue tempering, klik Submit

* ![](/lesson5/15.png)

2. Setelah login buka Temper Data

3. Klik data POST yang muncul paling atas, kemudian pilih POSTDATA pada Request Header lalu copy 

* ![](/lesson5/11.png)

| **Langkah 3: Konfigurasi crack_web_form.pl** |
| :--- |

1. Unduh file crack_web_form.pl pada link berikut
	* http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson5/cwf.tar.gz

2. Buka `/pentest/password/cwf/`

3. Extract cwf.tar.gz dengan command `tar xovfz cwf.tar.gz`

4. Ubah permission `chmod 700 crack_web_form.pl`

* ![](/lesson5/12.png)

| **Langkah 4: Hasil Crack** |
| :--- |

1. Jalankan command crack_web_form.pl pada direktori `/pentest/passwords/cwf`

2. `./crack_web_form.pl -U admin -P password.txt -http "http://10.151.34.215/dvwa/login.php" -data "username=USERNAME&password=PASSWORD&Login=Login" -M "Login failed"`

* ![](/lesson5/13.png)
      
3. Perhatikan hasil crack yang telah dilakukan, untuk menampilkan hasil percobaan crack yang success jalankan command di bawah:
     
4. `grep Successful crack_output.txt`

* ![](/lesson5/14.PNG)



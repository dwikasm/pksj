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

![](/laporan-final/DVWA/lesson5/8.PNG)

3. Buka halaman login dvwa

![](/laporan-final/DVWA/lesson5/9.PNG)

4. Jalankan Temper Data, buka menu Tool > Temper Data . setelah terbuka klik Start Temper

![](/laporan-final/DVWA/lesson5/10.PNG)

| **Langkah 2: Dapatkan POSTDATA** |
| :--- |

1. Lakukan login pada dvwa, saat muncul pop up hapus tanda centang pada continue tempering, klik Submit

![](/laporan-final/DVWA/lesson5/15.PNG)

2. Setelah login buka Temper Data

3. Klik data POST yang muncul paling atas, kemudian pilih POSTDATA pada Request Header lalu copy 

![](/laporan-final/DVWA/lesson5/11.PNG)

| **Langkah 3: Konfigurasi crack_web_form.pl** |
| :--- |

1. Unduh file crack_web_form.pl pada link berikut
	* http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson5/cwf.tar.gz

2. Buka `/pentest/password/cwf/`

3. Extract cwf.tar.gz dengan command `tar xovfz cwf.tar.gz`

4. Ubah permission `chmod 700 crack_web_form.pl`

![](/laporan-final/DVWA/lesson5/12.PNG)

| **Langkah 4: Hasil Crack** |
| :--- |

1. Jalankan command crack_web_form.pl pada direktori `/pentest/passwords/cwf`

2. `./crack_web_form.pl -U admin -P password.txt -http "http://10.151.34.215/dvwa/login.php" -data "username=USERNAME&password=PASSWORD&Login=Login" -M "Login failed"`

![](/laporan-final/DVWA/lesson5/13.PNG)
      
3. Perhatikan hasil crack yang telah dilakukan, untuk menampilkan hasil percobaan crack yang success jalankan command di bawah:
     
4. `grep Successful crack_output.txt`

![](/laporan-final/DVWA/lesson5/14.PNG)



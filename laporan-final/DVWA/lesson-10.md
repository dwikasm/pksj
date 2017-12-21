## Lesson 10 : Cross Site Request Forgery combined with curl

Pada lesson ini kita akan melakukan cross site request forgery attack dengan curl. pada lesson ini kita akan mencoba CSRF attack secara langsung, mendapatkan Cookie Session dengan menggunakan Reflective XSS attack, kemudian melakukan serangan CSRF dengan curl untuk mengubah password admin

NOTE
----

* ip website dvwa : 10.151.34.215
* ip backtack 	: 10.151.34.174

| **Langkah 1: Melakukan Serangan CSRF** |
| :--- |

1. Buka dvwa kemudian pilih menu CSRF

![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson10/index.166.jpg)

2. Masukkan password baru dan konfirmasi password dengan abc123 kemudian klik tombol Change untuk mengganti password.

![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson10/index.167.jpg)

3. Pada URL yang dikirim CSRF terdapat parameter password_new dan password_conf yang dipisahkan dengan &.  

![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson10/index.168.jpg)	

| **Langkah 2: Capture dan Manipulasi CSRF URL untuk merubah password Admin** |
| :--- |

1. Simpan URL CSRF dan pesan yang muncul setelah melakukan perubahan password admin. URL CSRF ini akan digunakan untuk dijalankan dengan curl.

![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson10/index.170.jpg)	

| **Langkah 3: Melakukan Relative XSS Attack untuk mendapatkan Cookie Session** |
| :--- |

1. Pada dvwa pilih menu XSS Reflective. kemudian pada form yang muncul submit command berikut :

``
	<script>alert(document.cookie)</script>
``

![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson10/index.176.jpg)	

2. Kemudian akan muncul pop up berupa session cookie kemudian select cookie dan copy paste dengan cara pilih menu Edit > Copy

![](http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson10/index.177.jpg)	

| **Langkah 4: Membuat Curl CSRF untuk mengubah password Admin** |
| :--- |

1. Dari Cookie dan URL yang sudah didapatkan masukkan pada tag --cookie dan --location pada command curl

![](/laporan-final/DVWA/lesson10/5.PNG)	

2. Kemudian jalankan curl tersebut pada command line dengan tambahan ` | grep "Password Change" | tee curl.txt`

![](/laporan-final/DVWA/lesson10/3.PNG)	

3. Berikut hasil percobaan yang kami lakukan

![](/laporan-final/DVWA/lesson10/4.png)

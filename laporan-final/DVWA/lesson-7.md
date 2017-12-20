## Lesson 7 : Automate SQL Injection with SqlMap 

Pada lesson ini diberikan contoh - contoh script sqlmap yang dapat digunakan tidak hanya untuk melakukan sql injection dalam mendapatkan data - data penting pada aplikasi web tapi juga dalam pengumpulan informasi terkait database suatu website. 

NOTE
----

* ip website dvwa : 10.151.34.215
* ip backtack 	: 10.151.34.174

| **Langkah 1: Mendapatkan Referer dan Cookie** |
| :--- |

1. Gunakan Temper Data seperti yang digunakan pada lesson 5. Login terlebih dahulu ke dalam dvwa, pilih menu SQL Injection     

2. Masukkan angka 1 pada form lalu klik tombol submit

![](/laporan-final/DVWA/lesson7/1.PNG)

3. Buka hasil Temper Data, dapatkan header Referer dan Cookie pada Request Header, copy informasi header tersebut

![](/laporan-final/DVWA/lesson7/2.PNG)

4. Paste header diatas pada notepad untuk digunakan selanjutnya

![](/laporan-final/DVWA/lesson7/3.PNG)

| **Langkah 2: Menggunakan SqlMap untuk mendapatkan DB dan User yang aktif** |
| :--- |

1. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan DB dan user yang aktif berikut SqlMap yang dijalankan

![](/laporan-final/DVWA/lesson7/4.PNG)

2. Berikut hasil yang didapatkan user yang aktif root, dan DB yang digunakan dvwa

![](/laporan-final/DVWA/lesson7/5.PNG)

| **Langkah 3: Menggunakan SqlMap untuk mendapatkan Username dan Password Database Management** |
| :--- |

1. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan Usernama dan Password Database Management berikut SqlMap yang dijalankan

![](/laporan-final/DVWA/lesson7/6.PNG)	

2. Berikut hasil berupa daftar user database management yang ada

![](/laporan-final/DVWA/lesson7/7.PNG)	

3. Berikut hasil berupa daftar user dan hashed password database management yang ada

![](/laporan-final/DVWA/lesson7/8.PNG)	

4. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan user privileges dari user db_hacker berikut SqlMap yang dijalankan.

![](/laporan-final/DVWA/lesson7/9.PNG)	

5. Berikut hasil yang didapatkan

![](/laporan-final/DVWA/lesson7/10.PNG)	

| **Langkah 4: Menggunakan SqlMap untuk mendapatkan Daftar DB yang ada** |
| :--- |

1. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan Database yang ada berikut SqlMap yang dijalankan

![](/laporan-final/DVWA/lesson7/11.PNG)	

2. Berikut hasil yang didapatkan

![](/laporan-final/DVWA/lesson7/12.PNG)	
      

| **Langkah 5: Menggunakan SqlMap untuk mendapatkan Table dan Content dari DB tertentu** |
| :--- |

1. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan data tabel yang ada pada database dvwa berikut SqlMap yang dijalankan.

![](/laporan-final/DVWA/lesson7/13.PNG)	

2. Berikut hasil tabel yang ada

![](/laporan-final/DVWA/lesson7/14.PNG)	

3. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan deskripsi pada tabel users berikut SqlMap yang dijalankan.

![](/laporan-final/DVWA/lesson7/15.PNG)	

4. Berikut deskripsi tabel users

![](/laporan-final/DVWA/lesson7/16.PNG)

5. Masukkan referer dan cookie sebagai parameter dari tag yang kan digunakan pada SqlMap, untuk mendapatkan data yang ada pada tabel users berikut SqlMap yang dijalankan.

![](/laporan-final/DVWA/lesson7/17.PNG)	

6. Berikut hasil tabel yang ada

![](/laporan-final/DVWA/lesson7/19.PNG)

7. Beriktu hasil akhir pada lesson ini

![](/laporan-final/DVWA/lesson7/20.PNG)
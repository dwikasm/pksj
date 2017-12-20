### Burp Suice, Man-in-the-middle-attack

* Apa itu Burp Suite?
  * Burp suite adalah aplikasi java yang bisa digunakan untuk mengamankan maupun membobol aplikasi web.

| **Section 1: Mengatur Setting Proxy ** |
| :--- |

1. Buka browser pada Kali
2. Ubah proxy
   * **Langkah:**
     1. Buka preferences
     2. Klik Advanced
     3. Buka tab Network 
     4. Klik tombol Settings
      * ![](/assets/lesson11/1.PNG)
     5. Ubah Proxy menjadi `127.0.0.1`
     6. Centang kotak dibawahnya
      * ![](/assets/lesson11/2.PNG)

| **Section 2: Konfigurasi Burp Suite** |
| :--- |

1. Membuka Burp Suite
   * **Langkah:**  
     1. Buka menu Kali.  
     2. Pilih `Web Application Analysis`
     3. Pilih `burpsuit`
   * ![](/assets/lesson11/3.PNG)

2. Menggunakan Burp Suite
   * **Langkah:**  
     1. Pilih tab Proxy 
     2. Pilih Option
     3. Pastikan port interface
     * ![](/assets/lesson11/4.PNG)
     4. Pilih Intercept
     5. klik tombol `intercept is on`
     * ![](/assets/lesson11/5.PNG)

| **Section 3: Intercept menggunakan Burp Suit** |
| :--- |

1. Buka homepage dvwa
   * **Langkah:**
     1. Buka browser.
     2. Masukkan `192.168.56.102/dvwa`
     3. Perhatikan halaman tidak terbuka
   * ![](/assets/lesson11/6.PNG)

2. Mendapatkan cookie
   * **Langkah:**
     1. Buka Burp Suit.
     2. Klik tombol forward sampai berhenti.
     * ![](/assets/lesson11/7.PNG)
     3. Buka tab HTTP History.
     4. Lihat hasil cookie.
     * ![](/assets/lesson11/8.PNG)

3. Intercept PHP Session
   * **Langkah:**
     1. Masukkan user dan password pada halaman login.
     * ![](/assets/lesson11/9.PNG)
     2. Buka Burp Suite.
     3. Klik tombol forward sampai berhenti.
     * ![](/assets/lesson11/10.PNG)
     4. Buka tab HTTP History.
     * ![](/assets/lesson11/11.PNG)
     5. Copy cookie
     * ![](/assets/lesson11/12.PNG)

4. Buat perintah curl sebagai berikut
  * ![](/assets/lesson11/13.PNG)

5. Jalankan di terminal. Kita dapat masuk tanpa login.
  * ![](/assets/lesson11/14.PNG)


| **Section 4: Menggunakan Cookie untuk Masuk ke DVWA** |
| :--- |

1. Install cookie manager pada browser
  * ![](/assets/lesson11/17.PNG)
  * ![](/assets/lesson11/18.PNG)

2. Buka cookie manager.
  * ![](/assets/lesson11/19.PNG)
   
3. Edit PHPSESSID. Ganti dengan cookie yang kita dapatkan sebelumnya.
  * ![](/assets/lesson11/20.PNG)
   
4. Buka halaman dvwa.
  * ![](/assets/lesson11/20.PNG)
5. Perhatikan kita dapat masuk tanpa harus login.

| **Section 5: Hasil Akhir** |
| :--- |

1. Mengembalikan setting proxy
   * ![](/assets/lesson11/22.PNG)

2. Bukti hasil akhir
  * ![](/assets/lesson11/23.PNG)



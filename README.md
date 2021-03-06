# Modul1_C09
Kelompok C09
- 05111840000028  M. Frediansyah Sinaga
- 05111840000072  Kresna Adhi Pramana

Praktikum Modul 1 berupa *Wireshark Filter Expression*.


## Soal
Terdapat tiga buah file *.pcapng yang mendukung soal-soal display filter, yaitu:
- File pertama untuk menjawab soal nomor 1-5 dan nomor 10.
- File kedua untuk menjawab soal nomor 6, 7, dan 9.
- File ketiga untuk menjawab soal nomor 8.

### A. Display Filter
   1. Sebutkan webserver yang digunakan pada "testing.mekanis.me"!
   2. Simpan gambar "Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg"!
   3. Cari username dan password ketika login di "ppid.dpr.go.id"!
   4. Temukan paket dari web-web yang menggunakan basic authentication method!
   5. Ikuti perintah di aku.pengen.pw! Username dan password bisa didapatkan dari file .pcapng!
   6. Seseorang menyimpan file zip melalui FTP dengan nama "Answer.zip". Simpan dan Buka file "Open This.pdf" di Answer.zip. Untuk mendapatkan password zipnya, 
       temukan dalam file zipkey.txt (passwordnya adalah isi dari file txt tersebut).
   7. Ada 500 file zip yang disimpan ke FTP Server dengan nama 1.zip, 2.zip, ..., 500.zip. Salah satunya berisi pdf yang berisi puisi. Simpan dan Buka file pdf tersebut.
       Your Super Mega Ultra Rare Hint = nama pdf-nya "Yes.pdf"
   8. Cari objek apa saja yang didownload (RETR) dari koneksi FTP dengan Microsoft FTP Service!
   9. Cari username dan password ketika login FTP pada localhost!
   10. Cari file .pdf di wireshark lalu download dan buka file tersebut!
        clue: "25 50 44 46" 

### B. Capture Filter
   11. Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!
   12. Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80!
   13. Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!
   14. Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!
   15. Filter sehingga wireshark hanya mengambil paket yang tujuannya ke monta.if.its.ac.id!


## Jawaban
   1. http.host == testing.mekanisme.me, follow HTTP stream, dan cek bagian server. Webserver yang digunakan yaitu nginx/1.14.0 (Ubuntu)
   ![Foto 1a](img/1a.PNG)
   ![Foto 1b](img/1b.PNG)
   
   2. http.host contains "dpr". Gambar lalu dicari melalui export dengan keywordnya : Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg , lalu disave
   ![foto 2a](img/2a.jpg)
   Gambar yang didapat adalah :  
   ![foto 2b](img/2b.jpg)
   
   3. http.host == ppid.dpr.go.id && http.request.method == POST. Username yang didapatkan yaitu "10pemuda" dan password yang digunakan yaitu "guncangdunia"
   ![Foto 3](img/3.PNG)
   
   4. http.authbasic
   ![Foto 4a](img/4a.PNG)
   ![Foto 4b](img/4b.PNG)
   
   5. http.host contains "aku.pengen.pw". Lalu, di Authorization, terlihat Credentialsnya yang dipakai sebagai Username dan Password-nya.
   ![Foto 5a](img/5a.jpg)
   aku.pengen.pw lalu menampilkan :  
   ![Foto 5b](img/5b.jpg)
   
   6. ftp-data, string filter “Answer.zip”, follow tcp stream, dan save as raw untuk zip, ftp-data, string filter “zipkey.txt”, follow tcp stream, dan save as raw untuk key.
   ![Foto 6a](img/6a.PNG)
   ![Foto 6b](img/6b.PNG)
   ![Foto 6c](img/6c.PNG)
   ![Foto 6d](img/6d.PNG)
   ![Foto 6e](img/6e.PNG)
   ![Foto 6f](img/6f.PNG)
   ![Foto 6g](img/6g.PNG)
   
   7. ftp-data contains "Yes.pdf" . Lalu akan terlihat bahwa zip bernomor 473 lah yang memiliki Yes.pdf didalamnya
   ![Foto 7a](img/7a.jpg)
   Dan isi puisi yang ada didalam file pdf adalah :  
   ![Foto 7b](img/7b.jpg)
   
   8. Pertama, mencari IP dari Microsoft FTP Service dengan menggunakan : ftp contains "Microsoft".
   ![Foto 8a](img/8a.jpg)
   Lalu setelah dapat, yaitu : 198.246.117.106 ,lanjut mencari objek yang didownload menggunakan : ftp.request.command == "RETR" && ip.addr == 198.246.117.106 .
   ![Foto 8b](img/8b.jpg)
   
   9. ftp.request.command == USER || ftp.request.command == PASS. Username yang digunakan yaitu "dhana" dan password yang digunakan yaitu "dhana123"
   ![Foto 9](img/9.PNG)
   
   10. frame contains "application/pdf" . Akan terlihat packet yang memuat pdf. Lalu di Follow TCP Streamnya, dan di findnya masukkan clue Hex-nya, dan dapat dilihat ada di tcp    streamnya, setelah itu download file-nya.
   ![Foto 10a](img/10a.jpg)
   Pdf-nya berisi :  
   ![Foto 10b](img/10b.jpg)
   
   11. port 21  
   ![Foto 11](img/11.PNG)
   
   12. src port 80  
   ![Foto 12](img/12.PNG)
   
   13. dst port 443  
   ![Foto 13](img/13.PNG)
   
   14. src host 192.168.1.3, ip 192.168.1.3  
   ![Foto 14](img/14.PNG)
   
   15. dst host monta.if.its.ac.id  
   ![Foto 15](img/15.PNG)

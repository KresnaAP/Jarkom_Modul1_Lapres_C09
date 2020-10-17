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
   ![Foto 1a](img/1a.png)
   ![Foto 1b](img/1b.png)
   
   2. http.host contains "dpr"
   
   3. http.host == ppid.dpr.go.id && http.request.method == POST. Username yang didapatkan yaitu "10pemuda" dan password yang digunakan yaitu "guncangdunia"
   ![Foto 3](img/3.png)
   
   4. http.authbasic
   ![Foto 4a](img/4a.png)
   ![Foto 4b](img/4b.png)
   
   5. http.host contains "aku.pengen.pw"
   
   6. ftp-data, string filter “Answer.zip”, follow tcp stream, dan save as raw untuk zip, ftp-data, string filter “zipkey.txt”, follow tcp stream, dan save as raw untuk key.
   ![Foto 6a](img/6a.png)
   ![Foto 6b](img/6b.png)
   ![Foto 6c](img/6c.png)
   ![Foto 6d](img/6d.png)
   ![Foto 6e](img/6e.png)
   ![Foto 6f](img/6f.png)
   ![Foto 6g](img/6g.png)
   
   7. ftp-data contains "Yes.pdf"
   
   8. 
   
   9. ftp.request.command == USER || ftp.request.command == PASS. Username yang digunakan yaitu "dhana" dan password yang digunakan yaitu "dhana123"
   ![Foto 9](img/9.png)
   
   10. frame contains "application/pdf"
   
   11. port 21
   ![Foto 11](img/11.png)
   
   12. src port 80
   ![Foto 12](img/12.png)
   
   13. dst port 443
   ![Foto 13](img/13.png)
   
   14. src host 192.168.1.3, ip 192.168.1.3
   ![Foto 14](img/14.png)
   
   15. dst host monta.if.its.ac.id
   ![Foto 15](img/15.png)

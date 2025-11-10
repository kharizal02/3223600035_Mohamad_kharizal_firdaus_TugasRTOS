# Button Task – ESP32-S3 FreeRTOS

Task ini digunakan untuk membaca dua tombol pada ESP32-S3 menggunakan mekanisme multitasking dari FreeRTOS. Tombol menggunakan mode INPUT_PULLUP, sehingga kondisi tombol dianggap aktif ketika ditekan dan menghasilkan logika LOW.

## Fitur Utama
- Membaca dua tombol secara independen (GPIO 4 dan GPIO 6)
- Menggunakan FreeRTOS Task sehingga pembacaan tombol berjalan paralel dengan task lain
- Memiliki debounce software untuk mencegah pembacaan berulang
- Menampilkan status tombol melalui Serial Monitor

## Cara Kerja
1. Kedua pin tombol diinisialisasi menggunakan INPUT_PULLUP.  
2. Task melakukan pengecekan kondisi tombol secara terus-menerus.  
3. Jika tombol ditekan (LOW), task mengirimkan pesan ke Serial Monitor.  
4. Debounce 200 ms digunakan untuk mencegah pembacaan ganda.  
5. Task diberi jeda 10 ms untuk mengurangi beban CPU.  
6. Task dapat dijalankan pada Core 0 atau Core 1 menggunakan xTaskCreatePinnedToCore.

## Penggunaan
- Tombol dihubungkan dari GPIO ke GND.
- Karena menggunakan INPUT_PULLUP, tidak diperlukan resistor eksternal.
- Buka Serial Monitor dengan baud 115200 untuk melihat output.



# Video demo menggunakan core1



https://github.com/user-attachments/assets/05b69536-9b42-428c-a6f6-543674cc3cdf



# Video demo menggunakan core0



https://github.com/user-attachments/assets/0a8f05cc-ffdf-4164-be27-56413ca8b439






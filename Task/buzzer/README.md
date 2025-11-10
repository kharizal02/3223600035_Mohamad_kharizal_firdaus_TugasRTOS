# Buzzer Task – ESP32-S3 FreeRTOS

Task ini digunakan untuk mengendalikan buzzer pada ESP32-S3 menggunakan FreeRTOS. Buzzer akan berbunyi dengan frekuensi tertentu selama jeda waktu tertentu, kemudian berhenti, dan pola ini berulang terus-menerus.

## Fitur Utama
- Menggunakan buzzer pada GPIO 4
- Menghasilkan bunyi menggunakan fungsi `tone()`
- Menghentikan bunyi dengan `noTone()`
- Menggunakan FreeRTOS Task untuk berjalan paralel dengan task lainnya
- Dapat dijalankan pada core 0 atau core 1

## Cara Kerja
1. Pin buzzer diinisialisasi sebagai OUTPUT.
2. Task membunyikan buzzer dengan frekuensi 1000 Hz selama 300 ms.
3. Buzzer kemudian dimatikan selama 500 ms.
4. Pola ini berulang terus-menerus menggunakan FreeRTOS `vTaskDelay`.
5. Task ditempatkan pada core tertentu menggunakan `xTaskCreatePinnedToCore`.

## Tujuan
- Memberikan contoh penggunaan buzzer dalam lingkungan multitasking.
- Menunjukkan cara mengatur timing suara dengan FreeRTOS.
- Memberikan dasar implementasi notifikasi suara pada ESP32-S3.

## Pinout
| Komponen | GPIO |
|----------|------|
| Buzzer   | 4    |

## Penggunaan
- Upload program ke ESP32-S3.
- Atur core yang ingin digunakan pada fungsi `xTaskCreatePinnedToCore`.
- Buzzer akan berbunyi mengikuti pola yang ditentukan.


# Video demo Menggunakan core1


https://github.com/user-attachments/assets/0c8ca827-0a7b-473b-a6a1-035a4acb6c53


# Video demo Menggunakan core0

https://github.com/user-attachments/assets/70506004-a1d2-423b-af1b-ab13328d6276


# LED Task – ESP32-S3 FreeRTOS

Task ini digunakan untuk mengendalikan tiga LED pada ESP32-S3 menggunakan FreeRTOS. LED akan menyala dan mati secara bergantian dalam pola yang berulang, dan task dapat dijalankan pada core 0 atau core 1.

## Fitur Utama
- Mengontrol 3 LED (GPIO 1, 2, dan 42)
- Menjalankan pola berkedip bergantian
- Menggunakan FreeRTOS Task
- Dapat dipindah ke core 0 atau core 1

## Cara Kerja
1. Ketiga pin LED diatur sebagai OUTPUT.
2. Task menyalakan LED1 dan LED3, sementara LED2 mati, selama 500 ms.
3. Task kemudian mematikan LED1 dan LED3, dan menyalakan LED2 selama 500 ms.
4. Pola ini berlangsung terus-menerus tanpa henti.
5. Task ditempatkan pada core tertentu menggunakan `xTaskCreatePinnedToCore`.

## Tujuan
- Memberikan contoh dasar penggunaan LED dengan FreeRTOS.
- Menampilkan cara membuat pola LED sebagai task terpisah.
- Menunjukkan cara kerja multicore pada ESP32-S3.

## Pinout
| LED | GPIO |
|-----|------|
| LED1 | 1 |
| LED2 | 2 |
| LED3 | 42 |

disini saya menggunakan resistor 1K oHm

## Penggunaan
- Upload program ke ESP32-S3.
- Atur core pada fungsi `xTaskCreatePinnedToCore`.
- LED akan berkedip mengikuti pola yang ditentukan.

# Video demo menggunakan core1


https://github.com/user-attachments/assets/e1c8ddc6-51d1-4137-ab4a-076ad4490c23


# Video demo menggunakan core0

https://github.com/user-attachments/assets/22d44de2-a71d-4817-bcbe-34b306f8ba81


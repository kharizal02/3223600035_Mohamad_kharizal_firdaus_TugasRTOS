# Stepper Motor Task – ESP32-S3 FreeRTOS

Task ini digunakan untuk mengendalikan motor stepper menggunakan library **AccelStepper** pada ESP32-S3. Motor bergerak maju dan mundur dengan jarak tertentu secara berulang menggunakan FreeRTOS Task.

## Fitur Utama
- Menggunakan driver mode AccelStepper (step dan direction pin).
- Kontrol posisi motor stepper secara halus menggunakan `setAcceleration()` dan `setMaxSpeed()`.
- Motor bergerak maju 200 langkah, lalu mundur 200 langkah secara terus-menerus.
- Task berjalan mandiri pada salah satu core ESP32-S3.
- Tidak mengganggu task lain karena loop utama (`loop()`) dibiarkan kosong.

## Cara Kerja
1. Motor stepper dikonfigurasi dengan mode driver, menggunakan:
   - **STEP pin = 13**
   - **DIR pin = 12**
2. Kecepatan maksimum diatur ke 800 langkah/detik dan akselerasi 400.
3. Task memerintahkan motor:
   - Bergerak maju sejauh 200 langkah.
   - Menunggu hingga posisi tercapai menggunakan `run()`.
   - Delay 200 ms.
   - Bergerak mundur sejauh 200 langkah.
   - Menunggu posisi tercapai.
   - Delay 200 ms.
4. Siklus ini diulang tanpa henti.
5. Task diletakkan pada core yang dipilih menggunakan `xTaskCreatePinnedToCore`.

## Tujuan
- Memberikan contoh penggunaan FreeRTOS untuk mengontrol motor stepper.
- Demonstrasi gerakan smooth dengan AccelStepper.
- Memisahkan kontrol motor dari loop utama sehingga lebih rapi dan stabil.

## Pinout
| Fungsi | GPIO |
|--------|------|
| STEP   | 13   |
| DIR    | 12   |

Pastikan driver motor (A4988/DRV8825/dll) sudah disetel arusnya dan memiliki power supply yang memadai.

## Penggunaan
- Upload program ke ESP32-S3.
- Pastikan wiring stepper driver benar.
- Buka Serial Monitor (115200) untuk melihat arah gerakan.
- Motor akan otomatis maju dan mundur secara bergantian.


# Video demo Menggunakan core1

https://github.com/user-attachments/assets/8856f553-87f6-498b-a925-dd62e26bbc28

# Video demo Menggunakan core0

https://github.com/user-attachments/assets/382dcddd-b240-480e-912b-8f7190639184




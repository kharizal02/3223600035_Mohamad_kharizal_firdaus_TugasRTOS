Task – ESP32-S3 FreeRTOS Peripheral Collection

Repository ini berisi kumpulan tugas implementasi berbagai peripheral menggunakan ESP32-S3, masing-masing dilengkapi dengan:

✅ Kode program (.ino)
✅ Video penjelasan (core0 / core1)
✅ Diagram wiring

Setiap folder mewakili satu peripheral atau gabungan beberapa peripheral yang dijalankan menggunakan FreeRTOS Tasks.

## Struktur Folder
Task/
│
├── button/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
├── buzzer/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── code0.mp4
│   └── code1.mp4
│
├── LED/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
├── motor stepper/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
├── oled/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
├── potensio/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
├── rotary/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
├── servo/
│   ├── sketch.ino
│   ├── wiring.png
│   ├── core0.mp4
│   └── core1.mp4
│
└── Gabungan semua peripheral/
    ├── sketch.ino
    ├── wiring.png
    └── video.mp4

## Deskripsi Tiap Folder
✅ 1. button/

Berisi program untuk membaca input tombol menggunakan interrupt atau polling, lalu ditampilkan melalui serial atau digunakan untuk mengontrol task lain.

✅ 2. buzzer/

Contoh penggunaan buzzer aktif maupun pasif dalam task FreeRTOS.
Terdapat contoh tone dan non-tone.

✅ 3. LED/

Menyalakan LED dengan berbagai pola menggunakan task terpisah:

Task untuk LED blink

Task untuk LED status

Task untuk efek tertentu

✅ 4. motor stepper/

Kontrol motor stepper menggunakan driver (ULN2003 / A4988) dengan AccelStepper.

✅ 5. oled/

Menampilkan data pada OLED SSD1306 menggunakan library Adafruit dengan multitasking.

✅ 6. potensio/

Membaca nilai ADC potensiometer yang kemudian ditampilkan ke serial atau OLED.

✅ 7. rotary encoder/

Pemrosesan rotary encoder incremental (A/B signal), lengkap dengan debouncing dan perubahan nilai.

✅ 8. servo/

Mengontrol servo menggunakan library ESP32Servo di task terpisah.

✅ 9. Gabungan semua peripheral/

Proyek integrasi lengkap:

Button

LED

Servo

Buzzer

OLED

Rotary / Potensio

Sensor lain (jika ada)

Folder ini menunjukkan bagaimana semua peripheral dapat berjalan bersamaan dalam sistem FreeRTOS ESP32-S3.

## Cara Menggunakan

Buka folder peripheral yang ingin diuji.

Buka file sketch.ino menggunakan Arduino IDE atau PlatformIO.

Pastikan board:
ESP32S3 Dev Module

Install library yang dibutuhkan:

Adafruit SSD1306

Adafruit GFX

ESP32Servo

AccelStepper

Upload ke ESP32-S3.

Ikuti wiring sesuai gambar wiring.png.

## Tujuan Repository

Menjadi dokumentasi praktis setiap peripheral ESP32-S3.

Referensi untuk pembuatan proyek lebih besar (robotik, IoT, dan sistem real-time).

Latihan memahami multitasking dengan FreeRTOS.
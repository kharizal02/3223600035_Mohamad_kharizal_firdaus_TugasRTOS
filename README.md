# Task -- ESP32-S3 FreeRTOS Peripheral Collection

Repository ini berisi kumpulan tugas implementasi berbagai peripheral
menggunakan ESP32-S3, masing-masing dilengkapi dengan:

-   Kode program (.ino)
-   Video penjelasan (core0 / core1)
-   Diagram wiring

## Struktur Folder

    Task/
    ├── button/
    ├── buzzer/
    ├── LED/
    ├── motor stepper/
    ├── oled/
    ├── potensio/
    ├── rotary/
    ├── servo/
    └── Gabungan semua peripheral/

## Deskripsi

Setiap folder berisi: - sketch.ino - wiring.png - video (core0 / core1)

Folder "Gabungan semua peripheral" berisi proyek integrasi dari seluruh
perangkat.

## Cara Menggunakan

1.  Buka folder peripheral.
2.  Buka `sketch.ino` pada Arduino IDE / PlatformIO.
3.  Pilih board **ESP32S3 Dev Module**.
4.  Install library:
    -   Adafruit SSD1306
    -   Adafruit GFX
    -   ESP32Servo
    -   AccelStepper
5.  Upload dan ikuti wiring.

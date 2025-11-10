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

1.  Buka folder setiap peripheral.
2.  Buka `sketch.ino` pada WOKWI / Arduino IDE / PlatformIO.
3.  Pilih board **ESP32S3 Dev Module**.
4.  Install library:
    -   Adafruit SSD1306
    -   Adafruit GFX
    -   ESP32Servo
    -   AccelStepper
5.  Upload dan ikuti wiring.

## Kesimpulan dari Praktikum RTOS ini dengan ESP32S3

Praktikum ini memberikan pemahaman mendalam mengenai cara kerja FreeRTOS pada platform ESP32-S3, terutama dalam menjalankan beberapa peripheral secara bersamaan. Dari seluruh percobaan, dapat disimpulkan bahwa:

Setiap peripheral (LED, Button, buzzer, servo, OLED, tombol, rotary, stepper) dapat dijalankan pada task yang berbeda tanpa saling mengganggu, selama pengaturan prioritas dan delay dilakukan dengan benar. Pembagian task membuat sistem tetap stabil karena masing-masing perangkat bekerja di thread terpisah yang diatur oleh scheduler FreeRTOS.

Pembagian ini dilakukan menggunakan fungsi:

```
xTaskCreatePinnedToCore(
    taskFunction,     // fungsi task
    "TaskName",       // nama task
    stackSize,        // ukuran stack
    NULL,             // parameter
    priority,         // prioritas task
    NULL,             // handle task
    coreID            // 0 atau 1 untuk menentukan core
);
```

Dengan `xTaskCreatePinnedToCore`, setiap task dapat dikunci pada core tertentu, sehingga tidak berpindah-pindah core. Hal ini membuat waktu eksekusi task lebih konsisten dan sangat penting untuk peripheral yang membutuhkan timing stabil, seperti servo, rotary encoder, dan sensor real-time lainnya.


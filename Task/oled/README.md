# OLED Task with ESP32 (FreeRTOS)

Program ini menampilkan teks dan counter pada OLED 128x64 menggunakan
library **Adafruit SSD1306**, dan dijalankan sebagai task terpisah pada
ESP32 menggunakan **FreeRTOS**.

## Fitur Utama

-   Menggunakan OLED 128x64 (I2C, alamat 0x3C)
-   Menampilkan:
    -   Teks status
    -   Counter yang terus bertambah
    -   Nomor core tempat task berjalan
-   Menggunakan `xTaskCreatePinnedToCore()` untuk menjalankan task di
    core tertentu

## Penjelasan Program

### 1. Inisialisasi OLED

``` cpp
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);
```

OLED menggunakan resolusi **128x64**, komunikasi **I2C**, dan alamat
**0x3C**.

### 2. TaskOLED

Task ini: - Mengecek apakah OLED berhasil di‑inisialisasi\
- Membersihkan layar - Menampilkan teks serta counter - Di‑render
melalui `display.display()` - Delay 500 ms per loop

### 3. Pemilihan Core

Task dapat dijalankan di core 0 atau core 1:

``` cpp
xTaskCreatePinnedToCore(TaskOLED, "OLED", 4096, NULL, 1, NULL, 1);
```

Angka terakhir adalah nomor core.

### 4. Fungsi loop Kosong

Semua pekerjaan dilakukan oleh FreeRTOS task.

## Hardware

-   ESP32 / ESP32‑S3
-   OLED 128x64 I2C (0x3C)
-   Pin default I2C:
    -   SDA → GPIO 8 (ESP32) / konfigurasi S3
    -   SCL → GPIO 9 (ESP32) / konfigurasi S3

## Output yang Ditampilkan di OLED

    Test OLED
    Running Task
    Counter: X
    Core: Y

# Video demo menggunakan core1


https://github.com/user-attachments/assets/b39677b9-4a52-4ff5-8cf1-a33d5c6726a8


# Video demo menggunakan core1



https://github.com/user-attachments/assets/29c90667-7e01-45d0-b2f1-03ce336ec9a0


# ESP32 FreeRTOS Task: Pembacaan Potensiometer

Program ini menggunakan **FreeRTOS Task** pada ESP32 untuk membaca nilai analog dari potensiometer secara terus‑menerus pada core tertentu.

## 📌 Fitur Utama
- Membaca nilai analog dari pin `POT_PIN` (GPIO 1).
- Menampilkan hasil pembacaan ke Serial Monitor.
- Task berjalan di **core 1** (dapat dipilih core 0 jika diperlukan).
- Menggunakan `vTaskDelay()` agar task stabil dan tidak membebani CPU.

## 📁 Penjelasan Kode

### Pin Potensiometer
```cpp
#define POT_PIN 1
```
Potensiometer dihubungkan ke **GPIO 1** sebagai input analog.

### Task Pembacaan Potensiometer
```cpp
void TaskPot(void *pvParameters) {
  while (1) {
    int value = analogRead(POT_PIN);
    Serial.println(value);
    vTaskDelay(100 / portTICK_PERIOD_MS);
  }
}
```
Isi task:
- Melakukan `analogRead()`
- Menampilkan hasil ke serial
- Delay 100 ms untuk stabilitas

### Menjalankan Task
```cpp
xTaskCreatePinnedToCore(TaskPot, "POT", 2048, NULL, 1, NULL, 1);
```
Task dijalankan di **core 1** dengan stack 2048 byte dan priority 1.

## ✅ Cara Penggunaan
1. Sambungkan potensiometer ke pin **GPIO 1** (output wiper).
2. Upload kode ke ESP32/ESP32-S3.
3. Buka Serial Monitor → lihat perubahan nilai saat memutar potensiometer.

# Video Demo Menggunakan core1


https://github.com/user-attachments/assets/cb0b145f-1d4a-4168-8abb-678318dcd3b5


# Video Demo Menggunakan core0


https://github.com/user-attachments/assets/0ae4aa6a-9763-4ff2-8215-a531151bc72f


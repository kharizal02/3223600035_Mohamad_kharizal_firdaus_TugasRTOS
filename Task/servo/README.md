# ESP32 FreeRTOS Task: Servo Control

Program ini menggunakan **FreeRTOS Task** untuk menggerakkan servo pada ESP32 menggunakan library **ESP32Servo**. Servo bergerak otomatis ke tiga posisi: 0°, 90°, dan 180° secara berulang.

## 📌 Fitur Utama
- Menggerakkan servo menggunakan FreeRTOS Task.
- Posisi servo: **0° → 90° → 180°**.
- Berjalan sepenuhnya di **core 1** (bisa dipindah ke core 0).
- Menggunakan PWM servo standar dengan frekuensi **50 Hz**.

---

## 📁 Penjelasan Kode

### Pin Servo
```cpp
#define SERVO_PIN 5
```
Servo dihubungkan ke pin **GPIO 5**.

### Inisialisasi Servo
```cpp
myservo.setPeriodHertz(50);        // Frekuensi servo standar
myservo.attach(SERVO_PIN, 500, 2400);
```

Rentang pulse:
- **500 µs** → 0°
- **2400 µs** → 180°

### Task Servo
```cpp
void TaskServo(void *pvParameters) {
  while (1) {
    myservo.write(0);   vTaskDelay(1000);
    myservo.write(90);  vTaskDelay(1000);
    myservo.write(180); vTaskDelay(1000);
  }
}
```

Servo bergerak setiap **1 detik**.

### Menjalankan Task
```cpp
xTaskCreatePinnedToCore(TaskServo, "SERVO", 4096, NULL, 1, NULL, 1);
```
- Task name: `SERVO`
- Stack: 4096 byte
- Priority: 1
- **Core 1**

---

## ✅ Cara Penggunaan
1. Sambungkan servo:
   - Sinyal → GPIO 5  
   - VCC → 5V  
   - GND → GND  
2. Upload program ke ESP32.
3. Servo akan bergerak otomatis ke tiga posisi.

# Video demo menggunakna core1



https://github.com/user-attachments/assets/cde89a41-2b46-4cec-844e-5ac09b98d368




# Video demo menggunakan core0

https://github.com/user-attachments/assets/bc65283f-29b8-47e8-afc5-0abb5a4ad0d9

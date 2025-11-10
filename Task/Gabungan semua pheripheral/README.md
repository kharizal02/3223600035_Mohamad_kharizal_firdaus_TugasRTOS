# ESP32-S3 Multitasking Project (FreeRTOS)
Proyek ini menunjukkan bagaimana ESP32-S3 menjalankan banyak task secara paralel menggunakan FreeRTOS. Setiap task bertugas mengontrol satu peripheral: LED, buzzer, tombol, potentiometer, OLED, encoder, servo, dan stepper motor.

Semua task dijalankan pada **dua core ESP32-S3**, dibagi rata agar performa tetap optimal.

---

## ✅ Fitur yang Digunakan
### 🔹 Task di Core 0
- LED Blink  
- Button Input  
- OLED Display  
- Servo Motor Control  

### 🔹 Task di Core 1
- Buzzer (manual PWM → agar tidak bentrok dengan servo)  
- Potentiometer Reader  
- Rotary Encoder  
- Stepper Motor  

---

## 📌 Penjelasan Per Task

### 1️⃣ LED Task
Menyalakan/mematikan LED setiap 500 ms menggunakan FreeRTOS delay.

### 2️⃣ Buzzer Task
Menghasilkan bunyi **manual PWM** (~800 Hz) agar tidak konflik dengan library servo (timer berbeda).

### 3️⃣ Button Task
Mendeteksi tombol ditekan menggunakan `INPUT_PULLUP`.

### 4️⃣ Potentiometer Task
Membaca nilai ADC dari pin potensiometer dan menampilkannya ke Serial.

### 5️⃣ OLED Display Task
Menampilkan teks status rutin setiap 500 ms menggunakan library Adafruit SSD1306.

### 6️⃣ Encoder Task
Membaca rotary encoder (CLK + DT) dan menghitung arah putaran (CW/CCW).

### 7️⃣ Servo Task
Menggerakkan servo ke:
- 0°
- 90°
- 180°

Dengan delay masing-masing 1 detik.

### 8️⃣ Stepper Motor Task
Menggerakkan stepper maju–mundur menggunakan AccelStepper:
- Max speed: 800  
- Acceleration: 400  
- Step 800 pulang–pergi  

---

## 🧩 Pembagian Core
Proyek ini mengoptimalkan core sebagai berikut:

### ✅ **Core 0 (I/O & Display)**
- LED  
- Button  
- OLED  
- Servo  

### ✅ **Core 1 (High-Frequency Tasks)**
- Buzzer (butuh timing presisi)
- Potentiometer  
- Encoder  
- Stepper Motor  

---

## 🛠️ Wiring Ringkas

| Peripheral | Pin |
|-----------|-----|
| LED | 2 |
| Buzzer | 4 |
| Button | 15 |
| Potentiometer | ADC1 |
| Servo | 17 |
| Encoder CLK | 18 |
| Encoder DT | 19 |
| Stepper Motor | Pin 13 (STEP), 12 (DIR) |
| OLED | I2C (SDA/SCL) |

---

## 🚀 Cara Menggunakan
1. Hubungkan semua perangkat sesuai tabel wiring.  
2. Upload program ke ESP32-S3.  
3. Serial Monitor akan menampilkan data:
   - Pot value  
   - Encoder count  
   - Button press  
4. OLED akan menampilkan status task.  
5. Servo & stepper berjalan otomatis.  
6. Buzzer berbunyi periodik tanpa memblokir task lain.

---

## ⚠️ Catatan Penting
- Gunakan **power supply eksternal** untuk servo dan stepper.
- Ground harus **shared** dengan ESP32.
- Buzzer menggunakan manual PWM, bukan `tone()`, agar tidak berbenturan dengan servo (timer conflict).
- Setiap task memiliki stack 2048–4096 byte agar stabil.

# Video demo



https://github.com/user-attachments/assets/f70c7051-e9b0-4ec0-b754-e42f77d2bcf7


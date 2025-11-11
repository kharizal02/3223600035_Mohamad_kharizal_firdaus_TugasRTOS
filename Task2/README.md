# **Program Task untuk masing-masing pheripheral **

Dokumentasi ini menjelaskan bagaimana ESP32-S3 menjalankan banyak peripheral secara paralel menggunakan FreeRTOS dual-core, serta analisa mengapa kombinasi task tertentu berjalan normal sedangkan kombinasi lain menyebabkan beberapa peripheral berhenti (stepper, encoder, servo) dan juga ada Video Demo nya diakhir README.
---

# ✅ 1. Deskripsi Project

Project ini menguji seluruh peripheral pada ESP32-S3 secara bersamaan:

* 3 LED
* 2 tombol
* OLED SSD1306
* Servo (PWM)
* Stepper (AccelStepper)
* Encoder
* Potensiometer
* Buzzer (PWM manual)

Semua komponen dijalankan menggunakan **FreeRTOS multitasking** dan dibagi ke 2 core.

---

# ✅ 2. Pembagian Task per Core

## **Core 0**

* LED1
* LED2
* LED3
* Button1
* Button2
* OLED Display

## **Core 1**

* Servo
* Buzzer
* Potensiometer
* Encoder
* Stepper Motor

---

# ✅ 3. Kombinasi yang Berjalan Normal

Pada konfigurasi berikut, **semua peripheral berjalan normal dan stabil**:

```
xTaskCreatePinnedToCore(TaskBuzzer,  "BUZZER", 2048, NULL, 1, NULL, 1);
```

Pada kombinasi ini:
✅ Buzzer diberi **prioritas rendah (1)**
✅ Stepper, encoder, servo, pot tetap mendapat jatah CPU
✅ Semua peripheral normal saat dilihat secara visual

---

# ❌ 4. Kombinasi yang Menyebabkan Peripheral Mati

Masalah terjadi saat Anda mengubah prioritas buzzer:

```
xTaskCreatePinnedToCore(TaskBuzzer,  "BUZZER", 2048, NULL, 10, NULL, 1);
```

Akibatnya:

* ❌ Stepper berhenti
* ❌ Encoder tidak terbaca
* ❌ Servo macet
* ❌ Task Core 1 menjadi tidak responsif

---

# ⚠️ 5. Penyebab Masalah

Ada **dua penyebab utama**:

### ✅ **1. Task Buzzer memakai PWM manual dengan loop berat**

Buzzer dijalankan dengan:

```
for (...) {
  digitalWrite(HIGH);
  delayMicroseconds();
  digitalWrite(LOW);
  delayMicroseconds();
}
```

Ini menyebabkan task:

* Mengunci CPU 100%
* Tidak memberi kesempatan pada task lain (**tidak ada yield**)

### ✅ **2. Prioritas Task = 10 (sangat tinggi)**

Prioritas 10 membuat FreeRTOS:

* Selalu menjalankan buzzer
* Tidak pernah memberi jatah CPU pada stepper, servo, dan encoder

Hasilnya → peripheral lain terlihat “mati”.

---

# ✅ 6. Kesimpulan

* Kombinasi pertama stabil karena prioritas buzzer rendah dan tidak memonopoli CPU.
* Kombinasi kedua gagal karena buzzer menggunakan loop blocking + prioritas tinggi.
* Dalam multitasking FreeRTOS, **prioritas + jenis delay** sangat menentukan stabilitas sistem.


# Video demo core 0 dan core 1 di pakai semua dengan priority task sama semua


https://github.com/user-attachments/assets/5ccd06ca-7a3c-4dcd-94ab-29f9967958b1

# Video demo core 0 dan core 1 di pakai semua dengan priority task buzzer 10 

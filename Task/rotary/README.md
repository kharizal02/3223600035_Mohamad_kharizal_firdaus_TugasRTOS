# ESP32 FreeRTOS Task: Rotary Encoder Reader

Program ini menggunakan **FreeRTOS Task** pada ESP32 untuk membaca nilai rotary encoder (tipe KY-040 atau sejenis) menggunakan dua pin: **CLK** dan **DT**.

## 📌 Fitur Utama
- Membaca putaran rotary encoder secara real-time.
- Menggunakan interrupt-like polling tanpa interrupt hardware.
- Menampilkan nilai putaran ke Serial Monitor.
- Task berjalan di **core 1** (bisa dipindah ke core 0).

## 📁 Penjelasan Kode

### Pin Encoder
```cpp
#define CLK 18
#define DT  19
```
- **CLK** = sinyal utama encoder  
- **DT** = sinyal pembanding untuk arah putaran

Keduanya menggunakan `INPUT_PULLUP` agar stabil.

### Variabel Utama
```cpp
volatile int count = 0;
int lastState;
```
- `count` = nilai posisi encoder  
- `lastState` = untuk memantau perubahan sinyal CLK

### Task Pembacaan Encoder
```cpp
void TaskEncoder(void *pvParameters) {
  pinMode(CLK, INPUT_PULLUP);
  pinMode(DT, INPUT_PULLUP);

  lastState = digitalRead(CLK);

  while (1) {
    int currentState = digitalRead(CLK);

    if (currentState != lastState) {
      if (digitalRead(DT) != currentState) count++;
      else count--;

      Serial.print("Encoder: ");
      Serial.println(count);
    }

    lastState = currentState;
    vTaskDelay(1 / portTICK_PERIOD_MS);
  }
}
```

✅ Logika:  
- Jika **CLK berubah**, berarti encoder diputar.  
- Arah ditentukan dengan membandingkan **DT** dengan **CLK**.

### Menjalankan Task
```cpp
xTaskCreatePinnedToCore(TaskEncoder, "ENC", 2048, NULL, 1, NULL, 1);
```
Task dijalankan pada **core 1**.

## ✅ Cara Penggunaan
1. Hubungkan encoder:  
   - CLK → GPIO 18  
   - DT → GPIO 19  
   - + → 3.3V  
   - GND → GND  
2. Upload kode ke ESP32.  
3. Putar encoder → lihat nilai naik/turun pada Serial Monitor.

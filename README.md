# 16_Buton_Basma_Suresi_Kadar_LED_Yan_Son (Duration to Count)

Bu proje, **STM32F407-Discovery** kartı üzerinde butona kaç saniye basılırsa, LED'in o sayıda yanıp sönmesini (blink) sağlayan bir uygulamadır.

Bu depo, `HAL_GetTick()` ile ölçülen zaman verisinin **işlenerek** (Integer Division / Tamsayı Bölmesi) bir döngü sayacına dönüştürülmesini gösterir.

---

### 🎯 Proje Senaryosu

Sistem şu adımları izler:

1.  **Ölçüm (Recording):**
    * Kullanıcı butona basar.
    * LED yanar (Kayıt başladı işareti).
    * Kullanıcı örneğin **3.8 saniye** (3800 ms) boyunca butona basılı tutar.
2.  **Hesaplama (Processing):**
    * Buton bırakılınca süre hesaplanır: `3800 ms`.
    * Bu süre saniyeye çevrilir: `3800 / 1000 = 3`. (C dilinde tamsayı bölmesi yapıldığı için küsurat atılır).
3.  **Bekleme:**
    * Karışıklığı önlemek için 3 saniye sönük beklenir.
4.  **Eylem (Action):**
    * Hesaplanan sonuç (`3`) kadar döngüye girilir.
    * LED 3 kez, 1'er saniye aralıklarla yanıp söner.

---

### ⚙️ Pull-Up Konfigürasyonu

Projenin düzgün çalışması için `.ioc` dosyasında buton pininin (`PA0`) **Pull-Up** olarak ayarlanması gereklidir.

* **Pin:** `PA0` -> `GPIO_Input`
* **Resistor:** `Pull-up`

<img width="843" height="644" alt="image" src="https://github.com/user-attachments/assets/a5bccc60-b813-4f18-9e9a-a4f0fd3519bf" />
---

### 🛠️ Gerekli Donanım

* **1x** STM32F407-Discovery Geliştirme Kartı
* **1x** LED
* **1x** 220 Ohm Direnç
* **1x** Push-Button
* **Breadboard ve Jumper Kablolar**

---

### 🔌 Devre Şeması

Buton bağlantısı **Pull-Up** mantığına göre (GND'ye) yapılmalıdır.

| Bileşen | STM32 Pini | Bağlantı Detayı |
| :--- | :--- | :--- |
| **Buton** | `PA0` | Bir bacak **PA0**, diğer bacak **GND** |
| **LED** | `PA1` | Anot -> **PA1**, Katot -> Direnç -> **GND** |

<img width="346" height="480" alt="image" src="https://github.com/user-attachments/assets/5b2998e0-3e4e-4f1a-84cc-8264f9fee38a" />

---

### 💻 Kod Bloğu

<img width="1160" height="731" alt="image" src="https://github.com/user-attachments/assets/fc37213a-c636-486b-b5c8-db72c3221ec8" />

---
### 🚀 Nasıl Kullanılır?

1.  Bu depoyu klonlayın (`git clone ...`).
2.  STM32CubeIDE yazılımını açın.
3.  `File > Open Projects from File System...` seçeneği ile proje klasörünü seçin.
4.  Proje içindeki `.ioc` dosyasını açarak pin yapılandırmasını inceleyebilirsiniz.
5.  Derleyin (Build) ve ST-Link V2 üzerinden kartınıza yükleyin (Run).

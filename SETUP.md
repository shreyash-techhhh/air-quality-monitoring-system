#  Project Setup & Configuration Guide
## Air Quality Monitoring System (ESP32 + Blynk)

This file explains **step-by-step setup** of:
- Blynk Cloud
- Mobile Dashboard
- Arduino IDE
- ESP32 Configuration
- Code Customization

Follow steps **in order**. Do not skip.

---

##  Step 1: Blynk Account Setup

1. Install **Blynk IoT App** from Play Store / App Store
2. Open app  Sign up / Login
3. Create a **New Template**

### Template Details
- **Name:** Air Quality
- **Hardware:** ESP32
- **Connection Type:** WiFi

After creation, note down:
- **Template ID**
- **Template Name**
- **Auth Token**

---

##  Step 2: Blynk Template Configuration

### Create Datastreams

Go to **Template  Datastreams  Virtual Pins**

| Virtual Pin | Name | Data Type |
|------------|------|----------|
| V0 | Temperature | Double |
| V1 | Humidity | Double |
| V2 | Air Quality (MQ135) | Integer |
| V3 | Gas Level (MQ2) | Integer |
| V4 | Green LED | Integer |
| V5 | ACK Button | Integer |
| V6 | Alert Cause | String |
| V7 | Red LED | Integer |

Save all datastreams.

---

##  Step 3: Blynk Dashboard Setup (Mobile App)

Add widgets and map them:

### Widgets Required

- **Labeled value (Integer)**  V0  Temperature
- **Labeled value (Integer)**  V1  Humidity
- **Labeled value (Integer)**  V2  MQ135
- **Labeled value (Integer)**  V3  MQ2
- **LED Widget**  V4  Green Status
- **LED Widget**  V7  Red Status
- **Label Value (String)**  V6  Alert Cause
- **Button Widget**  V5  
  - Mode: **Push**
  - ON Value: 255
  - OFF Value: 0

---

##  Step 4: Arduino IDE Setup

### Install Arduino IDE
Download from official Arduino website.

### Add ESP32 Board Support

1. Open **File  Preferences**
2. Add below URL in **Additional Boards Manager URLs**:
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
3. Go to **Tools  Board  Boards Manager**
4. Search `ESP32`
5. Install **esp32 by Espressif Systems**

---

##  Step 5: Install Required Libraries

Go to **Sketch  Include Library  Manage Libraries**

Install:
- **Blynk**
- **DHT sensor library**
- **Adafruit Unified Sensor**

---

##  Step 6: Hardware Connections

| Component | ESP32 Pin |
|--------|-----------|
| DHT11 Data | GPIO 4 |
| MQ135 AO | GPIO 36 |
| MQ2 AO | GPIO 39 |
| Buzzer | GPIO 18 |
| Red LED | GPIO 17 |
| Green LED | GPIO 16 |
| All VCC | 3.3V / 5V |
| All GND | GND |

 Use voltage divider for MQ sensors if required.

---

##  Step 7: Code Configuration

Open the project `.ino` file located in [sketch_feb10a/sketch_feb10a.ino](sketch_feb10a/sketch_feb10a.ino).

### Update Blynk Credentials
```cpp
#define BLYNK_TEMPLATE_ID "YOUR_TEMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "Air Quality"
#define BLYNK_AUTH_TOKEN "YOUR_AUTH_TOKEN"
```

### Update WiFi Credentials
```cpp
char ssid[] = "YOUR_WIFI_NAME";
char pass[] = "YOUR_WIFI_PASSWORD";
```

---

##  Step 8: Threshold Configuration

Change values only if needed for your environment:
```cpp
#define TEMP_THRESHOLD 40
#define MQ135_THRESHOLD 1500
#define MQ2_THRESHOLD 4000
```

---

##  Step 9: Upload Code to ESP32

1. Connect ESP32 via USB
2. Select in Arduino IDE:
   - **Board:** ESP32 Dev Module
   - **Port:** Correct COM Port
3. Click **Upload**
4. Open Serial Monitor (9600 baud)

---

##  Step 10: Testing & Verification

**Normal condition:**
- Green LED ON
- System in safe state

**Danger detected:**
-  Buzzer ON
-  Red LED ON
-  Alert displayed on Blynk dashboard

**Press ACK Button:**
- System waits until readings normalize
- Auto re-arms after safe condition detected

---

##  Offline Mode Behavior

If WiFi connection fails:
- Sensors still work normally
- LEDs & buzzer still function
- Blynk communication disabled automatically
- Re-connects when WiFi is available

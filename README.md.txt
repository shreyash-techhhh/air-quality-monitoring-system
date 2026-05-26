# 🌫️ Air Quality Monitoring System using ESP32 & Blynk

A smart **IoT-based Air Quality Monitoring System** built using **ESP32**, **DHT11**, **MQ135**, **MQ2**, and **Blynk Cloud**.  
System continuously monitors **temperature, humidity, air quality, and gas leakage** and triggers **alerts with latch + acknowledgment logic**.

---

## 🚀 Features

- 📡 **Real-time monitoring** on Blynk dashboard
- 🌡️ Temperature & Humidity monitoring (DHT11)
- 🫁 Air Quality detection (MQ135)
- 🔥 Gas leakage detection (MQ2)
- 🚨 **Alert system with latch mechanism**
- 🛑 **Manual ACK button** (alert won’t re-trigger until readings normalize)
- 🔴🟢 LED status indication
- 🔔 Buzzer alert
- 🌐 Works in **online & offline mode**
- 📊 Serial Monitor debugging support

---

## 🧠 Alert Logic (IMPORTANT)

This system **does NOT spam alerts**.

1. Alert triggers **only once** when threshold is crossed  
2. User must **ACK the alert** from Blynk
3. System waits for **NORMAL sensor readings**
4. Only then the system **re-arms itself**
5. Next alert triggers **only after new danger condition**

👉 This prevents false alerts and continuous buzzing.

---

## 🛠️ Hardware Components

|          Component        |   Quantity  |
|---------------------------|-------------|
|       ESP32 Dev Board     |       1     |
|        DHT11 Sensor       |       1     |
|  MQ135 Air Quality Sensor |       1     |
|       MQ2 Gas Sensor      |       1     |
|           Buzzer          |       1     |
|          Red LED          |       1     |
|         Green LED         |       1     |
|         Resistors         | As required |
|       Jumper Wires        | As required |

## For Blynk Setup and pin configuration, check [SETUP.md](SETUP.md)

## Build and Upload
1. Install Arduino IDE and ESP32 board support.
2. Install libraries: Blynk and DHT sensor library.
3. Open [sketch_feb10a/sketch_feb10a.ino](sketch_feb10a/sketch_feb10a.ino).
4. Update WiFi SSID/password and Blynk auth token.
5. Select the correct board and COM port.
6. Upload and open Serial Monitor at 9600 baud.

## Safety and Notes
- MQ sensors need a warm-up period for stable readings.
- MQ sensor output is analog and can vary by module; recalibrate thresholds for your environment.
- Do not expose MQ sensors to high concentrations for long periods.

## License
MIT
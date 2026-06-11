# IoT Patient Monitoring System (ESP32)

A comprehensive healthcare monitoring solution using two ESP32 microcontrollers. This system tracks vital signs (Heart Rate, SpO2, Body Temperature) and environmental conditions (Room Temperature) in real-time.

## Features
- **Dual-Board Architecture**: Uses ESP-NOW protocol for low-latency, low-power data transfer between a wearable unit and a master hub.
- **Real-time Monitoring**: High-accuracy tracking via MAX30100 and DS18B20 sensors.
- **Triple-Channel Alerting**:
  - **Local Webserver**: View data on any device connected to the same WiFi.
  - **Cloud Sync**: Global access via Firebase Realtime Database.
  - **Telegram Alerts**: Automatic emergency notifications for abnormal vitals.
- **Secure Connection**: Integrated NTP time synchronization for SSL/TLS Firebase communication.

## Hardware Requirements
- **Board A (Wearable)**: ESP32 (30-pin), MAX30100 Pulse Oximeter.
- **Board B (Master Hub)**: ESP32 (38-pin), DHT22 (Room Temp/Hum), DS18B20 (Body Temp).
- **Components**: 2x 4.7kΩ Resistors (for I2C and OneWire pull-ups), Breadboard, Jumper wires.

## Pin Mapping

### Board A (Wearable)
| Sensor | ESP32 Pin |
| :--- | :--- |
| MAX30100 SDA | GPIO 21 |
| MAX30100 SCL | GPIO 22 |

### Board B (Master Hub)
| Sensor | ESP32 Pin | Note |
| :--- | :--- | :--- |
| DHT22 Data | GPIO 27 | Requires 4.7kΩ Pull-up |
| DS18B20 Data | GPIO 33 | Requires 4.7kΩ Pull-up |

##Installation & Setup

1. **Libraries**: Install the following in Arduino IDE:
   - `MAX30100_PulseOximeter`
   - `Firebase ESP32 Client` (by Mobizt)
   - `UniversalTelegramBot`
   - `DHT sensor library`
   - `DallasTemperature` / `OneWire`

2. **MAC Address**: Run the provided MAC Scanner on **Board B**. Copy the address into the `broadcastAddress[]` array in **Board A's** code.

3. **Credentials**: Update the following in the code:
   - `WIFI_SSID` & `WIFI_PASSWORD`
   - `FIREBASE_HOST` & `FIREBASE_AUTH`
   - `BOT_TOKEN` & `CHAT_ID` (from Telegram BotFather)

4. **Firebase Rules**: Set your Realtime Database rules to `true` for initial testing:
   ```json
   {
     "rules": {
       ".read": "true",
       ".write": "true"
     }
   }
   <img width="643" height="468" alt="image" src="https://github.com/user-attachments/assets/9958855c-8994-4899-b369-c23a8c273766" />
   <img width="368" height="818" alt="image" src="https://github.com/user-attachments/assets/891598e1-61cc-4ad4-a866-561705dea629" />
   <img width="580" height="345" alt="image" src="https://github.com/user-attachments/assets/86076dee-e103-480f-b3fa-f076e06b14f7" />
   <img width="680" height="436" alt="image" src="https://github.com/user-attachments/assets/821d2c2c-d832-409f-a186-742873d23768" />
   <img width="541" height="403" alt="image" src="https://github.com/user-attachments/assets/624780ae-7a8a-4c31-aee4-5b9bc3690935" />






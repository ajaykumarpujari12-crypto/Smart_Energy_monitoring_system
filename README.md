# ⚡ Smart Energy Monitoring System using ESP32

<p align="center">
  <img src="https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white" alt="ESP32"/>
  <img src="https://img.shields.io/badge/IoT-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="IoT"/>
  <img src="https://img.shields.io/badge/MQTT-660066?style=for-the-badge&logo=mqtt&logoColor=white" alt="MQTT"/>
  <img src="https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino"/>
</p>

## 📖 Overview

An IoT-based real-time energy monitoring system that tracks power consumption, logs data to the cloud, and enables remote control of electrical loads using MQTT protocol. Built with ESP32 microcontroller and current sensors for accurate power measurement.

## ✨ Features

- ⚡ **Real-time Power Monitoring** - Track voltage, current, and power consumption
- ☁️ **Cloud Data Logging** - Store historical data for analysis
- 📊 **Data Visualization** - View consumption patterns on web dashboard
- 📱 **Remote Control** - Turn devices ON/OFF using MQTT
- 🔔 **Alerts & Notifications** - Get notified of unusual consumption
- 📈 **Energy Analytics** - Daily, weekly, and monthly reports
- 💰 **Cost Calculation** - Estimate electricity bills

## 🛠️ Hardware Components

| Component | Quantity | Purpose |
|-----------|----------|---------|
| ESP32 Development Board | 1 | Main microcontroller |
| ACS712 Current Sensor (30A) | 1 | Measure current flow |
| ZMPT101B Voltage Sensor | 1 | Measure AC voltage |
| 16x2 LCD Display (I2C) | 1 | Local display |
| Relay Module (5V) | 1 | Load control |
| AC Power Socket | 1 | Load connection |
| Breadboard & Jumper Wires | - | Connections |
| 5V Power Supply | 1 | ESP32 power |

## 📐 Circuit Diagram

```
[Add your circuit diagram image here]
```

### Pin Connections

| ESP32 Pin | Component | Connection |
|-----------|-----------|------------|
| GPIO34 | ACS712 | Current sensor output |
| GPIO35 | ZMPT101B | Voltage sensor output |
| GPIO21 | LCD | I2C SDA |
| GPIO22 | LCD | I2C SCL |
| GPIO25 | Relay | Control signal |
| 3.3V | Sensors | VCC |
| GND | All | Ground |

## 💻 Software Requirements

- Arduino IDE 2.x or VS Code with PlatformIO
- ESP32 Board Package
- Required Libraries:
  - `WiFi.h` - WiFi connectivity
  - `PubSubClient.h` - MQTT client
  - `Wire.h` - I2C communication
  - `LiquidCrystal_I2C.h` - LCD display
  - `ArduinoJson.h` - JSON parsing

## 📦 Installation

### 1. Arduino IDE Setup

```bash
# Install ESP32 Board
# Tools → Board → Boards Manager → Search "ESP32" → Install
```

### 2. Install Libraries

```bash
# Sketch → Include Library → Manage Libraries
# Search and install:
# - PubSubClient by Nick O'Leary
# - ArduinoJson by Benoit Blanchon
# - LiquidCrystal I2C by Frank de Brabander
```

### 3. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/smart-energy-monitoring-system.git
cd smart-energy-monitoring-system
```

### 4. Configure WiFi & MQTT

Open `src/config.h` and update:

```cpp
// WiFi Credentials
#define WIFI_SSID "Your_WiFi_Name"
#define WIFI_PASSWORD "Your_WiFi_Password"

// MQTT Broker
#define MQTT_BROKER "broker.hivemq.com"
#define MQTT_PORT 1883
#define MQTT_TOPIC_POWER "home/energy/power"
#define MQTT_TOPIC_CONTROL "home/energy/control"
```

### 5. Upload Code

1. Connect ESP32 via USB
2. Select Board: `ESP32 Dev Module`
3. Select Port: `COM X` (Windows) or `/dev/ttyUSB0` (Linux)
4. Click Upload ⬆️

## 🚀 Usage

### Power Monitoring

1. Connect the device between AC source and load
2. ESP32 connects to WiFi automatically
3. Power data updates every 5 seconds
4. View readings on LCD display

### Remote Control

Send MQTT message to control relay:

```json
{
  "device": "relay1",
  "state": "ON"
}
```

Or use MQTT client app (like MQTT Dash):
- Topic: `home/energy/control`
- Payload: `ON` or `OFF`

### Cloud Dashboard

Access the web dashboard to view:
- Real-time power consumption
- Historical data graphs
- Energy cost estimation
- Device status

## 📊 Data Format

### Published Data (MQTT)

```json
{
  "voltage": 230.5,
  "current": 2.45,
  "power": 564.7,
  "energy": 12.5,
  "cost": 0.15,
  "timestamp": 1645789123
}
```

## 🔧 Calibration

### Current Sensor (ACS712)

1. Remove all loads
2. Note zero-current reading
3. Update offset in code:
   ```cpp
   #define CURRENT_OFFSET 2.5  // Adjust based on reading
   ```

### Voltage Sensor (ZMPT101B)

1. Measure actual AC voltage with multimeter
2. Compare with sensor reading
3. Adjust calibration factor:
   ```cpp
   #define VOLTAGE_CALIBRATION 1.02  // Adjust based on error
   ```

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| ESP32 not connecting to WiFi | Check SSID/password, ensure 2.4GHz WiFi |
| Incorrect power readings | Calibrate sensors, check connections |
| MQTT not publishing | Verify broker address and port |
| LCD shows garbage | Check I2C address (0x27 or 0x3F) |
| Relay not switching | Check GPIO pin and relay module voltage |

## 📈 Future Enhancements

- [ ] Add multiple sensor support for different appliances
- [ ] Implement machine learning for load prediction
- [ ] Create mobile app for Android/iOS
- [ ] Add battery backup for data logging
- [ ] Integrate with Alexa/Google Home
- [ ] PCB design for compact form factor
- [ ] Solar panel monitoring support

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


## 👤 Author

**Ajay Kumar Pujari**
- Email: ajaykumarpujari22@gmail.com
- GitHub: [ajaykumarpujari12-svg](https://github.com/ajaykumarpujari12-svg)


## 🙏 Acknowledgments

- ESP32 community for excellent documentation
- MQTT protocol for IoT communication
- Open-source libraries used in this project



---

⭐ If you found this project helpful, please give it a star!

**Tags:** `esp32` `iot` `energy-monitoring` `mqtt` `arduino` `smart-home` `embedded-systems` `power-meter`

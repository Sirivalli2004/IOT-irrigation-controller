# IOT-irrigation-controller
Smart IoT-based irrigation controller using NodeMCU &amp; Blynk app | Monitors soil moisture and automates watering
# 💧 IoT-Based Smart Irrigation Controller

> 🎓 **Mini Project – ENIR11: Energy and Environment Laboratory**  
> 🏫 Department of Electronics and Communication Engineering  
> 🏛️ National Institute of Technology, Tiruchirappalli  
> 👨‍🏫 Guided by: **Mr. Kannan**, Department of Energy and Environment

---

## 📌 Project Overview

This project presents the design and implementation of an **IoT-enabled smart irrigation controller** using **NodeMCU ESP8266**, a **capacitive soil moisture sensor**, and a **relay-driven water pump**. The system enables users to monitor real-time soil moisture data and control watering remotely via the **Blynk IoT platform**.

The solution addresses key challenges in home gardening and small-scale agriculture:
- ✅ Overwatering or underwatering
- ✅ Inability to monitor plant health remotely
- ✅ Inefficient and manual irrigation systems

---

## 👥 Team Members

| Name              | Roll No     |
|------------------|-------------|
| Ananya S         | 108122013   |
| Elencheran M.P   | 108122033   |
| R. Pavithra      | 108122093   |
| S. Rakshana      | 108122117   |
| Rupika S         | 108122095   |
| Sruthi Kurra     | 108122047   |
| Thandu Sirivalli | 108122125   |
| Varun Karthick A | 108122133   |

---

## 🧩 System Architecture

### Core Components
- 🔌 **NodeMCU ESP8266** – Microcontroller with Wi-Fi
- 🌱 **Capacitive Soil Moisture Sensor** – Real-time soil monitoring
- ⚙️ **Relay Module** – Switches pump ON/OFF
- 💦 **Mini Water Pump** – Waters the plants
- 🔋 **Battery Source** – Portable power
- 📱 **Blynk App** – User interface for control and monitoring

---

## 🔧 Features and Functionality

- 📡 Real-time moisture monitoring via smartphone
- 🕹️ Remote control of irrigation system
- 🧠 Smart logic to automate watering based on moisture level
- 🔄 Fully automated operation; no manual toggling required
- 🌍 Sustainable and scalable for multi-plant systems

---

## 💻 System Workflow

1. Soil moisture is measured by the sensor and read by NodeMCU.
2. Moisture level is transmitted to the Blynk app over Wi-Fi.
3. Based on threshold, the user can remotely activate the pump.
4. The relay module controls the power to the water pump.
5. The system can be automated or manually triggered via the app.

---

## 📲 Mobile App Integration

- Blynk Dashboard:
  - 🌡️ Displays current moisture level (0–100%)
  - 🔘 Toggle to control the water pump
- Virtual Pins Used:
  - `V0`: Moisture sensor display
  - `V1`: Pump control button
- Data is updated every 100ms using BlynkTimer

---

## 🧠 Sample Arduino Code (ESP8266 + Blynk)

```cpp
#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char auth[] = "Your_Blynk_Auth_Token";
char ssid[] = "Your_WiFi_Name";
char pass[] = "Your_WiFi_Password";

#define sensor A0
#define waterPump D3

BlynkTimer timer;
bool Relay = 0;

void setup() {
  Serial.begin(9600);
  pinMode(waterPump, OUTPUT);
  digitalWrite(waterPump, HIGH);
  Blynk.begin(auth, ssid, pass, "blynk.cloud", 80);
  timer.setInterval(100L, soilMoistureSensor);
}

BLYNK_WRITE(V1) {
  Relay = param.asInt();
  digitalWrite(waterPump, Relay ? LOW : HIGH);
}

void soilMoistureSensor() {
  int value = analogRead(sensor);
  value = map(value, 0, 1024, 0, 100);
  value = (value - 100) * -1;
  Blynk.virtualWrite(V0, value);
}

void loop() {
  Blynk.run();
  timer.run();
}


------
📂 Project Deliverables
✅ ENIR11 Final SEM1 Project.docx – Complete documentation

✅ Arduino code (ESP8266 + Blynk)

✅ System architecture and component list

✅ Blynk interface configuration

✅ Testing results and observations

🌍 Future Improvements
Area	Enhancement Suggestion
🔔 Notifications	Push alerts when pump is turned ON/OFF
☀️ Power Efficiency	Add solar panel for off-grid operation
🌐 Connectivity	Upgrade to GSM/LTE module for non-Wi-Fi areas
📦 Product Design	Compact enclosure using 3D-printed casing
🌾 Multi-Zone Expansion	Support for multiple plants with individual sensors

✅ Project Outcomes
Successfully developed a cost-effective smart irrigation system

Demonstrated real-time monitoring and remote control

Integrated hardware + cloud app into a fully functional product

Promoted sustainable water usage in household agriculture

Applied IoT concepts in a real-world energy/environment project

📬 Contact
Thandu Sirivalli
🔗 LinkedIn
📧 sirivallithandu@gmail.com

🌱 “Smart agriculture begins with smarter water management. This project aims to bring sustainability to every drop.”

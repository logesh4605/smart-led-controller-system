# smart-led-controller-system
# 💡 Smart LED Control Using ESP32 & Blynk

A simple IoT-based **Smart LED Control System** that allows an LED connected to an ESP32 to be controlled remotely using the **Blynk mobile/web dashboard**.

The project is developed and tested using **Wokwi ESP32 simulation**, making it possible to verify the IoT communication and control logic without physical hardware.

---

## 📌 Project Overview

The system uses an ESP32 as the IoT controller. The ESP32 connects to the internet through Wi-Fi and communicates with the Blynk Cloud platform.

A switch on the Blynk dashboard sends an ON/OFF command to the ESP32. The ESP32 receives the command through a virtual datastream and controls an LED through GPIO.

### Working Flow

```text
Blynk Mobile/Web Dashboard
            ↓
       Blynk Cloud
            ↓
          Wi-Fi
            ↓
          ESP32
            ↓
         GPIO 2
            ↓
           LED
```

---

## 🚀 Features

* Remote LED ON/OFF control
* ESP32-based IoT implementation
* Blynk Cloud connectivity
* Mobile and Web Dashboard control
* Virtual Pin communication using `V0`
* GPIO-based LED control
* Wi-Fi connectivity
* Wokwi-based simulation
* No physical hardware required for simulation

---

## 🛠️ Components Required

### Hardware

| Component     |    Quantity |
| ------------- | ----------: |
| ESP32 DevKit  |           1 |
| LED           |           1 |
| 220Ω Resistor |           1 |
| Jumper Wires  | As required |

### Software / Platforms

* Wokwi
* Blynk IoT
* Arduino/C++
* ESP32 Arduino Core

---

## 🔌 Circuit Connections

The LED is connected to **GPIO 2** of the ESP32 through a 220Ω current-limiting resistor.

```text
ESP32 GPIO 2
      │
     220Ω
      │
     LED
      │
     GND
```

### Connection Table

| ESP32  | LED Circuit                     |
| ------ | ------------------------------- |
| GPIO 2 | LED Anode through 220Ω resistor |
| GND    | LED Cathode                     |

---

## ☁️ Blynk Configuration

The project uses Blynk IoT for remote control.

### Datastream

| Parameter   | Value       |
| ----------- | ----------- |
| Datastream  | LED Control |
| Virtual Pin | V0          |
| Data Type   | Integer     |
| Minimum     | 0           |
| Maximum     | 1           |

### Control Logic

```text
V0 = 1 → LED ON
V0 = 0 → LED OFF
```

The ESP32 receives the Blynk command using:

```cpp
BLYNK_WRITE(V0)
```

---

## 📱 Dashboard

The project can be controlled using:

* Blynk Web Dashboard
* Blynk Mobile App

### Control Flow

```text
User presses ON
       ↓
Blynk Dashboard
       ↓
Blynk Cloud
       ↓
ESP32
       ↓
GPIO 2 = HIGH
       ↓
LED ON
```

For OFF:

```text
User presses OFF
       ↓
Blynk Dashboard
       ↓
Blynk Cloud
       ↓
ESP32
       ↓
GPIO 2 = LOW
       ↓
LED OFF
```

---

## 💻 Source Code

```cpp
#define BLYNK_TEMPLATE_ID "YOUR_TEMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "Smart LED"
#define BLYNK_AUTH_TOKEN "YOUR_AUTH_TOKEN"

#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

char ssid[] = "Wokwi-GUEST";
char pass[] = "";

#define LED_PIN 2

BLYNK_WRITE(V0)
{
  int value = param.asInt();

  if (value == 1) {
    digitalWrite(LED_PIN, HIGH);
  }
  else {
    digitalWrite(LED_PIN, LOW);
  }
}

void setup()
{
  Serial.begin(115200);

  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, LOW);

  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
}

void loop()
{
  Blynk.run();
}
```

> **Security:** Never upload your real `BLYNK_AUTH_TOKEN` to GitHub. Replace it with a placeholder before committing your code.

---

## 🧪 Simulation

The project was simulated using **Wokwi**.

### Simulation Environment

```text
Microcontroller : ESP32
Simulation      : Wokwi
Network         : Wokwi-GUEST
Cloud Platform  : Blynk
LED GPIO        : GPIO 2
Blynk Datastream: V0
```

Wokwi provides a simulated Wi-Fi network that allows the ESP32 simulation to communicate with internet-connected services.

---

## 📊 Expected Result

When the Blynk switch is turned **ON**:

```text
Blynk V0 = 1
      ↓
ESP32 GPIO 2 = HIGH
      ↓
LED ON
```

When the switch is turned **OFF**:

```text
Blynk V0 = 0
      ↓
ESP32 GPIO 2 = LOW
      ↓
LED OFF
```

---

## 🎯 Learning Outcomes

Through this project, I gained practical experience with:

* ESP32 programming
* GPIO control
* Wi-Fi connectivity
* IoT architecture
* Blynk Cloud
* Virtual Datastreams
* Mobile/Web IoT dashboards
* Wokwi simulation
* Cloud-to-device communication

---

## 🔮 Future Improvements

The basic project can be extended with:

* Automatic LED scheduling
* LDR-based automatic lighting
* PIR-based motion detection
* Multiple LED/device control
* Energy monitoring
* Device status monitoring
* Sensor-based automation
* Firebase/database integration
* Real ESP32 hardware deployment

---

## 📁 Project Structure

```text
Smart-LED-Control/
│
├── README.md
├── sketch.ino
├── diagram.json
└── libraries.txt
```

---

## 🔐 Security Note

Do not commit sensitive credentials such as:

```text
BLYNK_AUTH_TOKEN
Wi-Fi passwords
API keys
```

For GitHub, use placeholders:

```cpp
#define BLYNK_TEMPLATE_ID "YOUR_TEMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "Smart LED"
#define BLYNK_AUTH_TOKEN "YOUR_AUTH_TOKEN"
```

For a real deployment, credentials should be stored securely rather than hard-coded in a public repository.

---

## 👨‍💻 Project Status

**Status:** Completed – Wokwi Simulation

The current version successfully demonstrates remote LED control through the Blynk IoT platform using an ESP32 simulation.

---

## 📜 License

This project is intended for educational and learning purposes.

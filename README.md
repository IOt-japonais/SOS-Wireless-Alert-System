Good catch. Since **Google Apps Script is a key part of the architecture**, it should have its own section in the repository description.

You can use this revised version:

# SOS Wireless Alert System (ATtiny85 + nRF24L01 + ESP32 + Google Apps Script + Firebase)

A complete wireless SOS alert system that combines low-power embedded hardware, Wi-Fi connectivity, cloud services, and Android push notifications.

## System Architecture

```text
[SOS Button]
      │
      ▼
[ATtiny85 + nRF24L01]
      │ Wireless RF
      ▼
[ESP32 + nRF24L01]
      │ Wi-Fi
      ▼
[Google Apps Script]
      │
      ▼
[Firebase Cloud Messaging]
      │
      ▼
[Android Application]
```

## Project Components

### 1. Sender Node

Hardware:

* ATtiny85
* nRF24L01+
* Push button

Responsibilities:

* Monitor the SOS button.
* Require three button presses before triggering an alert.
* Transmit the SOS message wirelessly via nRF24L01.

---

### 2. Receiver Node

Hardware:

* ESP32
* nRF24L01+
* SSD1306 OLED display

Responsibilities:

* Receive wireless SOS messages.
* Display system status on the OLED screen.
* Connect to Wi-Fi using WiFiManager.
* Send SOS requests to Google Apps Script.

---

### 3. Google Apps Script

Responsibilities:

* Receive HTTPS requests from the ESP32.
* Act as a secure bridge between the ESP32 and Firebase Cloud Messaging.
* Forward SOS notifications to Android devices.

Why use Google Apps Script?

Firebase Cloud Messaging no longer provides the legacy server key workflow used by many older ESP32 examples. Google Apps Script offers a simple cloud-based solution that allows the ESP32 to trigger notifications without exposing sensitive Firebase credentials on the device.

---

### 4. Android Application

Responsibilities:

* Register with Firebase Cloud Messaging.
* Display the device token.
* Receive SOS push notifications.
* Alert the user when an SOS message is received.

## Features

* Low-cost hardware design
* Wireless communication using nRF24L01
* Triple-press confirmation to prevent accidental alerts
* OLED status display
* WiFiManager support for easy Wi-Fi setup
* Cloud-based notification delivery
* Firebase Cloud Messaging integration
* Android push notifications
* Easy to customize and extend

## Repository Structure

```text
/
├── Sender/
│   └── ATtiny85 firmware
│
├── Receiver/
│   └── ESP32 firmware
│
├── GoogleAppsScript/
│   └── Web App source code
│
├── AndroidApp/
│   └── Android Studio project
│
└── README.md
```

## Required Hardware

### Sender

* ATtiny85
* nRF24L01+
* Push button

### Receiver

* ESP32
* nRF24L01+
* SSD1306 OLED Display

## Required Services

* Google Apps Script
* Firebase Project
* Firebase Cloud Messaging (FCM)

## How It Works

1. User presses the SOS button three times.
2. ATtiny85 transmits an SOS packet via nRF24L01.
3. ESP32 receives the packet.
4. ESP32 sends an HTTPS request to Google Apps Script.
5. Google Apps Script forwards the notification to Firebase Cloud Messaging.
6. Firebase delivers the notification to the Android application.
7. The user receives the SOS alert on their phone.

## Disclaimer

This project is intended for educational, research, and prototyping purposes. It should not be considered a substitute for certified emergency response or life-critical alert systems.

## License

Feel free to use, modify, and adapt this project for your own applications. Contributions and improvements are welcome. ⭐

# Tag Reader – RFID-Based Smart Fitting Room System

**Final-Year Capstone Project – Izmir University of Economics**  
**3rd Place Winner – Genç Beyinler Yeni Fikirler 2025, Industry & Agriculture Category**

**Authors:** Mert Çakı, Onur Yağcı  
**Supervisor:** Prof. Dr. Yusuf Murat Erten  

---

## Project Overview

Tag Reader is an IoT-based smart fitting room and inventory support system developed for textile and retail environments. The system reads RFID-tagged garments inside a fitting room and displays product information such as item name, size, color, and stock availability on a dedicated TFT screen in real time.

The project was designed as a modular and low-cost prototype that combines embedded systems, RFID technology, wireless communication, backend processing, and database-driven product lookup. It aims to reduce customer uncertainty during try-ons, improve in-store product visibility, and support more efficient retail operations.

---

## Motivation

The idea was inspired by real retail and automation-oriented use cases observed during internship experience in an RFID/IoT environment. Textile retailers often require fast product identification, stock visibility, and smoother interaction between customers and store personnel. This project explores how RFID, ESP32-based embedded devices, message queues, and a lightweight backend can be combined to create a scalable smart fitting room prototype.

---

## System Architecture

```text
RFID Tag
   ↓
MFRC522 RFID Reader
   ↓
ESP32 Reader Node
   ↓ MQTT
RabbitMQ Message Broker
   ↓
Python Backend Server
   ↓
SQLite Database Query
   ↓ MQTT / Routing
ESP32 Display Node
   ↓
TFT Screen in Fitting Room
```

The system consists of two ESP32-based modules per fitting room:

1. **RFID Reader Node**  
   Reads garment RFID tags using an MFRC522 RFID module and publishes tag data to RabbitMQ via MQTT.

2. **Display Node**  
   Receives product information from the backend and displays item details on a TFT screen.

A Python backend processes incoming RFID events, queries the SQLite database, and routes the correct product information to the related fitting-room display.

---

## Technologies Used

| Layer | Technologies |
|---|---|
| Hardware | ESP32 WROOM, ESP32-2432S028 TFT Display, MFRC522 RFID Reader |
| Firmware | C++, PlatformIO, PubSubClient |
| Backend | Python 3, Pika, SQLite3 |
| Messaging | MQTT, RabbitMQ, AMQP routing |
| Communication | 2.4 GHz Wi-Fi |
| Database | SQLite |
| Documentation | Final report, poster, GitHub repository |

---

## Key Features

- Real-time RFID-based garment identification
- ESP32-based reader and display modules
- MQTT-based lightweight communication
- RabbitMQ message routing
- Python backend for RFID event processing
- SQLite database for product information and stock data
- Cabin-specific routing for multi-fitting-room scenarios
- Modular and low-cost architecture
- Suitable baseline for smart retail and inventory tracking applications

---

## My Individual Contribution

This project was completed as a group final-year capstone project. My individual contribution focused mainly on the technical integration between embedded devices and backend components.

I contributed to the ESP32-based RFID reader and display-side implementation, supported the physical setup and testing of the reader/display units, and worked on the Python/SQLite backend for RFID event logging, product queries, stock data handling, and database matching logic. I also contributed to the RabbitMQ/MQTT topic and queue configuration, routing logic, and data processing flow so that tag events from the ESP32 reader could be routed to the correct fitting-room display in real time.

The project idea was also influenced by my internship experience in an RFID/automation-oriented environment, where I observed retail and textile-related stock tracking and operational efficiency use cases. In addition to technical implementation, I participated in system testing, troubleshooting, documentation, GitHub preparation, and presentation materials for the final prototype.

---

## Results

The prototype was tested with multiple RFID-tagged garments registered in the SQLite database. When a tag was scanned, the system successfully retrieved and displayed the corresponding product name, size, color, and stock information on the TFT display.

The average response time between RFID scanning and product display was measured below **700 ms** in the test setup, demonstrating near real-time interaction and stable message routing.

The system also showed successful cabin-specific message isolation using MQTT topic routing, preventing data from one fitting room from being displayed in another.

---

## Challenges and Solutions

| Challenge | Solution |
|---|---|
| PAHO MQTT compatibility problems in C++ | Backend was moved to Python with Pika for more stable development |
| ESP32 MQTT / RabbitMQ AMQP protocol mismatch | RabbitMQ exchange and routing configuration was adjusted |
| Multi-cabin message interference | Cabin-specific MQTT topic routing was implemented |
| Repeated RFID scans | Duplicate scan suppression logic was added |
| TFT display character issues | Character conversion and display formatting were adjusted |

---

## Folder Structure

```text
GraduationProject_TagReader/
├── Backend/
│   └── rabbitmq_DataBaseQuerryApp/
├── Firmware/
│   ├── RabbitToScreen/
│   ├── RF-ID Writer/
│   └── TagReader_RabbitMQConnectionforEsp/
├── Docs/
│   └── poster.pdf
└── README.md
```

---

## How to Run

### 1. Backend Server

Navigate to the backend folder:

```bash
cd Backend/rabbitmq_DataBaseQuerryApp
python main.py
```

The backend receives RFID events, queries the SQLite database, and publishes product information to the appropriate display topic.

### 2. ESP32 Firmware

Upload the relevant firmware folders using PlatformIO:

- `TagReader_RabbitMQConnectionforEsp` for the RFID reader node
- `RabbitToScreen` for the TFT display node

### 3. RabbitMQ

Make sure RabbitMQ is running and MQTT support is enabled.

RabbitMQ is used as the message broker for routing RFID events and product information between the ESP32 devices and backend server.

RabbitMQ documentation: https://www.rabbitmq.com/

---

## Future Improvements

- PostgreSQL or another scalable database for larger retail deployments
- Cloud-based inventory integration
- OTA firmware updates for ESP32 devices
- Touchscreen-based customer requests
- AI-based product recommendation or stock analytics
- Enhanced security, authentication, and encrypted message routing
- BLE or NFC support for broader tag compatibility

---

## Project Relevance

This project combines computer engineering topics such as embedded systems, computer networks, backend development, databases, message-oriented middleware, and real-time system integration. It demonstrates how software, hardware, communication protocols, and physical retail processes can be integrated into a working cyber-physical prototype.

---

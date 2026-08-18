# 🚗 CAN Bus Communication using LPC1768

A practical implementation of the **Controller Area Network (CAN) protocol** using the **NXP LPC1768 microcontroller** and **MCP2551 CAN transceiver**.

This project demonstrates real-time CAN communication between a transmitter and receiver node, including CAN message transmission, reception, serial monitoring, and LED-based status indication.

---

## 📌 Project Overview

**Controller Area Network (CAN)** is a robust communication protocol widely used in automotive and industrial embedded systems.

This project implements a basic two-node CAN network using LPC1768 development boards:

```text
                 CAN BUS
        ┌─────────────────────────┐
        │                         │
        │       CAN_H / CAN_L     │
        │                         │
        ▼                         ▼
┌───────────────┐         ┌───────────────┐
│ LPC1768       │         │ LPC1768       │
│ Transmitter   │         │ Receiver      │
│               │         │               │
│ CAN Controller│         │ CAN Controller│
└───────┬───────┘         └───────┬───────┘
        │                         │
        ▼                         ▼
   MCP2551 TX/RX             MCP2551 TX/RX
        │                         │
        └──────── CAN BUS ────────┘
```

The transmitter periodically sends a CAN message, while the receiver listens for incoming messages and indicates successful reception through onboard LEDs.

---

## ✨ Features

* CAN communication using LPC1768
* MCP2551 CAN transceiver interface
* Dedicated transmitter and receiver firmware
* Periodic CAN message transmission
* CAN message reception and processing
* CAN message ID configuration
* Incrementing message data
* LED-based transmission/reception indication
* Serial debugging using Tera Term
* Precompiled `.bin` firmware files
* Hardware circuit diagram included
* Suitable for learning automotive CAN communication

---

## 🧰 Hardware Requirements

| Component                  |    Quantity | Purpose                              |
| -------------------------- | ----------: | ------------------------------------ |
| LPC1768 Development Board  |           2 | CAN transmitter and receiver         |
| MCP2551 CAN Transceiver    |           2 | CAN physical-layer interface         |
| CAN Bus Wiring             |       1 set | CAN_H and CAN_L connection           |
| USB Cable                  |           2 | Programming and serial communication |
| LEDs                       | 4 per board | CAN activity indication              |
| 120 Ω Termination Resistor | As required | CAN bus termination                  |

> **Note:** CAN networks normally require appropriate termination at the two physical ends of the bus.

---

## 💻 Software Requirements

* **Keil Studio Cloud / Mbed environment**
* **C/C++**
* **Tera Term**
* LPC1768 USB/serial driver

The repository also includes the required precompiled firmware binaries.

---

## 🔌 Hardware Configuration

The project uses the LPC1768 CAN interface with the following pins:

| LPC1768 Pin | Function |
| ----------- | -------- |
| P30         | CAN RX   |
| P29         | CAN TX   |

The LPC1768 CAN controller interfaces with the **MCP2551**, which provides the physical CAN bus interface.

### CAN Bus

```text
LPC1768 TX ──► MCP2551 ──► CAN_H / CAN_L
                              │
                              │ CAN BUS
                              │
LPC1768 RX ◄── MCP2551 ◄──────┘
```

Refer to the included circuit diagram for the complete hardware connections.

---

## 📡 CAN Message Configuration

The transmitter sends a CAN message with:

```text
CAN ID   : 1337
Data     : 1 byte
Payload  : Counter value
Period   : 1 second
```

The counter is incremented after each successfully transmitted message.

For example:

```text
CAN ID: 1337
Data:   0

CAN ID: 1337
Data:   1

CAN ID: 1337
Data:   2

CAN ID: 1337
Data:   3
...
```

This provides a simple way to verify that messages are being transmitted continuously and received correctly.

---

## 📤 CAN Transmitter

The transmitter periodically generates a CAN message using an Mbed `Ticker`.

The basic sequence is:

```text
Initialize CAN
      │
      ▼
Initialize Timer
      │
      ▼
Wait for 1 second
      │
      ▼
Set Send Flag
      │
      ▼
Transmit CAN Message
      │
      ▼
Increment Counter
      │
      ▼
Repeat
```

The transmitter uses CAN ID **1337** and sends the counter value as a one-byte payload.

---

## 📥 CAN Receiver

The receiver continuously checks the CAN interface for incoming messages.

```text
Initialize CAN
      │
      ▼
Wait for CAN Message
      │
      ▼
Message Received?
   ┌──┴──┐
   │     │
  No    Yes
   │     │
   │     ▼
   │  Read Data
   │     │
   │     ▼
   │  Toggle LEDs
   │     │
   └─────┘
      │
      ▼
    Repeat
```

When a message is successfully received:

* The received data is printed through the serial interface.
* The onboard LEDs are toggled to indicate CAN activity.

---

## 💡 LED Indication

The project uses the LPC1768 onboard LEDs as a simple visual indication of CAN activity.

### Transmitter

LEDs toggle when the transmission timer triggers.

### Receiver

LEDs toggle whenever a valid CAN message is received.

This makes it possible to verify basic CAN communication without requiring additional display hardware.

---

## 🖥️ Serial Monitoring

The firmware uses serial output for debugging and monitoring.

A terminal application such as **Tera Term** can be used to observe messages.

Example transmitter output:

```text
main()
loop()
send()
wloop()
Message sent: 1
loop()
send()
wloop()
Message sent: 2
```

Example receiver output:

```text
main()
loop()
Message received: 1
loop()
Message received: 2
```

The exact output depends on the firmware execution and serial configuration.

---

## 📂 Repository Structure

```text
CAN-BUS-Protocol-LPC1768/
│
├── Bin Files/
│   ├── CAN_Receiver_.LPC1768.bin
│   └── CAN_Transmitter.LPC1768.bin
│
├── Codes/
│   ├── CAN Receiver.txt
│   └── CAN Transmitter.txt
│
├── CAN LPC1768 Circuit Diagram.png
│
├── lpc1768_pinout.png
│
├── mbedWinSerial_16466 - USB Driver.exe
│
├── teraterm-4.105.exe
│
└── README.md
```

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Amey-Chougule/CAN-BUS-Protocol-LPC1768.git
```

```bash
cd CAN-BUS-Protocol-LPC1768
```

### 2. Build the Hardware

Connect the LPC1768 boards to the MCP2551 transceivers according to the provided circuit diagram.

Connect:

```text
CAN_H ───────── CAN_H
CAN_L ───────── CAN_L
GND   ───────── GND
```

Ensure proper CAN bus termination.

### 3. Program the LPC1768

The repository contains precompiled firmware:

```text
Bin Files/
├── CAN_Transmitter.LPC1768.bin
└── CAN_Receiver_.LPC1768.bin
```

Program one LPC1768 as the transmitter and the other as the receiver.

### 4. Monitor Serial Output

Connect the LPC1768 board to the computer and open **Tera Term**.

Configure the appropriate COM port and serial parameters according to the firmware setup.

### 5. Verify CAN Communication

The transmitter should periodically send CAN messages.

The receiver should:

* Detect the incoming CAN message.
* Print the received data.
* Toggle the onboard LEDs.

---

## 🔬 Technical Concepts Demonstrated

This project provides hands-on experience with:

* Controller Area Network (CAN)
* CAN controllers
* CAN transceivers
* CAN message IDs
* CAN data frames
* Embedded C/C++
* LPC1768 microcontroller
* Mbed APIs
* Interrupt-driven timing
* Serial debugging
* Embedded hardware interfacing
* Automotive communication protocols

---

## 🚗 Applications

CAN communication is commonly used in:

* Engine Control Units (ECUs)
* Anti-lock Braking Systems (ABS)
* Airbag systems
* Body Control Modules
* Instrument clusters
* Battery Management Systems (BMS)
* Electric Vehicles
* Automotive diagnostics
* Industrial automation
* Robotics
* Embedded control systems

---

## 🔮 Possible Improvements

The current project provides a basic point-to-point CAN communication demonstration. It can be extended with:

* Multiple CAN nodes
* CAN message filtering
* Multiple CAN IDs
* Standard and extended CAN identifiers
* CAN error handling
* Bus-off detection
* CAN acknowledgement monitoring
* CAN bus load analysis
* CAN-based sensor communication
* CAN diagnostics
* UDS implementation
* CANopen implementation
* Automotive ECU-to-ECU communication
* Integration with an OBD-II interface

---

## 📚 Learning Outcomes

After completing this project, you can understand the complete basic communication path:

```text
Application Data
       │
       ▼
LPC1768 CAN Controller
       │
       ▼
MCP2551 CAN Transceiver
       │
       ▼
CAN_H / CAN_L Bus
       │
       ▼
MCP2551 CAN Transceiver
       │
       ▼
LPC1768 CAN Controller
       │
       ▼
Received Application Data
```

This makes the project a useful starting point for learning **automotive embedded systems and CAN-based ECU communication**.

---

## 📜 License

This project is intended for **educational, learning, and research purposes**.

Please ensure that any third-party software, drivers, libraries, or tools included in the repository are used according to their respective licenses.

---

## ⭐ Support

If this project helped you understand **CAN communication with LPC1768**, consider giving the repository a ⭐ on GitHub.

# **CAN BUS Protocol Implementation with LPC1768**

## Description
This project demonstrates the implementation of the CAN (Controller Area Network) protocol using the mbed LPC1768 microcontroller and MCP2551 transceiver. The project focuses on real-time communication between a transmitter and receiver, making it ideal for understanding the backbone of modern automotive electronics.

## **Features**
Transmitter and receiver code for seamless CAN communication.
Real-time monitoring of messages using TeraTerm and serial COM ports.
Hardware design with LEDs to visualize data transmission and reception.
.bin files for direct uploading to the LPC1768 microcontroller.

## **Why CAN Protocol?**
CAN is widely used in automotive systems to ensure efficient and reliable communication between components like ECUs, sensors, and actuators. It supports applications such as engine management, ABS, airbags, and advanced driver-assistance systems (ADAS).

## **Tools & Components:**
1.	Microcontroller: LPC1768
2.	Transceiver: MCP2551
3.	Software: Keil Studio Cloud, TeraTerm
4.	Programming Language: C++


## **How to Use?**
1.	Clone the repository: git clone https://github.com/Amey-Chougule/CAN-BUS-Protocol-LPC1768.git  
2.	Build the hardware circuit using the provided schematic.
3.	Compile the code using Keil Studio Cloud and upload the .bin files to the LPC1768.
4.	Monitor message transmission and reception via TeraTerm.

## **Repository Contents:**
1.	CAN Transmitter.txt: Source code for the transmitter.
2.	CAN Receiver.txt: Source code for the receiver.
3.	CAN_Transmitter.LPC1768.bin: Compiled binary file for the transmitter.
4.	CAN_Receiver_.LPC1768.bin: Compiled binary file for the receiver.
5.	CAN LPC1768 Circuit Diagram.png: Circuit schematic for hardware connections.
6.	mbedWinSerial_16466 - USB Driver : USB driver for mbed lpc1768 development board.
7.	teraterm-4.105 : TeraTerm Software.
8.	README.md: Project documentation.

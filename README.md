# SecureQuadcopter-NRF-RC4-Arduino

## Project Overview

This repository contains the code and documentation for a high school project conducted at NCD, Homs, Syria, from November 2016 to June 2017. The project implements secure communication for a locally-built quadcopter using RC4 encryption on an Arduino platform with NRF24L01 modules. The system ensures encrypted, real-time communication between a transmitter (sender) and a receiver, enhancing the security of quadcopter control.

### Key Features
- **RC4 Encryption**: Utilizes the RC4 stream cipher to encrypt and decrypt data, ensuring secure communication.
- **NRF24L01-Arduino Integration**: Establishes a reliable wireless communication link using NRF24L01 modules.
- **Secure Quadcopter Communication**: Enables encrypted data transmission for controlling a custom-built quadcopter.

This project is ideal for hobbyists, students, and developers interested in Arduino-based drone projects, wireless communication, and encryption techniques.

## Repository Contents
- `Sender.txt`: Arduino code for the transmitter, which encrypts a message using RC4 and sends it via the NRF24L01 module.
- `Receiver.txt`: Arduino code for the receiver, which receives and decrypts the message using RC4.
- `README.md`: This file, providing project details and setup instructions.

## Hardware Requirements
- 2x Arduino boards (e.g., Arduino Uno or Nano)
- 2x NRF24L01 wireless modules
- Jumper wires
- Breadboard or PCB for connections
- USB cables for programming the Arduinos
- Optional: A quadcopter setup for real-world testing

## Software Requirements
- Arduino IDE
- Required libraries:
  - `SPI.h` (included with Arduino IDE)
  - `RF24.h` (available via Arduino Library Manager or [GitHub](https://github.com/nRF24/RF24))

## Setup Instructions
1. **Hardware Setup**:
   - Connect the NRF24L01 modules to the Arduino boards:
     - **CE** to pin 9
     - **CSN** to pin 10
     - **MOSI**, **MISO**, **SCK** to the respective SPI pins (check your Arduino model’s pinout)
     - **VCC** to 3.3V, **GND** to GND
   - Ensure one Arduino acts as the sender and the other as the receiver.

2. **Software Setup**:
   - Install the Arduino IDE and the `RF24` library.
   - Rename `Sender.txt` to `Sender.ino` and `Receiver.txt` to `Receiver.ino`.
   - Open each file in the Arduino IDE.

3. **Configuration**:
   - Ensure the `key` variable in both `Sender.ino` and `Receiver.ino` is identical (default: `"SecretKey123"`).
   - Modify the `plaintext` variable in `Sender.ino` to change the message being sent (default: `"Hasan Ismail"`).
   - The communication pipe (`0xE8E8F0F0E1LL`) is the same in both files.

4. **Upload and Run**:
   - Upload `Sender.ino` to the sender Arduino and `Receiver.ino` to the receiver Arduino.
   - Open the Serial Monitor (9600 baud) on both Arduinos to view the encrypted data (sender) and decrypted data (receiver).
   - The sender transmits every 1 second, and the receiver prints the decrypted message when received.

## Code Explanation
- **Sender**:
  - Initializes the NRF24L01 module as a transmitter.
  - Encrypts a plaintext message using RC4 with a predefined key.
  - Sends the encrypted data wirelessly and prints the encrypted bytes (in HEX) to the Serial Monitor.
- **Receiver**:
  - Initializes the NRF24L01 module as a receiver.
  - Receives encrypted data, decrypts it using RC4 with the same key, and prints the decrypted message to the Serial Monitor.
- **RC4 Algorithm**:
  - Implements the Key-Scheduling Algorithm (KSA) and Pseudo-Random Generation Algorithm (PRGA) for RC4 encryption/decryption.
  - The same `rc4_crypt` function is used for both encryption and decryption due to RC4’s XOR-based operation.

## Usage
- The sender encrypts and transmits the message defined in `plaintext` every second.
- The receiver listens for incoming data, decrypts it, and displays the original message.
- To test different messages, modify the `plaintext` variable in `Sender.ino`.
- Ensure the `key` is consistent between sender and receiver for successful decryption.

## Notes
- The NRF24L01 data rate is set to 250 kbps for reliability, and retries are configured to handle transmission failures.
- The buffer size for encrypted/received data is 512 bytes, sufficient for most short messages. Adjust if needed, but ensure it matches the NRF24L01’s payload size limit.
- RC4 is used for educational purposes in this project. For production systems, consider stronger encryption algorithms like AES.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Developed as part of a high school project at NCD, Homs, Syria (2016–2017).
- Thanks to the Arduino and NRF24 communities for their libraries and resources.

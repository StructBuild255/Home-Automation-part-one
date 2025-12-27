Taking Back Control of Home Automation (Part 1)
This repository contains the source code for Part 1 of my video series on building a custom, privacy-focused home automation system. The project focuses on reclaiming control from cloud-based smart devices by flashing custom C++ firmware onto a Sonoff Basic R4.

📺 Watch the full video here: Taking Back Control of Home Automation Pt1

Project Overview
The goal of this project is to replace proprietary firmware with a custom solution that runs locally on your network. This ensures your devices are not sending telemetry to external servers and allows for integration with custom backends (like the Falco system referenced in the code).

Hardware Required
Sonoff Basic R4 (Powered by ESP32-C3)

USB-to-TTL Serial Adapter (Must use 3.3V logic)

Soldering Tools (For attaching header pins to the Sonoff board)

Software Requirements
Arduino IDE

ESP32 Board Manager (Install esp32 by Espressif Systems in Arduino IDE)

File Descriptions
The repository includes three sketches that progress from basic functionality to full network control:

1. BlinkWithoutDelay.ino
A foundational sketch that demonstrates non-blocking timing.

Functionality: Toggles the Relay and LED every 500ms.

Key Concept: Uses millis() instead of delay() to allow the processor to handle other tasks simultaneously.

2. ButtonControlWithDebounce.ino
Adds physical interaction to the device.

Functionality: Allows the onboard button (Pin 9) to toggle the Relay/LED.

Key Concept: Implements software debouncing to ensure clean signal readings from the physical button.

3. WIFIControl.ino
The complete firmware for Part 1, combining manual control with network capabilities.

Network Capabilities: Connects to WiFi and starts a TCP server on port 8081.

OTA Updates: Includes ArduinoOTA to allow for wireless firmware updates in the future.

Dual Control: The device can be controlled via the physical button or network commands.

Setup & Configuration
Prepare the Hardware:

Solder header pins to the Sonoff Basic R4.

Connect the USB-to-TTL adapter (RX to TX, TX to RX, 3.3V to 3.3V, GND to GND).

Configure the Code:

Open WIFIControl.ino.

Update the ssid and password variables with your network credentials.

(Optional) Set a unique hostName for the device.

Flash the Firmware:

Hold the physical button on the Sonoff while plugging it into your computer to enter Bootloader Mode.

Select the ESP32C3 Dev Module in Arduino IDE and upload the sketch.

Usage
Once flashed and connected to your network, you can control the relay using netcat (nc) or any TCP client. The server listens on port 8081.

Supported Commands:

ON - Turns the relay on.

OFF - Turns the relay off.

TOGGLE - Toggles the current state.

Example Terminal Command:

Bash

# Replace 192.168.1.XXX with your device's IP address
echo -n "TOGGLE" | nc 192.168.1.XXX 8081
Note: The code includes a placeholder comment for integration with "Falco commands," hinting at the backend server integration to come in future videos.

Disclaimer: Working with mains electricity is dangerous. Ensure the device is unplugged from mains power while flashing or modifying hardware.





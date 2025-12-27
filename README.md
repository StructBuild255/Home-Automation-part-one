# Taking Back Control of Home Automation (Part 1)

This repository contains the code for Part 1 of my video series on building a custom, privacy-focused home automation system using the Sonoff Basic R4. 

**📺 Watch the full video here:** [Taking Back Control of Home Automation Pt1](https://www.youtube.com/watch?v=V4xDByzqnBk)

## Project Overview

The goal of this project is to replace proprietary, cloud-dependent firmware with custom C++ code running on the ESP32-based Sonoff Basic R4. This allows for local control over your devices without sending telemetry data to external servers.

### Hardware Required
* **Sonoff Basic R4** (ESP32-C3 based)
* **USB-to-TTL Serial Adapter** (3.3V logic) for initial flashing
* Soldering iron and headers (for accessing programming pins)

### Software Requirements
* **Arduino IDE**
* **ESP32 Board Manager** installed in Arduino IDE (`esp32` by Espressif Systems)

## File Descriptions

This repository progresses from a basic "Hello World" equivalent to a fully network-controlled switch.

### 1. `BlinkWithoutDelay.ino`
A basic introduction to non-blocking code.
* **Function:** Toggles the Relay and LED every 500ms using `millis()` instead of `delay()`.
* **Purpose:** Establishes the foundation for multitasking, allowing the processor to do other things (like listen for WiFi or buttons) while timing the LED.

### 2. `ButtonControlWithDebounce.ino`
Adds physical interaction to the device.
* **Function:** Allows the onboard push button to toggle the Relay/LED.
* **Features:** Implements software debouncing to prevent false triggers and noisy signals from the mechanical button.

### 3. `WIFIControl.ino`
The final code for Part 1, combining manual control with network capabilities.
* **Function:** Connects the device to your local WiFi network.
* **Features:**
    * **TCP Server:** Listens on port **8081** for commands.
    * **OTA (Over-The-Air) Updates:** Allows you to upload new code wirelessly without plugging in the USB adapter again.
    * **Physical Control:** Retains the button functionality from the previous sketch.

## Configuration & Usage

### 1. Setup
Open `WIFIControl.ino` and update the following lines with your network credentials:
const char* ssid = "yourWifiName";
const char* password = "yourWifiPassword";
const char* hostName = "device-name"; 


2. Flashing
Connect your USB-to-TTL adapter to the Sonoff (TX to RX, RX to TX, GND to GND, 3.3V to 3.3V).

Hold the button on the Sonoff while plugging it in to enter Bootloader Mode.

Select the correct board (e.g., ESP32C3 Dev Module) and port in Arduino IDE.

Upload the sketch.

3. Controlling the Device
Once uploaded and connected to WiFi, you can control the relay using netcat (nc) from a terminal on the same network.

Commands: ON, OFF, TOGGLE

Example (Linux/Mac Terminal): Replace 192.168.1.XXX with your device's IP address (visible in Serial Monitor on boot).

Bash

# Turn ON
echo -n "ON" | nc 192.168.1.XXX 8081

# Turn OFF
echo -n "OFF" | nc 192.168.1.XXX 8081

# Toggle state
echo -n "TOGGLE" | nc 192.168.1.XXX 8081
Future Plans
This is just the beginning (Part 1). Future updates will cover the backend server (Falco) and more advanced integrations.

Disclaimer: Working with mains electricity is dangerous. Ensure all power is disconnected before modifying hardware. Proceed at your own risk.


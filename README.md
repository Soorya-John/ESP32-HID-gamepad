ESP32-S3 iBus to USB HID Bridge

Convert FlySky FS-iA10B iBus RC signals into a native USB HID Gamepad using the ESP32-S3.

This project allows a standard RC transmitter to function as a plug-and-play USB controller for PC flight simulators and other applications without requiring external adapters or drivers.

Overview

The ESP32-S3 reads iBus serial data from the FlySky FS-iA10B receiver over UART, decodes multi-channel control frames in real-time, and emulates a USB HID joystick using the TinyUSB stack.

When connected to a PC, the device is automatically detected as a standard USB game controller.

Features

iBus frame decoding (up to 14 channels)

Real-time channel normalization (1000–2000 µs to HID axis range)

Native USB HID Gamepad implementation (TinyUSB)

Low-latency signal processing

Plug-and-play compatibility (Windows / Linux / macOS)

Modular firmware design

Hardware Requirements

ESP32-S3 (USB OTG capable)

FlySky FS-iA10B receiver (iBus output)

Regulated 5V / 3.3V power supply

Compatible FlySky transmitter

Optional:

OLED display for debugging or telemetry

Wiring

FS-iA10B VCC → 5V / 3.3V (as required)
FS-iA10B GND → GND
FS-iA10B iBus → ESP32-S3 UART RX

Ensure correct voltage levels before connecting.

How It Works

The FS-iA10B outputs 32-byte iBus frames via UART.

ESP32-S3 parses channel values in real-time.

Channel data is mapped to joystick axes and buttons.

The TinyUSB stack enumerates the ESP32-S3 as a USB HID Gamepad.

The PC recognizes it automatically as a standard joystick device.

Tested With

Uncrashed FPV Simulator

Liftoff

Windows Game Controller Panel

Future Improvements

Telemetry parsing (RSSI, battery voltage)

OLED live diagnostics

Calibration mode

Configurable channel mapping

Wireless USB bridge version

License

MIT License

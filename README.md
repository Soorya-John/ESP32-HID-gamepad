ESP32-S3 iBus to USB HID Bridge (FlySky FS-iA10B)
A custom embedded firmware project that converts FlySky FS-iA10B iBus RC signals into a native USB HID gamepad using the ESP32-S3.
This allows a standard RC transmitter to function as a plug-and-play USB controller for PC flight simulators and other applications — without external adapters or drivers.
🔧 Features
iBus serial frame decoding (up to 14 channels)
Real-time channel mapping to USB HID axes & switches
Native USB Gamepad implementation (TinyUSB)
Low-latency signal processing
Plug-and-play compatibility (Windows/Linux/macOS)
Clean modular firmware structure
🛠 Hardware
ESP32-S3 (USB OTG capable)
FlySky FS-iA10B receiver (iBus output)
5V → 3.3V regulated power
Optional OLED display for debugging
⚙️ How It Works
The FS-iA10B outputs iBus serial data over UART.
ESP32-S3 parses 32-byte iBus frames in real-time.
Channel values (1000–2000 µs) are normalized to HID axis ranges.
ESP32-S3 enumerates as a USB Gamepad device.
PC recognizes it as a standard joystick.
📦 Applications
Drone flight simulators (Uncrashed, Liftoff, VelociDrone)
Robotics control systems
Custom RC-to-USB interfaces
Embedded USB device experimentation
🚀 Future Improvements
Telemetry parsing (RSSI, battery voltage)
OLED live diagnostics
Calibration mode
Configurable channel mapping
Wireless USB bridge version 

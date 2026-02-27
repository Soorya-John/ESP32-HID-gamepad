#include <Arduino.h>
#include "IBusBM.h"

// ===== ESP32-S3 TinyUSB HID Gamepad =====
#include "USB.h"
#include "USBHIDGamepad.h"
USBHIDGamepad Gamepad;

// ===== RGB LED (WS2812 / NeoPixel on S3 Zero) =====
#include <Adafruit_NeoPixel.h>

#define RGB_PIN 21        // Most ESP32-S3 Zero boards use GPIO48
#define RGB_COUNT 1
#define RGB_BRIGHTNESS 5 // LOW brightness to save power

Adafruit_NeoPixel rgb(RGB_COUNT, RGB_PIN, NEO_GRB + NEO_KHZ800);

// ===== IBUS SETTINGS =====
IBusBM ibus;
#define IBUS_RX 16

int ch[8];

// ===== Convert stick movement into RGB colour =====
// ===== Convert each axis into a UNIQUE RGB colour =====
void updateRGB(int lx, int ly, int rx, int ry) {

  // Each axis controls one colour channel so behaviour is predictable
  // Roll  (CH1 / lx) -> RED
  // Pitch (CH2 / ly) -> GREEN
  // Throttle (CH3 / rx) -> BLUE
  // Yaw (CH4 / ry) -> adds WHITE mix subtly

  int red   = map(abs(lx), 0, 127, 0, 255);
  int green = map(abs(ly), 0, 127, 0, 255);
  int blue  = map(abs(rx), 0, 127, 0, 255);

  // Yaw adds a slight brightness boost without overriding colours
  int yawMix = map(abs(ry), 0, 127, 0, 60);

  red   = constrain(red + yawMix,   0, 255);
  green = constrain(green + yawMix, 0, 255);
  blue  = constrain(blue + yawMix,  0, 255);

  rgb.setPixelColor(0, rgb.Color(red, green, blue));
  rgb.show();
}

void setup() {

  Serial.begin(115200);

  // ===== RGB INIT =====
  rgb.begin();
  rgb.setBrightness(RGB_BRIGHTNESS);
  rgb.clear();
  rgb.show();

  // ===== USB HID =====
  USB.begin();
  Gamepad.begin();

  // ===== IBUS =====
  Serial1.begin(115200, SERIAL_8N1, IBUS_RX, -1);
  ibus.begin(Serial1, IBUSBM_NOTIMER, IBUS_RX, -1);
}

void loop() {

  ibus.loop();

  for(int i=0;i<8;i++){
    ch[i] = ibus.readChannel(i);
  }

  // Convert iBUS to joystick range
  int lx = map(ch[0],1000,2000,-127,127);
  int ly = map(ch[1],1000,2000,-127,127);
  int rx = map(ch[2],1000,2000,-127,127);
  int ry = map(ch[3],1000,2000,-127,127);

  // ===== SEND HID REPORT =====
  Gamepad.send(
    lx,
    ly,
    rx,
    ry,
    0,
    0,
    0,
    0
  );

  // ===== UPDATE RGB LED =====
  updateRGB(lx, ly, rx, ry);

  delay(10);
}

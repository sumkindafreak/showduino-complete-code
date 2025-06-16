🧠 Showduino: Complete FX Control System
Showduino is a modular, open-source show control system built for immersive scare attractions, escape rooms, theatrical productions, and interactive props. This repository contains the complete ESP32 firmware for the touchscreen controller — integrating matrix effects, DMX lighting, relays, MP3 audio, and WebSocket-based control into one cohesive show system.

⚙️ System Overview
Component	Description
ESP32 Touchscreen	Handles the main UI, FX commands, scene selection, and diagnostics.
Arduino Mega	Listens for commands (via Serial), controls relays, DMX lights, NeoPixels, and more.
Web Interface	Connects via WebSocket or REST API to control shows from a browser or mobile app.

📦 Features
Matrix FX Engine: Custom XY-mapped 9×8 LED matrix with effects like shimmer, burst, rainbow wave, and spirals.

DMX Lighting Control: Supports up to 8 custom-defined fixtures (RGB PARs, moving heads, fog, strobes, etc.).

Relay Control: Activate up to 8 relay channels with duration, delay, and Web control.

Scene System: Load and play .shdo show files from SD, with full FX scheduling.

Touch UI Menus:

Live Controls: Trigger relays and FX on the fly.

Show Grid: Load and start scene files.

Settings: WiFi setup, brightness, DMX configuration.

Diagnostics: Performance, heap memory, connection status.

WebSocket + REST API: Real-time control from external dashboards or automation systems.

Offline-First: Host UI assets on the ESP32 SD card for full offline functionality.

🧱 Hardware Requirements
Module	Description
ESP32 (CYD 2.8" Display)	Main controller running this firmware.
Touchscreen TFT (ILI9341 + XPT2046)	Used for live control interface and diagnostics.
NeoPixel Matrix (9x8)	Connected to GPIO 27, 72 total LEDs.
Relays	Up to 8, connected via GPIOs.
SD Card	Stores scenes, logos, and web files.
Optional Add-ons	YX5300 MP3 Players, RTC, SX1509 buttons, sensors.

📁 File Structure
Folder/File	Purpose
src/	Main source code, matrix FX, DMX, and UI logic.
scenes/	Scene files in .shdo format for autoplay or Web loading.
data/ (for SPIFFS or SD)	HTML/JS/CSS for offline web control dashboard.
command_map.h	FX commands and relay definitions.
custom_matrix_fx.h	Fully mapped matrix effect engine.

🧩 Matrix FX Integration
Matrix FX are scheduled using scheduleMatrixFX() and include:

MATRIX_SHIMMER_WAVE

MATRIX_BURST_CENTER

MATRIX_RAINBOW_WAVE

MATRIX_SPIRAL

MATRIX_FILL

MATRIX_CLEAR

🔌 DMX Fixture Setup
DMX Fixtures can be configured with addDMXFixture(id, label, type, startChannel, channelCount). Supported fixture types:

RGB_PAR

SIMPLE_RGB

MOVING_HEAD

FOG

STROBE

These are initialized in initializeDMXSystem() and auto-detected by the UI.

🌐 API Usage
🔹 FX Command (POST /fx)
json
Copy
Edit
{
  "fx_id": 102,
  "start": 0,
  "count": 72,
  "color": "#FF00FF",
  "speed": 30,
  "brightness": 200,
  "delay": 100
}
🔹 Relay Command (POST /relay)
json
Copy
Edit
{
  "relay_id": 1,
  "state": "ON",
  "duration": 3000,
  "delay": 0
}
🔹 Scene Command (POST /scene)
json
Copy
Edit
{
  "action": "load",
  "scene": "chamber.shdo"
}
🚀 Getting Started
Flash this code to your ESP32 using Arduino IDE or PlatformIO.

Prepare an SD card:

/scenes/ for show files

/images/ for logos

/www/ for Web UI (if applicable)

Connect the matrix, relays, touchscreen, and optional peripherals.

Power on and access:

Touchscreen UI

Web control (via ESP32 IP)

Serial monitor for debug info

🔒 Dependencies
Adafruit_NeoPixel

Adafruit_GFX, Adafruit_ILI9341, XPT2046_Touchscreen

ESPAsyncWebServer, WebSockets

ArduinoJson

SD, FS, SPI

Any required custom libraries for MP3/DMX/SX1509

📌 Future Plans
Live FX editing via web UI

Scene scheduling with triggers

Advanced audio integration (DFPlayer Pro, WAV playback)

Voice command integration

Cloud sync via Firebase

🤘 Community & License
Showduino is open-source and shared to empower creators who can't afford expensive show control systems.

💸 Over £800 of personal investment.
🧪 Designed to be hackable, expandable, and terrifyingly fun.

📜 License: MIT
🧠 Creator: @sumkindafreak


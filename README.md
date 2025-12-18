<p align="center">
  <img src="docs/github_icon.png" alt="WeatherLight logo" width="640"><br>
</p>

WeatherLight ESP32-based intelligent LED weather display system with GitHub OTA updates.

## Features

- Real-time weather visualization on addressable LEDs (WS2812/NeoPixel)

- Open-Meteo integration (no API key required)

- Weather effects engine (clear, clouds, rain, storm, fog, snow + more)

- Sun tracker with automatic sunrise/sunset timing (daily schedule)

- Night Mode with PIR motion sensor (gentle red light, configurable hours)

- GitHub OTA updates (safe remote firmware upgrades)

- Captive portal Wi-Fi setup (AP mode for first-time configuration)

- Web status panel (device info, mode, update status, diagnostics)

- Persistent settings (NVS) — updates don’t wipe user configuration

- Offline / error fallbacks (Wi-Fi/NTP/API failure handling)

- Seasonal mode (Christmas effects support)

- Two languages - PL and EN

## Tested Hardware / Reference Setup

WeatherLight has been developed and tested on the following reference hardware configuration:

### Controller
- **ESP32-C6 Dev Module**
  - USB-C programming
  - Wi-Fi 2.4 GHz
  - GPIO pinout defined directly in firmware source code

### LEDs
- **Addressable RGB LEDs (WS2812 / NeoPixel compatible)**
  - Single DATA line control
  - External power supply required for medium and large LED installations

#### Signal & Power Best Practices
- **Series resistor on DATA line (recommended: 330Ω)**
  - Placed close to the ESP32 output pin
  - Reduces signal ringing and protects the first LED

- **Logic level shifter (3.3V → 5V)**
  - Strongly recommended for reliable DATA signaling
  - Especially important for longer LED strips or higher data rates

- **Power injection from both ends of the LED strip**
  - Recommended for longer LED chains
  - Reduces voltage drop and color shifting at the far end

- **Bulk capacitor across LED power rails**
  - **1000µF (or larger) electrolytic capacitor**
  - Placed close to the LED power input
  - Protects LEDs from inrush current and power spikes

### Power Supply
- **5V DC / 20A power supply**
  - Required for stable operation with high LED counts
  - LEDs powered externally (not from ESP32)
  - Common GND between ESP32 and LED power is mandatory

### Sensors
- **AM312 Mini PIR motion sensor**
  - Compact, low-power PIR module
  - Digital output (HIGH on motion)
  - Used for Night Mode activation (gentle red light)

### Wiring & Configuration
- GPIO assignments and pin mapping are defined in firmware source code
- Designed for external LED power distribution
- User settings persist across firmware updates via NVS

> Note:  
> WeatherLight is designed to be hardware-flexible.  
> Other ESP32 variants and compatible addressable LEDs may work, but the above setup is the officially tested reference configuration.


## License
This project is licensed under the MIT License.
Commercial use requires a separate commercial license – see COMMERCIAL_LICENSE.md.

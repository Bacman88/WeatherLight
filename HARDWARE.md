# WeatherLight – Hardware Reference & Wiring

This document describes the **official reference hardware configuration**
used during development and testing of the WeatherLight firmware.

---

## Controller

- **ESP32-C6 Dev Module**
  - USB-C programming
  - Wi-Fi 2.4 GHz
  - GPIO mapping defined in firmware source code
  - Logic level: 3.3V

---

## LED System

- **WS2812B / NeoPixel compatible addressable LEDs**
  - Voltage: 5V
  - Single DATA line
  - External power supply required

Typical configuration:
- 5 meters LED strip
- 30 LEDs per meter (150 LEDs total)

---

## Power Supply

- **5V DC power supply**
  - Recommended capacity: **10A–20A**
  - Depends on LED count and brightness
  - LEDs must NOT be powered from ESP32

⚠️ **Common GND between ESP32 and LED power is mandatory**

---

## Sensors

- **AM312 Mini PIR Motion Sensor**
  - Digital output (HIGH on motion)
  - Low power consumption
  - Used for Night Mode activation

Typical setup:
- 1–2 PIR sensors
- Additional sensors supported by firmware

---

## Signal & Power Best Practices

### DATA Line
- **330Ω series resistor**
  - Placed close to ESP32 DATA output
  - Improves signal integrity and protects first LED

### Logic Level Shifting
- **3.3V → 5V level shifter (e.g. Pixel Boost, 74AHCT125)**
  - Strongly recommended
  - Ensures reliable DATA signal, especially for longer strips

### Power Injection
- Inject **5V and GND from both ends** of the LED strip
- Reduces voltage drop and color shifting

### Bulk Capacitors
- **1000µF (or larger) electrolytic capacitor**
  - Rated ≥10V
  - Placed across LED +5V and GND near power entry
  - Protects against inrush current and voltage spikes

---

## Wiring Notes

- Use sufficiently thick wires for LED power distribution
- Keep DATA line as short as possible
- Avoid powering LEDs and ESP32 from the same thin wires
- GPIO pin assignments are defined directly in firmware source code

---

## Hardware Flexibility

WeatherLight is designed to be hardware-flexible.

Other ESP32 variants and compatible addressable LEDs may work,
but the configuration described above is the **officially tested reference setup**.

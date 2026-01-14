<p align="center">
  <img src="docs/github_icon.png" alt="WeatherLight logo" width="640"><br>
</p>

# WeatherLight

**WeatherLight** is an ESP32-based intelligent LED weather display firmware  
that visualizes real-time weather, astronomy and system status using
addressable RGB LEDs.

The project is designed as a **stable, production-ready firmware**
with OTA updates, persistent configuration and hardware flexibility.

---

## Features

- Real-time weather visualization on addressable LEDs (WS2812 / NeoPixel)
- Open-Meteo integration (no API key required)
- Advanced weather effects engine (clear, clouds, rain, storm, fog, snow, seasonal)
- Sun tracker with automatic sunrise and sunset handling
- Night Mode with PIR motion sensors (gentle red light)
- GitHub OTA updates with safe upgrade path
- Captive portal Wi-Fi setup (AP mode for first-time configuration)
- Web status panel (device info, diagnostics, update status)
- Persistent configuration stored in NVS
- Offline and error fallback modes (Wi-Fi / NTP / API failures)
- Multi-language support (EN / PL)

---

## Tested Hardware (Reference Setup)

The following configuration represents the **official reference setup**
used during development and testing.

- **ESP32-C6 Dev Module**
- **WS2812B addressable LEDs (5V)**
- **AM312 PIR motion sensors**
- **5V power supply (10A–20A depending on LED count)**

Full wiring details and hardware notes are available in  
➡️ **[HARDWARE.md](HARDWARE.md)**

---

## Documentation & Links

- **Hardware & Wiring**: [HARDWARE.md](HARDWARE.md)
- **License**: [LICENSE.md](LICENSE.md)
- **Issue Tracker**: [Report issues here](../../issues)
- **Releases**: [Firmware downloads](../../releases)

---

## Version Information

**Version**: 6.3.0  
**Status**: ✅ Production Ready  
**Compatibility**: OTA update from v6.1.0 and v6.1.1  
**Recommended**: ✅ Update recommended for legal compliance

---

🌟 **Star this repository if you find WeatherLight useful!** 🌟

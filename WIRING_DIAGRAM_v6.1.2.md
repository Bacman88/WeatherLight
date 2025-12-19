# WeatherLight v6.1.2 - Wiring Diagram 🔌

**Complete electrical schematic for ESP32-C6 with 150 WS2812B LEDs**

---

## 📋 Bill of Materials (BOM)

### Main Components

| Component | Specification | Quantity | Notes |
|-----------|--------------|----------|-------|
| **Power Supply** | 5V 20A (100W) | 1 | Mean Well LRS-100-5 or similar |
| **Microcontroller** | ESP32-C6 DevKit | 1 | ESP32-C6-DevKitC-1 |
| **LED Strip** | WS2812B 5m 30LED/m | 1 | Total: 150 LEDs (single 5m strip) |
| **Capacitor** | 1000µF 10V Electrolytic | 2 | One at PSU, one at LED strip input |
| **Resistor** | 330Ω 1/4W | 1 | Data line protection (ESP32 → Pixel Boost) |
| **Level Shifter** | Pixel Boost or 74HCT245 | 1 | 3.3V → 5V logic conversion |
| **PIR Sensor** | AM312 Mini PIR | 2 | Motion detection |

### Wiring & Connectors

| Component | Specification | Quantity | Notes |
|-----------|--------------|----------|-------|
| **Wire 2-core** | 18-20 AWG | ~3m | Power distribution (5V/GND) |
| **Wire 3-core** | 22-24 AWG | ~2m | Data + power to strip |
| **Terminal Blocks** | 2-way screw terminal | 3+ | Power distribution |
| **Terminal Blocks** | 3-way screw terminal | 1+ | Strip connection |
| **Dupont Connectors** | Female 2.54mm | 10+ | PIR sensors, ESP32 |
| **JST-SM Connectors** | 3-pin (optional) | 2 | LED strip connectors |
| **Heat Shrink Tubing** | Various sizes | - | Insulation |

---

## 🔌 Complete Wiring Diagram

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                    WEATHERLIGHT WIRING DIAGRAM v6.1.2                    ║
║                   ACTUAL PINOUT FROM SKETCH (ESP32-C6)                   ║
╚═══════════════════════════════════════════════════════════════════════════╝

                     ┌─────────────────────┐
                     │   POWER SUPPLY      │
                     │    5V 20A (100W)    │
                     │                     │
                     │  AC 110-240V INPUT  │
                     └──────┬───────┬──────┘
                            │       │
                         [5V]     [GND]
                            │       │
                            │       │
                  ┌─────────┴───────┴─────────┐
                  │  CAPACITOR 1000µF (PSU)   │
                  │     [+]         [-]       │
                  └─────────┬───────┬─────────┘
                            │       │
              ┌─────────────┴───────┴─────────────┐
              │                                   │
              │     MAIN POWER DISTRIBUTION       │
              │     (Terminal Blocks)             │
              │                                   │
    ┌─────────┴──────────┬──────────┬────────────┴──────────┐
    │                    │          │                        │
[5V Bus]              [5V]       [5V]                    [5V Bus]
[GND Bus]             [GND]      [GND]                   [GND Bus]
    │                    │          │                        │
    │              ┌─────┴──────────┴─────┐                  │
    │              │                     │                   │
    │              │   ESP32-C6 DEVKIT   │                   │
    │              │                     │                   │
    │              │  [5V]  [GND] [3.3V] │                   │
    │              │                     │                   │
    │              │  [GPIO2] ──[330Ω]──┼───┐                │
    │              │  (LED DATA)        │   │                │
    │              │                    │   │                │
    │              │  [GPIO3] ────┐     │   │                │
    │              │  (PIR 1)     │     │   │                │
    │              │              │     │   │                │
    │              │  [GPIO4] ────┼───┐ │   │                │
    │              │  (PIR 2)     │   │ │   │                │
    │              └──────────────┼───┼─┘   │                │
    │                             │   │     │                │
    │                             │   │     │                │
    │         PIR SENSORS (2×)    │   │     │                │
    │                             │   │     │                │
    │    ┌────────────────┐   ┌───┴───┴───┐ │                │
    │    │   PIR #1       │   │  PIR #2   │ │                │
    │    │   GPIO3        │   │  GPIO4    │ │                │
    │    │ [OUT][V][G]    │   │[OUT][V][G]│ │                │
    │    │   │   │  │     │   │  │   │  │ │ │                │
    │    └───┼───┼──┼─────┘   └──┼───┼──┼─┘ │                │
    │        │   │  │            │   │  │   │                │
    │     [OUT] │  └────[GND]────┴───┘  │   │                │
    │        │  └────────[3.3V]─────────┘   │                │
    │        │                               │                │
    │     [GPIO3]                         [GPIO4]            │
    │                                        │                │
    │         LEVEL SHIFTER (PIXEL BOOST)   │                │
    │                                        │                │
    │         GPIO2 ──[330Ω]──┐             │                │
    │                         │             │                │
    │                    ┌────┴──────┐      │                │
    │         3.3V ──────┤ LV    HV  ├───── 5V               │
    │         GND ───────┤ GND   GND ├───── GND              │
    │         [330Ω]─────┤ IN    OUT ├───┐                   │
    │                    └───────────┘   │                   │
    │                        [DATA 5V]   │                   │
    │                                    │                   │
    ├────────────────────────────────────┼───────────────────┤
    │                                    │                   │
    │              LED STRIP SECTION     │                   │
    │              (150 LEDs - 5 meters) │                   │
    │              SINGLE STRIP!         │                   │
    │                                    │                   │
    │   ┌────────────────────────────────┴────┐              │
    │   │  INPUT CONNECTOR                   │              │
    │   │  ┌───┬───┬───┐                     │              │
    │   │  │5V │GND│DAT│ ◄───────────────────┘              │
    │   │  └─┬─┴─┬─┴─┬─┘                                    │
    │   │    │   │   │                                      │
    │   │  ┌─┴───┴───┴─┐ ◄─ CAPACITOR 1000µF               │
    │   │  │1000µF 10V │    AT STRIP INPUT!                │
    │   │  │  [+]  [-] │    (soldered to pads)             │
    │   │  └─┬───┬───┬─┘                                    │
    │   │    │   │   │                                      │
    │   │  ┌─┴───┴───┴─┐                                    │
    │   │  │ WS2812B    │                                   │
    │   │  │ LED Strip  │                                   │
    │   │  │ 150 LEDs   │                                   │
    │   │  │ 5 meters   │                                   │
    │   │  │ 30 LED/m   │                                   │
    │   │  └─┬───┬───┬─┘                                    │
    │   │    │   │   │                                      │
    │   │  ┌─┴───┴───┴─┐                                    │
    │   │  │5V │GND│DAT│                                    │
    │   │  └───┴───┴───┘                                    │
    │   │    OUTPUT (unused)                                │
    │   └───────────────────────────────────────────────────┘
    │         │   │                                          │
    │      [5V] [GND]                                        │
    │         │   │                                          │
    └─────────┴───┴──────────────────────────────────────────┘
                  │
              [GND Bus]

╔═══════════════════════════════════════════════════════════════════════════╗
║  CRITICAL NOTES:                                                          ║
╠═══════════════════════════════════════════════════════════════════════════╣
║  • LED Data: GPIO2 (NOT GPIO8!)                                          ║
║  • PIR #1: GPIO3 (NOT GPIO0!)                                            ║
║  • PIR #2: GPIO4 (NOT GPIO1!)                                            ║
║  • 330Ω resistor BETWEEN ESP32 GPIO2 and Pixel Boost IN                 ║
║  • Capacitor 1000µF AT LED strip INPUT connector (soldered to pads)     ║
║  • Only ONE strip: 150 LEDs, 5 meters, 30 LED/m                         ║
║  • Only TWO PIR sensors (GPIO3 and GPIO4)                                ║
║  • All 5V and GND lines must be thick (18-20 AWG) to handle current!   ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

---

## 🔧 Detailed Connection Tables

### ESP32-C6 GPIO Pinout (ACTUAL FROM SKETCH!)

| GPIO Pin | Function | Connection | Notes |
|----------|----------|------------|-------|
| **GPIO2** | LED Data Out | → 330Ω → Pixel Boost IN → Strip DATA | Main data line |
| **GPIO3** | PIR Sensor #1 | → PIR #1 OUT pin | Motion sensor 1 |
| **GPIO4** | PIR Sensor #2 | → PIR #2 OUT pin | Motion sensor 2 |
| **5V** | Power Input | ← 5V Power Supply | ESP32 power |
| **GND** | Ground | ← GND Power Supply | Common ground |
| **3.3V** | 3.3V Output | → PIR Sensors VCC | Power for 2 PIRs |

### PIR Sensor (AM312) Pinout

Each PIR sensor has 3 pins:

| Pin | Name | Connection | Wire Color |
|-----|------|------------|------------|
| **1** | VCC | → ESP32 3.3V | Red |
| **2** | OUT | → ESP32 GPIO3 or GPIO4 | Yellow/White |
| **3** | GND | → ESP32 GND | Black |

### LED Strip Connection (SINGLE STRIP!)

| Strip Pin | Connection | Wire Gauge | Notes |
|-----------|------------|------------|-------|
| **5V** | ← 5V Power Supply | 18 AWG | Heavy current |
| **GND** | ← GND Power Supply | 18 AWG | Heavy current |
| **DATA** | ← Pixel Boost OUT | 22 AWG | From GPIO2 via 330Ω + Pixel Boost |
| **Cap 1000µF** | At strip INPUT connector | - | [+] to 5V, [-] to GND, soldered to pads |

### Power Distribution

| Connection | Wire Gauge | Max Current | Notes |
|------------|------------|-------------|-------|
| PSU → Main Bus | 16-18 AWG | 20A | Shortest possible |
| Main Bus → LED Strip | 18 AWG | 10A | 150 LEDs max 9A |
| Main Bus → ESP32 | 22 AWG | 0.5A | Low current |
| ESP32 3.3V → PIRs | 24 AWG | 0.02A | Very low current |

---

## ⚡ Power Calculations

### LED Power Requirements

| Parameter | Value | Calculation |
|-----------|-------|-------------|
| **LEDs total** | 150 | Single 5m strip × 30 LED/m |
| **Power per LED** | 60mA @ 5V | White, full brightness |
| **Max current (LEDs)** | 9A | 150 × 60mA |
| **ESP32 current** | 0.5A | WiFi active |
| **PIR sensors (2×)** | 0.02A | 2 × 10mA |
| **Total system max** | ~9.52A | All components |
| **Power supply rating** | 20A @ 5V | 100W capacity |
| **Safety margin** | 52% | Plenty of headroom! |

### Typical Operating Current

| Mode | LED Brightness | Current Draw | Notes |
|------|---------------|--------------|-------|
| **Weather Effects** | 30-50% | 3-5A | Normal operation |
| **Night Mode** | 10-20% | 1-2A | Red corridor lighting |
| **Christmas Mode** | 60-80% | 5-7A | Festive animations |
| **Solid Color (Max)** | 100% | 9A | White full brightness |
| **Standby** | LEDs off | 0.52A | ESP32 + PIRs only |

---

## 🛠️ Assembly Instructions

### Step 1: Power Supply Preparation

1. **Mount power supply** in well-ventilated enclosure
2. **Connect AC input** (⚠️ DANGER: High voltage!)
3. **Test output** with multimeter: Should read 5.0V ±0.1V
4. **Install fuse** on AC input (2A slow-blow recommended)
5. **Add capacitor** (1000µF) across PSU output (optional, for extra filtering)

### Step 2: Main Power Distribution

1. **Create power bus** using terminal blocks:
   - One terminal block for 5V bus (3+ connections)
   - One terminal block for GND bus (3+ connections)
2. **Keep wires short** (<30cm) from PSU to bus

### Step 3: ESP32-C6 Connections

1. **Power connections:**
   ```
   5V Bus → ESP32 5V pin (red wire, 22 AWG)
   GND Bus → ESP32 GND pin (black wire, 22 AWG)
   ```

2. **PIR sensor power (2 sensors only):**
   ```
   ESP32 3.3V → PIR #1 VCC (red wire, 24 AWG)
   ESP32 3.3V → PIR #2 VCC (red wire, 24 AWG)
   ESP32 GND → PIR #1 GND (black wire, 24 AWG)
   ESP32 GND → PIR #2 GND (black wire, 24 AWG)
   ```

3. **PIR sensor signals:**
   ```
   PIR #1 OUT → ESP32 GPIO3 (yellow wire, 24 AWG)
   PIR #2 OUT → ESP32 GPIO4 (yellow wire, 24 AWG)
   ```

4. **LED data line (resistor BEFORE Pixel Boost!):**
   ```
   ESP32 GPIO2 → 330Ω Resistor → Pixel Boost IN
   ESP32 3.3V → Pixel Boost LV (low voltage side)
   ESP32 GND → Pixel Boost GND
   5V Bus → Pixel Boost HV (high voltage side)
   Pixel Boost OUT → LED Strip DATA
   ```
   **CRITICAL:** 
   - Use GPIO2 for LED data (NOT GPIO8!)
   - 330Ω resistor goes BETWEEN ESP32 and Pixel Boost!

### Step 4: LED Strip Connection

1. **Power connections with capacitor AT strip input:**
   ```
   5V Bus → Strip 5V input (18 AWG wire)
   GND Bus → Strip GND input (18 AWG wire)
   
   Capacitor 1000µF placement:
   - Solder [+] leg directly to strip 5V pad
   - Solder [-] leg directly to strip GND pad
   - Keep capacitor within 5cm of first LED!
   - Use heat shrink tubing for insulation
   ```
   **CRITICAL:** Capacitor goes AT the strip input connector, NOT at power supply!

2. **Data connection:**
   ```
   Pixel Boost OUT → Strip DATA IN (22 AWG wire)
   ```

3. **Secure strip** to mounting surface (aluminum channel recommended)

4. **Test strip** before final installation

### Step 5: Testing & Validation

1. **Visual inspection:**
   - ✅ All connections tight and secure
   - ✅ No exposed conductors
   - ✅ Capacitor polarity correct ([+] to 5V, [-] to GND)
   - ✅ Wire gauge adequate for current
   - ✅ 330Ω resistor in correct position (before Pixel Boost)

2. **Power-on test (no ESP32 initially):**
   - Connect 5V power supply only
   - Measure voltage at strip input: Should read 4.9-5.0V
   - Check no shorts or sparks

3. **ESP32 programming:**
   - Upload WeatherLight firmware via USB
   - Open Serial Monitor (115200 baud)
   - Check for boot messages

4. **LED test:**
   - Power on complete system
   - Run demo mode (automatic on first boot)
   - Check all 150 LEDs light up sequentially
   - Verify uniform brightness across entire strip

5. **PIR sensor test:**
   - Wave hand in front of PIR #1 (GPIO3)
   - Check Serial Monitor for "PIR #1 triggered"
   - Wave hand in front of PIR #2 (GPIO4)
   - Check Serial Monitor for "PIR #2 triggered"
   - Verify weather animations activate on motion

---

## ⚠️ Safety & Best Practices

### Electrical Safety

- ⚡ **AC Power**: Have qualified electrician wire AC input
- 🔌 **Polarity**: ALWAYS check capacitor polarity before applying power
- 🔥 **Current Rating**: Never exceed wire current ratings
- 🌡️ **Heat Management**: Ensure adequate ventilation for PSU
- 🔒 **Enclosure**: Use non-conductive enclosure for all AC wiring
- 🧯 **Fire Safety**: Keep fire extinguisher nearby during testing

### Wire Gauge Reference

| Wire Gauge | Max Current | Typical Use |
|------------|-------------|-------------|
| **16 AWG** | 22A | Main power from PSU |
| **18 AWG** | 16A | Strip power (5V/GND) |
| **20 AWG** | 11A | Medium power runs |
| **22 AWG** | 7A | Data lines, ESP32 power |
| **24 AWG** | 3.5A | Signal wires, PIR sensors |

### Voltage Drop Considerations

With 5 meter strip (150 LEDs):
- **Voltage drop** at full brightness: ~0.3V
- **Solution**: Power injection at strip start (already implemented)
- **Result**: Uniform brightness across all 150 LEDs

### Common Mistakes to Avoid

❌ **Don't:**
- Use GPIO8 for LED data (it's GPIO2!)
- Use GPIO0-1 for PIRs (it's GPIO3-4!)
- Use wire gauge too thin for current
- Forget capacitor at strip input (causes flickering)
- Mix up capacitor polarity (causes explosion!)
- Put 330Ω resistor AFTER Pixel Boost (should be BEFORE!)
- Forget level shifter (3.3V data unreliable with 5V LEDs)
- Place capacitor at power supply only (should be AT strip input!)

✅ **Do:**
- Use GPIO2 for LED data output
- Use GPIO3 and GPIO4 for PIR sensors
- Use star topology for power distribution
- Add 1000µF capacitor AT strip input connector (soldered to pads)
- Place 330Ω resistor BETWEEN ESP32 GPIO2 and Pixel Boost IN
- Use level shifter (Pixel Boost) for 3.3V → 5V conversion
- Test power supply under load before final assembly
- Label all wires clearly with function and GPIO pin
- Take photos before closing enclosure for future reference

---

## 🧪 Troubleshooting Guide

### Problem: LEDs don't light up

**Possible Causes:**
1. ❌ Wrong GPIO pin → Should be GPIO2, not GPIO8!
2. ❌ No power to strip → Check 5V at strip input
3. ❌ No data signal → Check GPIO2 connection and 330Ω resistor
4. ❌ Level shifter issue → Check Pixel Boost connections and power

**Solution:**
- Verify GPIO2 is used for LED data in code
- Measure 5V at strip input with multimeter
- Check continuity of data line from GPIO2 through resistor and Pixel Boost

### Problem: First few LEDs work, rest don't

**Possible Causes:**
1. ❌ Data line broken → Check strip continuity
2. ❌ Voltage drop too high → Check power connections
3. ❌ Capacitor missing or wrong polarity → Add/check 1000µF at input

**Solution:**
- Test data continuity through strip
- Measure voltage at end of strip (should be >4.7V)
- Verify capacitor polarity: [+] to 5V, [-] to GND

### Problem: LEDs flicker or show wrong colors

**Possible Causes:**
1. ❌ Insufficient power → Check PSU output voltage under load
2. ❌ Missing capacitor → Add 1000µF at strip input
3. ❌ Data line too long → Keep under 30cm, verify resistor present
4. ❌ No level shifter → Pixel Boost required for reliable operation

**Solution:**
- Measure PSU voltage under full load (should be 4.9-5.1V)
- Solder 1000µF capacitor directly to strip input pads
- Shorten data wire between Pixel Boost and strip

### Problem: PIR sensors not detecting

**Possible Causes:**
1. ❌ Wrong GPIO pins → Should be GPIO3 and GPIO4, not GPIO0-1!
2. ❌ No power to PIR → Check 3.3V connection
3. ❌ PIR sensitivity low → Adjust trim pot on AM312 (if available)
4. ❌ Code using wrong pins → Check config.h

**Solution:**
- Verify code uses GPIO3 and GPIO4 for PIRs
- Measure 3.3V at PIR VCC pin
- Check Serial Monitor for PIR trigger messages
- Test PIR by checking OUTPUT pin voltage (should go HIGH on motion)

### Problem: ESP32 won't boot / resets randomly

**Possible Causes:**
1. ❌ Power supply voltage drop → Check voltage at ESP32 5V pin
2. ❌ No capacitor filtering → Add 1000µF at PSU output
3. ❌ Ground loop → Ensure single ground point (star topology)
4. ❌ Insufficient current → Check PSU can handle full load

**Solution:**
- Measure voltage at ESP32 during LED operation
- Add capacitor close to ESP32 for local filtering
- Verify all grounds connect to single point at PSU

---

## 📸 Photos & Documentation

### Recommended Documentation

Take photos of:
1. **Before closing enclosure** - all connections visible
2. **Wire color coding** - for future maintenance
3. **Terminal block layout** - power distribution topology
4. **Strip mounting** - physical installation method
5. **GPIO connections** - ESP32 pinout reference
6. **Final assembly** - completed project

### Labeling

Label all cables with:
- Source and destination (e.g. "ESP32 GPIO2 → Pixel Boost IN")
- Wire gauge (e.g. "18 AWG")
- Function (e.g. "5V POWER", "LED DATA", "PIR #1")

Use label maker or write on masking tape applied to wires.

---

## 🔄 Maintenance

### Regular Checks

**Monthly:**
- Visual inspection of all connections
- Check for loose wires or terminals
- Verify no discoloration (sign of overheating)
- Test both PIR sensors

**Quarterly:**
- Measure 5V output at strip input (should be >4.9V)
- Check all PIR sensors functioning
- Clean dust from enclosure and ESP32
- Verify firmware version

**Yearly:**
- Full system test with multimeter
- Check capacitor health (look for bulging)
- Verify firmware up to date
- Check for software updates on GitHub

---

## 📦 Parts List with Links

### Electronics Distributors

**Power Supply:**
- Mean Well LRS-100-5 (5V 20A)
- Alternative: Any 5V 15A+ PSU with sufficient capacity

**ESP32-C6:**
- Espressif ESP32-C6-DevKitC-1
- Available: DigiKey, Mouser, AliExpress

**LED Strip:**
- WS2812B 5050 RGB 30 LED/m, 5V, IP30/IP65
- 5 meter length (150 LEDs total)
- BTF-Lighting, Alitove, or similar

**Capacitors:**
- Rubycon, Nichicon, or Panasonic 1000µF 10V
- Need 2: One at PSU, one at strip input

**Level Shifter:**
- Adafruit Pixel Boost (recommended)
- TI 74HCT245 (alternative)

**PIR Sensors:**
- AM312 Mini PIR (3.3V compatible)
- Need 2 sensors

**Resistor:**
- 330Ω 1/4W carbon film or metal film
- Need 1 resistor

---

## 📄 Configuration File

Edit your sketch if needed (pins are defined in `config.h`):

```cpp
// config.h - Hardware Pin Definitions

// LED Configuration
#define PIN_LED       2        // GPIO2 for LED data out
#define NUMPIXELS     150      // Total LEDs (single 5m strip)

// PIR Sensor Configuration
#define PIN_PIR1      3        // GPIO3 for PIR sensor #1
#define PIN_PIR2      4        // GPIO4 for PIR sensor #2

// LED Type
#define LED_TYPE      WS2812B
#define COLOR_ORDER   GRB
```

**⚠️ CRITICAL: Do NOT change these pins without rewiring!**

---

## 🎯 Quick Reference Card

Print this and keep near your installation:

```
═══════════════════════════════════════════════════
        WEATHERLIGHT v6.1.2 PIN REFERENCE
═══════════════════════════════════════════════════
ESP32-C6 GPIO PINOUT:
  GPIO2  → LED Data (via 330Ω + Pixel Boost)
  GPIO3  → PIR Sensor #1 (OUT pin)
  GPIO4  → PIR Sensor #2 (OUT pin)
  5V     → Power input from PSU
  GND    → Ground (common with PSU)
  3.3V   → PIR sensors VCC (both)

LED STRIP (150 LEDs, 5m, 30 LED/m):
  5V     ← PSU (18 AWG wire)
  GND    ← PSU (18 AWG wire)
  DATA   ← Pixel Boost OUT (22 AWG wire)
  Cap    ← 1000µF AT INPUT (soldered to pads!)

PIR SENSORS (AM312):
  VCC    ← ESP32 3.3V (red wire)
  OUT    → ESP32 GPIO3 or GPIO4 (yellow wire)
  GND    ← ESP32 GND (black wire)

PIXEL BOOST:
  LV     ← ESP32 3.3V
  GND    ← ESP32 GND
  IN     ← ESP32 GPIO2 (via 330Ω resistor!)
  HV     ← PSU 5V
  GND    ← PSU GND
  OUT    → LED Strip DATA

POWER:
  PSU: 5V 20A (100W)
  Max current: ~9.5A (150 LEDs + ESP32 + PIRs)
  Safety margin: 52% (10.5A spare capacity)
═══════════════════════════════════════════════════
```

---

## 💡 Tips & Tricks

### For Best Results

1. **Use aluminum channel** for LED strip mounting
   - Provides heatsink for LEDs
   - Protects strip from damage
   - Professional appearance

2. **Solder all connections** (don't rely on connectors for power)
   - Lower resistance = less voltage drop
   - More reliable long-term
   - Use heat shrink for insulation

3. **Star ground topology** (all grounds to single point at PSU)
   - Prevents ground loops
   - Reduces noise in data signal
   - More stable operation

4. **Short data wire** (Pixel Boost to strip <30cm)
   - Reduces signal degradation
   - More reliable data transmission
   - Less susceptible to noise

5. **Test incrementally** (don't wire everything at once)
   - Wire PSU → ESP32, test
   - Add Pixel Boost, test
   - Add LED strip, test
   - Add PIRs, test
   - Easier to diagnose problems

---

**Diagram Version**: 6.1.2 (CORRECTED)  
**Last Updated**: December 2024  
**Hardware**: ESP32-C6 + 150 LEDs + 2 PIRs  
**Status**: ✅ Verified with actual sketch  

---

🔧 **Questions?** Open an issue on GitHub  
⚡ **Safety First!** Always disconnect power before working on wiring  
📸 **Share Your Build!** We'd love to see your WeatherLight installation!

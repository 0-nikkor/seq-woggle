# Wiring Schematic

All connections for Seq/Woggle V4.8.  
No PCB required — build on perfboard or stripboard.

## Power

```
USB-C power bank ── USB-C port on ESP32-C3 SuperMini
```

The ESP32-C3 SuperMini has an onboard LDO (3.3V). No external regulator needed.  
The 5V VBUS pin is available for the LCD.

## CV Output (3.5mm jack — CV)

```
GPIO 2 ──── R 1kΩ ────┬──── CV OUT tip
                      │
                    C 100nF
                      │
                     GND ──── CV OUT sleeve
```

Cut-off frequency ≈ 1.6 kHz (R=1kΩ, C=100nF).  
For slower CV / pitch use, increase C to 10µF → Fc ≈ 16 Hz.

## Clock Output (3.5mm jack — CLOCK)

```
GPIO 21 ──── CLOCK OUT tip
GND     ──── CLOCK OUT sleeve
```

## Burst Output (3.5mm jack — BURST)

```
GPIO 3  ──── BURST OUT tip
GND     ──── BURST OUT sleeve
```

## Encoder KY-040

```
GPIO 4  ──── CLK
GPIO 5  ──── DT
GPIO 6  ──── SW
3.3V    ──── VCC
GND     ──── GND
```

INPUT_PULLUP is enabled in firmware. The KY-040 module has onboard pull-ups — no extras needed.

## LCD 16×2 I2C (PCF8574 backpack)

```
GPIO 8  ──── SDA
GPIO 9  ──── SCL
5V      ──── VCC  (ESP32 VBUS pin)
GND     ──── GND
```

> **Note:** If the LCD shows garbled characters, add 4.7kΩ pull-ups from SDA and SCL to 3.3V.

## Decoupling capacitors (solder on perfboard)

| Cap | Location |
|-----|----------|
| 10µF electrolytic | Across 5V VBUS and GND |
| 10µF electrolytic | Across 3.3V and GND |
| 100nF ceramic | Directly on ESP32 VCC and GND pins |

## Output voltage notes

- CV, Clock and Burst outputs are **3.3V logic**.
- Most Eurorack and semi-modular modules accept 3.3V gates.
- If a destination module requires 5V, add a level shifter (BSS138 or 74AHCT125).

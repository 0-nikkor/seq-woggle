# Seq / Woggle

**Version 4.8** · Semi-modular generative CV and gate module · ESP32-C3 SuperMini · USB-C powered

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Platform: ESP32-C3](https://img.shields.io/badge/Platform-ESP32--C3-red.svg)](https://www.espressif.com/en/products/socs/esp32-c3)

---

## What is this?

**Seq/Woggle** is a dual-mode generative music module built on an ESP32-C3 SuperMini, housed in a small cardboard or wooden box and powered by any USB-C power bank. It produces three outputs:

| Output | Jack | Description |
|--------|------|-------------|
| **CV** | 3.5mm mono | Quantized pitch/modulation voltage, 0–3.3V |
| **Clock** | 3.5mm mono | Main gate / clock pulse |
| **Burst** | 3.5mm mono | Euclidean gate (Seq) or random burst (Woggle) |

Two modes are switchable at any time without interrupting output:

- **Seq** — probabilistic step sequencer with quantized CV, swing, jitter, lock phrase memory, and a Euclidean gate pattern with rotation
- **Woggle** — organic random voltage generator with stepped/smooth/woggle CV layers, lag, burst engine, and 9 factory presets

A single rotary encoder with push button navigates all parameters. A 16×2 I2C LCD shows the current mode and value. All settings are saved automatically to internal flash.

---

## Quick start

1. Wire the components following `hardware/wiring.md`
2. Flash `firmware/SeqWoggle_v48/SeqWoggle_v48.ino` via Arduino IDE
3. Power from a USB-C power bank
4. Plug 3.5mm cables and patch

---

## Repository structure

```
seq-woggle/
├── firmware/
│   └── SeqWoggle_v48/
│       └── SeqWoggle_v48.ino       # Full Arduino sketch v4.8
├── hardware/
│   ├── wiring.md                   # Connection schematic (text)
│   ├── bom.md                      # Bill of materials with links
│   └── panel_layout.md             # Suggested enclosure layout
├── docs/
│   ├── user_manual.md              # Full user manual (EN)
│   ├── parameters.md               # Parameter reference (EN)
│   ├── presets.md                  # Woggle preset descriptions
│   └── AGENTS.md                   # AI assistant context file
├── .github/
│   └── ISSUE_TEMPLATE.md
├── LICENSE                         # GPL v3 (firmware) + CC BY-SA 4.0 (docs)
├── CONTRIBUTING.md
└── README.md
```

---

## Hardware

- **MCU**: ESP32-C3 SuperMini (~$2, AliExpress)
- **Display**: LCD 16×2 I2C with PCF8574 backpack
- **Input**: Rotary encoder KY-040 with push button
- **Outputs**: 3× 3.5mm mono jack PJ301M
- **Power**: USB-C → any power bank, no additional PSU needed
- **Enclosure**: cardboard prototype box or small wooden box
- **Estimated build cost**: ~$14–18 USD total

See [`hardware/bom.md`](hardware/bom.md) for the full parts list with AliExpress links.

---

## Firmware

Written in C++ for Arduino / ESP32 Arduino Core ≥ 3.0.

**Dependencies:**
- [hd44780](https://github.com/duinoWitchery/hd44780) by Bill Perry
- ESP32 Arduino Core ≥ 3.0.0

**Key firmware features:**
- Non-blocking timing with `millis()` / `micros()`
- Hardware RNG via `esp_random()`
- New `ledcAttach()` PWM API (ESP-IDF v5 compatible)
- Lazy NVS save (1.5s debounce after last edit)

---

## CV output and PWM freq

The CV output is a 10-bit PWM signal filtered through a 1kΩ + 100nF RC network.
The **PWM FREQ** parameter is both a technical and expressive control:

- **High freq** → less ripple → clean stable pitch CV
- **Lower freq** → more ripple → micro-movement, grain, analogue texture

---

## Documentation (PDF)

Pre-built PDFs are available in the [Releases](../../releases) section:

| Document | Description |
|----------|-------------|
| `SeqWoggle_V48_UserManual.pdf` | Full user manual, 7 chapters |
| `SeqWoggle_V48_UserRef.pdf` | Quick reference card, all parameters |
| `SeqWoggle_V48_BuildGuide.pdf` | DIY build guide, BOM, wiring, assembly |
| `AGENTS_SeqWoggle_v4.8.pdf` | AI context document |
| `AGENTS_SeqWoggle_v4.8_developer.pdf` | Developer-oriented AI context |

---

## License

- **Firmware** (all `.ino` and `.cpp` files): [GNU GPL v3](LICENSE)
- **Documentation, schematics, BOM, guides**: [Creative Commons BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

You are free to build, modify, share and sell derivative works under the same license terms.  
Attribution: **Seq/Woggle by [your name or handle]**

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Issues, bug reports and pull requests are welcome.

---

## Acknowledgements

Inspired by the Make Noise Wogglebug and the tradition of generative Eurorack modules.  
Built with Arduino, ESP32, and a lot of patch cables.

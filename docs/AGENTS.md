# AGENTS.md — Seq/Woggle V4.8

Context file for AI coding assistants working on this codebase.

## Project overview

Dual-mode generative music module on ESP32-C3 SuperMini.
- **Seq**: quantized probabilistic step sequencer with Euclidean gate
- **Woggle**: organic random CV generator with burst engine

## Hardware target

| Block | Detail |
|-------|--------|
| MCU | ESP32-C3 SuperMini, RISC-V single-core 160MHz, 4MB flash |
| Display | LCD 16×2 I2C, PCF8574 expander, library: hd44780_I2Cexp |
| Input | 1 rotary encoder + push button |
| CV out | GPIO2 PWM 10-bit, filtered RC, 0–3.3V |
| Clock out | GPIO21 |
| Burst out | GPIO3 |
| Encoder CLK | GPIO4 |
| Encoder DT | GPIO5 |
| Encoder SW | GPIO6 |
| LCD SDA | GPIO8 |
| LCD SCL | GPIO9 |

## Architecture

Non-blocking loop pattern:

```
loop()
  readEncoderStep()
  handleButton()
  if Seq: serviceSequencer()
  if Woggle: serviceWoggle()
  if pendingSave and timeout: save all
  if lcd refresh due: updateLCD()
```

## Key function map

| Function | Role |
|----------|------|
| readEncoderStep() | Quadrature decode with 4-bit lookup |
| handleButton() | Debounce, short/long press |
| applyEncoderDelta*() | Route changes to Seq or Woggle params |
| writeQuantizedSample() | Pick quantized note, write PWM |
| serviceSequencer() | Seq runtime engine |
| generateWoggleStep() | Stepped/smooth/woggle CV |
| serviceWoggle() | Woggle runtime engine |
| serviceBurstOut() | Burst pulse timing |
| updateLCD() | Render display |
| save* / load* | Versioned NVS persistence |
| onProgramChanged() | Mode switch reset |

## Coding rules

- No `delay()` — all timing via `millis()` / `micros()`
- Use `esp_random()` — never `random()`
- PWM API: `ledcAttach()` / `ledcWrite()` / `ledcChangeFrequency()` (ESP-IDF v5)
- New parameter: enum → modeName() → valueText() → applyEncoderDelta() → save/load
- NVS namespaces: `global48`, `seq48`, `wog48` — bump suffix on breaking changes
- Save is lazy: 1500ms debounce after last change

## Non-blocking timing pattern

```cpp
// Raise signal
riseTime = millis();
duration = calc();
digitalWrite(PIN, HIGH);

// Fall check (every loop)
if (high && millis() - riseTime >= duration)
    digitalWrite(PIN, LOW);
```

## CV pitch formula

```
adj  = (note/12)*12 + ((note%12) + transpose + 12) % 12
duty = (adj / tuneFactor) * PWM_MAX
```

## Euclidean gate with rotation

```
rpos = (pos + rot) % len
hit  = (rpos * hits % len) < hits
```

# Parameter Reference — Seq / Woggle V4.8

Navigation: short press on encoder advances to the next parameter.  
At **PROGRAM**, rotate to switch between Seq and Woggle.

---

## Sequencer Parameters

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| TEMPO | 60ms – 60s | 240ms | Base step duration |
| PWM FREQ | 48 – 20kHz | 20kHz | CV carrier frequency. Lower = more ripple = more expressive texture |
| SWING | 0.00 – 0.35 | 0.12 | Groove amount. Alternates shorter/longer steps |
| JITTER | 0 – 50% | 5% | Random timing variation per step |
| RANGE | 1 – 40 | 12 | Note span in semitones |
| SCALE | 0 – 19 | 0 | Quantisation scale (see scale table) |
| TRANSPOSE | -11 – +11 | 0 | Semitone transposition |
| MUTE | 0 – 100% | 0% | Probability of suppressing the main gate |
| LOCK LEN | 0 – 128 | 0 | Phrase loop length. 0 = always new random |
| LOCK PROB | 0 – 100% | 100% | Chance a loop note is mutated each cycle |
| GATE LEN | 0 / 5–95% | 5% | Main gate duration. 0 = random 5–95% |
| EUC HITS | 0 – eLen | 0 | Euclidean hits on BURST output |
| EUC ROT | 0 – eLen-1 | 0 | Euclidean pattern phase rotation |
| TUNE | 35.0 – 39.6 | 39.6 | V/oct calibration factor |

---

## Woggle Parameters

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| PRESET | 1 – 9 | 2 | Select factory preset (long press to load) |
| RATE | 35 – 5000ms | 220ms | Internal clock speed |
| CHAOS | 0 – 100% | 60% | Movement intensity and burst density |
| B.PROB | 0 – 100% | 45% | Probability of burst starting each tick |
| B.MIN | 1 – 16 | 2 | Minimum burst pulse count |
| B.MAX | 1 – 16 | 7 | Maximum burst pulse count |
| B.SPRD | 0 – 100% | 55% | Spread of spacing between burst pulses |
| LAG | 0 – 100% | 42% | Smooth branch inertia |
| MIX | 0 – 100% | 58% | Blend stepped ↔ smooth CV |
| JIT | 0 – 50% | 10% | Jitter on internal clock |
| PULSE | 500 – 20000µs | 2200µs | Burst pulse width |
| PWM | 1 – 30kHz | 20kHz | CV carrier frequency |

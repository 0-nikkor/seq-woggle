# Contributing to Seq / Woggle

Thank you for your interest in contributing!

## Ways to contribute

- **Bug reports**: open an Issue describing the problem, firmware version, and hardware setup
- **Feature requests**: open an Issue with the label `enhancement`
- **Code contributions**: fork the repo, create a branch, submit a Pull Request
- **Documentation**: corrections, translations, additional patch ideas
- **Build logs**: share your enclosure photos and patches in Discussions

## Code style

- No `delay()` — all timing is non-blocking with `millis()` / `micros()`
- Use `esp_random()` for all random values (hardware RNG)
- New parameters must be added to: `EditMode` enum, `modeName()`, `valueText()`, `applyEncoderDelta*()`, `save*Settings()`, `load*Settings()`
- PWM API: use `ledcAttach()` / `ledcWrite()` / `ledcChangeFrequency()` — not the old `ledcSetup()`
- NVS namespace: bump version suffix (e.g. `seq48` → `seq49`) if breaking NVS compatibility

## Pull Request checklist

- [ ] Code compiles without warnings on ESP32 Arduino Core ≥ 3.0
- [ ] No blocking calls in `loop()`
- [ ] New parameters are persistent (save/load)
- [ ] README and parameter docs updated if needed

## Development context

See `docs/AGENTS.md` for a full description of the codebase, useful when working with AI coding assistants.

# Firmware

## File

`SeqWoggle_v48/SeqWoggle_v48.ino` — main Arduino sketch

## Requirements

- Arduino IDE 2.x or PlatformIO
- ESP32 Arduino Core **≥ 3.0.0**
- Library: **hd44780** by Bill Perry (install via Library Manager)

## Board settings (Arduino IDE)

| Setting | Value |
|---------|-------|
| Board | ESP32C3 Dev Module |
| Upload speed | 921600 |
| Flash mode | DIO |
| Flash frequency | 80MHz |
| Partition scheme | Default 4MB |

## Flashing

1. Connect ESP32-C3 SuperMini via USB-C data cable
2. Select the correct COM/USB port in IDE
3. Click Upload
4. On first boot: LCD shows current mode, all params at default

## Notes

- Uses `ledcAttach()` API — do not use deprecated `ledcSetup()` / `ledcAttachPin()`
- Hardware RNG: `esp_random()` only
- No blocking calls allowed in `loop()`

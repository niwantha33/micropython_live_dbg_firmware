# MicroPython Live Debugger — Firmware Builds

Auto-built firmware for the [MicroPython Live Debugger](https://github.com/niwantha33/micropython_live_debugger).

**Do not edit files manually.** A GitHub Actions workflow in the source repo rebuilds and pushes here whenever the patches change.

## Layout

| Folder    | Board                          | Status            |
|-----------|--------------------------------|-------------------|
| Pico2w/   | Raspberry Pi Pico 2 W (RP2350) | ✅ Active         |
| Picow/    | Raspberry Pi Pico W (RP2040)   | ⏳ Coming soon    |
| Pico/     | Raspberry Pi Pico (RP2040)     | ⏳ Coming soon    |
| ESP32S3/  | Espressif ESP32-S3             | ⏳ v0.2           |
| ESP32S2/  | Espressif ESP32-S2             | ⏳ v0.2           |
| ESP32C3/  | Espressif ESP32-C3             | ⏳ Later          |

Each folder contains the latest binary + a `VERSION.txt` with the source commit hash.

## Flashing manually

**Pico family (UF2):** hold BOOTSEL, plug USB, drag `firmware.uf2` from the relevant folder onto the mounted drive.

**ESP32 (esptool):**
```
esptool.py --chip esp32s3 -p COM7 write_flash 0 ESP32S3/firmware.bin
```

**Easier:** use the **Flash Debug Firmware** command in the MicroPython Studio VS Code extension — it auto-downloads from this repo.

## License

MIT — see the [source repo](https://github.com/niwantha33/micropython_live_debugger/blob/main/LICENSE).

# Test firmware downloads

These files are **automatically rebuilt candidates**; a CI build does not mean hardware validation. For a pinned release use the [official download page](../README.md).

| Board | Latest candidate |
| --- | --- |
| Pico 2 W | [UF2](Pico2w/firmware_pico2_w.uf2?raw=1) |
| Pico 2 | [UF2](Pico2/firmware_pico2.uf2?raw=1) |
| Pico W | [UF2](Picow/firmware_pico_w.uf2?raw=1) |
| Pico | [UF2](Pico/firmware_pico.uf2?raw=1) |
| ESP32-S3 | [Preview release](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/tag/v2.6.0-esp32s3-preview) · [latest candidate files](ESP32S3/) |

[Build versions and checksums](LATEST.json) · [CI history](https://github.com/niwantha33/micropython_live_dbg_firmware/actions/workflows/weekly-candidate-builds.yml)

Pico: match the exact board and back up user files before entering BOOTSEL. ESP32-S3: use Serial/JTAG for REPL/upload and native USB for debugger. Read the preview flashing instructions before installation. ESP32-C3 has **no debugger release**.

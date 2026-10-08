# MicroPython Studio — Debugger Firmware

**Find your board, download the firmware, then debug in VS Code.**

## Latest test builds — Pico / ESP32-S3

**[Open easy firmware downloads →](TestBuilds/README.md)**

| Board | Latest experimental firmware |
| --- | --- |
| **Pico 2 W** | [Download UF2](TestBuilds/Pico2w/firmware_pico2_w.uf2?raw=1) |
| Pico 2 | [Download UF2](TestBuilds/Pico2/firmware_pico2.uf2?raw=1) |
| Pico W | [Download UF2](TestBuilds/Picow/firmware_pico_w.uf2?raw=1) |
| Pico | [Download UF2](TestBuilds/Pico/firmware_pico.uf2?raw=1) |
| ESP32-S3 | [Download test firmware](TestBuilds/ESP32S3/firmware_esp32s3.bin?raw=1) · [flash instructions](TestBuilds/README.md) |

**Important:** These are **unvalidated test images**, not stable releases. Check the exact board before flashing. ESP32-C3 and ESP32-S2 debugger images are not available yet.

## Current stable/legacy firmware

Existing released files are in [Pico 2 W](Pico2w/), [Pico 2](Pico2/), [Pico W](Picow/), [Pico](Pico/), and [ESP32-S3 legacy](ESP32S3/). The published ESP32-S3 image in this stable/legacy folder is **not** the newer two-USB test build.

## How updates work

- **Test firmware:** every Monday at **04:53 UTC**; all four frozen Pico builds and ESP32-S3 must pass CI. The workflow updates **only** `TestBuilds/` on GitHub, with source versions and SHA256 hashes. [Build history](https://github.com/niwantha33/micropython_live_dbg_firmware/actions/workflows/weekly-candidate-builds.yml).
- **Stable Pico firmware:** every Monday at **03:17 UTC**; stable downloads are replaced **only** after an explicitly approved source commit passes the build checks. [Stable workflow](https://github.com/niwantha33/micropython_live_dbg_firmware/actions/workflows/sync-debugger-firmware.yml).

For requirements, validation gates and planned board support, see [ROADMAP](ROADMAP.md) and the [firmware source](https://github.com/niwantha33/micropython_live_debugger). Studio extension: [install from VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=niwantha33.micropython-studio).

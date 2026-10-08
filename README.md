# MicroPython Studio — Debugger Firmware

**Find your board, download the firmware, then debug in VS Code.**

## Official v2.6.0 — Pico W frozen debugger

**[Download Raspberry Pi Pico W v2.6.0 UF2](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/download/v2.6.0/micropython-studio-picow-debugger-v2.6.0.uf2)**

[Release notes, version metadata and checksum](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/tag/v2.6.0)

Tested on a physical **Raspberry Pi Pico W** without separately uploading `boot.py`, `dbgref.py` or `trace_pump.py`. One USB cable: CDC0 for REPL/upload, CDC1 for the debugger. The Pico W firmware's full long-duration stability qualification remains ongoing.

**Not for Pico, Pico 2, Pico 2 W, ESP32-S3 or ESP32-C3.** The old `Picow/` folder retains a legacy binary; use the **v2.6.0 Release asset** for the new frozen debugger.


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

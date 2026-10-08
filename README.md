# MicroPython Studio — Debugger Firmware

Choose your board. **Only flash firmware built for your exact model.**

## Releases

| Board | Firmware | Status |
| --- | --- | --- |
| **Raspberry Pi Pico W** | [**Download v2.6.0 UF2**](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/download/v2.6.0/micropython-studio-picow-debugger-v2.6.0.uf2) | Hardware-tested frozen debugger |
| **ESP32-S3** | [**Download v2.6.0 Preview**](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/tag/v2.6.0-esp32s3-preview) | Preview — long RTA/reset test pending |

The Pico W needs **no separate debugger Python files**. Its USB CDC0 is REPL/upload; CDC1 is debugger.

ESP32-S3 requires **two USB connections**: Serial/JTAG for REPL/upload and native USB for debugging. [Read the flashing instructions](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/download/v2.6.0-esp32s3-preview/ESP32S3-READ-ME-FIRST.txt) before installing the preview.

## Other boards

[**Pico / Pico 2 / Pico W / Pico 2 W / ESP32-S3 test builds**](TestBuilds/README.md)

Other Pico frozen-debugger images still need their own hardware checks. **ESP32-C3/S2 debugger firmware is not available.** Do not use an S3 image on a C3.

Previously published files remain in the legacy board folders; they are not necessarily the newest debugger images.

[MicroPython Studio v2.6.0 VSIX](https://github.com/niwantha33/micropython-studio/releases/download/v2.6.0/micropython-studio-2.6.0.vsix) · [Source code](https://github.com/niwantha33/micropython_live_debugger) · [Roadmap](ROADMAP.md)

Test candidates are rebuilt weekly; releases are pinned and do not change when new candidates are built.

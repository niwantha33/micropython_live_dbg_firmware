# MicroPython Studio — Debugger Firmware

Choose your board. **Only flash firmware built for your exact model.**

## Firmware distribution and Monday safety policy

**This repository is the sole public firmware download location.** Development
source and experimental pull requests in `micropython_live_debugger` are build
inputs only; MicroPython Studio must never link directly to development-branch
images or build artifacts as approved releases.

- **Monday 03:17 UTC:** Build four Pico boards from the immutable
  `.github/approved-pico-source.sha`. Update the stable Pico directories only
  if that source was separately approved for hardware and its SHA changed.
- **Monday 04:53 UTC:** Build four integrated frozen Pico/RTA test candidates
  plus ESP32-S3 from *pinned source commit SHAs*. Verify each build, board and
  checksum; publish all five to `TestBuilds/` only when every job succeeds.
- A manual run, pull request or workflow-file push is **build-only**: it cannot
  publish or replace firmware downloads.
- The historical v2.6.0 Pico W release and ESP32-S3 preview release are
  immutable. They never point to `TestBuilds` or track a moving branch.
- When tests fail, preserve all existing published files and the previous
  `TestBuilds/LATEST.json`. Revert an accidental candidate commit instead of
  overwriting the approved release.
- For ESP32-S3, retain the bootloader, partition table, firmware and
  board-specific flashing instructions together. A raw .bin alone is not
  sufficient guidance.

**Hardware caution:** CI compile success is not proof of Windows CDC
enumeration, USB reconnection, correct boot.py migration or 30-second RTA
stability. Test candidates remain explicitly UNVALIDATED until board checks.

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

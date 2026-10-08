# MicroPython Live Debugger — firmware downloads and validation

Firmware distribution for [MicroPython Live Debugger](https://github.com/niwantha33/micropython_live_debugger) and the [MicroPython Studio VS Code extension](https://github.com/niwantha33/micropython-studio).

> **Important — 8 October 2026:** Files already in this repository are not necessarily the newest **test** firmware. **Do not mistake a successful GitHub Actions build for hardware validation.** Do not flash an image from another board family. This update changes **documentation only**; no firmware binaries have been replaced.

## Current published files

| Path | Board | What's actually present / current validation |
| --- | --- | --- |
| [Pico2w/](Pico2w/) | Raspberry Pi Pico 2 W | Published, pre-frozen debugger UF2 from source `e79fab2a` (2026-10-07). Older Pico 2 W debugger workflow has been used successfully on hardware. |
| [Pico/](Pico/) | Raspberry Pi Pico | Published pre-frozen UF2 from `e79fab2a`; do not claim new no-upload workflow validated. |
| [Picow/](Picow/) | Raspberry Pi Pico W | Published pre-frozen UF2 from `e79fab2a`; do not claim new no-upload workflow validated. |
| [Pico2/](Pico2/) | Raspberry Pi Pico 2 | Published pre-frozen UF2 from `e79fab2a`; do not claim new no-upload workflow validated. |
| [ESP32S3/](ESP32S3/) | ESP32-S3 | **Legacy April 2026 image** (`ESP-IDF v5.3`, patches `0001–0016`). It is **not** the Oct 2026 two-USB-connector debugger image successfully tested with breakpoints. Not approved as the new debugger release. [Details](ESP32S3/README.md). |
| [ESP32S2/](ESP32S2/) | ESP32-S2 | No published debugger image; placeholder only. |
| [ESP32C3/](ESP32C3/) | ESP32-C3 | No published debugger image; **hardware/transport feasibility only**. [C3 notes](ESP32C3/README.md). |

Each current **Pico** folder has a UF2 and `VERSION.txt` with the source commit, board and hash. The legacy S3 VERSION format is different and must not be interpreted as certification.

## New self-contained firmware — test only, not in this repository

The target user experience for **new frozen-debugger firmware** is:

1. Flash the appropriate **board-specific debugger firmware once**.
2. Use the normal working MicroPython REPL/upload COM port.
3. Select **Start Debug → Connect only** and use the **separate debugger COM**.
4. Set a breakpoint, inspect variables, continue; use RTA after stability checks.

No separate `boot.py`, `dbgref.py`, `trace_pump.py` upload is required **only for the new frozen-debugger images**. Older published Pico UF2 images can still require Studio's *Legacy Pico setup* file-upload option. Never overwrite unrelated user boot files without permission.

| Candidate | Evidence | Location, test only | Outstanding |
| --- | --- | --- | --- |
| Pico / Pico W / Pico 2 / Pico 2 W frozen candidates | **Four out of four** CI builds passed | [Actions run 37741930577](https://github.com/niwantha33/micropython_live_debugger/actions/runs/37741930577), [draft PR #6](https://github.com/niwantha33/micropython_live_debugger/pull/6) | Device-specific REPL/CDC enumeration, upload, breakpoints, resets, 30-second RTA |
| ESP32-S3 Serial REPL + native debugger | CI passed; physical Serial REPL and native debugger breakpoint/short RTA observed | [Actions run 37687220777](https://github.com/niwantha33/micropython_live_debugger/actions/runs/37687220777), [PR #4](https://github.com/niwantha33/micropython_live_debugger/pull/4) | 30-second RTA/watchdog stability, resets/reconnect, full qualification |
| ESP32-C3 | No debugger build or hardware acceptance yet | [Feasibility plan](https://github.com/niwantha33/micropython_live_debugger/tree/feature/esp32-c3-feasibility-v1/esp32c3) | Confirm actual board and alternate transport first |
| Studio Connect-only extension | CI lint/tests and VSIX build passed | [draft PR #52](https://github.com/niwantha33/micropython-studio/pull/52) | Match and test the selected board firmware |

CI artifacts are **temporary** and can expire; **they are not the stable firmware download channel**. Do not copy test images into the folders above until board-specific hardware acceptance and explicit release approval.

### Physical USB mapping

- **Pico family (frozen test UF2):** one USB cable; `CDC0` = REPL/file upload, `CDC1` = debugger/RTA.
- **ESP32-S3 tested board:** physical **Serial/JTAG USB** = REPL/file upload; separate physical **native USB** = debugger/RTA. Windows COM numbers may change.
- **ESP32-C3:** integrated USB Serial/JTAG is a *fixed-function* serial/JTAG device, **not the ESP32-S3 native USB OTG**. No automatic dual-CDC clone; select a separate UART or other transport only after inspecting the actual board. [Official Espressif documentation](https://docs.espressif.com/projects/esp-idf/en/v5.5/esp32c3/api-guides/usb-serial-jtag-console.html).

**RTA note:** `Observed VM %` is the share of captured *exclusive MicroPython execution-segment elapsed time*, not CPU utilization. `Total` reports inclusive elapsed time. Sleep/native waiting is not separately measured; unresolved function pointers are not proof of CPU saturation.

## Current published Pico UF2 installation (legacy workflow)

For an **existing released Pico UF2**, select the file matching your exact board. Hold BOOTSEL while connecting its USB cable; copy the UF2 onto the device drive. Existing firmware builds may need the Studio *Legacy Pico setup* upload to install debugger Python helpers; use it only with informed consent and never on ESP32-S3 or on the new frozen Pico candidates.

The new firmware candidates have different instructions in [Pico test guide](https://github.com/niwantha33/micropython_live_debugger/blob/feature/pico-frozen-debugger-v1/rp2/README.md) and [S3 test guide](https://github.com/niwantha33/micropython_live_debugger/blob/feature/esp32-s3-debugger-v1/esp32/README.md). They must be individually validated before replacing a release.

## Source and automatic synchronization

The [source repository](https://github.com/niwantha33/micropython_live_debugger) remains authoritative. This repository now runs [weekly validated Pico firmware builds](.github/workflows/sync-debugger-firmware.yml) **every Monday at 03:17 UTC** and on manual dispatch. Each run builds all **four Pico-family** UF2s from the explicit hardware-approved SHA in [`.github/approved-pico-source.sha`](.github/approved-pico-source.sha), checks compiled debugger APIs, and uploads testable CI artifacts. A release to `Pico/`, `Picow/`, `Pico2/`, `Pico2w/` occurs **only when the approved source SHA changes** and every build/checksum check succeeds. The existing approved SHA is the source of the already published legacy Pico images, not the unvalidated frozen candidate. If no new approved source exists, the weekly builds still run but the public binary files stay untouched.

The prior 30-minute source-`main` poll was removed: documentation commits and development branches cannot silently replace stable firmware. Frozen Pico/ESP32-S3/ESP32-C3 work is **not** auto-promoted. To approve a later release, first complete the exact-board hardware checklist in [ROADMAP.md](ROADMAP.md), then explicitly update the approval SHA in a reviewed commit.

See [ROADMAP.md](ROADMAP.md) for the validation/publishing gate. Do not replace manually the binary assets or their `VERSION.txt` files outside the approved release workflow.

## License

MIT — see the [debugger source repository](https://github.com/niwantha33/micropython_live_debugger/blob/main/LICENSE).

## Weekly experimental firmware builds (never auto-published)

A second [GitHub Actions workflow](.github/workflows/weekly-candidate-builds.yml)
runs **Mondays at 04:53 UTC**, or manually, after the approved Pico build.
It independently builds the **four frozen no-upload Pico candidates** from
`feature/pico-frozen-debugger-v1` and the **ESP32-S3 native-debugger candidate**
from `feature/esp32-s3-debugger-v1`. The artifacts are visibly marked
`weekly-candidate-*-UNVALIDATED` and retained for 14 days.

**These five firmware images are test artifacts only.** This workflow has
`contents: read` permission and contains **no publish or push step**;
none are copied into the stable board folders automatically.

ESP32-C3 is excluded until its fixed-function native USB Serial/JTAG plus
CH340 bridge solution is implemented, compiled and bench-tested. The supplied
board photo matches a dual USB-C C3-MINI-1 carrier, but its actual connector
enumeration remains to be verified.

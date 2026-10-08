# Firmware publication roadmap — 8 October 2026

The **firmware source repository** is [micropython_live_debugger](https://github.com/niwantha33/micropython_live_debugger).
This repository is a **binary distribution channel**, not the place for
untested developer firmware. Preserve known-working Pico downloads.

## Board qualification matrix

| Family | CI | Bench proof | Release decision |
| --- | --- | --- | --- |
| Pico 2 W current published UF2 | Existing published build | Previous working breakpoint/RTA workflow | Keep currently published UF2 until successor accepted |
| Pico, Pico W, Pico 2, Pico 2 W **new frozen UF2s** | **All 4 pass** ([run 37741930577](https://github.com/niwantha33/micropython_live_debugger/actions/runs/37741930577)) | **Pending new-UF2 hardware tests** | NOT released |
| ESP32-S3 **Oct 2026 debugger** | **Pass** ([run 37687220777](https://github.com/niwantha33/micropython_live_debugger/actions/runs/37687220777)) | Serial REPL, native debug COM, breakpoint, short RTA proved; watchdog/reset and 30s test pending | NOT released; old Apr 2026 S3 image is legacy |
| ESP32-S2 | No current candidate | Not tested | NOT released |
| ESP32-C3 | No current candidate | Board/transport inspection pending | NOT released |

## Release criteria for each exact board and firmware identity

- [ ] Full CI build with verified `dbg` exports, pinned MicroPython revision,
      exact `VERSION.txt`, and SHA256 digest.
- [ ] Cold boot and stable `>>>` REPL on the correct port.
- [ ] Project upload/download works repeatedly without restarting or deleting
      user files.
- [ ] Separate debugger transport connects without uploading helper scripts.
- [ ] Breakpoint set/hit/remove, Continue, step in/out/over, named locals and stack
      tested on physical hardware.
- [ ] RTA 30-second capture, OFF confirmation, and no USB disconnect/watchdog.
- [ ] Soft reset, power cycle, reconnect and recovery confirmed.
- [ ] Identify board-specific USB mapping, firmware version, and migration from
      any older filesystem `boot.py` without overwriting user content.
- [ ] Approved matching MicroPython Studio extension and release notes.
- [ ] Explicit approval to copy artifacts and update board-specific
      `VERSION.txt`. Never infer hardware compatibility from a compilation.

## Automation caution

[`sync-debugger-firmware.yml`](.github/workflows/sync-debugger-firmware.yml)
now builds Pico/Pico W/Pico 2/Pico 2 W **weekly, Monday at 03:17 UTC** and on
manual dispatch. It uses [`approved-pico-source.sha`](.github/approved-pico-source.sha)
rather than polling source `main`. All four builds and symbol checks run
every week; public Pico firmware folders are updated **only after** a new
hardware-approved source commit is explicitly entered and all four builds,
board ID checks and SHA256 verification succeed. A docs-only source change
does not trigger firmware promotion.

- [x] Replace unsafe 30-minute automatic source-`main` polling.
- [x] Pin published stable Pico source; retain legacy binaries until accepted.
- [x] Add automated full four-target weekly build and CI artifact upload.
- [x] Gate published firmware on approved source SHA and full-matrix success.
- [ ] Hardware-certify frozen Pico candidates before updating approval SHA.
- [ ] Certify ESP32-S3 and C3 separately and design board-specific release
      workflows if those versions are approved. They are not published weekly.

The supplied ESP32-C3 board photo visually matches a dual-USB-C C3-MINI-1
board (likely left fixed USB Serial/JTAG, right CH340 UART). This allows a
candidate **independent two-port** design, but physical COM mapping and
single-core debugger/watchdog testing are still outstanding.

### Related development

- [Pico frozen CI candidate / PR #6](https://github.com/niwantha33/micropython_live_debugger/pull/6).
- [ESP32-S3 hardware-validation / PR #4](https://github.com/niwantha33/micropython_live_debugger/pull/4).
- [ESP32-C3 feasibility branch](https://github.com/niwantha33/micropython_live_debugger/tree/feature/esp32-c3-feasibility-v1).
- [Studio frozen Connect-only / PR #52](https://github.com/niwantha33/micropython-studio/pull/52).

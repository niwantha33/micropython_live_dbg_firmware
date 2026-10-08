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
automatically polls the **source `main` SHA**, not a fingerprint of compiled
firmware inputs. If source `main` changes for documentation alone, the workflow
may rebuild and publish current Pico UF2s. This is an existing release-management
risk. Keep unvalidated changes on their isolated branches and improve the sync
gate before merging development candidates. The current sync matrix publishes
Pico, Pico W, Pico 2 and Pico 2 W, not S3/C3.

### Related development

- [Pico frozen CI candidate / PR #6](https://github.com/niwantha33/micropython_live_debugger/pull/6).
- [ESP32-S3 hardware-validation / PR #4](https://github.com/niwantha33/micropython_live_debugger/pull/4).
- [ESP32-C3 feasibility branch](https://github.com/niwantha33/micropython_live_debugger/tree/feature/esp32-c3-feasibility-v1).
- [Studio frozen Connect-only / PR #52](https://github.com/niwantha33/micropython-studio/pull/52).

# ESP32-S3 — legacy firmware in this folder

**Warning — 8 October 2026.** The files currently in this folder date from
**25 April 2026** (see [VERSION.txt](VERSION.txt)) and use
**ESP-IDF v5.3, MicroPython master + debugger patches 0001–0016, no PSRAM**.
They are **not** the newer Oct 2026 S3 debugger test image.

The newer S3 image from
[`feature/esp32-s3-debugger-v1`](https://github.com/niwantha33/micropython_live_debugger/tree/feature/esp32-s3-debugger-v1)
([PR #4](https://github.com/niwantha33/micropython_live_debugger/pull/4))
uses MicroPython pinned to `a129b2fba1`, ESP-IDF v5.5.5 and a split transport:

- Physical **Serial/JTAG connector** → working normal REPL/file-upload COM.
- Separate physical **native USB connector** → debugger/RTA COM.

A candidate image [passed compilation/CI](https://github.com/niwantha33/micropython_live_debugger/actions/runs/37687220777).
On the user's real S3 board a breakpoint was set/hit and a 3.17-second
RTA trace recorded 1,056 events. This is **partial hardware testing only**:
30-second RTA/watchdog stability, reset/reconnection and exact build identity
remain outstanding. Do **not** label the newer image production-ready.

**No binaries or `VERSION.txt` were overwritten by this documentation update.**
Do not confuse this legacy folder with the new hardware-test artifact.
Follow the [S3 beginner test guide](https://github.com/niwantha33/micropython_live_debugger/blob/feature/esp32-s3-debugger-v1/esp32/BEGINNER_TEST_GUIDE.md)
only when deliberately validating the new image; never upload Pico
`boot.py` or install `usb-device-cdc` via MIP on the new frozen build.

# ESP32-C3 — no debugger firmware published

**Status (2026-10-08): research / board identification only.**
This directory intentionally has **no flashable C3 debugger firmware**.

The ESP32-C3 has a fixed-function **USB Serial/JTAG** peripheral. Unlike
ESP32-S3 it does **not** have a configurable native USB OTG device controller
for Studio's second TinyUSB debugger CDC.

Reference: [Espressif USB Serial/JTAG guide](https://docs.espressif.com/projects/esp-idf/en/v5.5/esp32c3/api-guides/usb-serial-jtag-console.html).

**Do not flash** `ESP32S3/firmware.bin` to an ESP32-C3.

Next steps are documented in
[the isolated C3 feasibility branch](https://github.com/niwantha33/micropython_live_debugger/blob/feature/esp32-c3-feasibility-v1/esp32c3/README.md):
identify the exact board and its USB/UART interfaces, verify the REPL and file
upload, choose an independent debugger transport, then build a C3-only test
candidate. No C3 GPIO assignments or USB cable layout are assumed.

Neither binary publication nor support is promised until a board-specific,
30-second RTA/breakpoint/recovery validation passes.

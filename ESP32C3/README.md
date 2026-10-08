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

## User hardware identified from front photograph (8 October 2026)

The user's board visually matches the **dual USB-C ESP32-C3-MINI-1
development board** with RST/BOOT buttons, RGB LED and CH340-family bridge.
A matching annotated listing identifies **left USB-C as the C3 native
fixed-function USB Serial/JTAG** and **right USB-C as the CH340 USB-UART**.
This suggests an independent debugger COM may be possible without GPIO
wiring: right port = normal MicroPython UART REPL/upload, left port =
**potential C3-specific debugger CDC**.

This is a **visual match**, not electrical verification of the user's
exact board revision. Both Windows USB/COM enumerations and the working REPL
must be checked before firmware implementation. The C3 cannot use the S3
programmable TinyUSB dual-CDC approach; the native C3 serial/JTAG device has
to be serviced via a suitable target-specific driver without interfering
with USB logging/console.

Supporting photo reference:
https://nl.bestdealplus.com/product/47949195/Dual-Type-C-ESP32-C3-DevKitC-1-ESP32-C3-Wifi-Bluetooth-Compatibel-5-0-Mesh-Development-Board-Esp32-Draadloze-Module-Voor-Arduino

No ESP32-C3 firmware is released by the weekly Pico workflow. Only after
board-specific breakpoint/RTA/watchdog/recovery checks can C3 publication
be considered.

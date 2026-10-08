# ESP32-S3 legacy folder

This folder contains the older April 2026 image, **not** the dual-USB debugger released as a preview.

**[Download ESP32-S3 v2.6.0 Preview](https://github.com/niwantha33/micropython_live_dbg_firmware/releases/tag/v2.6.0-esp32s3-preview)**

The preview uses Serial/JTAG USB for REPL/upload and the separate native USB port for debugging. It has demonstrated real-device breakpoints and short RTA. **Long RTA, watchdog and reconnect acceptance are still pending.**

Read the preview's `ESP32S3-READ-ME-FIRST.txt` before flashing. Do not install Pico debugger files or the `usb-device-cdc` MIP package on the new frozen image. This folder's existing binary remains unchanged.

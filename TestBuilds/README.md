# Latest debugger firmware — TEST BUILDS

**Experimental firmware for hardware testing. Not yet approved as a stable release.**

Choose the **exact board**. The links below download firmware files directly from GitHub—no need to open Actions, find a run, or extract an artifact ZIP.

| Your board | Direct download |
| --- | --- |
| Raspberry Pi Pico 2 W | [Download Pico 2 W UF2](Pico2w/firmware_pico2_w.uf2?raw=1) |
| Raspberry Pi Pico 2 | [Download Pico 2 UF2](Pico2/firmware_pico2.uf2?raw=1) |
| Raspberry Pi Pico W | [Download Pico W UF2](Picow/firmware_pico_w.uf2?raw=1) |
| Raspberry Pi Pico | [Download Pico UF2](Pico/firmware_pico.uf2?raw=1) |
| ESP32-S3 | [Download ESP32-S3 firmware](ESP32S3/firmware_esp32s3.bin?raw=1) — [other required flash files](ESP32S3/) |

Each board folder contains its `VERSION.txt` (source revision, build time, SHA256). [Build manifest](LATEST.json) records the latest candidate versions.

**Pico:** use BOOTSEL and the UF2 for your exact model. The new frozen candidate has an independent debugger CDC port; old user-installed Studio `boot.py` can conflict. Back it up before testing; never delete unrelated user files.

**ESP32-S3:** use the [S3 flashing and dual-USB instructions](https://github.com/niwantha33/micropython_live_debugger/blob/feature/esp32-s3-debugger-v1/esp32/BEGINNER_TEST_GUIDE.md). Serial/JTAG USB is REPL/upload; native USB is debugger. Do not flash a raw .bin at an invented address.

**ESP32-C3:** no debugger firmware exists yet. Do **not** flash the S3 image.

New candidate images are copied here **automatically after all five CI builds and firmware checks pass**. Existing stable firmware directories are never overwritten by this test process. See the [stable release folders](../) and [hardware acceptance checklist](../ROADMAP.md).

# ESP32-A1S Audio Kit with ES8388

Tested on `esp-idf` 5.0.2. Should work with `esp-idf` 4.x.

Note that AC101 is not supported.

For `esp-adf`, NOT `arduino`. For `arduino`, use [arduino-audiokit](https://github.com/pschatzmann/arduino-audiokit/).

Note that `ESP32-A1S` boards from Ai Thinker are not maintained, have bugs in
the hardware and the software. The SDK the vendor provides is outdated. If you
don't have a brave soul, buy
[supported development boards](https://docs.espressif.com/projects/esp-adf/en/latest/get-started/)
from `espressif`.

## Tested features

* [x] Audio output from the speaker outputs (L/R,
  `examples/player/pipeline_http_mp3`, requires WiFi)
* [x] Keys (`examples/checks/check_board_buttons`)
* [ ] Headphone jack output and insertion detection
* [ ] Line-in jack input
* [ ] Microphones
* [ ] SD card

## Configuring

Follow the official [Get Started](https://docs.espressif.com/projects/esp-adf/en/latest/get-started/)
guide.

Choose an example under `$ADF_PATH/examples`, such as
`$ADF_PATH/examples/player/pipeline_http_mp3`.

```console
cd examples/player/pipeline_http_mp3
```

Run `idf.py menuconfig` and choose `Audio HAL` -> `ESP32-A1S Audio Kit (Rev.
B)`. If the audio does not work at all, try `ESP32-A1S Audio Kit (Rev A)
`.

Also make sure that SPIRAM is enabled by `CONFIG_SPIRAM`,
`CONFIG_SPIRAM_BOOT_INIT` and `CONFIG_SPIRAM_ALLOW_STACK_EXTERNAL_MEMORY`.
They are under `Component config` -> `ESP PSRAM` -> `Support for external,
SPI-connected RAM`.

Build and flash the example:

```console
idf.py build
idf.py flash monitor
```

## `esp-idf` v5.x

`esp-adf`, as of this writing, does not fully support `esp-idf` 5.x, yet. Run:

```console
cd $IDF_PATH
git apply $ADF_PATH/idf_patches/idf_v5.0_freertos.patch
```

## Links

* [Microphone and line-in issues](https://www.pschatzmann.ch/home/2021/12/15/the-ai-thinker-audiokit-audio-input-bug/#comment-1505).
  Inputs from a microphone and line-in are always mixed up due to a hardware bug.
* [A workaround](https://github.com/pschatzmann/arduino-audiokit/commit/9116e840a5e88724e06e1a0e50fed5a97d82ece4)
  for microphone issue in `arduino-audiokit`

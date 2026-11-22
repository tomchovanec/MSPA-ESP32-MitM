# MSpa Tribeca F-TR062W – local control

> **🚧 IN PROGRESS / NOT FINISHED — under development and not ready for normal use.**

[Česky](README.md) · [Documentation](docs/INDEX.md) · [Wiring proposal](docs/wiring/README.md)

This project aims to control the MSpa Tribeca **F-TR062W** locally using ESPHome and Home Assistant while keeping the original control panel functional. The target panel PCB is `M22W(T)-DB(WIFI) Rev2.0`. The intended solution does not use the MSpa cloud.

## Current status

- A passive ESP32-C6 capture on the green wire received `A5 06 2C D7` and `A5 08 00 AD` at 9600 baud, 8N1. `06 2C` corresponds to the **22 °C** displayed on the functioning panel.
- The owner measured red as +5 V and white as GND. The black-wire direction, actual signal levels and complete protocol compatibility remain unverified.
- An ESP32-WROOM-32U was damaged by reverse insertion. A replacement is awaited; check the socket and level converter before connecting it.
- Active two-way control and ESP32 failure behaviour have not been tested. The physical panel must remain usable; a hardware bypass is not yet designed or verified.

## Contents

- [Findings and proposed wiring](docs/wiring/README.md)
- [Passive ESP32-C6 test](docs/wiring/esp32-c6-pasivni-test.md) · [test YAML](esphome/mspa-c6-pasivni-test.yaml)
- [Experimental ESP32-WROOM-32U YAML](esphome/mspa-f-tr062w.yaml) · [configuration guide](docs/esphome-f-tr062w.cs-CZ.md)
- [Project status and next steps](docs/STAV.md)

**The controller configuration is experimental.** The current component may discard unrecognised panel frames and does not guarantee panel operation if the ESP32 fails. Do not rely on active control before verifying the wiring and communication. It does not replace spa safety features.

![F-TR062W control board](assets/images/f-tr062w-panel-pcb.jpg)

## Attribution and license

Derived from [EtienneESP32/MSPA-ESP32-EEDOMUS](https://github.com/EtienneESP32/MSPA-ESP32-EEDOMUS). The original copyright and [MIT license](LICENSE) remain in effect. The upstream project and documentation are available at that link.

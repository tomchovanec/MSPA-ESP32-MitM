# Upstream bill of materials

[Česky](hardware_bom.cs-CZ.md) · [Original](hardware_bom.md) · [Index](INDEX.md)

The upstream author lists an ESP32 DevKit, project enclosure, four-pin JST-SM connectors and 3.3/5 V level shifters. Their examples: [ESP32](https://www.amazon.fr/dp/B0BWN595WY), [enclosure](https://www.amazon.fr/dp/B0824HTB4F), [connectors](https://www.amazon.fr/dp/B0CBWX98NF) and [level shifters](https://www.amazon.fr/dp/B0CJ6PD2GR).

The author used these parts with their own unit and firmware v6.3.6. Connector compatibility, data signal levels, supply current capacity and the suitability of a specific level shifter have not been verified for the F-TR062W. Never connect a 5 V signal directly to ESP32 3.3 V GPIO. Measure the voltages and verify that the chosen converter is suitable for UART.

The original guide gives a 95 × 55 × 23 mm enclosure and a JST-SM extension cable as an example of a reversible installation. Check the actual connector and water protection required for the specific spa. The [original guide](hardware_bom.md) contains the author's component photos; our [hardware guide](hardware.en.md) includes the F-TR062W PCB photographs.

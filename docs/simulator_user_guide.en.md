# MSpa simulator v1.6.9 – user guide

[Česky](simulator_user_guide.cs-CZ.md) · [Original](simulator_user_guide.md) · [Index](INDEX.md)

The simulator is a test environment for the controller. Its interface separates input values `SIM: XXX` injected on the bus from outputs `LUE: XXX (Bus)` showing what the controller actually decodes.

## Filter alert and reset

The `ALERTE FILTRE F1` button simulates an alert: the 0x1A bit flashes and the pump stops. The controller's `Action Reset Alerte` switch sends a burst of `0x02 0x01` frames for four seconds. The simulator accepts reset after three seconds of uninterrupted reception; a gap longer than 500 ms fails that requirement. During reset detection, the 500 ms repeat filter does not apply to command 0x02, permitting reception at 10 Hz.

## Bubbles

According to the author, the D-series cycle is simulated in the order `0 (off) → 2 (medium) → 3 (strong) → 1 (gentle) → 0`. Each `0x03` command moves to the next level.

## Connecting the two ESP32 boards on a test bench

| Simulator | Controller |
| --- | --- |
| GND | GND |
| GPIO17 (TX1) | GPIO16 (RX_SPA) |
| GPIO16 (RX1) | GPIO17 (TX_SPA) |
| GPIO13 (TX2) | GPIO14 (RX_KBD) |
| GPIO14 (RX2) | GPIO13 (TX_KBD) |

This table connects two development boards on a bench; it is not a verified F-TR062W spa pinout.

The author says the LED on GPIO2 flashes rapidly during UART activity and stays on for one second when a valid `A5` command is handled. The `DIAG: Erreurs 4b/5b` counters help inspect communication errors. The simulator accepts values up to 50 °C; the author states that controller v6.x limits displayed values and setpoints to 40 °C.

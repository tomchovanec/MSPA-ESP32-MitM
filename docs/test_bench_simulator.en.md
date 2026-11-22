# MSpa simulator test bench

[Česky](test_bench_simulator.cs-CZ.md) · [Original](test_bench_simulator.md) · [Index](INDEX.md)

A second ESP32 can simulate the spa and help test the controller firewall before connecting to a real unit. Passing simulator tests does not itself establish safety or compatibility with the real spa.

| Controller v6.3.7 | Simulator v1.6.9 | Purpose |
| --- | --- | --- |
| GPIO16 (RX_SPA) | GPIO17 (TX_MB) | Simulate mainboard |
| GPIO17 (TX_SPA) | GPIO16 (RX_MB) | Receive mainboard commands |
| GPIO14 (RX_KBD) | GPIO13 (TX_KBD) | Simulate keypad |
| GPIO13 (TX_KBD) | GPIO14 (RX_KBD) | Receive keypad commands |
| GND | GND | Common ground |

## Simulator behaviour

1. The mainboard loop sends `A5 06`, `A5 08`, `A5 1A`, `A5 1B` and `A5 12` every 100 ms.
2. The keypad loop sends heartbeat `A5 0D` every 100 ms.
3. When it receives `A5 01 01` (heat), the simulator triggers internal phases and changes its response frames.

## Checks

Enable `sw_lock` on the controller, use the simulator's `ACTION` buttons and check that commands are intercepted and logged without reaching the main bus. Under load, check decoding of five-byte `1B` frames and confirm that UART traffic does not prevent OTA updates.

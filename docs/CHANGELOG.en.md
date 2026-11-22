# MSpa ESP32 changelog

[Original French file](CHANGELOG.md) · [Česky](CHANGELOG.cs-CZ.md) · [Index](INDEX.md)

## 2026-04-16 – filter reset and sync optimisation (controller v6.3.7 / simulator v1.6.9)
- Added `Action Reset Alerte`, sending a four-second burst to acknowledge a filter change remotely.
- Simulator v1.6.9 separates long-press detection from the 500 ms debounce filter to capture rapid reset frames.
- Made `inject_cmd` public in `mspa_uart.h` so YAML can call it directly.
- Restored target-temperature synchronisation in v1.6.9.

## 2026-04-04 – Eedomus alert and master sync (v6.3.6-STABLE)
- Automatic Eedomus filter alert (ID 3536562).
- Startup sync of eight entities with a 500 ms delay.
- Fallback `MSPA-RECOVERY` AP is protected by a password from secrets.
- Aligned entity names for compatibility with Eedomus settings. The author reports stability validation on 4 April 2026.

## 2026-03-28 – audit and diagnostics (v6.3.5-STABLE)
- Enabled native ESPHome API on port 6053 with `reboot_timeout: 0s` for monitoring and logs without cyclic restarts.

## 2026-03-28 – final release (v6.3.4-STABLE)
- Active UART firewall blocks physical commands when locked while retaining heartbeat `0x0D`.
- State display follows the UART bus.
- Sniper v2 retries on lost frames.
- Filter alert diagnostic detects blinking with `0x1A/0x08`.

## 2026-03-27 – lab simulator (v1.6.0-STABLE)
- Bubbles cycle `0 -> 2 -> 3 -> 1 -> 0`.
- Removed direct memory access; simulation communicates via UART.
- Dedicated bridge supports five-byte `0x1B` frames.

## 2026-03-22 – earlier stable base (v3.9.3)
- ESPHome-managed filtration, heating and UVC shutdown interlocks.

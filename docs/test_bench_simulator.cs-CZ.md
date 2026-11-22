# Testovací prostředí se simulátorem MSpa

[English](test_bench_simulator.en.md) · [Originál](test_bench_simulator.md) · [Přehled](INDEX.md)

Druhé ESP32 může simulovat vířivku a umožnit otestovat firewall řadiče před připojením ke skutečnému zařízení. Úspěšný test simulátoru sám o sobě nezaručuje bezpečnost ani kompatibilitu skutečné vířivky.

| Řadič v6.3.7 | Simulátor v1.6.9 | Účel |
| --- | --- | --- |
| GPIO16 (RX_SPA) | GPIO17 (TX_MB) | Simulace řídicí desky |
| GPIO17 (TX_SPA) | GPIO16 (RX_MB) | Příjem příkazů pro řídicí desku |
| GPIO14 (RX_KBD) | GPIO13 (TX_KBD) | Simulace panelu |
| GPIO13 (TX_KBD) | GPIO14 (RX_KBD) | Příjem příkazů pro panel |
| GND | GND | Společná zem |

## Chování simulátoru

1. Smyčka řídicí desky odesílá `A5 06`, `A5 08`, `A5 1A`, `A5 1B` a `A5 12` každých 100 ms.
2. Smyčka panelu odesílá heartbeat `A5 0D` každých 100 ms.
3. Po přijetí `A5 01 01` (ohřev) simulátor spouští interní fáze a mění odpovědi.

## Kontroly

Na řadiči zapněte `sw_lock`, použijte tlačítka `ACTION` na simulátoru a ověřte, že příkazy jsou zachyceny a zaznamenány bez předání na hlavní sběrnici. Při zátěži sledujte dekódování pětibajtových rámců `1B` a ověřte, že provoz UART nebrání aktualizacím OTA.

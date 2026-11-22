# Seznam součástek původního projektu

[English](hardware_bom.en.md) · [Originál](hardware_bom.md) · [Přehled](INDEX.md)

Původní autor uvádí jako základ ESP32 DevKit, krabičku, čtyřpinové konektory JST-SM a převodníky úrovní 3,3/5 V. Jeho konkrétní příklady: [ESP32](https://www.amazon.fr/dp/B0BWN595WY), [krabička](https://www.amazon.fr/dp/B0824HTB4F), [konektory](https://www.amazon.fr/dp/B0CBWX98NF) a [převodníky](https://www.amazon.fr/dp/B0CJ6PD2GR).

Autor tyto díly použil se svým zařízením a firmwarem v6.3.6. Pro F-TR062W zatím nebyla ověřena shoda konektoru, napětí datových signálů, proudová rezerva napájení ani vhodnost konkrétního převodníku. Na 3,3V GPIO ESP32 nepřipojujte přímo 5V signál. Vhodnost převodníku pro UART i obě napěťové úrovně ověřte měřením.

Originál uvádí příklad krabičky 95 × 55 × 23 mm a prodlužovacího kabelu s konektory JST-SM pro vratnou instalaci. Skutečný konektor a potřebné krytí proti vodě ověřte na konkrétní vířivce. Původní fotografie dílů jsou v [originálním dokumentu](hardware_bom.md); naše [dokumentace k hardwaru](hardware.cs-CZ.md) obsahuje i fotografie desky F-TR062W.

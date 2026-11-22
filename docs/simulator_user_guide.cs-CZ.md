# Simulátor MSpa v1.6.9 – uživatelský návod

[English](simulator_user_guide.en.md) · [Originál](simulator_user_guide.md) · [Přehled](INDEX.md)

Simulátor tvoří testovací prostředí pro řadič. Jeho rozhraní odděluje vstupní hodnoty `SIM: XXX`, které se vkládají na sběrnici, od výstupů `LUE: XXX (Bus)`, které ukazují, co řadič skutečně dekódoval.

## Upozornění na filtr a reset

Tlačítko `ALERTE FILTRE F1` simuluje upozornění: bit 0x1A bliká a čerpadlo se zastaví. Přepínač `Action Reset Alerte` na řadiči odešle po dobu čtyř sekund sérii rámců `0x02 0x01`. Simulátor reset potvrdí po třech sekundách souvislého příjmu; přerušení mezi rámci delší než 500 ms tento požadavek nesplňuje. Během detekce resetu se 500ms ochrana proti opakování na příkaz 0x02 nevztahuje, aby byl možný příjem při 10 Hz.

## Bubliny

Podle autora simuluje cyklus série D pořadí `0 (vypnuto) → 2 (střední) → 3 (silné) → 1 (jemné) → 0`. Každý příkaz `0x03` přejde na další úroveň.

## Propojení dvou ESP32 na testovacím stole

| Simulátor | Řadič |
| --- | --- |
| GND | GND |
| GPIO17 (TX1) | GPIO16 (RX_SPA) |
| GPIO16 (RX1) | GPIO17 (TX_SPA) |
| GPIO13 (TX2) | GPIO14 (RX_KBD) |
| GPIO14 (RX2) | GPIO13 (TX_KBD) |

Jde o propojení dvou desek na testovacím stole, nikoli o ověřený pinout vířivky F-TR062W.

LED na GPIO2 podle autora rychle bliká při provozu UART a svítí jednu sekundu při zpracování platného příkazu `A5`. Počítadla `DIAG: Erreurs 4b/5b` pomáhají sledovat chyby komunikace. Simulátor přijímá hodnoty až do 50 °C; autor uvádí, že řadič v6.x omezuje zobrazení a nastavení na 40 °C.

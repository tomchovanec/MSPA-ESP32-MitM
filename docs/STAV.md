# Stav projektu – IN PROGRESS / NOT FINISHED

## Cíl

Lokální ovládání MSpa Tribeca F-TR062W s Home Assistantem při zachování původního panelu. Projekt je rozpracovaný a aktivní most nebyl vyzkoušen na vířivce.

## Ověřeno při pasivním odposlechu

- Červený vodič na konektoru z řídicí jednotky: naměřeno +5 V; bílý: GND. GND na pinu 4 panelu byl také ověřen odporem. Přiřazení konkrétní pozice +5 V na panelu ještě vyžaduje proměření.
- Zelený vodič přes převodník `HV1 → LV1`, bílo-zelený kablík a GPIO6 ESP32-C6: opakovaně `A5 06 2C D7` a `A5 08 00 AD`, 9600 baudů, 8N1. Kontrolní součty rámců odpovídají součtu prvních tří bajtů modulo 256.
- Hodnota `0x2C / 2 = 22 °C` souhlasila s displejem. Panel byl připojený a pracoval normálně. Směr zelené linky jednotka → panel je tím silně podpořen, ale neověřuje to celý protokol.

## Neověřeno a omezení

- Směr černého vodiče a úrovně obou datových linek, chování při zapnutí filtrace, ohřevu, UVC a bublinek.
- Převodník úrovní a napájení celého zapojení po poškození předchozí desky, proudová rezerva, zpětné napájení a izolace.
- Aktivní most, jeho reakce na neznámé rámce, současné ovládání panelem a HA, případná ztráta ESP32 nebo sítě a hardware bypass.
- ESPHome firmware pro původní ESP32 před ověřením na reálné jednotce neslibuje kompatibilitu ani zachování všech funkcí.

## Pokračování po dodání náhradní desky

1. Porovnat počet a polohu všech pinů nové vývojové desky s paticí; označit orientaci. Předchozí ESP32 se zahřívalo a mělo cca 3,2 Ω mezi 3V3 a GND.
2. Bez napájení zkontrolovat patici, propojení a převodník; následně ověřit napájení a úrovně správným postupem. Nesmí se opakovat obrácené zasunutí.
3. Nejprve ověřit novou desku samostatně a obnovit pasivní odposlech se zachovaným přímým propojením panelu. Před návrhem aktivního mostu zkontrolovat i druhou linku a bezpečné předávání.
4. Aktivní řízení a režimy při výpadku testovat postupně až po ověření. Do té doby ponechat původní panel ve funkčním přímém spojení.

# Ovládání MSpa pomocí ESP32

[English](README.en.md) | [Původní francouzská dokumentace](README.md)

Tato kopie projektu [EtienneESP32/MSPA-ESP32-EEDOMUS](https://github.com/EtienneESP32/MSPA-ESP32-EEDOMUS) vkládá ESP32 mezi původní ovládací panel MSpa a řídicí jednotku vířivky. ESP32 předává komunikaci panelu a poskytuje lokální ovládání přes ESPHome a Home Assistant. Projekt obsahuje také sniffer a simulátor. Původní autor jej vytvořil pro Tribecu řady D; kompatibilita s F-TR062W a deskou M22W(T)-DB(WIFI) Rev2.0 zatím není ověřena.

**Nepřebírej bez ověření barvy vodičů, pořadí pinů, napětí ani protokol jiného modelu.** Není ověřeno, jak se původní panel zachová při výpadku nebo zamrznutí ESP32; samotný aktivní most nezaručuje hardwarové přemostění. Neobcházej ochrany vířivky.

## Součásti

- [Řadič](esphome/mspa-controller.yaml): průchozí UART most, entity Home Assistantu a volitelná HTTP integrace Eedomus.
- [Sniffer](esphome/mspa-sniffer.yaml): odposlech před pokusem o aktivní ovládání.
- [Simulátor](esphome/mspa-simulator.yaml): testovací prostředí pro vývoj.
- [Hardware a zapojení](docs/hardware.cs-CZ.md): referenční zapojení původního projektu a poznatky o F-TR062W.

## Začínáme

1. Urči zapojení konektoru, napájení a úrovně signálů. Před připojením vysílače pasivně zaznamenej oba směry komunikace a porovnej rámce s protokolem projektu.
2. Nainstaluj [ESPHome](https://esphome.io/). Zkopíruj `esphome/secrets.yaml.example` do `esphome/secrets.yaml`, vyplň údaje Wi-Fi a záložního přístupového bodu a soubor s hesly neukládej do repozitáře. Pro Home Assistant bez Eedomus nastav `eedomus_enabled: "false"`; ostatní klíče ale mohou být v souboru stále vyžadovány.
3. Po ověření zapojení a kompatibility sestav a nahraj firmware příkazem `py -m esphome run esphome/mspa-controller.yaml`.
4. Přidej zařízení přes integraci ESPHome v Home Assistantu. Před běžným provozem vyzkoušej původní panel, čtení stavu, jednotlivé příkazy a chování při výpadku ESP32, Wi-Fi a HA.

Původní francouzská dokumentace a zdrojové kódy jsou zachovány. Podmínky použití a uvedení autora najdeš v [LICENSE](LICENSE).

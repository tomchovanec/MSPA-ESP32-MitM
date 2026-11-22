# Historie změn MSpa ESP32

[Původní francouzský soubor](CHANGELOG.md) · [English](CHANGELOG.en.md) · [Přehled](INDEX.md)

## 16. 4. 2026 – reset filtru a synchronizace (řadič v6.3.7 / simulátor v1.6.9)
- Přidán `Action Reset Alerte`, který odesílá čtyřsekundovou sérii pro vzdálené potvrzení výměny filtru.
- Simulátor v1.6.9 odděluje detekci dlouhého stisku od 500ms ochrany proti zákmitům, aby zachytil rychlou sérii resetovacích rámců.
- Metoda `inject_cmd` v `mspa_uart.h` je veřejná pro přímé volání z YAML.
- Obnovena synchronizace požadované teploty ve v1.6.9.

## 4. 4. 2026 – upozornění Eedomus a synchronizace (v6.3.6-STABLE)
- Automatické upozornění na filtr v Eedomus (ID 3536562).
- Úvodní synchronizace osmi entit s prodlevou 500 ms.
- Záložní AP `MSPA-RECOVERY` je chráněn heslem ze secrets.
- Sjednocení názvů entit kvůli kompatibilitě s nastavením Eedomus. Autor uvádí ověření stability této verze 4. 4. 2026.

## 28. 3. 2026 – diagnostika (v6.3.5-STABLE)
- Aktivní nativní API ESPHome na portu 6053 s `reboot_timeout: 0s` pro sledování a logy bez cyklických restartů.

## 28. 3. 2026 – finální vydání (v6.3.4-STABLE)
- Aktivní UART firewall blokuje povely panelu při zámku, ale zachovává heartbeat `0x0D`.
- Zobrazení stavu vychází ze sběrnice UART.
- Sniper v2 opakuje povely při ztrátě rámce.
- Diagnostika rozpoznává blikání upozornění filtru pomocí `0x1A/0x08`.

## 27. 3. 2026 – laboratorní simulátor (v1.6.0-STABLE)
- Cyklus bublinek `0 -> 2 -> 3 -> 1 -> 0`.
- Odstraněn přímý přístup do paměti; simulace komunikuje přes UART.
- Most podporuje pětibajtové rámce `0x1B`.

## 22. 3. 2026 – starší stabilní základ (v3.9.3)
- Ochranné vazby vypínání filtrace, ohřevu a UVC spravované ESPHome.

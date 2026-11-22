# Řešení problémů

[English](troubleshooting.en.md) · [Francouzský originál](troubleshooting.md) · [Přehled dokumentace](INDEX.md)

Tento překlad vychází z návodu původního autora. Konkrétní hodnoty a vlastnosti vířivky F-TR062W je nutné ověřit měřením.

## Diagnostické kódy 4b a 5b

**4b – chyba rámce:** ESP32 přijalo data, ale nerozpoznalo začátek platného rámce `0xA5`. Ověřte správné propojení TX a RX přes odpovídající převodník úrovní, rušení a délku kabelu. Původní projekt používá rychlost 9600 baudů; pro jiné zařízení ji nelze předpokládat bez ověření.

**5b – chyba kontrolního součtu:** Přijatý rámec má nesprávný čtvrtý bajt. Příčinou může být rušení nebo nestabilní společná zem mezi vířivkou, ESP32 a převodníky úrovní. Počet chyb sledujte v souvislosti s chováním zařízení; nízký počet sám o sobě neprokazuje spolehlivost.

## Wi-Fi a napájení

- **ESP32 se nepřipojuje k Wi-Fi:** zkontrolujte údaje sítě a signál v místě instalace. Pokud je ve firmwaru správně nakonfigurovaný záložní přístupový bod a captive portal, připojte se k němu a zkontrolujte nastavení.
- **Opakované restarty:** možné příčiny zahrnují pokles napájecího napětí při zapnutí Wi-Fi. Změřte napětí při zátěži a ověřte proudovou rezervu zdroje. Původní návod zmiňuje kondenzátor 100–470 µF mezi 5 V a GND; sám ale nedokáže nahradit nedostatečný zdroj.
- **Statická IP:** pokud používáte `manual_ip`, zkontrolujte i platný DNS server `dns1`. Autor uvádí, že chybná DNS konfigurace může způsobit problémy se síťovými službami a restart.

## Home Assistant a Eedomus

Pokud se stavy neaktualizují, zkontrolujte připojení zařízení a integraci ESPHome v Home Assistantu. Původní návod uvádí, že automatické rozpoznání může trvat až dvě minuty. V Eedomus zkontrolujte HTTP odpovědi a při chybách 401/403 přihlašovací údaje API v `secrets.yaml`.

## Viditelnost repozitáře

Původní autor doporučuje ověřit veřejnou dostupnost z anonymního okna prohlížeče nebo v nastavení GitHubu v části **Settings → Danger Zone → Change visibility**.

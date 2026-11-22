# Přístupové údaje a nastavení

[English](secrets_reference.en.md) · [Francouzský originál](secrets_reference.md) · [Přehled dokumentace](INDEX.md)

Vytvořte místní `esphome/secrets.yaml` z `esphome/secrets.yaml.example`. Soubor s opravdovými hesly a klíči nikdy neukládejte do Gitu. Před nahráním nahraďte výchozí Wi-Fi a případně Eedomus údaje. Pro instalaci bez Eedomus nastavte `eedomus_enabled: "false"`; klíče vyžadované konfigurací musí být přesto přítomné.

| Klíč | Účel |
| --- | --- |
| `wifi_ssid`, `wifi_password` | Název a heslo Wi-Fi |
| `ap_ssid`, `ap_password` | Název a heslo záložního přístupového bodu |
| `eedomus_enabled` | Zapnutí nebo vypnutí integrace Eedomus |
| `eedomus_host` | IP adresa nebo hostname jednotky Eedomus |
| `eedomus_api_user`, `eedomus_api_secret` | Uživatelské jméno a tajný klíč API Eedomus |
| `eedomus_periph_filtration` | ID filtrace |
| `eedomus_periph_chauffage` | ID ohřevu |
| `eedomus_periph_bulles` | ID bublinek |
| `eedomus_periph_uvc` | ID UVC |
| `eedomus_periph_verrouillage` | ID zámku |
| `eedomus_periph_consigne_temp` | ID požadované teploty |
| `eedomus_periph_temp_eau` | ID teploty vody |
| `eedomus_periph_alerte_filtre` | ID upozornění na filtr |
| `static_ip`, `gateway`, `subnet` | Nastavení pevné IP, pokud je použito v konfiguraci Wi-Fi |

Pokud zůstane `eedomus_host` nastavený na `IP_OU_HOST_EEDOMUS`, připojení k Eedomus nebude fungovat. Klíče `eedomus_url_*` ve vzoru obsahují připravené URL pro vložení do Eedomus; ESP32 je přímo nepoužívá. Příklady pro požadovanou teplotu jsou `eedomus_url_consigne_25` až `eedomus_url_consigne_38` podle hodnot uvedených ve vzoru.

Řadič používá údaje Wi-Fi, záložního AP a Eedomus; sniffer používá Wi-Fi údaje a v původní konfiguraci má název záložního AP uvedený přímo. Podrobné nastavení zařízení a URL uvádí [původní návod pro Eedomus](config_eedomus.md).

# Nastavení zařízení Eedomus

[English](config_eedomus.en.md) · [Francouzský originál](config_eedomus.md) · [Přehled](INDEX.md)

Skutečné IP adresy, ID a klíče API nepatří do veřejného repozitáře. Uložte je lokálně v Eedomus a `esphome/secrets.yaml`. ESP posílá stavy do Eedomus přes HTTP API (push); příkazy Eedomus → ESP používají webový server ESP na portu 80, ne nativní API ESPHome. Bez webového serveru nebudou HTTP příkazy do ESP fungovat. Originál uvádí port 3232 pro API, jiná verze projektu uvádí 6053; ověřte aktuální konfiguraci.

## Entity a ID

Každá entita má zobrazované `name`, interní `id:` a URL slug obvykle odvozený z názvu. Skutečné slugy zkontrolujte na `http://<IP_ESP>/json`.

| Funkce | Název v UI | ID v YAML | Eedomus |
| --- | --- | --- | --- |
| Filtrace | Filtration | `sw_f` | ON/OFF |
| Ohřev | Chauffage | `sw_h` | ON/OFF |
| Bubliny | Mode Bulles | `sel_b` | `Arret`, `Niveau1`, `Niveau2`, `Niveau3` |
| UVC | UVC | `sw_u` | ON/OFF |
| Zámek | Verrouillage Clavier | `sw_lock` | ON/OFF |
| Požadovaná teplota | Temperature Consigne | `test_setpoint` | seznam hodnot |
| Teplota vody | Temperature Eau | `cur_temp` | číselný údaj |
| Upozornění na filtr | Alerte Changement Filtre | `filt_alert` | pouze příjem stavu |
| Reset upozornění | Action Reset Alerte | `sw_reset_filt` | HTTP akční člen |

Číselná ID Eedomus se nastavují pomocí klíčů `eedomus_periph_*` v `esphome/secrets.yaml`; viz [nastavení secrets](secrets_reference.cs-CZ.md).

## Požadovaná teplota

ESP posílá přesnou nastavenou hodnotu bez zaokrouhlení, včetně hodnot jako 37,5. Eedomus zobrazuje přijatý stav. Pro změnu vytvořte akční člen typu seznam, s hodnotami 25, 30, 35, 36, 37 a 38 °C. Pro každou hodnotu použijte odpovídající URL `eedomus_url_consigne_25`, `_30`, `_35`, `_36`, `_37`, `_38` ze `secrets.yaml` a metodu POST. Šest možností slouží k nastavení, nikoli k zaokrouhlení přijímaného stavu.

## HTTP volání ESP z Eedomus

Nahraďte `<IP_ESP>` skutečnou adresou a ověřte slug pomocí `/json`.

| Funkce | URL / hodnoty |
| --- | --- |
| Filtrace | `http://<IP_ESP>/switch/filtration/turn_on` nebo `turn_off` |
| Ohřev | `http://<IP_ESP>/switch/chauffage/turn_on` nebo `turn_off` |
| UVC | `http://<IP_ESP>/switch/uvc/turn_on` nebo `turn_off` |
| Zámek | `http://<IP_ESP>/switch/verrouillage_clavier/turn_on` nebo `turn_off` |
| Bubliny | `http://<IP_ESP>/select/mode_bulles/set?option=Arret` nebo přesně `Niveau1`, `Niveau2`, `Niveau3` |
| Teplota | `http://<IP_ESP>/number/temperature_consigne/set?value=38` |
| Reset filtru | `http://<IP_ESP>/switch/action_reset_alerte/turn_on` |

Resetovací URL lze nastavit pro stav 0 (Normal) upozornění filtru; po ručním návratu do tohoto stavu Eedomus vyvolá čtyřsekundový reset. Ve vzoru jsou i URL `eedomus_url_filtration_off/on`, `eedomus_url_chauffage_off/on`, `eedomus_url_uvc_off/on`, `eedomus_url_verrouillage_off/on`, `eedomus_url_bulles_arret` a `eedomus_url_bulles_niveau1/2/3`. Jednotlivé URL vložte do příslušného stavu akčního členu HTTP s metodou POST.

## Vytvoření zařízení

V Eedomus vytvořte zařízení pro každou entitu: přepínače jako seznam ON/OFF, cílovou teplotu jako seznam šesti hodnot a teplotu vody jako desetinné číslo pro příjem stavu. U filtrace lze použít 0 = OFF a 1 = ON. Do stavů, které mají ovládat ESP, vložte odpovídající URL. Pro příjem push nechte dotaz/XPATH prázdný; používá se API `periph.value`. Získaná ID vložte do `eedomus_periph_*` v `secrets.yaml` a soubor necommitujte.

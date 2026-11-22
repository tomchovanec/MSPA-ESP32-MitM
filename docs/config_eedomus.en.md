# Eedomus device configuration

[Česky](config_eedomus.cs-CZ.md) · [Original French](config_eedomus.md) · [Index](INDEX.md)

Do not put real IP addresses, IDs or API keys into a public repository. Configure them locally in Eedomus and `esphome/secrets.yaml`. ESP pushes states to Eedomus via HTTP API; commands from Eedomus to ESP use the ESP web server on port 80, not the native ESPHome API. Disabling the web server disables HTTP commands to the ESP. The original guide mentions API port 3232 while another project revision says 6053; check the current configuration.

## Entities and IDs

Each entity has a displayed `name`, an internal `id:` and a URL slug usually derived from its name. Check actual slugs at `http://<IP_ESP>/json`.

| Function | UI name | YAML ID | Eedomus |
| --- | --- | --- | --- |
| Filter | Filtration | `sw_f` | ON/OFF |
| Heater | Chauffage | `sw_h` | ON/OFF |
| Bubbles | Mode Bulles | `sel_b` | `Arret`, `Niveau1`, `Niveau2`, `Niveau3` |
| UVC | UVC | `sw_u` | ON/OFF |
| Keypad lock | Verrouillage Clavier | `sw_lock` | ON/OFF |
| Target temperature | Temperature Consigne | `test_setpoint` | value list |
| Water temperature | Temperature Eau | `cur_temp` | number |
| Filter alert | Alerte Changement Filtre | `filt_alert` | push only |
| Reset alert | Action Reset Alerte | `sw_reset_filt` | HTTP actuator |

Configure numeric Eedomus IDs via `eedomus_periph_*` keys in `esphome/secrets.yaml`; see the [secrets guide](secrets_reference.en.md).

## Target temperature

ESP pushes the exact target without rounding, including values such as 37.5. Eedomus displays the received state. To change it, configure a list actuator with options 25, 30, 35, 36, 37 and 38 °C. Use the matching URL `eedomus_url_consigne_25`, `_30`, `_35`, `_36`, `_37`, `_38` from `secrets.yaml` for each option and use POST. These six options send commands; they do not round the incoming state.

## Eedomus → ESP HTTP calls

Replace `<IP_ESP>` with the actual address and verify slugs via `/json`.

| Function | URL / values |
| --- | --- |
| Filter | `http://<IP_ESP>/switch/filtration/turn_on` or `turn_off` |
| Heater | `http://<IP_ESP>/switch/chauffage/turn_on` or `turn_off` |
| UVC | `http://<IP_ESP>/switch/uvc/turn_on` or `turn_off` |
| Lock | `http://<IP_ESP>/switch/verrouillage_clavier/turn_on` or `turn_off` |
| Bubbles | `http://<IP_ESP>/select/mode_bulles/set?option=Arret` or exactly `Niveau1`, `Niveau2`, `Niveau3` |
| Target | `http://<IP_ESP>/number/temperature_consigne/set?value=38` |
| Filter reset | `http://<IP_ESP>/switch/action_reset_alerte/turn_on` |

The reset URL may be configured for state 0 (Normal) of the filter alert; manually returning to that state triggers a four-second reset burst. The example also lists `eedomus_url_filtration_off/on`, `eedomus_url_chauffage_off/on`, `eedomus_url_uvc_off/on`, `eedomus_url_verrouillage_off/on`, `eedomus_url_bulles_arret` and `eedomus_url_bulles_niveau1/2/3`. Paste the matching URL into each HTTP actuator state and use POST.

## Create devices

Create an Eedomus device per entity: switches as ON/OFF lists, the target as a six-option list, and water temperature as a decimal number receiving pushed state. For filtration, 0 can mean OFF and 1 ON. Paste the corresponding URL into states that should control the ESP. Leave query/XPATH blank for pushed states using the `periph.value` API. Put the resulting IDs into `eedomus_periph_*` in `secrets.yaml` and do not commit that file.

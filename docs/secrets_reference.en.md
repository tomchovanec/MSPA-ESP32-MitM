# Secrets and configuration

[Česky](secrets_reference.cs-CZ.md) · [Original French guide](secrets_reference.md) · [Documentation index](INDEX.md)

Create a local `esphome/secrets.yaml` from `esphome/secrets.yaml.example`. Never commit real passwords or keys. Before flashing, replace the Wi-Fi credentials and, when used, Eedomus settings. For a setup without Eedomus set `eedomus_enabled: "false"`; keys required by the configuration may still need to be present.

| Key | Purpose |
| --- | --- |
| `wifi_ssid`, `wifi_password` | Wi-Fi network name and password |
| `ap_ssid`, `ap_password` | Fallback access point name and password |
| `eedomus_enabled` | Enable or disable Eedomus integration |
| `eedomus_host` | Eedomus box IP address or hostname |
| `eedomus_api_user`, `eedomus_api_secret` | Eedomus API username and secret |
| `eedomus_periph_filtration` | Filter device ID |
| `eedomus_periph_chauffage` | Heater device ID |
| `eedomus_periph_bulles` | Bubbles device ID |
| `eedomus_periph_uvc` | UVC device ID |
| `eedomus_periph_verrouillage` | Lock device ID |
| `eedomus_periph_consigne_temp` | Target temperature device ID |
| `eedomus_periph_temp_eau` | Water temperature device ID |
| `eedomus_periph_alerte_filtre` | Filter alert device ID |
| `static_ip`, `gateway`, `subnet` | Static IP settings if used by the Wi-Fi configuration |

Leaving `eedomus_host` set to `IP_OU_HOST_EEDOMUS` prevents Eedomus connectivity. The template's `eedomus_url_*` keys are ready-made URLs to paste into Eedomus; they are not read directly by the ESP32. Target-temperature examples include `eedomus_url_consigne_25` through `eedomus_url_consigne_38` for the values listed in the template.

The controller uses Wi-Fi, fallback AP and Eedomus settings; the sniffer uses Wi-Fi credentials and hard-codes its fallback AP name in the original configuration. See the [original Eedomus guide](config_eedomus.md) for detailed device and URL configuration.

# Troubleshooting

[Česky](troubleshooting.cs-CZ.md) · [Original French guide](troubleshooting.md) · [Documentation index](INDEX.md)

This translation follows the upstream author's guide. Parameters and behaviour of the F-TR062W must be verified on the actual device.

## Diagnostic codes 4b and 5b

**4b – frame error:** The ESP32 received data but did not recognise a valid `0xA5` frame start. Check TX/RX wiring through suitable level converters, interference and cable length. The upstream project uses 9600 baud; verify the setting on a different device.

**5b – checksum error:** The received frame has an incorrect fourth byte. Interference or an unstable common ground between the spa, ESP32 and level converters can cause this. Evaluate error counts alongside actual behaviour; a low count alone does not establish reliability.

## Wi-Fi and power

- **ESP32 cannot connect to Wi-Fi:** check the network credentials and signal at the installation site. If a fallback access point and captive portal have been configured correctly, connect to the fallback AP and check its settings.
- **Repeated restarts:** a supply voltage drop when Wi-Fi starts is one possible cause. Measure the supply under load and check its current capacity. The upstream guide suggests a 100–470 µF capacitor between 5 V and GND, but a capacitor cannot compensate for an inadequate supply.
- **Static IP:** if using `manual_ip`, check that `dns1` specifies a valid DNS server. The author reports that incorrect DNS configuration can cause network service problems and restarts.

## Home Assistant and Eedomus

If states do not update, check connectivity and the ESPHome integration in Home Assistant. The upstream guide says discovery may take up to two minutes. For Eedomus, check HTTP responses and, for 401/403 errors, the API credentials in `secrets.yaml`.

## Repository visibility

The upstream author suggests checking public access in a private browser window or through GitHub **Settings → Danger Zone → Change visibility**.

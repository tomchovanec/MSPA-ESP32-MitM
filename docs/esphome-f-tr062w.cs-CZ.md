# ESPHome pro MSpa F-TR062W

[Konfigurace](../esphome/mspa-f-tr062w.yaml) vychází z původního řadiče a obsahuje čtyři sítě Wi-Fi ze vzoru, ESPHome API, OTA, webové rozhraní a entity vířivky. Používá DHCP; adresa `192.168.1.178` z původního příkladu patří jinému zařízení.

**Konfigurace je experimentální.** Protokol ani datové piny F-TR062W nejsou ověřené. Původní komponenta není průhledný převodník: ze směru panel → vířivka předává pouze rámce, kterým rozumí a mají platný kontrolní součet. Ostatní může zahodit. Selhání ESP32 může vyřadit panel. Na skutečnou vířivku nepřipojujte konfiguraci před ověřením komunikace, napětí a chování na testovacím prostředí. Ověřte také chování nastavení teploty, filtrace, ohřevu a ochranných funkcí.

Starší verze tohoto YAML posílala při startu vypínací příkazy pro filtraci, ohřev a UVC. Aktuální verze nastavuje u všech tří přepínačů `restore_mode: DISABLED`, aby ESPHome tyto akce při startu samo nevyvolávalo. Zkontrolujte výsledek v logu po restartu s odpojenou vířivkou; uvedená změna nezaručuje další chování původní komponenty ani celého systému.

## Instalace

Do ESPHome zkopírujte YAML. Komponentu `mspa_uart` si konfigurace stahuje z připnuté verze tohoto veřejného repozitáře. Internet je potřebný při sestavení, ne pro komunikaci s Home Assistantem. Do souboru `secrets.yaml` v ESPHome doplňte vlastní hodnoty:

```yaml
# Použijte své dosavadní klíče Wi-Fi a webového serveru:
wifi_ssid_iot: "..."
wifi_password_iot: "..."
wifi_ssid_dilna: "..."
wifi_password_dilna: "..."
wifi_ssid_pracovna: "..."
wifi_password_pracovna: "..."
wifi_ssid_tominet: "..."
wifi_password_tominet: "..."
wifi_password_n3: "..."

# Pro toto zařízení vytvořte vlastní jedinečné údaje:
mspa_api_key: "BASE64_32_BAJTU"
mspa_ota_password: "VLASTNI_HESLO_PRO_OTA"
mspa_ap_password: "VLASTNI_HESLO_HOTSPOTU"
```

API klíč musí být Base64 zakódovaných 32 náhodných bajtů, heslo hotspotu alespoň 8 znaků. Zástupné hodnoty nahraďte skutečnými a nikdy je neukládejte do veřejného repozitáře. Vzorové hodnoty z dotazu pro jiné zařízení nejsou v repozitáři uložené. První nahrání proveďte přes USB podle pokynů ESPHome a teprve po ověření zařízení přidejte přes integraci ESPHome v Home Assistantu.

Piny jsou `GPIO16` RX a `GPIO17` TX na straně vířivky; `GPIO14` RX a `GPIO13` TX na straně panelu. `GPIO` nejsou 5V tolerantní; vhodnost převodníku a úrovně je nutné předem ověřit. Viz [návrh zapojení](wiring/README.md).

Volby bublinek mají hodnoty `Arret`, `Niveau1`, `Niveau2`, `Niveau3`, protože je používá původní C++ komponenta. Nativní rozhraní ESPHome je lokální; nastavení Eedomus ani cloud MSpa konfigurace nevyužívá. Není přidán zámek panelu. To nezaručuje správný průchod všech příkazů.

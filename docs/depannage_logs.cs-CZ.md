# Diagnostika a analýza logů

[English](depannage_logs.en.md) · [Francouzský originál](depannage_logs.md) · [Přehled](INDEX.md)

Tento návod popisuje chování uváděné původním autorem; časování a parametry se mezi verzemi mohou lišit. Před úpravou porovnejte nastavení se skutečným YAML.

## HTTP a sokety

Chyby `Failed to create socket (family 2 socktype 1 protocol 0)`, `Failed to open a new connection: 32770`, `Connection failed, sock < 0` a `ESP_ERR_HTTP_CONNECT` znamenají, že se nepodařilo vytvořit nebo navázat TCP spojení. Chyba 32770 může souviset s omezením soketů či paměti. `http_request cleared Error flag` znamená vynulování chybového příznaku pro další pokus.

Možné příčiny: Eedomus je vypnutý, na jiné síti, blokovaný firewallem nebo má chybnou IP v `secrets.yaml`; případně ESP vyčerpalo sokety kvůli otevřené UI a HTTP požadavkům. Originál uvádí první test po 90 s, následné testy po 120 s při dostupnosti nebo po 5 minutách při nedostupnosti. Nastavení ověřte v aktuálním firmwaru.

Ověřte dostupnost Eedomus z téže sítě (ping). Při vývoji zavřete nepoužívané karty UI. Pokud nepotřebujete příkazy z Eedomus do ESP ani webové UI, lze zvážit vypnutí `web_server` kvůli úspoře prostředků; tím přestanou fungovat i HTTP příkazy do ESP.

## Nevyplněný hostname

`Error parse url http://IP_OU_HOST_EEDOMUS/api/` ukazuje, že zůstala příkladová hodnota. V `esphome/secrets.yaml` nahraďte `eedomus_host` skutečnou IP nebo hostname a `eedomus_api_user` a `eedomus_api_secret` skutečnými údaji. Znovu sestavte a nahrajte firmware. Při prvním neúspěchu testu může firmware zobrazit upozornění ke kontrole secrets.

## Chyba HTTP serveru

`httpd_accept_conn: error in accept (23)` odpovídá podle originálu chybě ENFILE: příliš mnoho otevřených deskriptorů. Zmenšete počet souběžných připojení, zavřete UI nebo zvažte vypnutí webového serveru s výše uvedeným omezením funkcí.

## Omezení zatížení UI

Sokety sdílí API, webový server a odchozí HTTP požadavky. Originál popisuje `max_connections: 4`, `listen_backlog: 2`, první test po 90 s, další po 120 s nebo 5 min, `http_request.timeout: 1s`, `max_trames = 2` a dvě `yield()`. Tyto hodnoty jsou specifické pro popisovanou verzi a před změnami je ověřte ve zdrojovém kódu.

Před OTA aktualizací zavřete kartu UI a při běžném používání mějte otevřenou jen jednu; zbytečně ji často nenačítejte. Přetrvává-li problém, lze v `interval:` prodloužit dostupný Eedomus probe ze 120 s na 180 s nebo 5 min, pokud aktuální verze takový interval používá. Za snížení provozu zaplatíte pomalejším rozpoznáním dostupnosti. Další podrobnosti: [Eedomus](config_eedomus.cs-CZ.md), [secrets](secrets_reference.cs-CZ.md), [změny](CHANGELOG.cs-CZ.md).

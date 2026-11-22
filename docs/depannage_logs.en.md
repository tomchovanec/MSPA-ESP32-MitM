# Troubleshooting and log analysis

[Česky](depannage_logs.cs-CZ.md) · [Original French](depannage_logs.md) · [Index](INDEX.md)

This describes behaviour reported by the upstream author; timings and options may differ between versions. Compare the actual YAML before making changes.

## HTTP and sockets

Errors `Failed to create socket (family 2 socktype 1 protocol 0)`, `Failed to open a new connection: 32770`, `Connection failed, sock < 0` and `ESP_ERR_HTTP_CONNECT` indicate failure to create or establish a TCP connection. Error 32770 may reflect a socket or memory limit. `http_request cleared Error flag` means the component reset its error flag for the next attempt.

Possible causes include Eedomus being off, on another network, blocked by a firewall or using a wrong IP in `secrets.yaml`; the ESP may also exhaust sockets due to the open UI and HTTP requests. The original describes a first probe after 90 s, later every 120 s when reachable or every 5 min when unreachable. Check the actual firmware configuration.

Check that Eedomus can be reached from the same network (ping). During development close unused UI tabs. If neither Eedomus → ESP commands nor the web UI are needed, consider disabling `web_server` to save resources; this also disables HTTP commands to the ESP.

## Placeholder host

`Error parse url http://IP_OU_HOST_EEDOMUS/api/` indicates the example value remains. In `esphome/secrets.yaml` replace `eedomus_host` with the real IP or hostname and set the real `eedomus_api_user` and `eedomus_api_secret`. Rebuild and flash. The first failed probe may log a warning to check secrets.

## HTTP server error

According to the original, `httpd_accept_conn: error in accept (23)` is ENFILE: too many open descriptors. Reduce simultaneous connections, close the UI or consider disabling the web server with the loss of functionality described above.

## Reducing UI load

The API, web server and outgoing HTTP requests share sockets. The original describes `max_connections: 4`, `listen_backlog: 2`, first probe after 90 s, later at 120 s or 5 min, `http_request.timeout: 1s`, `max_trames = 2` and two `yield()` calls. These are specific to the documented version; verify them in code before changing anything.

Close the UI tab before OTA updates, keep only one tab open during use, and avoid frequent refreshes. If problems persist, the reachable Eedomus probe in `interval:` can be increased from 120 s to 180 s or 5 min if the current version uses that interval. Reduced traffic comes at the expense of slower availability detection. See [Eedomus](config_eedomus.en.md), [secrets](secrets_reference.en.md), and [changelog](CHANGELOG.en.md).

# Konfiguration

Öffentliche Voreinstellungen in `config/tuwunel.toml`. Die Datei enthält nur Platzhalter: Werte für Geheimnisse kommen aus dem Tresor (ADR 0067), wenn die Datei auf dem Server erzeugt wird. Erzeugt aus `config/schema.toml`.

| Einstellung | Typ | Standard | Geheimnis | Beschreibung |
|---|---|---|---|---|
| `global.server_name` | string | - | nein | Name des Matrix-Servers (Endung der Nutzer- und Raum-IDs). Lässt sich nach dem ersten Start nur mit Löschen der Datenbank ändern. Kein Geheimnis; je Installation verschieden. |
| `global.database_path` | path | `/srv/freesynergy/tuwunel/db` | nein | Verzeichnis für alle Daten einschließlich Medien. |
| `global.http.listen.address` | list | `["127.0.0.1"]` | nein | Lausch-Adressen; nur Loopback, weil Zentinel das öffentliche Tor ist. |
| `global.http.listen.port` | list | `[8008]` | nein | Lausch-Ports. |
| `global.well_known.client` | string | - | nein | Öffentliche Client-URL für die Matrix-Erkennung. Domain aus dem Tresor (kein Geheimnis). |
| `global.registration.enable` | boolean | `false` | nein | Offene Registrierung mit Passwort. Aus: Konten kommen von Kanidm. |
| `global.telemetry.sentry.enable` | boolean | `false` | nein | Sentry-Fehlerberichte (in Standard-Builds enthalten). Bleiben aus. |
| `global.identity_provider.client_id` | string | `tuwunel` | nein | OAuth2-Client-Name, in Kanidm eingetragen. |
| `global.identity_provider.client_secret_file` | path | - | ja (aus dem Tresor: `fs/tuwunel/oidc-client-secret#file`) | Datei mit dem OAuth2-Client-Geheimnis. Der Tresor schreibt die Datei; der Pfad im Muster ist ein Platzhalter. |
| `global.identity_provider.issuer_url` | string | - | nein | Issuer-URL des Kanidm-OIDC-Clients (`/oauth2/openid/tuwunel`); Kanidm-Domain aus dem Tresor (kein Geheimnis). |
| `global.identity_provider.callback_url` | string | - | nein | Callback-URL, bei Kanidm eingetragen; muss genau `/_matrix/client/unstable/login/sso/callback/<client_id>` sein. |
| `global.identity_provider.scope` | list | `["openid", "profile", "email"]` | nein | Angeforderte OIDC-Bereiche. |

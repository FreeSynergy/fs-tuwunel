# Bekannte Grenzen und offene Punkte

git-bug ist in den FreeSynergy-Repos noch nicht eingerichtet, deshalb stehen offene Punkte hier. „Geprüft“ heißt: im lokalen Podman-Test gesehen (`fs-kanidm/scripts/test/podman-stack.sh`, Tuwunel 2.0.0, Kanidm 1.12.0); „laut Hersteller-Doku“ heißt: nur gelesen.

## 1. SICHERHEIT: Der erste Single-Sign-on-Nutzer wird Admin (und bekommt einen Ersatznamen)

- **Geprüft:** Im lokalen Test wurde die erste Person, die sich über Kanidm anmeldete, Tuwunel-Server-Admin, ohne dass jemand das verlangt hat. Ihr Kanidm-Name `tester@idm.test.local` (der Kanidm-Kontoname mit Domain, gesendet als Angabe `preferred_username`) ist als Matrix-Benutzername ungültig; Tuwunel meldete `Username invalid ... contains disallowed characters` und wich auf eine andere Angabe aus: `@tester:matrix.test.local`. Die Registrierungs-Logzeile nannte als Grund, dass es der erste Nutzer ist.
- **Laut Hersteller-Doku:** `registration.grant_admin_to_first_user` ist standardmäßig an: das erste Konto, das sich auf einem neuen Server registriert, wird Admin ([tuwunel-example.toml](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/tuwunel-example.toml), Abschnitt registration). Bei leerem `userid_claims` werden die Angaben in dieser Reihenfolge versucht: `preferred_username`, `username`, `nickname`, `login`, dann der Teil von `email` vor dem `@` ([docs/authentication/providers.md](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/providers.md)). Nur bestimmte Angaben werden erkannt; beliebige lassen sich nicht eintragen.
- **Risiko:** Auf einem echten Server würde die erste Person, die sich nach dem ersten Start anmeldet, still Server-Admin, und ihr Name wäre ein erzeugter Ersatz. Wer zuerst kommt, darf nie entscheiden, wer Admin ist.
- **Plan (vor node1):**
  1. `config/tuwunel.toml`: `grant_admin_to_first_user = false` in `[global.registration]`, damit niemand automatisch Admin wird.
  2. Der Matrix-Name kommt aus einer festen Angabe: `userid_claims = ["preferred_username"]` und `unique_id_fallbacks = false` (Fehler statt Zufallsname). Damit Kanidm einen sauberen Kurznamen sendet, wird der OAuth2-Client in Kanidm mit der Kurznamen-Option angelegt (`kanidm system oauth2 prefer-short-username tuwunel`), sodass `preferred_username` `tester` ist statt `tester@idm.test.local`. Beide Schalter werden vor dem Einbau gegen die Referenz des Herstellers geprüft.
  3. Admin wird ausdrücklich gesetzt: `!admin users make-user-admin <Benutzername>` (oder der Startbefehl `admin.execute`, oder `--execute`) als dokumentierter Einrichtungsschritt. Tuwunel 2.0.0 kennt keine Zuordnung von einer Gruppe des Identitätsanbieters zu Admin; wenn Kanidm-Gruppe zu Tuwunel-Admin gewünscht ist, ist das eine Anfrage an den Hersteller oder eine spätere eigene Automatik.
  4. Ein Testfall im Podman-Aufbau: Der erste Single-Sign-on-Nutzer darf KEIN Admin sein (Admin-Status über die Matrix-API: ist der Nutzer in `#admins:<server_name>` beigetreten, ohne Geheimnisse). Einmal rot ohne die Einstellung, dann grün.

Sprache: [English](../en/known-limits.md)

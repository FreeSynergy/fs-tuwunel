# Fähigkeiten

Fähigkeiten-Tags für den FreeSynergy-Katalog (ADR 0068). `provides` = bietet an, `requires` = braucht, `recommends` = kann nutzen. Unterstützung ist `yes`, `no` oder `unstable` (ja, nein, instabil); jedes `yes` und `unstable` nennt die Quelle beim Hersteller. Erzeugt aus `capabilities.toml`; geprüft für Version Tuwunel 2.0.0 (2026-11-11).

| Tag | Beziehung | Unterstützung | Bedeutung | Quelle |
|---|---|---|---|---|
| `messaging.matrix` | provides | ja | Matrix-Heimserver (Client-Server- und Föderations-API, Ende-zu-Ende-verschlüsselte Räume, MatrixRTC-Unterstützung). | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/README.md) |
| `messaging.matrix.oidc-server` | provides | ja | Eingebauter OAuth-2.0-/OpenID-Connect-Server nur für Matrix-Clients; kein Anmeldedienst für andere Programme. | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/oidc-server.md) |
| `identity.oidc` | recommends | ja | Anmeldung über einen vorgeschalteten OIDC-Anbieter (dokumentiert für GitHub, Google, Keycloak, Authelia, Authentik, MAS; Kanidm steht nicht in der Liste und wird von diesem Repo getestet). | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/providers.md) |
| `identity.ldap` | recommends | ja | Passwort-Anmeldung gegen ein LDAP-Verzeichnis (Tuwunel nutzt LDAP, bietet keinen LDAP-Server an). Build-Feature, in Standard-Builds an. | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/ldap.md) |
| `identity.oauth2` | provides | nein | Wird nicht als Anmeldedienst für andere Programme angeboten (siehe messaging.matrix.oidc-server). | - |
| `identity.radius` | provides | nein | Wird nicht angeboten. | - |
| `identity.pam` | provides | nein | Wird nicht angeboten. | - |
| `identity.ssh-keys` | provides | nein | Wird nicht angeboten. | - |
| `identity.passkeys` | provides | nein | Wird nicht angeboten; die Anmeldung läuft über den Identitätsanbieter. | - |
| `identity.scim` | provides | nein | In 2.0.0 nichts dokumentiert. | - |

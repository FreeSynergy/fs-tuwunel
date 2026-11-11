# Capabilities

Capability tags for the FreeSynergy catalog (ADR 0068). `provides` = offers it, `requires` = needs it, `recommends` = can use it. Support is `yes`, `no` or `unstable`; every `yes` and `unstable` cites the upstream source. Generated from `capabilities.toml`; checked on version Tuwunel 2.0.0 (2026-11-11).

| Tag | Relation | Support | Meaning | Source |
|---|---|---|---|---|
| `messaging.matrix` | provides | yes | Matrix homeserver (client-server and federation APIs, end-to-end encrypted rooms, MatrixRTC support). | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/README.md) |
| `messaging.matrix.oidc-server` | provides | yes | Built-in OAuth 2.0 / OpenID Connect authorisation server for Matrix clients only; it is not a login service for other programs. | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/oidc-server.md) |
| `identity.oidc` | recommends | yes | Single sign-on through an upstream OIDC provider (documented for GitHub, Google, Keycloak, Authelia, Authentik, MAS; Kanidm is not in the list and is tested by this repository). | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/providers.md) |
| `identity.ldap` | recommends | yes | Password sign-in against an LDAP directory (Tuwunel uses LDAP; it does not offer an LDAP server). Compile-time feature, on in default builds. | [link](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/ldap.md) |
| `identity.oauth2` | provides | no | Not offered as a login service for other programs (see messaging.matrix.oidc-server). | - |
| `identity.radius` | provides | no | Not offered. | - |
| `identity.pam` | provides | no | Not offered. | - |
| `identity.ssh-keys` | provides | no | Not offered. | - |
| `identity.passkeys` | provides | no | Not offered; sign-in goes through the identity provider. | - |
| `identity.scim` | provides | no | Nothing documented in 2.0.0. | - |

# Configuration

Public default configuration in `config/tuwunel.toml`. It holds placeholders only: values for secrets come from the vault (ADR 0067) when the file is rendered on the server. Generated from `config/schema.toml`.

| Setting | Type | Default | Secret | Description |
|---|---|---|---|---|
| `global.server_name` | string | - | no | Name of the Matrix server (suffix of user and room ids). Cannot change after the first start without wiping the database. Not a secret; differs per installation. |
| `global.database_path` | path | `/srv/freesynergy/tuwunel/db` | no | Directory for all data including media. |
| `global.http.listen.address` | list | `["127.0.0.1"]` | no | Listen addresses; loopback, because Zentinel is the public gate. |
| `global.http.listen.port` | list | `[8008]` | no | Listen ports. |
| `global.well_known.client` | string | - | no | Public client URL for Matrix discovery. Domain from the vault (not a secret). |
| `global.rocksdb.direct_io` | boolean | `false` | no | RocksDB direct I/O. Off because the data directory is on ZFS (upstream advises false on ZFS and on file systems without direct I/O). |
| `global.database.pool.max_workers` | integer | `256` | no | Upper limit of the database worker threads in total. Upstream allows up to 2048 (default per worker pool: 4 times the CPU threads, clamped to 32..1024); on a large host that exceeded a container's default task limit and stopped the start with os error 11. Raise it together with the task limit. |
| `global.registration.enable` | boolean | `false` | no | Open password registration. Off: accounts come from Kanidm. |
| `global.telemetry.sentry.enable` | boolean | `false` | no | Sentry error reporting (compiled into default builds). Stays off. |
| `global.identity_provider.client_id` | string | `tuwunel` | no | OAuth2 client name registered in Kanidm. |
| `global.identity_provider.client_secret_file` | path | - | yes (from vault: `fs/tuwunel/oidc-client-secret#file`) | File with the OAuth2 client secret. The vault writes the file; the path in the template is a placeholder. |
| `global.identity_provider.issuer_url` | string | - | no | Issuer URL of the Kanidm OIDC client (`/oauth2/openid/tuwunel`); Kanidm's domain from the vault (not a secret). |
| `global.identity_provider.callback_url` | string | - | no | Callback URL registered with Kanidm; must be exactly `/_matrix/client/unstable/login/sso/callback/<client_id>`. |
| `global.identity_provider.scope` | list | `["openid", "profile", "email"]` | no | Requested OIDC scopes. |

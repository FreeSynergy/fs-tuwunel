# fs-tuwunel

FreeSynergy.Tuwunel: everything FreeSynergy needs to ship the [Tuwunel](https://matrix-construct.github.io/tuwunel/) Matrix homeserver (messaging; also the home of AI participants with ordinary Matrix accounts, ADR 0054).

- **Signed build mirror** (ADR 0068): Tuwunel's release files carry no signature, so `mirror.toml` pins the upstream tag `v2.0.0` and its commit; GitHub Actions builds from that commit, adds the source tarball of the same version and an SBOM, and signs everything with the FreeSynergy release key.
- **Public configuration** `config/tuwunel.toml` with defaults. It is a template: secrets are `${vault:…}` placeholders filled from the vault (ADR 0067); no secret is ever stored here (ADR 0054).
- **Capability tags** `capabilities.toml` for the catalog (Matrix, OIDC, OAuth2, LDAP, RADIUS, PAM, SSH keys, passkeys, SCIM: yes / no / unstable, each with its upstream source).
- **Docs** in English and German (`docs/en`, `docs/de`) and an **export** of the configuration (`export/config-export.json`).

```sh
python3 -I scripts/repo_tool.py check    # validate everything; secrets must be placeholders
python3 -I scripts/repo_tool.py docs     # regenerate capabilities.md and configuration.md (en + de)
python3 -I scripts/repo_tool.py export   # regenerate export/config-export.json
scripts/verify-mirror.sh <release-dir>   # check checksums and signatures of a downloaded release
```

Packages are release files, not Git content. Tuwunel itself is not changed; fixes go upstream (ADR 0015). The protocol is Matrix; the program is Tuwunel, hence the name `fs-tuwunel`.

Licence of this repository: MIT OR Apache-2.0. Tuwunel is Apache-2.0 (`LICENSE-Apache-2.0` ships with every release).

# FreeSynergy.Tuwunel

Tuwunel is the Matrix homeserver of FreeSynergy: chat, calls and the ordinary Matrix accounts that AI participants use (ADR 0054). People sign in through Kanidm (single sign-on).

- [Capabilities](capabilities.md): what Tuwunel offers, uses and does not do, with sources.
- [Configuration](configuration.md): the public defaults and what comes from the vault.
- [Mirror](mirror.md): where the package comes from and how to check it.

Tuwunel listens on the loopback only (in a container the listen address must be `0.0.0.0`, a check in Tuwunel complains about loopback under Podman; the local test pod shares the loopback so the template works unchanged). The database worker pool is capped (`max_workers`); whether io_uring works on node1 (systemd, not rootless) is a separate later check. [Zentinel](https://github.com/FreeSynergy/fs-zentinel) is the public gate. Version 2.0 organises the configuration in tables; the old flat names keep working throughout 2.x, but this repository uses the table form.

Language: [Deutsch](../de/index.md)

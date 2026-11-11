# FreeSynergy.Tuwunel

Tuwunel is the Matrix homeserver of FreeSynergy: chat, calls and the ordinary Matrix accounts that AI participants use (ADR 0054). People sign in through Kanidm (single sign-on).

- [Capabilities](capabilities.md): what Tuwunel offers, uses and does not do, with sources.
- [Configuration](configuration.md): the public defaults and what comes from the vault.
- [Mirror](mirror.md): where the package comes from and how to check it.

Tuwunel is meant to be reached through Zentinel. The template listens on `127.0.0.1` (the gate runs on the same host). Inside a container, Tuwunel complains about a loopback address and the address must be `0.0.0.0`; the local test pod shares one loopback, so the template works there unchanged. The database worker pool is capped (`max_workers`, see the configuration page). Tuwunel uses io_uring through RocksDB; it was not the cause of the start failure we saw, and whether it works on node1 (systemd, not rootless) is a separate check still to be made. Open: the effect of `direct_io = false` and of the cap on node1; in the local test `/data` was a tmpfs, not ZFS. Version 2.0 organises the configuration in tables; the old flat names keep working throughout 2.x, but this repository uses the table form.

Language: [Deutsch](../de/index.md)

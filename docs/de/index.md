# FreeSynergy.Tuwunel

Tuwunel ist der Matrix-Heimserver von FreeSynergy: Chat, Anrufe und die gewöhnlichen Matrix-Konten, die KI-Teilnehmer nutzen (ADR 0054). Menschen melden sich über Kanidm an (Single Sign-on).

- [Fähigkeiten](capabilities.md): was Tuwunel bietet, nutzt und nicht kann, mit Quellen.
- [Konfiguration](configuration.md): die öffentlichen Voreinstellungen und was aus dem Tresor kommt.
- [Spiegel](mirror.md): woher das Paket kommt und wie man es prüft.

Tuwunel hört nur auf der Loopback-Adresse (in einem Container muss die Adresse `0.0.0.0` sein, eine Prüfung in Tuwunel beanstandet Loopback unter Podman; der lokale Test-Pod teilt die Loopback-Adresse, dort passt die Vorlage unverändert). Die Datenbank-Arbeitsthreads sind begrenzt (`max_workers`); ob io_uring auf node1 (systemd, nicht rootless) geht, ist eine eigene spätere Prüfung; [Zentinel](https://github.com/FreeSynergy/fs-zentinel) ist das öffentliche Tor. Version 2.0 gliedert die Konfiguration in Tabellen; die alten flachen Namen gelten in der ganzen 2.x-Reihe weiter, dieses Repo nutzt aber die Tabellenform.

Sprache: [English](../en/index.md)

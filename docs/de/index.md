# FreeSynergy.Tuwunel

Tuwunel ist der Matrix-Heimserver von FreeSynergy: Chat, Anrufe und die gewöhnlichen Matrix-Konten, die KI-Teilnehmer nutzen (ADR 0054). Menschen melden sich über Kanidm an (Single Sign-on).

- [Fähigkeiten](capabilities.md): was Tuwunel bietet, nutzt und nicht kann, mit Quellen.
- [Konfiguration](configuration.md): die öffentlichen Voreinstellungen und was aus dem Tresor kommt.
- [Spiegel](mirror.md): woher das Paket kommt und wie man es prüft.

Tuwunel soll über Zentinel erreicht werden. Die Vorlage hört auf `127.0.0.1` (das Tor läuft auf demselben Rechner). In einem Container beanstandet Tuwunel eine Loopback-Adresse, dort muss die Adresse `0.0.0.0` sein; der lokale Test-Pod teilt eine Loopback-Adresse, dort passt die Vorlage unverändert. Die Datenbank-Arbeitsthreads sind begrenzt (`max_workers`, siehe Konfigurationsseite). Tuwunel nutzt io_uring über RocksDB; es war nicht die Ursache des beobachteten Startfehlers, ob es auf node1 (systemd, nicht rootless) funktioniert, ist eine eigene, noch ausstehende Prüfung. Offen: die Wirkung von `direct_io = false` und der Begrenzung auf node1; im lokalen Test lag `/data` auf einem tmpfs, nicht auf ZFS. Version 2.0 gliedert die Konfiguration in Tabellen; die alten flachen Namen gelten in der ganzen 2.x-Reihe weiter, dieses Repo nutzt aber die Tabellenform.

Sprache: [English](../en/index.md)

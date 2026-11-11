# Spiegel und Prüfung

Die Release-Dateien von Tuwunel (`.deb`, `.rpm`, Programme, Container) tragen keine Signatur, nur die SHA-256-Werte, die GitHub berechnet; Tag `v2.0.0` und Commit sind unsigniert (geprüft am 11.11.2026). Ein Wert vom selben Server sagt nichts über die Herkunft, deshalb übernimmt FreeSynergy diese Dateien nicht. Stattdessen (ADR 0068):

1. `mirror.toml` legt Tag und **Commit-SHA** fest. Der Workflow bricht ab, wenn der Upstream-Tag nicht mehr genau auf diesen Commit zeigt.
2. GitHub Actions baut aus diesem Commit (Standard-Features wie die Releases des Herstellers) und fügt das Quellcode-Archiv derselben Version (Apache-2.0) und eine SBOM hinzu.
3. Jede Datei bekommt eine OpenPGP-Signatur (`.asc`) vom FreeSynergy-Release-Schlüssel, `SHA256SUMS.txt` listet die Dateien, GitHub fügt die Herkunft des Baus hinzu.

Selbst prüfen:

```sh
scripts/verify-mirror.sh <Verzeichnis-mit-den-Release-Dateien>
```

Das Skript prüft die Signaturen gegen den Schlüssel mit dem Fingerabdruck aus `mirror.toml` (`16A4 A3EE 563A EF51 FCF0 C55D ED7B 57C4 A190 4342`) und die Prüfsummen.

Der Hersteller betreibt außerdem ein signiertes apt-Repository (`apt.f.dog`); bei der letzten Prüfung (10.10.2026) enthielt es nur 1.9.4. Es wird nicht genutzt.

Sprache: [English](../en/mirror.md)

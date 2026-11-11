# Mirror and verification

Tuwunel's release files (`.deb`, `.rpm`, binaries, containers) carry no signature, only the SHA-256 digests GitHub computes, and the tag `v2.0.0` and its commit are unsigned (checked 2026-11-11). A digest from the same server proves nothing about origin, so FreeSynergy does not take those files over. Instead (ADR 0068):

1. `mirror.toml` pins the tag and the **commit SHA**. The workflow stops unless the upstream tag still points to exactly that commit.
2. GitHub Actions builds from that commit (default features, as upstream's releases) and adds the source tarball of the same version (Apache-2.0) and an SBOM.
3. Every file gets an OpenPGP signature (`.asc`) from the FreeSynergy release key, `SHA256SUMS.txt` lists the files, and GitHub adds build provenance.

Check a release yourself:

```sh
scripts/verify-mirror.sh <directory-with-the-release-files>
```

The script verifies the signatures against the key with the fingerprint in `mirror.toml` (`16A4 A3EE 563A EF51 FCF0 C55D ED7B 57C4 A190 4342`) and the checksums.

Upstream also runs a signed apt repository (`apt.f.dog`); at the last check (2026-10-10) it offered 1.9.4 only. It is not used.

Language: [Deutsch](../de/mirror.md)

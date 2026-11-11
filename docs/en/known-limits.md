# Known limits and open items

git-bug is not set up in the FreeSynergy repositories yet, so open items live here. "Verified" means we saw it in the local Podman test (`fs-kanidm/scripts/test/podman-stack.sh`, Tuwunel 2.0.0, Kanidm 1.12.0); "from upstream docs" means we only read it.

## 1. SECURITY: the first single-sign-on user becomes admin (and gets a fallback name)

- **Verified:** In the local test the first person who signed in through Kanidm became a Tuwunel server admin without anyone asking for it. Her Kanidm name `tester@idm.test.local` (the Kanidm account name including the domain, sent as the `preferred_username` claim) is not a valid Matrix user name, so Tuwunel logged `Username invalid ... contains disallowed characters` and fell back to another claim, giving `@tester:matrix.test.local`. The registration log line said it granted admin because this was the first user.
- **From upstream docs:** `registration.grant_admin_to_first_user` is on by default: the first account that registers on a new server becomes admin ([tuwunel-example.toml](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/tuwunel-example.toml), section registration). Claims are tried in this order when `userid_claims` is empty: `preferred_username`, `username`, `nickname`, `login`, then the part of `email` before the `@` ([docs/authentication/providers.md](https://github.com/matrix-construct/tuwunel/blob/v2.0.0/docs/authentication/providers.md)). Only some claims are recognised; arbitrary ones cannot be listed.
- **Risk:** On a real server the first person to sign in after the first start would silently become server admin, and the name of that person would be a generated fallback. Who signs in first must never decide who is admin.
- **Plan (before node1):**
  1. `config/tuwunel.toml`: `grant_admin_to_first_user = false` in `[global.registration]`, so nobody becomes admin automatically.
  2. The Matrix name comes from one fixed claim: `userid_claims = ["preferred_username"]` and `unique_id_fallbacks = false` (an error instead of a random name). To make Kanidm send a clean short name, the Kanidm OAuth2 client is created with the short-username option (`kanidm system oauth2 prefer-short-username tuwunel`), so `preferred_username` is `tester`, not `tester@idm.test.local`. Both switches are checked against upstream's reference before they go in.
  3. Admin is set explicitly: `!admin users make-user-admin <username>` (or the startup command `admin.execute`, or `--execute`) as a documented setup step. Tuwunel 2.0.0 has no mapping from an identity-provider group to admin; if Kanidm group to Tuwunel admin is wanted, that is a request to upstream or our own later automation.
  4. A test case in the Podman stack: the first single-sign-on user must NOT be admin (admin status is read through the Matrix API: is the user joined to `#admins:<server_name>`, no secrets involved). It is shown red once without the setting, then green.

Language: [Deutsch](../de/known-limits.md)

# badmlabs.github.io — Org site & App Links hosting

Deploy **contents of this folder** (not the `links-site` folder itself) to the root of the
[`badmlabs.github.io`](https://github.com/badmlabs/badmlabs.github.io) repo.

## Contents

| Path | Purpose |
|------|---------|
| `index.html` | Org homepage at [badmlabs.github.io](https://badmlabs.github.io/) |
| `styles.css` | Brand styles |
| `assets/badmlabs-wordmark.png` | Wordmark image |
| `court/import/index.html` | Drill deep-link redirect into the Android app |
| `.well-known/assetlinks.json` | Android App Links verification |

## Setup

1. Enable GitHub Pages: repo **Settings → Pages →** branch `main`, folder `/ (root)`.
2. Verify:
   ```bash
   curl -I https://badmlabs.github.io/
   curl https://badmlabs.github.io/.well-known/assetlinks.json
   curl -I "https://badmlabs.github.io/court/import?d=test"
   ```

## Org profile README

The GitHub org profile README lives in [`org-profile/profile/README.md`](../org-profile/profile/README.md).

Deploy to the [`badmlabs/.github`](https://github.com/badmlabs/.github) repo:

1. Create repo `badmlabs/.github` (if it does not exist).
2. Copy `org-profile/profile/README.md` to `profile/README.md` on `main`.
3. Profile appears at [github.com/badmlabs](https://github.com/badmlabs).

Deploy the wordmark to GitHub Pages **before** the org profile README, so the image URL resolves.

## Release fingerprint

`assetlinks.json` includes the **debug** keystore SHA256 for local/emulator builds.

For Play Store builds, add your **release/upload** certificate SHA256:

```bash
keytool -list -v -keystore YOUR_RELEASE_KEYSTORE -alias YOUR_ALIAS
```

Or Play Console → **Setup → App signing → SHA-256 certificate fingerprint**.

Append the fingerprint to the `sha256_cert_fingerprints` array in `.well-known/assetlinks.json`.

## Share URL format

```
https://badmlabs.github.io/court/import?d=<base64>
```

## Future apps

Add another path (e.g. `shuttlrs/import/index.html`) and another entry in `assetlinks.json` for each Android app package.

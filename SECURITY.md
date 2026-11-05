# Security policy

## Reporting a problem

Please **don't** open a public issue for a security problem. Use GitHub's private
[**Report a vulnerability**](../../security/advisories/new) button on this repo instead, so it can be fixed
before anyone else hears about it. You'll get an answer as soon as possible.

## Supported versions

Only the [latest release](../../releases/latest) gets fixes. **Versions 1.0.0 to 1.0.4 install updates
without checking any signature. Please update.** Version 1.0.5 checks the installer's signature; 1.0.6 and
later check a signed manifest (version, file name, SHA-256), which also stops old releases being replayed.

## How releases are protected

- Every release has a `HuntTrackerSetup-x.y.z.manifest.json` signed with an Ed25519 key. The app verifies
  it against the public keys built into the app, refuses versions that aren't newer
  than the installed one, and checks the downloaded installer's size and SHA-256 against the manifest
  before running it.
- The everyday signing key is encrypted with a passphrase and never committed. A second, offline backup key
  is also trusted, so a lost or leaked everyday key can be retired without everyone reinstalling.
- GitHub immutable releases are enabled, so a published release's files can't be swapped later.

## Known limits

- The installer isn't Authenticode-signed yet, so Windows SmartScreen warns on first install. A first-time
  download can only be checked against the hash in its manifest, which also lives on GitHub.
- Kills and Hunt Dollars are read from the screen (Windows OCR); nothing is ever written to disk or sent.
- The app can't speak for Crytek or Easy Anti-Cheat. It doesn't touch game memory or inject anything.

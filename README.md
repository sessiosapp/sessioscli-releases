# sessioscli — releases

Binaries only. The source lives in a private repository; this one exists so the
downloads have a home that needs no token.

## Install

```sh
curl -fsSL https://github.com/sessiosapp/sessioscli-releases/releases/latest/download/install.sh | sh
```

Linux (x86_64, arm64) and macOS (Apple silicon, Intel). sessioscli runs inside
tmux, which the installer checks for.

## What each release holds

- **`sessioscli-<version>-<platform>.tar.gz`**: the binary, its licence and
  the third-party notices.
- **`SHA256SUMS`**: what the installer checks every archive against.
- **`latest.json` + `latest.json.minisig`**: what `sessioscli update` reads.
  The manifest names each archive with its SHA-256 and is signed; the signature
  is checked against the public key compiled into sessioscli, so a tampered
  archive is refused by the program rather than by a server anyone has to
  trust. The same key is in [`sessioscli.pub`](sessioscli.pub):

  ```sh
  minisign -Vm latest.json -p sessioscli.pub
  ```

Releases are published normally, never as pre-releases: `sessioscli update`
reads `/releases/latest/`, which skips pre-releases, and one wrong flag would
silently stop every installed copy from finding updates.

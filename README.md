# Kepler releases

Download channel for [Kepler](https://rubixkube.ai). Binaries only. The source
lives in private repositories; nothing here is built from this repository.

Published automatically by CI when a version is tagged.

## Kepler CLI

The terminal client. Normally installed from the desktop app, under
**Settings → CLI helper → Install**, which fetches the right binary for your
machine and puts `kepler` on your PATH.

To install it by hand, download the asset matching your platform, make it
executable, and put it somewhere on your PATH:

| Platform | Asset |
| --- | --- |
| macOS, Apple silicon | `kepler-cli-aarch64-apple-darwin` |
| Linux, x86_64 | `kepler-cli-x86_64-unknown-linux-gnu` |
| Windows, x86_64 | `kepler-cli-x86_64-pc-windows-msvc.exe` |

Intel Macs are not supported. The desktop app is built for Apple silicon only,
and the client needs an agent to talk to.

```sh
chmod +x kepler-cli-aarch64-apple-darwin
mv kepler-cli-aarch64-apple-darwin ~/.local/bin/kepler
```

The client talks to a Kepler agent over a local connection. Today the desktop
app is what runs one, so install the app first.

On macOS the binary is not notarized yet, so Gatekeeper will refuse a
hand-downloaded copy until you clear it:

```sh
xattr -d com.apple.quarantine ~/.local/bin/kepler
```

Installing from the app does not hit this.

## Versions

Asset versions track the Kepler release they shipped with, so a CLI from tag
`v0.0.6-alpha` is the one built to talk to that version's agent. Mixing versions
is not supported: the client speaks a fair amount of the agent's API and the two
are only guaranteed to agree within a release.

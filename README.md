# Kepler releases

Download channel for [Kepler](https://trykepler.rubixkube.ai), the SRE IDE by
[RubixKube](https://rubixkube.ai). Kepler is a desktop app you run on your own machine. It
investigates with a real terminal and browser, keeps a local memory of your systems, watches
the things you care about, runs automations for you, and acts only when you allow it.

This repository carries binaries only. The source lives in private repositories and nothing
here is built from this one. Releases are published by CI when a version is tagged and a
human presses publish.

Kepler is in beta. Expect rough edges, and tell us about them: open an
[issue](https://github.com/rubixkube-io/kepler-releases/issues) here, or find us on Discord.

## Download

The current version is always at
**[releases/latest](https://github.com/rubixkube-io/kepler-releases/releases/latest)**.

| Platform | Asset | Notes |
| --- | --- | --- |
| macOS, Apple silicon | `Kepler-<version>-arm64.dmg` | macOS 13 or newer. Intel Macs are not supported. |
| Windows, x64 | `Kepler_<version>_x64-setup.exe` | Windows 10 or newer. |
| Linux, Debian and Ubuntu | `Kepler-<version>-amd64.deb` | Needs `libwebkit2gtk-4.1-0` and `libgtk-3-0`. |
| Linux, Fedora, RHEL and openSUSE | `Kepler-<version>-x86_64.rpm` | Needs `webkit2gtk4.1` and `gtk3`. |
| Linux, Arch | `Kepler-<version>-x86_64.pkg.tar.zst` | |

The other files on a release (`.app.tar.gz`, `.sig`, `latest-*.json`, `kepler-cli-*`) are what
the app's own updater and CLI installer read. You do not need them.

## Install

**macOS.** Open the DMG and drag Kepler to Applications. The app is signed and notarized, so it
opens without warnings. If macOS says the app is damaged, you have a build from before signing
was set up; download the current release again.

**Windows.** Run the installer. Until code signing lands, SmartScreen shows "Windows protected
your PC". Click "More info", then "Run anyway". The installer is the one published here; the
warning is about the missing certificate, not the file.

**Linux.**

```sh
# Debian, Ubuntu
sudo apt install ./Kepler-<version>-amd64.deb

# Fedora, RHEL, openSUSE
sudo dnf install ./Kepler-<version>-x86_64.rpm

# Arch
sudo pacman -U ./Kepler-<version>-x86_64.pkg.tar.zst
```

On first launch Kepler signs you in, or you can bring your own model keys in Settings. Keys
never leave your machine.

## Updates

Kepler checks this repository for a newer version when it starts and every few hours after
that. When one exists, a line appears at the bottom of the sidebar. On macOS and Windows,
clicking it downloads the update, installs it in place, and offers a restart. On Linux it
links back here, because the packages above update through your package manager.

Nothing installs without your click. Settings, General has a manual check.

## Kepler CLI

The terminal client. Normally installed from the desktop app, under
**Settings, Experiments, CLI helper, Install**, which fetches the right binary for your
machine and puts `kepler` on your PATH.

To install it by hand, download the asset matching your platform, make it executable, and put
it somewhere on your PATH:

| Platform | Asset |
| --- | --- |
| macOS, Apple silicon | `kepler-cli-aarch64-apple-darwin` |
| Linux, x86_64 | `kepler-cli-x86_64-unknown-linux-gnu` |
| Windows, x86_64 | `kepler-cli-x86_64-pc-windows-msvc.exe` |

```sh
chmod +x kepler-cli-aarch64-apple-darwin
mv kepler-cli-aarch64-apple-darwin ~/.local/bin/kepler
```

The client talks to a Kepler agent over a local connection. The desktop app is what runs one,
so install the app first.

On macOS the CLI binary is not notarized yet, so Gatekeeper refuses a hand-downloaded copy
until you clear it:

```sh
xattr -d com.apple.quarantine ~/.local/bin/kepler
```

Installing from the app does not hit this.

## Versions

Every asset on a release belongs to that release's tag, and the CLI on a release is the one
built to talk to that release's agent. Mixing versions is not supported: the client speaks a
fair amount of the agent's API and the two are only guaranteed to agree within a release.

When the CLI has not changed, a release carries the same CLI binaries as the one before it.
Take the CLI from the same release as your app all the same.

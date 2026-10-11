# Echocue CLI downloads

Official Developer ID signed, Apple-notarized Echocue CLI downloads.
No GitHub account, repository access, sudo, Xcode, or Python is required to install.
This repository contains distribution files and documentation only. The Echocue
product source remains private; publishing these binaries does not grant a source
code license.

## Install

Download the bootstrap, inspect it if desired, then execute it:

```sh
curl -fL https://github.com/burger66leo/echocue-cli-releases/releases/latest/download/install.sh -o /tmp/echocue-cli-install.sh
bash /tmp/echocue-cli-install.sh
export PATH="$HOME/.local/bin:$PATH"
echocue --help
echocue status --json
```

The bootstrap uses an immutable release URL and pinned SHA-256, then executes
the ZIP's installer. That installer checks Apple's signed identity and
Gatekeeper acceptance. No quarantine removal or Gatekeeper changes are made.
It installs the intact App Group profile-bearing bundle into
`~/.local/share/echocue-cli/EchocueCLI.app` and links `~/.local/bin/echocue`.
It retains the previous bundle when upgrading and refuses unrelated executables.
Shell profiles and Agent settings are not modified automatically.

[Download the ZIP manually](https://github.com/burger66leo/echocue-cli-releases/releases/latest).
Verify it with SHA256SUMS, extract it, then run `bash echocue-cli/install.sh`.
`--prefix /absolute/path` selects a different install prefix.

## Requirements

- macOS 26 or later; universal arm64/x86_64 CLI.
- Library commands require Echocue 27.1.2 or later on an Apple silicon Mac
  (the Designed for iPad App, from App Store or TestFlight).
- App Store 27.1.2 is in review at the time of this release; existing TestFlight
  testers can use build 12. Downloading the CLI does not grant TestFlight access.
- Pro enables the App's existing private iCloud sync. Offline document commands
  do not require the main App.

## Agents

Expose `~/.local/bin` in PATH, then read `echocue --help` and
`echocue capabilities --connected --json`. Always use `--json` for machine results.
The package includes optional SKILL.md guidance; no skill installation is required.

```sh
echocue library import script.md --json
```

The CLI talks to the main App's script repository, with no companion service or
second sync database. `app_update_required` means update the main App;
`app_unavailable` means open the App and let its library finish loading.
`local_committed` means the Mac saved the script, not that another device received it.

The notarization ticket is stapled to the App bundle. release.json records the
artifact version, checksum, architectures and Apple notarization result.

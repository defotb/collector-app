# OutsideTheBox Collector App

**Installation Guide:** [INSTALLATION.md](INSTALLATION.md)

Multichain Geth node collector for the OutsideTheBox
Node Directory.

## Version

Collector App: v2.0.0

Supported networks:
- Altcoinchain (ALT)
- Etho Protocol (ETHO)
- Etica (EGAZ)

Installer: v2.0.0{alt,etho,etica}
Supporting components: v2.0.0{alt,etho,etica}

## Components

- otb-install.py — installer and lifecycle management
- otb-collect.py — node observation
- otb-push.py — authenticated submissions
- otb-run.py — collector runner

## Download

https://nodelist.outsidethebox.top/downloads/otb-install.py

The installer downloads supporting files from the
Node Directory and verifies their SHA-256 checksums.

### Install from GitHub

Clone the repository:

    git clone https://github.com/defotb/collector-app.git
    cd collector-app
    git checkout v2.0.0
    sudo python3 otb-install.py --probe
    sudo python3 otb-install.py --preflight
    sudo python3 otb-install.py --install

The installer downloads verified components from the OTB Node Directory server.

## Installation

Download:

    curl -fLO https://nodelist.outsidethebox.top/downloads/otb-install.py

Inspect available commands:

    python3 otb-install.py --help

Discover local Geth services:

    python3 otb-install.py --probe

Interactively prepare installation:

    python3 otb-install.py --plan

Check installation readiness:

    python3 otb-install.py --preflight

Install and enroll:

    sudo python3 otb-install.py --install

## Management

List installed collectors:

    sudo python3 otb-install.py --list

Validate installations:

    sudo python3 otb-install.py --validate

Preview removal:

    sudo python3 otb-install.py --uninstall-preview

The installer also supports --resume and --uninstall.

## Enrollment

New collectors require authorization from the
Node Directory. Pending collectors are displayed
separately until administrator approval.

## Security

Never commit authentication tokens, private keys,
machine credentials, or runtime configuration.

## Links

Node Directory:
https://nodelist.outsidethebox.top/

GitHub:
https://github.com/defotb/collector-app

Releases:
https://github.com/defotb/collector-app/releases

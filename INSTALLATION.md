# OTB Collector App — Installation Guide

The OutsideTheBox (OTB) Collector App collects node and peer information
from Altcoinchain, ETHO and Etica blockchain nodes and submits observations to the
OTB Node Directory.

Supported blockchains:
- Altcoinchain (ALT)
- ETHO (Etho Protocol)
- Etica

Current release: **v2.0.0**

### Install from GitHub

Clone the repository:

    git clone https://github.com/defotb/collector-app.git
    cd collector-app
    git checkout v2.0.0
    sudo python3 otb-install.py --probe
    sudo python3 otb-install.py --preflight
    sudo python3 otb-install.py --install

The installer downloads verified components from the OTB Node Directory server.

## 1. Requirements

Before installing, ensure you have:

- A Linux server running an ALT, ETHO or Etica Geth node
- Python 3
- systemd
- A working Geth IPC socket
- Internet connectivity to `nodelist.outsidethebox.top`
- sudo/root access for installation

The Geth service must be running and accessible through its IPC socket.

The installer automatically discovers compatible Geth services and
verifies their blockchain network IDs.

## 2. Download the Installer

Download the latest stable installer:

```bash
wget https://nodelist.outsidethebox.top/downloads/otb-install.py

```

The installer automatically downloads and verifies the required collector components.

## 3. Install a New Collector

Run:

```bash
sudo python3 otb-install.py --install
```

Follow the interactive prompts to select your Geth service, enter a collector identity, review the installation, and register with the OTB Node Directory.

The installer verifies the network ID and performs a local collection test before registration.

Successful installation creates:

- Configuration files in `/etc/otb-collector/`
- Private collector data in `/var/lib/otb-collector/`
- Shared scripts in `/usr/local/lib/otb-collector/`
- A systemd collector service and timer

The collector runs approximately every 60 seconds.

## 4. Registration and Approval

New collectors are automatically registered with **PENDING** status.

An administrator must approve the registration before the collector appears in the public directory.

Pending Explorer: https://nodelist.outsidethebox.top/pending/

Public Explorer: https://nodelist.outsidethebox.top/

Authentication tokens are stored securely. Never publish or share them.

## 5. Update an Existing Collector

Download the latest installer:

```bash
wget -O otb-install.py https://nodelist.outsidethebox.top/downloads/otb-install.py
```

Run:

```bash
sudo python3 otb-install.py --update
```

Choose between:

1. Updating an existing managed collector.
2. Migrating a legacy collector using its existing identity and token.

Updates preserve existing authentication credentials and registrations.

Legacy migrations may require a second step:

```bash
sudo python3 otb-install.py --resume
```

For legacy migrations, verify a successful authenticated upload before retiring the original collector timer.

## 6. Check Collector Status

List managed collectors:

```bash
sudo python3 otb-install.py --list
```

Check a collector timer:

```bash
systemctl status otb-collector-<chain>-<collector>.timer
```

Check recent uploads:

```bash
sudo journalctl -u otb-collector-<chain>-<collector>.service -n 30 --no-pager
```

Replace `<chain>` and `<collector>` with your installed values.

Successful uploads report:

```text
Upload HTTP: 200
Server response: Observation accepted
```

## 7. Collector App Version

Starting with v1.0.4, collectors report their installed Collector App version.

The version is displayed in the Public and Pending Node Explorers.

## 8. Project Links

Collector App: https://github.com/defotb/collector-app

Node Directory: https://nodelist.outsidethebox.top/

Multiple ALT, ETHO and Etica collectors can operate on one Linux server with separate credentials and configurations while sharing the collector software.

---
weight: 10
date: "2023-05-03T22:37:22+01:00"
draft: false
author: "Parash Maity"
title: "Download"
icon: "download"
toc: true
description: "Fleare Download the archive from your preferred source"
publishdate: "2023-05-03T22:37:22+01:00"
tags: ["Linux"]
---


{{< download type="Linux" >}}

{{< tabs tabTotal="3">}}
{{% tab tabName="Linux" %}}

#### Linux Installation

##### Prerequisites

Ensure the following are installed on your Linux system:

* `curl` or `wget`
* `unzip`
* `shell`
* `systemctl` (for systemd-based Linux systems)

You can install missing dependencies using:

```shell
sudo apt update && sudo apt install -y curl unzip
```

---

##### 1. Download the ZIP File

Download the archive from your preferred source:

```shell
curl -L "https://www.fleare.com/download/binary/fleare-1-0-1-linux-amd64.tar.gz" -o fleare-1-0-1-linux-amd64.tar.gz
```
Or Extract directly

```shell
curl -L "https://www.fleare.com/download/binary/fleare-1-0-1-linux-amd64.tar.gz" \
  | tar -xz
```
---

##### 2. Extract the ZIP File

Unzip the contents to a temporary directory:

```shell
mkdir -p fleare_install
tar -xvzf fleare-1-0-1-linux-amd64.tar.gz -C fleare_install
cd fleare_install
```

Expected contents:


```treeview
fleare_install/
    ├── README.md
    ├── install.sh
    └── fleare (binary)
```

---

#### 2. **Run the Installer Script permissions**

```shell 
chmod +x install.sh
```

#### 3. **Run the Installer Script**
```shell 
./install.sh
```

or

```shell 
sudo ./install.sh
```


##### 4. Check Service Status

Once installed, verify that the service is running:

```shell
systemctl status fleare
```

Expected output:

```
● fleare.service - Fleare Service
   Loaded: loaded (/etc/systemd/system/fleare.service; enabled; vendor preset: enabled)
   Active: active (running) ...
```

To check logs:

```shell
journalctl -u fleare -f
```

---

##### 5. (Optional) Restart or Stop the Service

```shell
sudo systemctl restart fleare    # Restart
sudo systemctl stop fleare       # Stop
```

#### Note

Refer to `README.md` inside the ZIP file for any custom configurations or usage instructions specific to your system.

---

{{% /tab %}}

{{% tab tabName="Mac OS" %}}

### macOS Installation Guide

#### Prerequisites

Ensure the following tools are available on your macOS system:

* `curl` or `wget`
* `unzip` or `tar`
* `bash` or compatible shell

To install missing tools (using [Homebrew](https://brew.sh)):

```bash
brew install curl unzip
```

---

#### 1. Download the Archive

Use `curl` or `wget` to download the archive:

```bash
curl -O "https://www.fleare.com/download/binary/fleare-1-0-1-darwin-arm64.tar.gz"
```

> **Note:** Ensure you're downloading the **macOS version** of the binary (`fleare-1-0-1-darwin-arm64.tar.gz`).

---

#### 2. Extract the Archive

Use `tar` to extract the `.tar.gz` file:

```bash
mkdir fleare_install
tar -xzf fleare-1-0-1-darwin-arm64.tar.gz -C fleare_install
cd fleare_install
```

Expected contents:

```treeview
fleare_install/
    ├── README.md
    ├── install.sh
    └── fleare (binary)
```

---

#### 3. Run the Installer Script

Make the script executable:

```bash
chmod +x install.sh
```

Run the script:

```bash
./install.sh
```

If elevated permissions are needed:

```bash
sudo ./install.sh
```

---

#### 4. Run Fleare as a Background Service (Optional)

To set it up as a **LaunchAgent** (for user-level services):

1. Create a `plist` file at `~/Library/LaunchAgents/com.fleare.service.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" 
"http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.fleare.service</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/fleare</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>StandardOutPath</key>
    <string>/usr/local/fleare/log/fleare.log</string>
    <key>StandardErrorPath</key>
    <string>/usr/local/fleare/log/fleare.err</string>
</dict>
</plist>
```

2. Load the agent:

```bash
launchctl load ~/Library/LaunchAgents/com.fleare.service.plist
```

3. To stop it:

```bash
launchctl unload ~/Library/LaunchAgents/com.fleare.service.plist
```

---

#### 5. Check Fleare Logs (if running as background process)

```bash
tail -f /usr/local/fleare/log/fleare.log
```

---

#### Notes

* The `README.md` inside the archive may include custom configurations or usage.
* On macOS Services should be run with `launchctl` or manually in the background.

{{% /tab %}}

{{< /tabs >}}

Here's a **User Installation Manual** document for the provided `fleare` installation script.

---

# **Fleare Database Installation Manual (macOS arm64 Only)**

## 📄 Overview

This manual will guide you through the installation and initial setup of the `Fleare` database on macOS using the provided Bash installation script.

---

## 🖥️ System Requirements

* **Operating System**: macOS arm64 (required)
* **Privileges**: Root/admin privileges (for directory creation and file placement)
* **Binary**: Ensure the compiled `fleare` binary is present in the same directory as the script

---

## 📁 Installation Steps

### 1. **Prepare the Environment**

Before running the script, ensure:

* The script file is saved, e.g., `install.sh`
* The `fleare` binary file is compiled and available in the same directory

```bash
ls
# Output should include:
# install.sh  fleare
```

---

### 2. **Run the Installer**

Make the script executable:

```bash
chmod +x install.sh
```

Then run the script using `sudo` to allow system modifications:

```bash
sudo ./install.sh
```

---

### 3. **Script Actions Explained**

The script will:

* **Verify Operating System**: Checks if the OS is macOS
* **Create Directories**:

  * Configuration: `/etc/fleare`
  * Logs: `/usr/local/fleare/log`
  * Data: `/usr/local/fleare/db`
  * Backups: `/usr/local/fleare/backups`
* **Copy Binary**: Installs the `fleare` binary to `/usr/local/bin/fleare` and makes it executable
* **Generate Default Configuration**: Creates `config.yaml` with standard settings at `/etc/fleare/config.yaml`

---

## ⚙️ Configuration File

**Path**: `/etc/fleare/config.yaml`

This file controls all runtime behavior. Default sections include:

* **Server Settings**
* **Logging**
* **Memory Limits & Policies**
* **Security & Authentication**
* **Persistence Settings**
* **Sharding Configuration**
* **Backup Scheduling**
* **Miscellaneous Options**

💡 **Tip**: Modify the configuration file to suit your deployment requirements before running the server.

---

## 🧪 Verification

After installation:

```bash
which fleare
# Should return: /usr/local/bin/fleare

cat /etc/fleare/config.yaml
# Should display the configuration file
```

---

## 🚀 Starting the Application

Once installed, run:

```bash
fleare
```

Monitor the logs:

```bash
tail -f /usr/local/fleare/log/fleareDB.log
```

---

## 🔐 Default Credentials

* **Username**: `root`
* **Password**: `root`
  ⚠️ *Change this in production environments.*

---

## 📦 Backup & Persistence

* **Backups**: Enabled every 60 minutes
* **Persistence**: Data saved to `/usr/local/fleare/db` after every 100 writes

---

## 🧹 Uninstallation (Manual)

To remove all installed files:

```bash
sudo rm /usr/local/bin/fleare
sudo rm -rf /usr/local/fleare
sudo rm -rf /etc/fleare
```

---

## 📞 Support

For assistance, please contact the Fleare development team or visit the repository documentation.

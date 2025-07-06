---
weight: 10
date: "2023-05-03T22:37:22+01:00"
draft: false
author: "Parash Maity"
title: "Config"
icon: "settings"
toc: true
showTitle: false
description: "Fleare `config.yaml` Configuration Reference"
publishdate: "2023-05-03T22:37:22+01:00"
tags: ["Config"]
---

---

#### Fleare `config.yaml` Configuration Reference

The `config.yaml` file is the primary configuration file for Fleare, your high-performance, in-memory database. This document describes all available configuration sections and attributes.

---

#### Server Settings

```yaml
server:
  host: "127.0.0.1"
  port: 9210
```

* **`host`**: The IP address Fleare should bind to.

  * Example: `"0.0.0.0"` to listen on all interfaces, or `"127.0.0.1"` for localhost-only access.
* **`port`**: The port number the database server listens on.

  * Default: `9210`.

---

#### Logging Settings

```yaml
logging:
  level: "info"
  file: "/usr/local/fleare/log/fleareDB.log"
```

* **`level`**: Controls the verbosity of logs. Valid options:

  * `"debug"` – Most detailed logging (for development)
  * `"info"` – General operational logs (recommended for production)
  * `"warn"` – Only warnings and errors
  * `"error"` – Errors only
* **`file`**: The absolute path to the log file where Fleare will write logs.

---

#### Memory Settings

```yaml
memory:
  max_size_mb: 1024
  eviction_policy: "LRU"
```

* **`max_size_mb`**: Maximum allowed memory (in megabytes) that Fleare can use for storing in-memory data.
* **`eviction_policy`**: Strategy used when memory is full:

  * `"LRU"` – Least Recently Used (default)
  * `"LFU"` – Least Frequently Used
  * `"FIFO"` – First In, First Out

---

#### Security Settings

```yaml
security:
  enable_auth: true
  auth_method: "basic"
  users:
    - username: "root"
      password: "root"
      role: "root"
```

* **`enable_auth`**: Enable or disable user authentication (`true`/`false`).
* **`auth_method`**: Method of authentication. Supported options:

  * `"basic"` – Username/password-based
  * `"token"` – Token-based (if implemented)
* **`users`**: List of user credentials.

  * `username`: Login username.
  * `password`: Login password (plain-text here; use hashed values in production).
  * `role`: User role (e.g., `"root"` for full access). Role-based permissions can be extended in future versions.

---

#### Data Persistence

```yaml
persistence:
  enable: true
  path: "/usr/local/fleare/db"
  after_write_count: 1
```

* **`enable`**: Enable/disable on-disk data persistence.
* **`path`**: Filesystem path where data files are stored.
* **`after_write_count`**: Number of write operations after which Fleare persists data to disk.

  * Example: `1` = persist after every write (safe, but may affect performance); higher values = batch persistence.

---

#### Shard Settings

```yaml
shard:
  mode: "local"
  shard_count: 2
```

* **`mode`**: Sharding mode.

  * `"local"` – All shards run locally on the same server.
  * Future modes (e.g., `"cluster"`) can be supported in distributed setups.
* **`shard_count`**: Number of memory shards to distribute data across.

  * Improves concurrency and performance.

---

#### Backup Settings

```yaml
backup:
  enable: true
  interval_minutes: 60
  backup_dir: "/usr/local/fleare/backups"
```

* **`enable`**: Enables automatic periodic backups (`true`/`false`).
* **`interval_minutes`**: Frequency of backup in minutes.
* **`backup_dir`**: Directory to store backup files.

---

#### Miscellaneous Settings

```yaml
misc:
  max_connections: 200
  timeout_seconds: 30
  strict_mode: true
```

* **`max_connections`**: Maximum concurrent client connections allowed.
* **`timeout_seconds`**: Timeout duration (in seconds) for handling client requests.
* **`strict_mode`**: Enables strict validation of commands and data formats.

  * If `true`, invalid requests are rejected with descriptive errors.
  * Useful for development and debugging.

---

#### Sample Configuration

```yaml
# Server settings
server:
  host: "127.0.0.1" # Listen on all network interfaces
  port: 9210 # Port number for the database server

# Logging settings
logging:
  level: "info" # Logging level: debug, info, warn, error
  file: "/usr/local/fleare/log/fleareDB.log" # Log file path

# Memory settings
memory:
  max_size_mb: 1024 # Maximum memory usage in MB
  eviction_policy: "LRU" # Eviction policy: LRU, LFU, FIFO

# Security settings
security:
  enable_auth: true # Enable authentication
  auth_method: "basic" # Authentication method: basic, token, etc.
  users:
    - username: "root"
      password: "root" # In a real-world scenario, use hashed passwords!
      role: "root"

# Data persistence
persistence:
  enable: true # Enable data persistence
  path: "/usr/local/fleare/db" # Path to store data
  after_write_count: 1 # save data on Path after

shard:
  mode: "local" # Path to store data
  shard_count: 2 # save data on Path after

# Backup settings
backup:
  enable: true # Enable automated backups
  interval_minutes: 60 # Backup interval in minutes
  backup_dir: "/usr/local/fleare/backups"

# Other settings
misc:
  max_connections: 200 # Maximum number of client connections
  timeout_seconds: 30 # Timeout for client requests
  strict_mode: true

```

---


---
weight: 9
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "CONNECT"
icon: "arrow_range"
toc: true
showTitle: false
description: "Fleare CLI is a command-line client designed for communicating with a Fleare in-memory server"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["CONNECT"]
---


##### Fleare CLI Installation

Fleare CLI is a command-line client designed for communicating with a Fleare in-memory server. It allows users to send commands, authenticate, and receive responses in a structured format.

---

{{< tabs tabTotal="3">}}
{{% tab tabName="Linux" %}}

##### Install using `curl` or `wget`

To install the Fleare CLI directly using a one-liner:

**Using `curl` or `wget`:**

`Linux ARM-64`
```sh
wget https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-arm64.zip
```

```sh
curl https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-arm64.zip
```
---
`Linux AMD-64`
```sh
wget https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-amd64.zip
```

```sh
curl https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-amd64.zip
```
---

##### Install binary by downloading files

1. Visit the [Fleare CLI Releases](https://github.com/extendsware/fleare-cli/releases/latest) page.
2. Download the ZIP or TAR file matching your OS and architecture (e.g., `fleare-cli-darwin-X.X.X-x64.zip`).
3. Unzip it:

   ```sh
   unzip fleare-cli-v1.0.1-darwin-arm64.zip
   ```
4. Move the binary to a directory in your `PATH`:

   ```sh
   sudo mv fleare-cli /usr/local/bin/fleare-cli
   chmod +x /usr/local/bin/fleare-cli
   ```


{{% /tab %}}
{{% tab tabName="MacOS" %}}

##### Install using `curl` or `wget`

To install the Fleare CLI directly using a one-liner:

**Using `curl` or `wget`:**

`ARM-64`
```sh
wget https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-arm64.zip
```

```sh
curl https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-arm64.zip
```
---
`AMD-64`
```sh
wget https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-amd64.zip
```

```sh
curl https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-darwin-amd64.zip
```
---

##### Install binary by downloading files

1. Visit the [Fleare CLI Releases](https://github.com/extendsware/fleare-cli/releases/latest) page.
2. Download the ZIP or TAR file matching your OS and architecture (e.g., `fleare-cli-darwin-X.X.X-x64.zip`).
3. Unzip it:

   ```sh
   unzip fleare-cli-v1.0.1-darwin-arm64.zip
   ```
4. Move the binary to a directory in your `PATH`:

   ```sh
   sudo mv fleare-cli /usr/local/bin/fleare-cli
   chmod +x /usr/local/bin/fleare-cli
   ```


{{% /tab %}}
{{% tab tabName="Windows" %}}

##### Download cli binary
`Windows-amd64` -> [fleare-cli-v1.0.1-windows-amd64.exe.zip](https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-windows-amd64.exe.zip)

`Windows-arm` -> [fleare-cli-v1.0.1-windows-arm.exe.zip](https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-windows-arm.exe.zip)

`Windows-arm64` -> [fleare-cli-v1.0.1-windows-arm64.exe.zip](https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-windows-arm64.exe.zip)

`Windows-386` -> [fleare-cli-v1.0.1-windows-386.exe.zip](https://www.fleare.com/download/binary/cli/fleare-cli-v1.0.1-windows-386.exe.zip)


{{% /tab %}}
{{< /tabs >}}


---

##### Check installation status

Verify that Fleare CLI is installed and accessible:

```sh
fleare-cli version
```

Expected response:

```sh
fleare-cli
Version: v1.0.1
Build Date: 2025-07-05
```

##### Connecting localhost with `enable_auth: false`
```sh
fleare-cli
```

```js
Ok Connected
127.0.0.1:9219>
```

---

##### Command-Line Arguments

##### Authenticate

The CLI accepts the following command-line arguments:

| Flag    | Description                 | Default     |
| ------- | --------------------------- | ----------- |
| `--host` | Server host address         | `127.0.0.1` |
| `--port` | Server port                 | `9219`      |
| `-u`    | Username for authentication | Optional    |
| `-p`    | Password for authentication | Optional    |

Example usage:

```sh
fleare-cli --host 192.168.0.1 --port 9219 -u admin -p <secret>
```

---

##### Features

* **Authentication**: Authenticate using a username and password.
* **Command Execution**: Send structured commands to the Fleare server.
* **Response Parsing**: Automatically parse and display JSON responses.
* **Command History**: Maintains history at `~/.Fleare_history`.
* **Graceful Exit**: Supports `CTRL+C` for safe termination.

---

##### Authentication Flow

Once the CLI establishes a TCP connection to the server:

1. It sends the provided username and password.
2. If credentials are valid, the server responds with:

```js
Ok Connected
127.0.0.1:9219>
```

After a successful connection, you can begin issuing commands immediately.

##### More Configuration
Visit [Fleare config](/docs/configure/config)
---
title: CLI Commands
is_title_visible: true
description: Fleare CLI Documentation for Bash
date: '2021-07-01T05:26:12.863Z'
is_breadcrumb_visible: true
is_menu_transparent: false
is_menu_visible: true
is_navigation_button_visible: false
is_table_of_content_visible: false
is_left_navigation_visible: true
is_root_content_hidden: false
is_folder_visible_in_listing: true
padding: 15px 0
draft: false
is_summary_visible: true
is_taxonomy_visible: true
icon: terminal
weight: 1000000
---
# Fleare CLI Documentation

## Overview
Fleare CLI is a command-line client designed for communicating with an Fleare in-memory server. It allows users to send commands, authenticate, and receive responses in a structured format.

Check `Fleare-cli` is installed currently :
```sh
Fleare --version
```
Response:
```sh
Version: Fleare version v1.0.0
Platform: linux/amd64
```

## Command-Line Arguments
### Authenticate
The CLI accepts the following command-line arguments:

| Flag        | Description                                    | Default         |
|------------|--------------------------------|---------------|
| `-host`     | Server host address               | `127.0.0.1`   |
| `-port`     | Server port                       | `4775`        |
| `-u`        | Username for authentication      | Required      |
| `-p`        | Password for authentication      | Required      |

Example usage:
```sh
Fleare-cli -host 192.168.0.1 -port 4775 -u admin -p <secret>
```

## Features
- **Authentication**: Users must authenticate with a username and password.
- **Command Execution**: Send commands to the server with parameters.
- **Response Parsing**: Parses JSON responses from the server.
- **Command History**: Stores command history in `~/.Fleare_history`.
- **Graceful Exit**: Handles `CTRL+C` to prompt for an exit command.

## Authentication
Once the CLI establishes a TCP connection with the server, it sends the username and password for authentication. If the authentication succeeds, the server responds with `CONNECTED`.



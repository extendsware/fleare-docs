---
draft: false
title: PING
is_title_visible: false
description: Sends a PING command to the server and receives a PONG response.
date: '2021-09-01T05:26:12.863Z'
authors: "Parash Maity"
is_breadcrumb_visible: true
is_menu_transparent: false
is_menu_visible: true
is_navigation_button_visible: false
is_table_of_content_visible: true
is_left_navigation_visible: true
is_root_content_hidden: false
padding: 15px 0
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
weight: 1000000
id: /documentations/cli-commands/ping.md
__system:
  last_published: '2025-06-21T20:35:27.634Z'
  new: false
  created_by: i-602132207af9e10032069067
---
---

#### Command: `PING` 

***

 `PING` 

#### **Description**

Sends a **PING** command to the server and receives a **PONG** response.
Optionally, arguments can be passed which are echoed back after `PONG` .

This is commonly used to check if the server is responsive (like a health check or heartbeat).

***

#### **Syntax**

```bash 
PING [<args>]
```

*  `PING` : The base command

*  `<args>` (optional): Any additional string(s) you want to send. The server will echo them back after `PONG` .

***

#### **Examples**

##### **Example 1: Simple Ping**

**Input:**

```bash 
localhost:9219> ping
```

**Output:**

```bash 
Ok PONG
```

***

##### **Example 2: Case-insensitive Command**

**Input:**

```bash 
localhost:9219> PING
```

**Output:**

```
Ok PONG
```

***

##### **Example 3: Ping with Arguments**

**Input:**

```bash 
localhost:9219> ping hello world
```

**Output:**

```bash 
Ok PONG hello world
```

***

#### **Behavior**

* The server reads the command using the `Cmd` structure.

* It prepends `PONG` to the joined string of provided arguments.

* Returns the full response as `PONG <args>` .

* The result is wrapped in a `comm.Response` object and sent back as `CmdResponse` .

***

#### **Use Cases**

* Connectivity test between client and server.

* Latency/response check.

* Debugging input arguments being received by the server.

 

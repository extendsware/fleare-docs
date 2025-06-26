---
draft: false
title: TTL.EXPIRE
is_title_visible: false
description: The TTL.EXPIRE command is used to set a Time-To-Live (TTL) on a key.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T18:07:56.477Z'
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
id: /documentations/cli-commands/ttl-commands/ttl-expire.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.469Z'
---
#### Command: `TTL.EXPIRE` 

***

#### Overview

The `TTL.EXPIRE` command is used to set a **Time-To-Live (TTL)** on a key. Once the specified duration elapses, the key is **automatically deleted** from the database. This feature is helpful for scenarios involving **temporary data**, **session expiration**, or **auto-cleanup mechanisms**.

#### Description

Sets a TTL (Time-To-Live) on an existing key. The TTL determines how long the key remains in the system before it is automatically removed. Time can be specified in:
* Default (Seconds)
* Seconds ( `s` )

* Minutes ( `m` )

* Hours ( `h` )

* Days ( `d` )

```
If the key does not exist, the command returns 0.
```

```
If TTL is set successfully, the command returns 1.
```

#### Use Cases

* Expiring temporary session tokens after 30 minutes.

* Automatically deleting cache entries after 2 hours.

* Setting a key to expire in 7 days for time-limited promotions or trials.

* Managing lifecycle of transient data.

***

#### Syntax

```bash 
TTL.EXPIRE <key> <duration>
```

Where `<duration>` can be:

* A number (in seconds by default)

* A duration with unit suffix:

  *  `10s` → 10 seconds

  *  `15m` → 15 minutes

  *  `2h` → 2 hours

  *  `3d` → 3 days

#### Permissions

* User must have **write permission** on the specified key.

* If ACLs are implemented in your environment, ensure the user has permission for `expire` or `ttl` operations.

##### Examples

##### Set TTL with various formats

```bash 
localhost:9219> SET mykey "Hello"
OK

localhost:9219> TTL.EXPIRE mykey 10
Ok 1

localhost:9219> TTL.EXPIRE mykey 10s
Ok 1

localhost:9219> TTL.EXPIRE mykey 10m
Ok 1

localhost:9219> TTL.EXPIRE mykey 2h
Ok 1

localhost:9219> TTL.EXPIRE mykey 1d
Ok 1
```

##### Trying to expire a non-existent key

```bash 
localhost:9219> TTL.EXPIRE unknownKey 30s
Ok 0
```

***

#### Behavior on Error

| Error Scenario                   | Output/Error Message                                   |
| -------------------------------- | ------------------------------------------------------ |
| Missing key or duration argument |  `InvalidArgsError: Key and time must be provided...`  |
| Invalid duration format          |  `InvalidArgsError: Invalid time value provided`       |
| Key does not exist               |  `Ok 0`                                                |

 

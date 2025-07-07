---
draft: false
title: TTL
is_title_visible: false
description: >-
  The TTL command checks the remaining time-to-live (in seconds) for a specific
  key in the database.

date: '2025-06-20T18:19:37.082Z'
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
weight: 2000000
id: /documentations/cli-commands/ttl-commands/ttl.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.470Z'
---
#### Command: `TTL` 

***

#### Overview

The `TTL` command checks the **remaining time-to-live (in seconds)** for a specific key in the database. It's useful for understanding when a key is going to expire or confirming whether it has an expiration at all.

#### Command Name

**TTL**

#### Description

The `TTL` command returns the time remaining before a key expires:

* Returns `-2` if the key does **not exist**.

* Returns `-1` if the key exists but **does not have an expiry** set.

* Returns **a positive integer (in seconds)** indicating how much time is left before expiration.

#### Use Cases

* Check how much longer a session or cache key is valid.

* Debug TTL-related logic in applications (e.g., auto-expiring keys).

* Verify if a key has expired or not.

* Check the difference between keys with and without expirations.

***

#### Syntax

```bash 
TTL <key>
```

*  `<key>` : The name of the key you want to check for time-to-live.

***

#### Permissions

* Requires **read access** to the key.

* No special write permissions are required.

#### Examples

#### Check TTL on a valid key with expiration:

```bash 
localhost:9219> TTL.EXPIRE mykey 120
OK 1

localhost:9219> TTL mykey
Ok 85
```

Explanation:

*  `TTL.EXPIRE mykey 120` sets a TTL of 120 seconds.

*  `TTL mykey` returns the remaining TTL (e.g., 85 seconds).

#### Check TTL on a nonexistent key:

```bash 
localhost:9219> TTL nonexistent
Ok -2
```

Explanation:

* The key `"nonexistent"` does not exist in the store.

* TTL returns `-2` .

#### Check TTL on a key without expiration:

```bash 
localhost:9219> TTL keExists
Ok -1
```

Explanation:

* The key `"keExists"` exists but has no expiration set.

* TTL returns `-1` .

***

#### Behavior on Error

| Error Condition     | Error Message                              |
| ------------------- | ------------------------------------------ |
| Key is not provided |  `InvalidArgsError: Key must be provided`  |

***

#### Notes

* TTL values are rounded to seconds.

* This command **does not reset or affect** the TTL of the key—it is read-only.

* A TTL of `0` is **not** valid output; if seen, verify underlying storage behavior.

 

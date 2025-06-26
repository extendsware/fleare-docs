---
draft: false
title: DELETE
is_title_visible: false
description: Deletes a key and its associated value from the database.
cover_image: 'https://www.bakemyweb.com/preview1/docs.fleare.com/box.png'
date: '2025-06-18T18:28:19.344Z'
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
weight: 7000000
id: /documentations/cli-commands/delete.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T20:35:27.644Z'
---

#### Command: `DELETE`

---

#### **Overview**

The `DELETE` command is used to remove a key-value pair from the in-memory database. It ensures the specified key is validated, removes it from the appropriate memory shard.


#### **Command Name**

`DELETE`

---

#### **Description**

Deletes a key and its associated value from the database. If the key exists, it is removed. If the key does not exist, the command still responds with a successful "Ok" to maintain idempotency.

#### **Syntax**

```bash 
DELETE <key>
```

* `<key>`: The string identifier of the key to be deleted from the database.


#### **Permissions**

* No authentication or role-based permission checks are implemented in the current version.
* All connected clients can issue `DELETE` commands.


#### **Examples**

##### **Example 1: Valid key**

```bash 
localhost:9219> DELETE user:1001
```

##### **Example 2: Key does not exist**

```bash 
localhost:9219> DELETE unknownKey
```

##### **Example 3: Invalid syntax**

```bash 
localhost:9219> DELETE
```

##### **Example 1: Key successfully deleted**

```bash 
Ok
```

##### **Example 2: Key did not exist (still considered successful)**

```bash 
Ok
```

##### **Use Cases**

##### Cleanup stale data

Applications can use `DELETE` to remove expired or stale data from the database once it's no longer needed.

##### Idempotent API behavior

`DELETE` can be called multiple times safely — even if the key doesn't exist — making it ideal for REST-like APIs where DELETE operations are meant to be idempotent.

##### User data revocation

In systems that manage user sessions or temporary keys, `DELETE` is used to revoke access or clear temporary state.

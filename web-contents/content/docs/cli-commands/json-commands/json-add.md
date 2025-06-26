---
draft: false
title: JSON.ADD
is_title_visible: false
description: >-
  The JSON.ADD command allows users to insert or append a key-value pair into an
  existing JSON object stored at a given key.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline
date: '2025-06-22T13:53:39.830Z'
authors: "Parash Maity"
is_breadcrumb_visible: true
is_menu_transparent: false
is_menu_visible: true
is_navigation_button_visible: false
is_table_of_content_visible: false
is_left_navigation_visible: true
is_root_content_hidden: false
padding: 15px 0
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
id: /documentations/cli-commands/json-commands/json-add.md
weight: 3000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-23T15:58:21.600Z'
---
#### **Command:** `JSON.ADD` 

***

#### **Overview**

The `JSON.ADD` command allows users to insert or append a key-value pair into an existing JSON object stored at a given key. If the key does not exist, a new JSON object will be created. This command supports adding data at any depth using dot-notation paths.

#### **Command Name**

 `JSON.ADD` 

#### **Description**

Adds a key-value pair to a JSON object stored at the specified key in the database.

* If the key doesn't exist, a new JSON object will be initialized with the provided path and value.

* Nested paths are supported using `.` (dot) notation. Intermediate objects will be created if they do not already exist.

* The value must be a valid JSON string or primitive (string, number, boolean, array, etc.).

#### **Use Cases**

* Add a new field to an existing JSON object (e.g., `salary` , `hobbies` , `department.head` )

* Create nested JSON structures dynamically (e.g., `profile.address.street` )

* Add arrays or primitives at any depth

* Automatically initialize missing keys or intermediate objects

***

#### **Syntax**

```bash 
JSON.ADD <key> <path> <value>
```

* **`<key>`**: The primary key under which the JSON object is stored.

* **`<path>`**: The JSON path (dot-notation) where the new key-value should be added.

* **`<value>`**: A valid JSON primitive or stringified value (must be JSON-decodable).

#### **Permissions**

* Write access to the key’s shard is required.

* No special roles or authentication layers beyond shard permissions are enforced.

***

#### **Examples**

##### Example 1: Add a new array to an existing object

```bash 
localhost:9219> JSON.SET myObj '{"name":"John Doe","age":30,"isActive":true,"address":{"street":"123 Main St","city":"New York"}}'
Ok
```
```json 
localhost:9219> JSON.ADD myObj "hobbies" '["reading","hiking"]'
Ok {
  "address": {
    "city": "New York",
    "street": "123 Main St"
  },
  "age": 30,
  "hobbies": [
    "reading",
    "hiking"
  ],
  "isActive": true,
  "name": "John Doe"
}
```

##### Example 2: Add a number to the object

```json 
127.0.0.1:9219> JSON.ADD myObj 'salary' 10000
Ok {
  ...
  "salary": 10000
}
```

##### Example 3: Add nested field using dot-notation

```json 
127.0.0.1:9219> JSON.ADD myObj 'office.members' 134
Ok {
  ...
  "office": {
    "members": 134
  }
}
```

***

#### **Behavior on Error**

| Error Case                | Description                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------- |
| **Missing arguments**     | Returns: `InvalidKeyError` if fewer or more than 3 arguments are provided.         |
| **Non-JSON value at key** | Returns: `Invalid value error` if the current key does not hold a JSON object.     |
| **InvalidValueError**     | Returns: `InvalidValueError` if the value is not a valid JSON string or primitive. |

#### Summary

The `JSON.ADD` command is ideal for incrementally building or updating JSON objects stored in the database. With support for nested structures and automatic initialization, it simplifies dynamic schema-less data manipulation.

 

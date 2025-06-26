---
draft: true
title: JSON.PGET
is_title_visible: false
description: >-
  JSON.PGET is used to retrieve the full JSON object or a specific nested value
  from a key in the database that holds JSON data.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline
date: '2025-06-22T14:07:36.706Z'
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
weight: 5000000
id: /documentations/cli-commands/json-commands/json-pget.md
__system:
  created_by: i-602132207af9e10032069067
  new: true
---
#### **Command**: `JSON.PGET`

---

#### **Overview**

`JSON.PGET` is used to retrieve the full JSON object or a specific nested value from a key in the database that holds JSON data. It is a partial JSON path-based getter, providing access to deeply nested fields within structured JSON documents.


#### **Command Name**

**JSON.PGET**

#### **Description**

The `JSON.PGET` command retrieves a value from a JSON object stored at the specified key. Optionally, a path can be specified to extract a nested field within the object.

This command is similar to `JSON.GET` but designed to support path-based partial retrieval with nested dot notation (`address.city`), enabling efficient data access without extracting the entire JSON object.

---

#### **Use Cases**

* Retrieve full JSON content stored under a key.
* Access nested fields in a JSON object, such as:

  * A specific field like `"name"` or `"age"`.
  * A nested object like `"address.city"`.
* Extract arrays or elements within arrays from the JSON structure.
* Support efficient lookups in structured documents without client-side parsing.

---

#### **Syntax**

```bash
JSON.PGET <key> [<path>]
```

* `<key>` (required): The name of the key that holds a JSON object.
* `<path>` (optional): The path to the nested field using dot notation (e.g., `address.city`).

#### **Permissions**

* **Read access** to the keyspace is required.
* The key must exist and must be of JSON type.

---

#### **Examples**

##### Set up sample data

```bash
localhost:9219> JSON.SET myObj '{"name":"John Doe","age":30,"isActive":true,"hobbies":["reading","hiking"],"address":{"street":"123 Main St","city":"New York"}}'
Ok
```

##### Example 1: Get the entire JSON object

```bash
localhost:9219> JSON.PGET myObj
Ok {
  "name": "John Doe",
  "age": 30,
  "isActive": true,
  "hobbies": ["reading", "hiking"],
  "address": {
    "street": "123 Main St",
    "city": "New York"
  }
}
```

---

##### Example 2: Get a nested object

```bash
localhost:9219> JSON.PGET myObj address
Ok {
  "street": "123 Main St",
  "city": "New York"
}
```

---

##### Example 3: Get a nested field

```bash
localhost:9219> JSON.PGET myObj address.city
Ok "New York"
```

---

##### Example 4: Get an array

```bash
localhost:9219> JSON.PGET myObj hobbies
Ok ["reading", "hiking"]
```

---

# **Behavior on Error**

| **Scenario**                                     | **Error Message**                                                                             |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| Key not provided                                 | `InvalidKeyError: Key must be provided`                                                       |
| Too many arguments                               | `InvalidArgsError: invalid number of arguments, Syntax: JSON.GET <key> [<path>]`              |
| Key exists but is not a JSON object              | `InvalidValueError: The current value associated with the provided key must be a json object` |
| Path doesn't exist in JSON                       | `key not found: <missing key>`                                                                |
| Invalid nested path (e.g., indexing into string) | `invalid path: <path>`                                                                        |

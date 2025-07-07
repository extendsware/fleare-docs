---
draft: false
title: JSON.MERGE
is_title_visible: false
description: >-
  The JSON.MERGE command allows users to merge a new JSON object into an
  existing JSON object stored at a given key.
date: '2025-06-22T14:00:34.978Z'
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
id: /documentations/cli-commands/json-commands/json-merge.md
weight: 4000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-23T15:58:21.603Z'
---
#### **Command**: `JSON.MERGE` 

***

#### **Overview**

The `JSON.MERGE` command allows users to **merge a new JSON object** into an existing JSON object stored at a given key. This enables incremental updates to structured JSON data without overwriting the entire value.

If the key does not exist, the command **creates a new JSON object**. During the merge, **nested fields are merged recursively**, and in case of conflict, **existing fields are overwritten by new values**.

#### **Command Name**

 `JSON.MERGE` 

#### **Description**

Merges the provided JSON object into the existing JSON object stored at the specified key.

* **Creates a new JSON object** if the key does not exist.

* **Merges nested fields recursively.**

* **Conflicting fields are overwritten** by the new values.

* Only keys holding **valid JSON objects** can be merged into.

#### **Use Cases**

* Add additional fields to a user profile JSON without replacing existing data.

* Update nested settings or configuration objects.

* Append metadata to existing records dynamically.

* Safely merge structured logs or telemetry data.

***

#### **Syntax**

```bash 
JSON.MERGE <key> <json-object>
```

*  `<key>` : The key under which the JSON object is stored or to be created.

*  `<json-object>` : A valid JSON object (must be a stringified object).

#### **Permissions**

* Write access to the key.

***

#### **Examples**

##### Example 1: Basic Merge

```bash 
localhost:9219> JSON.SET myObj '{"name":"John Doe","age":30,"isActive":true,"address":{"street":"123 Main St","city":"New York"}}'
Ok
```
```json 
localhost:9219> JSON.MERGE myObj '{"hobbies":["reading","hiking"]}'
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

##### Example 2: Recursive Merge with Overwrite

```json 
localhost:9219> JSON.MERGE myObj '{"address":{"city":"Boston"},"salary":10000}'
Ok {
  "address": {
    "city": "Boston",
    "street": "123 Main St"
  },
  "age": 30,
  "hobbies": [
    "reading",
    "hiking"
  ],
  "isActive": true,
  "name": "John Doe",
  "salary": 10000
}
```

##### Example 3: Key Does Not Exist

```json 
localhost:9219> JSON.MERGE newProfile '{"username":"jane_doe","role":"admin"}'
Ok {
  "username": "jane_doe",
  "role": "admin"
}
```

***

#### **Behavior on Error**

| Condition                       | Error Message                                                                                   | Description                             |
| ------------------------------- | ----------------------------------------------------------------------------------------------- | --------------------------------------- |
| No key provided                 |  `InvalidKeyError: Key must be provided`                                                        | Missing key argument                    |
| Invalid number of arguments     |  `InvalidArgsError: invalid number of arguments, Syntax: JSON.MERGE <key> <value>`              | Command must have exactly 2 arguments   |
| Non-JSON value at key           |  `InvalidValueError: The current value associated with the provided key must be a json object`  | Cannot merge into non-JSON values       |
| Value to merge is not an object |  `InvalidValueError: The value to merge must be a JSON object`                                  | Only JSON objects are valid for merging |

***

#### **Additional Notes**

* Only JSON objects can be merged. Arrays, strings, numbers, and other types are **not valid** as merge values.

* The merge is **non-destructive** for unrelated keys.

 

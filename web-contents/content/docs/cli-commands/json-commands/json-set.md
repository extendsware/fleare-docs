---
draft: false
title: JSON.SET
is_title_visible: true
description: >-
  The JSON.SET command allows clients to store structured JSON objects under a
  specific key in a distributed, in-memory data store.
date: '2025-06-22T12:14:34.580Z'
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
id: /documentations/cli-commands/json-commands/json-set.md
weight: 1000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-23T15:58:21.596Z'
---
#### Command: `JSON.SET` 

***

#### **Overview**

The `JSON.SET` command allows clients to store structured JSON objects under a specific key in a distributed, in-memory data store. If the key already exists, the stored JSON value is **overwritten**. This is particularly useful for schema-less data use cases like storing user profiles, configurations, and nested records.

#### **Command Name**

**`JSON.SET`**

#### **Description**

Stores a **valid JSON object** at the specified key.
If the key already exists, its previous value is replaced.
The value must be a valid JSON object (e.g., not a number, string, or array as the top-level structure). This supports flexible, nested data models and is typically used for structured configurations, user metadata, and document storage.

#### **Use Cases**

* Store user profile data:

  ```json 
  {"name": "Alice", "age": 27}
  ```

* Save application settings:

  ```json 
  {"theme": "dark", "notifications": {"email": true, "sms": false}}
  ```

* Manage nested business objects or configuration trees.

***

#### **Syntax**

```bash 
JSON.SET <key> <json_value>
```

*  `<key>` : String identifier under which the JSON object is stored.

*  `<json_value>` : A stringified JSON object (must be valid JSON). The top-level structure **must be an object ( `{}` )**.

#### **Permissions**

* **Write Access Required**: The user/client must have write access to the targeted key's shard.

* Internally WAL (Write-Ahead Log) records the command for durability and persistence.

***

#### **Examples**

##### Basic JSON Set

```bash 
localhost:9219> JSON.SET myObj '{"name":"John","age":30,"hobbies":["reading","hiking"]}'
Ok
```

##### Retrieve It

```bash 
localhost:9219> JSON.GET myObj
```
```json 
Ok {
  "age": 30,
  "hobbies": [
    "reading",
    "hiking"
  ],
  "name": "John"
}
```

##### Update with Nested Object

```bash 
localhost:9219> JSON.SET myObj '{"name":"John Doe","age":30,"isActive":true,"hobbies":["reading","hiking"],"address":{"street":"123 Main St","city":"New York"}}'
Ok
```

```bash 
localhost:9219> JSON.GET myObj
```
```json 
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

***

#### **Behavior on Error**

| Condition                     | Error Message                                                                       |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| Missing key or value          |  `InvalidKeyError: Key must be provided`                                            |
| Incorrect number of arguments |  `InvalidArgsError: invalid number of arguments, Syntax: LIST.FILTER <key> <path>`  |
| Invalid JSON value            |  `InvalidValueError: provided value not a valid json object`                        |

 

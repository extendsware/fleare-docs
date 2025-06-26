---
draft: false
title: JSON.GET
is_title_visible: false
description: >-
  The JSON.GET command retrieves JSON data stored at a specified key. You can
  optionally query nested fields within the JSON object using a dot-path syntax.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline
date: '2025-06-22T12:22:28.215Z'
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
id: /documentations/cli-commands/json-commands/json-get.md
weight: 2000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-23T15:58:21.598Z'
---
#### Command: `JSON.GET` 

***

#### Overview

The `JSON.GET` command retrieves JSON data stored at a specified key. You can optionally query nested fields within the JSON object using a dot-path syntax. Additionally, the command supports resolving references (e.g., `$ref:` values) and attaching the referenced data inline in the response.

#### Command Name

 `JSON.GET` 

#### Description

* Retrieves the JSON value stored at a given key.

* You may specify a **path** to retrieve nested fields (e.g., `address.city` ).

* You may specify one or more **ref fields** to resolve JSON references marked with `$ref:<key>` .

* If the path is not provided, the full JSON object is returned.

* If the key does not exist, an empty result is returned.

* If the value at the key is not a valid JSON object, an error is returned.

* If the path is invalid, an error is returned.

#### Use Cases

* Fetch the full user profile stored as a JSON object.

* Retrieve nested values like a user’s city or hobbies.

* Automatically expand and include referenced data from related keys (e.g., userId → `users:<id>` ).

#### Syntax

```bash 
JSON.GET <key> [<path>] [<ref_field>...]
```

#### Arguments:

*  `key` (string): The key holding the JSON object.

*  `path` (optional string): Dot-separated path to the nested field.

*  `ref_field` (optional list): Dot-separated paths to reference fields inside the JSON object that should be expanded.

#### Permissions

* Requires **read** access to the specified key.

* Requires **read** access to any reference keys specified through `$ref` .

#### Examples

##### Basic JSON fetch

```bash 
localhost:9219> JSON.SET myObj '{"name":"John Doe","age":30,"isActive":true}'
Ok
```

```bash 
localhost:9219> JSON.GET myObj
```
Response:
```json 
Ok {
  "name": "John Doe",
  "age": 30,
  "isActive": true
}
```

##### Nested object retrieval

```bash 
localhost:9219> JSON.SET myObj '{"address":{"city":"New York","zip":"10001"}}'
Ok

```

```bash 
localhost:9219> JSON.GET myObj address
```
Response:
```json 
Ok {
  "city": "New York",
  "zip": "10001"
}
```
```bash 
localhost:9219> JSON.GET myObj address.city
Ok "New York"
```

##### Array access

```bash 
localhost:9219> JSON.SET myObj '{"hobbies":["reading","hiking"]}'
Ok

localhost:9219> JSON.GET myObj hobbies
Ok ["reading", "hiking"]
```

##### Reference expansion
* Object with references

```bash 
localhost:9219> JSON.SET order001 '{
  "orderId": "orders:OD001",
  "productId": "$ref:products:001",
  "userId": "$ref:users:001"
}'
Ok
```
#### Referenced objects
```bash 
localhost:9219> JSON.SET products:001 '{"id":"products:001","name":"Laptop","price":1000.5}'
Ok

localhost:9219> JSON.SET users:001 '{"id":"users:001","name":"John Doe","email":"john.doe@example.com"}'
Ok
```

##### Get order with expanded productId and userId
```bash 
localhost:9219> JSON.GET order001 "" productId userId
```
```json 
Ok {
  "orderId": "orders:OD001",
  "productId": "$ref:products:001",
  "_productId": {
    "id": "products:001",
    "name": "Laptop",
    "price": 1000.5
  },
  "userId": "$ref:users:001",
  "_userId": {
    "id": "users:001",
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
}
```

##### **Nested reference inside object path**

```bash 
localhost:9219> JSON.SET order:ODX '{
  "orderId": "ODX",
  "item": {
    "productId": "$ref:products:501"
  }
}'

localhost:9219> JSON.SET products:501 '{
  "id": "products:501",
  "name": "Monitor",
  "price": 199.99
}'
```

```bash 
localhost:9219> JSON.GET order:ODX item.productId
```

Output:

```json 
{
  "productId": "$ref:products:501",
  "_productId": {
    "id": "products:501",
    "name": "Monitor",
    "price": 199.99
  }
}
```

##### Multi-level reference resolution**

*Data Setup:

```bash 
localhost:9219> JSON.SET booking:B1 '{
  "bookingId": "B1",
  "user": {
    "userId": "$ref:users:9001"
  },
  "vehicleId": "$ref:vehicles:VX01"
}'

localhost:9219> JSON.SET users:9001 '{
  "id": "users:9001",
  "name": "David",
  "email": "david@example.com"
}'

localhost:9219> JSON.SET vehicles:VX01 '{
  "id": "vehicles:VX01",
  "model": "SUV",
  "plate": "MH12AB1234"
}'
```

```bash 
localhost:9219> JSON.GET booking:B1 "" user.userId vehicleId
```

*Output:

```json 
{
  "bookingId": "B1",
  "user": {
    "userId": "$ref:users:9001",
    "_userId": {
      "id": "users:9001",
      "name": "David",
      "email": "david@example.com"
    }
  },
  "vehicleId": "$ref:vehicles:VX01",
  "_vehicleId": {
    "id": "vehicles:VX01",
    "model": "SUV",
    "plate": "MH12AB1234"
  }
}
```


#### Behavior on Error

| Condition                          | Error Message                                                                                   |
| ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| Missing key argument               |  `InvalidKeyError: Key must be provided`                                                        |
| Value not JSON                     |  `InvalidValueError: The current value associated with the provided key must be a json object`  |
| Reference not found                |  `ERR referenced key not found: <key>`                                                          |
| Reference value not a string       |   Skips resolution silently                                                                     |

 

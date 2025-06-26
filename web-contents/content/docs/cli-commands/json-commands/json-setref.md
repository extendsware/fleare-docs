---
draft: false
title: JSON.SETREF
is_title_visible: false
description: >-
  The JSON.SETREF command stores a JSON object at a specified key in the
  database and simultaneously replaces specified fields with reference pointers
  to other keys.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline
date: '2025-06-23T15:43:09.680Z'
authors: "Parash Maity"
is_breadcrumb_visible: true
is_menu_transparent: false
is_menu_visible: true
is_navigation_button_visible: false
is_table_of_content_visible: true
is_left_navigation_visible: true
is_root_content_hidden: false
padding: 15px 0
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-23T15:58:21.609Z'
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
weight: 7000000
id: /documentations/cli-commands/json-commands/json-setref.md
---
#### Command: `JSON.SETREF` 

***

#### **Overview**

The JSON.SETREF command stores a JSON object at a specified key in the database and simultaneously replaces specified fields with reference pointers to other keys. This allows relational-like linking between JSON documents using reference tags. This command is useful for creating relationships between JSON documents.

#### **Command Name**

**`JSON.SETREF`**

#### **Description**

Stores a JSON object in the database with certain fields marked as *references* to other stored keys. The referenced fields are substituted with special values prefixed by `$ref:` .

It is used to embed *logical links* between documents such as linking an order to a user, a product, or an offer.

#### **Use Cases**

* Link an order JSON to a user or product.

* Replace nested keys in a JSON object with references to existing documents.

* Normalize documents by storing shared structures once and referencing them.

* Maintain cleaner and modular data structures in memory.

***

#### **Syntax**

```bash 
JSON.SETREF <key> <value> <ref_object>
```

*  `<key>` : The key at which to store the final JSON object.

*  `<value>` : The actual JSON object (as a string) to be stored.

*  `<ref_object_key>` : A JSON object with key paths from `<value>` and reference keys from the database.

#### **Permissions**

* Write access is required to store JSON data.

* In **strict mode**, the reference keys **must exist**; otherwise, the command will fail with an error.

***

#### **Examples**

##### Example 1: Basic Reference

```bash 
localhost:9219> JSON.SET users:001 '{"name":"John","age":30,"hobbies":["reading","hiking"]}'
Ok

localhost:9219> JSON.SETREF orders:OD001 '{"orderId":"orders:OD001","details":"This order is for a new laptop.","status":"pending"}' '{"userId":"users:001"}'
Ok

localhost:9219> JSON.GET orders:OD001
Ok {
  "orderId": "orders:OD001",
  "details": "This order is for a new laptop.",
  "status": "pending",
  "userId": "$ref:users:001"
}
```

##### Example 2: Reference with Nested Keys

```bash 
localhost:9219> JSON.SET offers:001 '{"offer":{"offerId": "001","code":"MDX50","flat":true}}'
Ok

localhost:9219> JSON.SETREF orders:OD002 '{"orderId":"OD002","offer":{"name":"Offer one"}}' '{"offer.offerId":"offers:001"}'
Ok

localhost:9219> JSON.GET orders:OD002
Ok {
  "orderId": "OD002",
  "offer": {
    "name": "Offer one",
    "offerId": "$ref:offers:001"
  }
}
```

##### Example 3: Multiple References

```bash 
localhost:9219> JSON.SETREF orders:OD003 '{"orderId":"OD003","userId":"U001","productId":"P001"}' '{"userId":"users:001","productId":"products:001"}'
Ok

localhost:9219> JSON.GET orders:OD003
Ok {
  "orderId": "OD003",
  "userId": "$ref:users:001",
  "productId": "$ref:products:001"
}
```

***

#### **Behavior on Error**

| Error Type                 | Condition                                                | Message Example                                                                                   |
| -------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Invalid Key                | If `<key>` is missing or invalid                         |  `InvalidKeyError: Key must be provided`                                                          |
| Invalid Argument Count     | If all three arguments are not provided                  |  `InvalidArgsError: invalid number of arguments, Syntax: JSON.SETREF <key> <value> <ref_object>`  |
| Invalid JSON (value)       | If `<value>` is not a valid JSON string                  |  `InvalidValueError: provided value not a valid json object`                                      |
| Invalid JSON (ref\_object) | If `<ref_object>` is not a valid JSON string             |  `InvalidValueError: provided refObject not a valid json object`                                  |
| Reference Not Found        | In strict mode, if a referenced key is missing in the DB |  `InvalidReferenceError: reference key users:001 not found`                                       |

***

#### **Implementation Behavior**

* Parses `<value>` and `<ref_object>` into JSON objects.

* Validates keys and values.

* Walks through `<ref_object>` and replaces corresponding fields in `<value>` with `$ref:<ref_value>` .

* Stores the final JSON in the key.

***

#### **Notes**

* **Strict Mode** (from `config` ) enforces referenced keys to exist.

 

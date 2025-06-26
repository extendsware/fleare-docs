---
draft: false
title: SET
is_title_visible: false
description: The SET command is used to store a key-value pair in the database.
cover_image: 'https://www.bakemyweb.com/preview1/docs.fleare.com/box.png'
date: '2025-06-18T11:50:48.189Z'
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
weight: 4000000
id: /documentations/cli-commands/set.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T20:35:27.638Z'
---

#### Command: `SET` 

---

### **Overview**

The `SET` command is used to store a key-value pair in the database. If the key already exists, the value is overwritten. It is a common operation to persist data in memory Database.

***

### **Command Name**

 `SET` 

### **Description**

Stores the given key with its associated value in the in-memory store.
If the key already exists, its value is replaced.
The key must be a valid string (as per `key validation rules` ), and exactly two arguments must be provided: a key and a value.

***

### **Syntax**

```bash 
SET <key> <value>
```

*  `<key>` : A valid string identifier for the value.

*  `<value>` : A string value to be associated with the key.

***

### **Permissions**

No special permissions are required. All clients connected to the database can use this command.

***

### **Input Examples**

#### Store a simple string

```bash 
localhost:9219> SET username john
```

#### Store numeric string value

```bash 
localhost:9219> SET age 30
```

***

### **Output Examples**

```bash 
localhost:9219> SET username john

Ok
```

#### Example 2:

```bash 
localhost:9219> SET age 30

Ok
```

***

### **Behavior on Error**

The `SET` command may return the following error responses:

| Condition                  | Error Message                                            |
| -------------------------- | -------------------------------------------------------- |
| No arguments provided      |  `InvalidArgumentError: Key and value must be provided`  |
| Only one argument provided |  `InvalidArgumentError: Key and value must be provided`  |
| Invalid key format         |  `InvalidKeyError: <reason>`                             |
| Internal store error       |  `<detailed error from store.Set>`                       |

#### Missing value

```bash 
localhost:9219> SET onlykey

InvalidArgumentError: Key and value must be provided
```

#### Invalid key

```bash 
localhost:9219> SET /invalid key value

InvalidKeyError: key contains invalid characters
```

***

#### **Use Cases**

1. **Store user profile data**

   ```bash 
   SET username alice

   SET email alice@example.com
   ```

2. **Temporary session data**

   ```bash 
   SET session_abc123 active
   ```

3. **Overwrite existing key**

   ```bash 
   SET username alice

   SET username bob

   GET username  // returns "bob"
   ```

##### **JSON String**

```bash 
localhost:9219> SET user:123 '{"id":123,"name":"Alice","roles":["admin","editor"]}'

Ok
```

##### **Output**

```bash 
localhost:9219> GET config
```

```json 
Ok {
    "id": 123,
    "name": "Alice",
    "roles": [
        "admin",
        "editor"
    ]
}
```

##### **Multiline String (escaped)**

```bash 
localhost:9219> SET message 'Hello,\nWelcome to our service!\nRegards,\nTeam'

Ok
```

##### **Nested JSON**

```bash 
localhost:9219> SET config '{"logging":{"level":"debug","enabled":true},"max_conn":100}'

Ok
```

##### **Output**

```bash 
localhost:9219> GET config
```

```json 
Ok {
    "logging": {
        "level": "debug",
        "enabled": true
    },
    "max_conn": 100
}
```

#### **Boolean Value (as string)**

```bash 
localhost:9219> SET feature_x_enabled true

Ok
```

#### **Array-like String**

```bash 
localhost:9219> SET fruits '["apple", "banana", "mango"]'

Ok
```

#### **Long String (truncated view)**

```bash 
localhost:9219> SET longtext 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'

Ok
```

#### **Key with Namespace Prefix**

```bash 
localhost:9219> SET session:user:456 "active"

Ok
```

***

### **Optional: GET Output Examples**

If you subsequently run `GET` on the above keys, the values will return as-is:

```bash 
localhost:9219> GET user:123
```

```json 
Ok {
    "id": 123,
    "name": "Alice",
    "roles": [
        "admin",
        "editor"
    ]
}
```

 

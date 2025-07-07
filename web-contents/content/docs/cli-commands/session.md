---
draft: false
title: SESSION
is_title_visible: false
description: The SESSION command returns the current session information
date: '2021-09-01T05:26:12.863Z'
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
weight: 3000000
id: /documentations/cli-commands/session.md
__system:
  last_published: '2025-06-21T20:35:27.636Z'
  new: false
  created_by: i-602132207af9e10032069067
---
#### Command: `SESSION`
---

#### Overview

The `SESSION` command returns the current session information for the authenticated client. It is typically used for diagnostics, auditing, or session lifecycle inspection.

***

#### **Command Name**

```bash 
SESSION
```

***

#### **Description**

Retrieves and returns the current session object associated with the client connection. This includes session metadata and user authentication details.

***

#### **Syntax**

```bash 
SESSION
```

This command takes no arguments. It must be executed from an active client connection that has previously authenticated.

***

#### **Permissions**

* Requires a valid authenticated session.

* Available to all authenticated roles (e.g., Admin, User).

***

#### **Input Format**

There are no input parameters or flags. It is a standalone command.

##### Example Input:

```bash 
localhost:9219> session
```

***

#### **Output Format**

The command returns a JSON-encoded object describing the session:

##### Output Fields:

| Field                | Type   | Description                                     |
| -------------------- | ------ | ----------------------------------------------- |
|  `created_at`        | string | RFC3339 timestamp when the session was created. |
|  `last_accessed_at`  | string | RFC3339 timestamp of the last client activity.  |
|  `session_id`        | string | Unique identifier of the session.               |
|  `status`            | int    | Session status (1 = active).                    |
|  `user`              | object | Authenticated user object.                      |
|  `user.Username`     | string | Username of the session owner.                  |
|  `user.Password`     | string | Redacted password (always masked).              |
|  `user.Role`         | string | Role of the authenticated user (e.g., Admin).   |

***

#### **Example Output**

```json 
Ok {
  "created_at": "2025-05-01T17:33:15.497273Z",
  "last_accessed_at": "2025-05-01T17:33:15.497273Z",
  "session_id": "8-127.0.0.1:53531",
  "status": 1,
  "user": {
    "Password": "*******",
    "Role": "Admin",
    "Username": "admin"
  }
}
```

***

#### **Behavior on Error**

* If the client is not authenticated or the session is invalid:

  ```
  Error: unauthorized or session not found
  ```

* If an internal server error occurs (e.g., session store failure):

  ```
  Error: internal server error
  ```

***

#### **Use Cases**

* Validate that a session is correctly established.

* Debug which user is currently authenticated.

* View timestamp metadata for tracking or audit logging.

* Confirm role-based access was properly set up post-login.

 

### `GET /api/client/account`

Retrieves the account details of the authenticated user.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |

### Example Response

```json
{
  "object": "user",
  "attributes": {
    "id": 1,
    "admin": true,
    "username": "admin",
    "email": "example@example.com",
    "first_name": "Admin",
    "last_name": "User",
    "language": "en"
  }
}
```
### `GET /api/client/account/two-factor`

Returns a TOTP QR code, which can be used to set up two-factor authentication for a user's account.

### Responses

| Code | Description                                |
| ---- | ------------------------------------------ |
| 200  | The request was successful                 |
| 400  | Two factor already enabled                 |

### Example Response

```json
{
  "data": {
    "image_url_data": "otpauth://totp/Pterodactyl%20Demo:john.doe%40example.com?secret=JBSWY3DPEHPK3PXP&issuer=Pterodactyl%20Demo",
    "secret": "JBSWY3DPEHPK3PXP"
  }
}
```

### `POST /api/client/account/two-factor`

Enables two-factor authentication for a user's account.

### Body

| Name     | Visibility | Type   | Description                    |
| -------- | ---------- | ------ | ------------------------------ |
| code     | Required   | string | Two-factor authentication code |
| password | Required   | string | User's account password        |

### Responses

| Code | Description                                     |
| ---- | ----------------------------------------------- |
| 200  | Two-factor authentication enabled successfully. |
| 400  | Invalid password                                |

### Example Response

```json
{
  "object": "recovery_tokens",
  "attributes": {
    "tokens": [
      "MpBjHH8O08",
      "D9H0hktN6L",
      "ho8KiUpeV8",
      "06vZEfrYPf",
      "nFRySZ2ryh",
      "7K1cTrhGoV",
      "n6xpwwlJfv",
      "hAmyCsZxYO",
      "5FiMKFyNpH",
      "IViSFoRFvW"
    ]
  }
}
```

### `DELETE /api/client/account/two-factor`

Disables two-factor authentication on a user's account.

### Body

| Name     | Visibility | Type   | Description             |
| -------- | ---------- | ------ | ----------------------- |
| password | Required   | string | User's account password |

### Responses

| Code | Description                                      |
| ---- | ------------------------------------------------ |
| 204  | Two-factor authentication disabled successfully. |
| 400  | Invalid password                                 |

### `PUT /api/client/account/email`

Updates the authenticated user's email address.

### Body

| Name     | Visibility | Type     | Description                |
| -------- | ---------- | -------- | -------------------------- |
| email    | Required   | string | The new email address.     |
| password | Required   | string | The current user password. |

### Responses

| Code | Description                      |
| ---- | -------------------------------- |
| 201  | The request was successful.      |
| 400  | Invalid email format or password |

### `PUT /api/client/account/password`

Updates the authenticated user's password.

### Body

| Name                  | Visibility | Type     | Description                           |
| --------------------- | ---------- | -------- | ------------------------------------- |
| current_password      | Required   | string   | The current user password.            |
| password              | Required   | string   | The new password.                     |
| password_confirmation | Required   | string   | The confirmation of the new password. |

#### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |

### `GET /api/client/account/activity`

Returns a paginated set of the user's activity logs.

### Query Parameters

| Name      | Visibility | Type    | Description                             |
| --------- | ---------- | ------  | -------------------------------------   |
| per_page  | Optional   | integer | Number of activity logs per page        |
| filter    | Optional   | string  | Filter activity logs by event (partial) |
| sort      | Optional   | string  | Sort activity logs by timestamp         |

### Responses

| Code | Description                      |
| ---- | -------------------------------- |
| 200  | The request was successful.      |

### Example Response

```json
{
    "data": [
        {
            "id": "7f5a04394d5a7c6a8e4917d3d5a0a4f92d89f819",
            "batch": "2023-06-10 09:25:17",
            "event": "user.account.password_reset",
            "is_api": false,
            "ip": "127.0.0.1",
            "description": "User requested a password reset",
            "properties": {
                "email": "john@example.com",
                "count": 1
            },
            "has_additional_metadata": false,
            "timestamp": "2023-06-10T09:25:17+00:00"
        },
        {
            "id": "eaf4397b9c47b61483f5e72a3077d11f739c6059",
            "batch": "2023-06-09 14:02:58",
            "event": "user.account.update",
            "is_api": false,
            "ip": null,
            "description": "User updated their account",
            "properties": {},
            "has_additional_metadata": false,
            "timestamp": "2023-06-09T14:02:58+00:00"
        }
    ]
}
```

### `GET /api/client/account/ssh-keys`

Retrieves all the SSH keys configured for the authenticated user's account.

### Responses

| Code | Description                    |
| ---- | ------------------------------ |
| 200  | List of SSH keys for the user. |

### Example Response

```json
{
  "data": {
    "name": "My SSH Key",
    "fingerprint": "1a:2b:3c:4d:5e:6f:7g:8h:9i:10j:11k:12l:13m:14n:15o",
    "public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAB...",
    "created_at": "2020-05-18T00:12:43+01:00"
  }
}
```

### `POST /api/client/account/ssh-keys`

Creates a new SSH key for the authenticated user.

### Body

| Name       | Visibility | Type     | Description              |
| ---------- | ---------- | -------- | ------------------------ |
| name       | Required   | string   | The name of the SSH key. |
| public_key | Required   | string   | The public key contents. |

### Responses

| Code | Description                   |
| ---- | ----------------------------- |
| 200  | The SSH key was added.        |
| 422  | Validation error(s) occurred. |

### `POST /api/client/account/ssh-keys/remove`

Deletes an SSH key from the user's account.

### Body

| Name        | Visibility | Type   | Description                           |
| ----------- | ---------- | ------ | ------------------------------------- |
| fingerprint | Required   | string | Fingerprint of the SSH key to delete. |

### Responses

| Code | Description                           |
| ---- | ------------------------------------- |
| 204  | The SSH key was deleted successfully. |

### `GET /api/client/account/api-keys`

Retrieves all the API keys that exist for the authenticated user's account.

### Responses

| Code | Description                    |
| ---- | ------------------------------ |
| 200  | List of API keys for the user. |

### Example Response

```json
{
  "data": [
    {
      "identifier": "wwQ5DJ6X1XaFznQS",
      "description": "API Docs",
      "allowed_ips": [],
      "last_used_at": "2020-06-03T15:04:47+01:00",
      "created_at": "2020-05-18T00:12:43+01:00"
    }
  ]
}
```

### `POST /api/client/account/api-keys`

Creates a new API key for the authenticated user.

### Body

| Name        | Visibility | Type     | Description                                                         |
| ----------- | ---------- | -------- | ------------------------------------------------------------------- |
| description | Optional   | string   | A description for the API key.                                      |
| allowed_ips | Optional   | array    | An array of IP addresses or CIDR ranges allowed to use the API key. |

### Responses

| Code | Description                   |
| ---- | ----------------------------- |
| 200  | The request was successful.   |
| 422  | Validation error(s) occurred. |

### `DELETE /api/client/account/api-keys/{identifier}`

Deletes a specific API key from the user's account.

### Body

| Name       | Type   | Visibility | Description                              |
| ---------- | ------ | ---------- | ---------------------------------------- |
| identifier | string | required   | Identifier of the API key to be deleted. |

### Responses

| Code | Description                           |
| ---- | ------------------------------------- |
| 204  | The API key was deleted successfully. |


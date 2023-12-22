## Contents

- [Authenticate SFTP](#authenticate-sftp)

---

## Authenticate SFTP

### `POST /api/remote/sftp/auth`

Authenticate a set of credentials and return the associated server details for a SFTP connection on the daemon. This supports both public key and password based credentials.

### Body

| Name     | Visibility | Type   | Description                                                                                       |
| -------- | ---------- | ------ | ------------------------------------------------------------------------------------------------- |
| type     | optional   | string | Determine if the password should check authentication with either the "password" or "public_key". |
| username | required   | string | The username of the user attempting to login.                                                     |
| password | required   | string | The password of the user attempting to login.                                                     |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 403  | Incorrect credentials.               |
| 422  | One or more validation rules failed. |

### Example Response

```json
{
  "user": "1abc23de-4567-89f0-ghi1-h2kl345m6nop",
  "server": "1a234567-8b9c-01d2-ef3g-45hi67j890kl",
  "permissions": [
    "*",
    "admin.websocket.errors",
    "admin.websocket.install",
    "admin.websocket.transfer"
  ]
}
```

### Sources

- [SftpAuthenticationController.php#L34](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/SftpAuthenticationController.php#L34)

### `POST /api/remote/sftp/auth`

Authenticate a set of credentials and return the associated server details for a SFTP connection on the daemon. This supports both public key and password based credentials.

### Body

| Name           | Visibility | Type   | Description                                                                                       |
| -------------- | ---------- | ------ | ------------------------------------------------------------------------------------------------- |
| type           | optional   | string | Determine if the password should check authentication with either the "password" or "public_key". |
| username       | required   | string | The username of the user attempting to login.                                                     |
| password       | required   | string | The password of the user attempting to login.                                                     |
| ip             | optional   | string | The remote address of the connection.                                                             |
| session_id     | optional   | []byte | The connection's session id.                                                                      |
| client_version | optional   | []byte | The connection's client version.                                                                  |

### Responses

| Code | Description                              |
| ---- | ---------------------------------------- |
| 200  | The response was successful.             |
| 403  | Incorrect credentials.                   |
| 422  | Missing fields. (ex. username, password) |

### Response example

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

Sources

- [app/Http/Controllers/Api/Remote/SftpAuthenticationController.php#L34](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/SftpAuthenticationController.php#L34)

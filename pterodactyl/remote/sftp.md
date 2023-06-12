### `POST /api/remote/sftp/auth`

Authenticate a set of credentials and return the associated server details for a SFTP connection on the daemon. This supports both public key and password based credentials.

### Body


| Name  | Visibility | Type   | Description                                  |
| ----- | ---------- | ------ | -------------------------------------------- |
| type | required | string | Determine if the password should check authentication with either the "public_key" or "ssh_key". |
| username | required | string | The username of the user attempting to login. |
| password | required | string | The password of the user attempting to login. |

### Responses

WIP.

Sources

- [app/Http/Controllers/Api/Remote/SftpAuthenticationController.php#L34](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/SftpAuthenticationController.php#L34)

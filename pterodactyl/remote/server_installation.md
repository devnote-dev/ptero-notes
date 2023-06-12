### `GET /api/remote/servers/:uuid`

Returns details about the server that allows Wings to self-recover and ensure that the state of the server matches the Panel at all times.

### Responses

WIP.

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L35](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L35)

### `GET /api/remote/servers/:uuid/install`

Returns installation information for a server.

### Responses

WIP.

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L30](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L30)

### `POST /api/remote/servers/:uuid/install`

Updates the installation state of a server.

### Body

| Name  | Visibility | Type   | Description                                  |
| ----- | ---------- | ------ | -------------------------------------------- |
| successful | required | boolean | Notifies the server has completed the installation process. |
| reinstall | required | boolean | The state of the server. |

### Responses

WIP.

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L48](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L48)

### `POST /api/remote/servers/:uuid/transfer/success`

The daemon notifies the panel about a transfer success.

### Responses

| Code | Description                       |
| ---- | --------------------------------- |
| 204  | The request was successful.       |
| 404  | The server was not found.         |
| 409  | Server is not being transferred   |

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerTransferController.php#L50](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerTransferController.php#L50)

---

### `POST /api/remote/servers/:uuid/transfer/failure`

The daemon notifies the panel about a transfer failure.

### Responses

| Code | Description                       |
| ---- | --------------------------------- |
| 204  | The request was successful.       |
| 404  | The server was not found.         |
| 409  | Server is not being transferred   |

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerTransferController.php#L34](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerTransferController.php#L34)

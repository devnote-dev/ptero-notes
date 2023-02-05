### `POST /api/servers/:uuid/backup`

Creates a backup of the server's volume in the node to the specified backup store and returns no content.

### Body

| Field   | Visibility | Type   | Description                                   |
| ------- | ---------- | ------ | --------------------------------------------- |
| adapter | required   | string | The name of the backup adapter to use.        |
| uuid    | required   | string | The UUID of the server in the panel.          |
| ignore  | required   | string | A string containing the ignored files format. |

Sources:

- [router/router_server_backup.go#L19](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_backup.go#L19)

### `POST /api/servers/:uuid/backup/:id/restore`

Restores a backup on the server. This is a synchronous/blocking endpoint, meaning that the request will not be completed until the backup is restored or fails to restore.

### Body

| Field              | Visibility             | Type    | Description                                                                           |
| ------------------ | ---------------------- | ------- | ------------------------------------------------------------------------------------- |
| adapter            | required               | string  | The name of the backup adapter.                                                       |
| truncate_directory | required               | boolean | Whether the existing server volume should be truncated before the backup is restored. |
| download_url       | only with "s3" adapter | string  | The download URL to the S3 storage bucket.                                            |

### Responses

| Code | Description                                                                               |
| ---- | ----------------------------------------------------------------------------------------- |
| 204  | The request was accepted.                                                                 |
| 400  | The request body could not be parsed, the S3 download URL was not present or was invalid. |

Sources:

- [router/router_server_backup.go#L68](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_backup.go#L68)

### `DELETE /api/servers/:uuid/backup/:id`

Deletes a specified backup from a server.

### Responses

| Code | Description                         |
| ---- | ----------------------------------- |
| 204  | The request was accepted.           |
| 404  | The server or backup was not found. |

Sources:

- [router_server_backup.go#L178](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_backup.go#L178)

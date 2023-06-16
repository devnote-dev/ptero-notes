### `POST /api/client/servers/:serverId/settings/rename`

Renames a server.

### Body

| Name        | Visibility | Type   | Description                         |
| ----------- | ---------- | ------ | ----------------------------------- |
| name        | Required   | string | The new name for the server.        |
| description | Optional   | string | The new description for the server. |

### Responses

| Code | Description                   |
| ---- | ----------------------------- |
| 204  | The server was renamed.       |
| 422  | The request body was invalid. |

### `POST /api/client/servers/:serverId/settings/reinstall`

Reinstalls the server on the daemon.

### Responses

| Code | Description                        |
| ---- | ---------------------------------- |
| 202  | The server reinstall was accepted. |

### `PUT /api/client/servers/:serverId/settings/docker-image`

Changes the Docker image in use by the server.

### Body

| Name         | Visibility | Type   | Description                          |
| ------------ | ---------- | ------ | ------------------------------------ |
| docker_image | Required   | string | The new Docker image for the server. |

### Responses

| Code | Description                         |
| ---- | ----------------------------------- |
| 204  | The Docker image was updated.       |
| 400  | The Docker image cannot be updated. |

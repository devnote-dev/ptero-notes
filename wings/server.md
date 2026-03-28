### `GET /api/servers/:uuid`

Returns a server object by its UUID.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The server was not found.   |

<!-- ### Example Object -->

Sources:

- [router/router_server.go#L21](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L21)

### `DELETE /api/servers/:uuid`

Deletes a specified server by its UUID and removes all the files in the server's volume on the node.

### Responses

| Code | Description               |
| ---- | ------------------------- |
| 204  | The request was accepted. |
| 404  | The server was not found. |

Sources:

- [router/router_server.go#L192](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L192)

### `GET /api/servers/:uuid/logs`

Returns an object containing a list of logs from the server's console.

### Parameters

| Name | Visibility | Description                                     |
| ---- | ---------- | ----------------------------------------------- |
| size | optional   | The number of logs to return (defaults to 100). |

### Responses

| Code | Description                    |
| ---- | ------------------------------ |
| 200  | The request was successful.    |
| 400  | The logs could not be fetched. |
| 404  | The server was not found.      |

Sources:

- [router/router_server.go#L26](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L26)

### `POST /api/servers/:uuid/power`

Updates the power state of a server. The `action` field must be either "start", "stop", "restart", or "kill", and the `wait_seconds` field must be an integer value between 0 and 300.

### Body

| Field        | Visibility | Type    | Description                                                    |
| ------------ | ---------- | ------- | -------------------------------------------------------------- |
| action       | required   | string  | The power action to set.                                       |
| wait_seconds | required   | integer | The amount of wait time to allow when setting the power state. |

### Responses

| Code | Description                              |
| ---- | ---------------------------------------- |
| 204  | The request was successful.              |
| 400  | The request body could not be parsed.    |
| 404  | The server was not found.                |
| 422  | The request body could not be validated. |

Sources:

- [router/router_server.go#L53](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L53)

### `POST /api/servers/:uuid/commands`

Sends one or more commands to the server console.

### Body

| Field    | Visibility | Type            | Description                          |
| -------- | ---------- | --------------- | ------------------------------------ |
| commands | required   | array of string | The commands to the server commands. |

### Responses

| Code | Description                           |
| ---- | ------------------------------------- |
| 204  | The request was successful.           |
| 400  | The request body could not be parsed. |
| 404  | The server was not found.             |
| 502  | The server is not running.            |

Sources:

- [router/router_server.go#L108](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L108)

### `POST /api/servers/:uuid/install`

Triggers the install process of a server and returns no content.

Sources:

- [router/router_server.go#L153](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L153)

### `POST /api/servers/:uuid/reinstall`

Triggers the reinstall process for a server.

### Responses

| Code | Description                                       |
| ---- | ------------------------------------------------- |
| 204  | The request was successful.                       |
| 404  | The server was not found.                         |
| 409  | Another power action is currently being executed. |

Sources:

- [router/router_server.go#L172](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L172)

### `POST /api/servers/:uuid/sync`

Triggers the synchronize process of the server on the panel and the node.

### Responses

| Code | Description                                      |
| ---- | ------------------------------------------------ |
| 204  | The request was successful.                      |
| 400  | An error occured while synchronizing the server. |
| 404  | The server was not found.                        |

Sources:

- [router/router_server.go#L142](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L142)

### `POST /api/deauthorize-user`

Disconnects user from server websockets and SFTP sessions.

### Body

| Field    | Visibility | Type            | Description                     |
| -------- | ---------- | --------------- | ------------------------------- |
| user     | required   | string          | The UUID of the user to deny.   |
| servers  | required   | array of string | A list of server UUIDs to deny. |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |

Sources:

- [router/router_system.go#L159](https://github.com/pterodactyl/wings/blob/a97e8ae09fd682057ef229d4940d6dcb0cdaf3af/router/router_system.go#L159)

### `POST /api/servers/:uuid/ws/deny`

> Deprecated. Use `POST /api/deauthorize-user` instead.

Adds the given JWT IDs (or "jti"s) to the server websocket's deny list, preventing tokens with the JTIs from connecting or interacting with the server websocket.

### Body

| Field | Visibility | Type            | Description             |
| ----- | ---------- | --------------- | ----------------------- |
| jtis  | required   | array of string | A list of JTIs to deny. |

### Responses

| Code | Description                           |
| ---- | ------------------------------------- |
| 204  | The request was successful.           |
| 400  | The request body could not be parsed. |
| 404  | The server was not found.             |

Sources:

- [router/router_server.go#L249](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server.go#L249)

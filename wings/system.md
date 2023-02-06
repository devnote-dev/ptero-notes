### `POST /api/update`

Updates the Wings configuration.

### Body

| Field          | Visibility | Type    | Description                                                               |
| -------------- | ---------- | ------- | ------------------------------------------------------------------------- |
| debug          | required   | boolean | Whether the node should be in debug mode (always `false`).                |
| uuid           | required   | string  | The UUID of the node in the panel.                                        |
| token_id       | required   | string  | The token ID of the node.                                                 |
| token          | required   | string  | The full (decrypted) daemon token.                                        |
| api            | required   | object  | An object containing the host, port, SSL and upload limit configurations. |
| system         | required   | object  | An object containing the data and configurations.                         |
| allowed_mounts | required   | array   | An array of allowed mount paths in the node host.                         |
| remote         | required   | string  | The remote URL to the node.                                               |

<!-- See the [node configuration](/pterodactyl/application/nodes.md) for more information. -->

### Responses

| Code | Description                             |
| ---- | --------------------------------------- |
| 204  | The request was accepted.               |
| 400  | The configuration could not be updated. |

Sources:

- [router/router_system.go#L117](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_system.go#L117)

### `GET /api/system`

Returns the system information for the host that Wings is running on.

### Parameters

| Name | Visibility | Description                                                                         |
| ---- | ---------- | ----------------------------------------------------------------------------------- |
| v    | optional   | Determines which format of the configuration to return (only accepts value of "2"). |

### Responses

| Code | Description                                  |
| ---- | -------------------------------------------- |
| 200  | The request was successful.                  |
| 400  | The system information could not be fetched. |

<!-- ### Example Object -->

Sources:

- [router/router_system.go#L20](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_system.go#L20)

### `GET /api/servers`

Returns a HTTP 200 response with a list of server objects (separate from the server objects in the panel's APIs).

<!-- ### Example Object -->

Sources:

- [router/router_system.go#L49](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_system.go#L49)

### `POST /api/servers`

Creates a server on the node and begins the installation process for it.

### Body

| Field               | Visibility | Type    | Description                                           |
| ------------------- | ---------- | ------- | ----------------------------------------------------- |
| uuid                | required   | string  | The UUID of the server in the panel.                  |
| start_on_completion | required   | boolean | Whether the server should start once it is installed. |

### Responses

| Code | Description                              |
| ---- | ---------------------------------------- |
| 204  | The request was accepted.                |
| 400  | The request body could not be parsed.    |
| 422  | The request body could not be validated. |

Sources:

- [router/router_system.go#L60](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_system.go#L60)

### `DELETE /api/transfers/:uuid`

Cancels an incoming server transfer request.

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 204  | The request was accepted.            |
| 400  | The server is not being transferred. |

Sources:

- [router/router_transfer.go#L252](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_transfer.go#L252)

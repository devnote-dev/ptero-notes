### `POST /api/servers/:uuid/transfer`

Initializes a transfer request for the specified server and returns a HTTP 204 status response. In summary, the process goes as follows:

1. The request body is validated along with the server state
2. Wings will attempt to stop the server within a given deadline if the server is running
3. A multipart form-data request is initialized between the source node and destination node
4. An archive of the server volume is created
5. The archive is encoded into form-data and streamed to the destination node

### Body

| Field  | Visibility | Type   | Description                                                                    |
| ------ | ---------- | ------ | ------------------------------------------------------------------------------ |
| url    | required   | string | The URL of the destination node.                                               |
| token  | required   | string | The JWT token.                                                                 |
| server | optional   | object | An object containing the UUID of the server and the start-on-completion state. |

Sources:

- [router/router_server_transfer.go#L27](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_transfer.go#L27)

### `DELETE /api/servers/:uuid/transfer`

Cancels an outgoing transfer request for the server.

### Responses

| Code | Description                                    |
| ---- | ---------------------------------------------- |
| 204  | The request was accepted.                      |
| 404  | The server was not found.                      |
| 409  | The server is not currently being transferred. |

Sources:

- [router/router_server_transfer.go#L109](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_transfer.go#L109)

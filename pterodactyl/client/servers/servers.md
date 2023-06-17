### `GET /servers/:identifier`

Returns a server identified by its `identifier` (string).
The `allocations` and `variables` parameters are included in the response by default.

### Parameters

| Name     | Supported | Type   | Description                            |
| -------- | --------- | ------ | -------------------------------------- |
| filter   | false     | -      | Not supported for filtering results    |
| include  | true      | string | allocations, eggs, subusers, variables |
| sort     | false     | -      | Not supported for sorting results      |
| page     | true      | number | Retrieve a specific page of results    |
| per_page | true      | number | Number of results to include per page  |

### Responses

| Code | Description                                 |
| ---- | ------------------------------------------- |
| 200  | The request was successful.                 |
| 404  | The server with the given ID was not found. |

### Example Response

```json
{
  "object": "server",
  "attributes": {
    "server_owner": true,
    "identifier": "1a7ce997",
    "internal_id": "1a7ce997-259b-452e-8b4e-cecc464142ca",
    "name": "Wuhu Island",
    "node": "Test",
    "is_node_under_maintenance": false,
    "sftp_details": {
      "ip": "pterodactyl.file.properties",
      "port": 2022
    },
    "description": "Matt from Wii Sports",
    "limits": {
      "memory": 512,
      "swap": 0,
      "disk": 200,
      "io": 500,
      "cpu": 0,
      "threads": 4,
      "oom_killer": false
    },
    "invocation": true,
    "docker_image": "example_docker_image",
    "egg_features": true,
    "feature_limits": {
      "databases": 5,
      "allocations": 5,
      "backups": 2
    },
    "status": "running",
    "is_transferring": false,
    "relationships": {
      "allocations": {
        "object": "list",
        "data": [
          {
            "object": "allocation",
            "attributes": {
              "id": 1,
              "ip": "45.86.168.218",
              "ip_alias": null,
              "port": 25565,
              "notes": null,
              "is_default": true
            }
          }
        ]
      }
    }
  },
  "meta": {
    "is_server_owner": true,
    "user_permissions": [
      "*",
      "admin.websocket.errors",
      "admin.websocket.install"
    ]
  }
}
```

### `GET /servers/:identifier/websocket`

Returns the websocket authentication details for a server. This includes the socket URL and JWT authentication token. See the [wings/websockets](../../../wings/websocket.md) page for more information.

### Responses

| Code | Description                                   |
| ---- | --------------------------------------------- |
| 200  | The request was successful.                   |
| 403  | The user does not have permission to connect. |

### Example Response

```json
{
  "data": {
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "socket": "wss://your-node-url/api/servers/{server_uuid}/ws"
  }
}
```

### `GET /servers/:identifier/resources`

Returns the current resource usage for a server, including the status and uptime.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |

### Example Response

```json
{
  "object": "stats",
  "attributes": {
    "current_state": "starting",
    "is_suspended": false,
    "resources": {
      "memory_bytes": 588701696,
      "cpu_absolute": 0,
      "disk_bytes": 130156361,
      "network_rx_bytes": 694220,
      "network_tx_bytes": 337090,
      "uptime": 0
    }
  }
}
```

### `GET /servers/:identifier/activity`

Returns a list of activity objects recorded on the server.

### Responses

| Code | Description                             |
| ---- | --------------------------------------- |
| 200  | Successful response containing the logs |
| 403  | Forbidden: The user is not authorized   |
| 404  | Not Found: The server was not found     |

### Example Response

```json
{
  "data": [
    {
      "attributes": {
        "object": "activity_log",
        "id": "d62fcd14cc3dfda30b4746e8540e5d582c68388d",
        "batch": null,
        "event": "Server Created",
        "is_api": false,
        "ip": null,
        "description": "The server was created.",
        "properties": {},
        "has_additional_metadata": false,
        "timestamp": "2023-06-10T15:30:00Z",
        "actor": {
          "id": 1,
          "username": "john.doe"
        }
      }
    }
  ]
}
```

### `POST /servers/:identifier/command`

Sends a command to the server console.

### Body

| name    | Visibility | Type   | Description         |
| ------- | ---------- | ------ | ------------------- |
| command | Required   | string | The command to send |

### Responses

| Code | Description                                                          |
| ---- | -------------------------------------------------------------------- |
| 204  | The request was accepted                                             |
| 409  | The server is unavailable (installing/transferring/restoring backup) |

### `POST /servers/:identifier/power`

Sends a signal request to change the power state of the server. Accepted power states are "start", "stop", "restart", and "kill".

### Body

| name  | Visibility | Type   | Description                              |
| ----- | ---------- | ------ | ---------------------------------------- |
| Power | Required   | string | The power action signal (e.g., "start"). |

### Body

| Code | Description                                                          |
| ---- | -------------------------------------------------------------------- |
| 204  | The request was accepted                                             |
| 400  | An invalid power state was sent                                      |
| 409  | The server is unavailable (installing/transferring/restoring backup) |

### `GET /api/client/servers/:serverId/network/allocations`

Returns a list of all the network allocations available for a server, along with information about whether they are currently assigned as the primary allocation for the server.

### Responses

| Code | Description                                     |
| ---- | ----------------------------------------------- |
| 200  | List of network allocations for the given server |

### Example Response

```json
{
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
```

### `POST /api/client/servers/:serverId/network/allocations`

Sets the note for the allocation in a server.

### Body

| Name  | Visibility | Type   | Description     |
| ----- | ---------- | ------ | --------------- |
| notes |  Required  | string | New notes value |

### Responses

| Code | Description                |
| ---- | -------------------------- |
| 200  | Created allocation for server |
| 400  | Limit has been reached        |

### `POST /api/client/servers/:serverId/network/allocations/:allocationId`

Updates the notes of a specific allocation for a server.

### Request Parameters

| Name       | Type   | Description                    |
| ---------- | ------ | ------------------------------ |
| server     | string | ID of the server                |
| allocation | string | ID of the allocation            |

### Body

| Name  | Visibility | Type   | Description     |
| ----- | ---------- | ------ | --------------- |
| notes |  Required  | string | New notes value |

### Responses

| Code | Description                  |
| ---- | ---------------------------- |
| 200  | Updated allocation for server |


### `POST /api/client/servers/:serverId/network/allocations/:allocationId/primary`

Sets a specific allocation as the primary allocation for a server.

### Request Parameters

| Name       | Type   | Description                    |
| ---------- | ------ | ------------------------------ |
| server     | string | ID of the server                |
| allocation | string | ID of the allocation            |

### Responses

| Code | Description                    |
| ---- | ------------------------------ |
| 200  | Primary allocation set for server |

### `DELETE /api/client/servers/:serverId/network/allocations/:allocationId`

Deletes a specific allocation from a server.

### Request Parameters

| Name       | Type   | Description                    |
| ---------- | ------ | ------------------------------ |
| server     | string | ID of the server                |
| allocation | string | ID of the allocation            |

### Responses

| Code | Description                   |
| ---- | ----------------------------- |
| 204  | Allocation deleted from server |
| 400  | Cannot delete primary allocation or no limit was set       |


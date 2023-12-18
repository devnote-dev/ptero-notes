## Contents

- [Get Server Network Allocations](#get-server-network-allocations)
- [Create Server Network Allocation](#create-server-network-allocation)
- [Update Server Network Allocation](#update-server-network-allocation)
- [Update Primary Server Network Allocation](#update-primary-server-network-allocation)
- [Delete Server Network Allocation](#delete-server-network-allocation)

---

## Get Server Network Allocations

### `GET /api/client/servers/:id/network/allocations`

Returns a list of all the network allocations available for a server, along with information about whether they are currently assigned as the primary allocation for the server.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The server was not found.   |

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

### Sources

- [NetworkAllocationController.php#L36](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Client/Servers/NetworkAllocationController.php#L36)

## Create Server Network Allocation

### `POST /api/client/servers/:id/network/allocations`

<!-- TODO: needs more information -->

Creates a new network allocation on the server.

### Responses

| Code | Description                                                     |
| ---- | --------------------------------------------------------------- |
| 200  | The request was successful.                                     |
| 400  | Auto-allocation is disabled or server allocation limit reached. |

### Sources

- [NetworkAllocationController.php#L93](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Client/Servers/NetworkAllocationController.php#L93)

## Update Server Network Allocation

### `POST /api/client/servers/:server_id/network/allocations/:id`

Updates the notes of a specific allocation for a server.

### Body

| Name  | Visibility | Type   | Description           |
| ----- | ---------- | ------ | --------------------- |
| notes | required   | string | The allocation notes. |

### Responses

| Code | Description                             |
| ---- | --------------------------------------- |
| 200  | The request was successful.             |
| 404  | The server or allocation was not found. |

### Sources

- [NetworkAllocationController.php#L49](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Client/Servers/NetworkAllocationController.php#L49)

## Update Primary Server Network Allocation

### `POST /api/client/servers/:server_id/network/allocations/:id/primary`

Sets a specific allocation as the primary allocation for a server.

### Responses

| Code | Description                             |
| ---- | --------------------------------------- |
| 200  | The request was successful.             |
| 404  | The server or allocation was not found. |

### Sources

- [NetworkAllocationController.php#L73](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Client/Servers/NetworkAllocationController.php#L73)

## Delete Server Network Allocation

### `DELETE /api/client/servers/:server_id/network/allocations/:id`

Deletes a specific allocation from a server.

> [!CAUTION]
> This will not work if the allocation is the primary allocation for the server.

### Responses

| Code | Description                                              |
| ---- | -------------------------------------------------------- |
| 204  | The request was successful.                              |
| 400  | No allocation limit is set or the allocation is primary. |
| 404  | The server or allocation was not found.                  |

### Sources

- [NetworkAllocationController.php#L116](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Client/Servers/NetworkAllocationController.php#L116)

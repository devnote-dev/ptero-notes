## Contents

- [Get Nodes](#get-nodes)
- [Get Deployable Nodes](#get-deployable-nodes)
- [Get Node](#get-node)
- [Get Node Allocations](#get-node-allocations)
- [Create Node Allocation](#create-node)
- [Delete Node Allocation](#delete-node-allocation)
- [Get Node Configuration](#get-node-configuration)
- [Create Node](#create-node)
- [Update Node](#update-node)
- [Delete Node](#delete-node)

---

## Get Nodes

### `GET /api/application/nodes`

Returns a list of node objects.

### Parameters

| Name     | Visibility | Type           | Allowed Values                    |
| -------- | ---------- | -------------- | --------------------------------- |
| filter   | optional   | \[key]=value   | daemon_token_id, fqdn, name, uuid |
| include  | optional   | array\[string] | allocations, locations, servers   |
| sort     | optional   | string         | disk, id, memory, uuid            |
| page     | optional   | number         | >= 1                              |
| per_page | optional   | number         | >= 1                              |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |

### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "object": "node",
      "attributes": {
        "allocated_resources": {
          "disk": 26512,
          "memory": 12368
        },
        "behind_proxy": false,
        "created_at": "2022-01-03T09:25:00+00:00",
        "daemon_base": "/var/lib/pterodactyl/volumes",
        "daemon_listen": 7373,
        "daemon_sftp": 3033,
        "description": "ptero test node",
        "disk": 72000,
        "disk_overallocate": -1,
        "fqdn": "nodes.pterodactyl.test",
        "id": 1,
        "location_id": 1,
        "maintenance_mode": false,
        "memory": 16000,
        "memory_overallocate": -1,
        "name": "ID1",
        "public": true,
        "scheme": "https",
        "updated_at": "2022-08-25T10:49:25+00:00",
        "upload_size": 100,
        "uuid": "21412d5d-4f65-4ba8-8803-6e1754b9b4e6"
      }
    }
  ]
}
```

### Sources

- [NodeController.php#L35](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeController.php#L35)

## Get Deployable Nodes

### `GET /api/application/nodes/deployable`

Returns a list of deployable nodes determined by the request body requirements.

### Parameters

| Name     | Visibility | Type   | Allowed Values |
| -------- | ---------- | ------ | -------------- |
| page     | optional   | number | >= 1           |
| per_page | optional   | number | >= 1           |

### Body

| Field        | Visibility | Type           | Description                               |
| ------------ | ---------- | -------------- | ----------------------------------------- |
| disk         | required   | number         | The disk limit to query by.               |
| memory       | required   | number         | The memory limit to query by.             |
| location_ids | optional   | array\[number] | Only use nodes in the given location IDs. |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 429  | One or more validation rules failed. |

### Sources

- [NodeDeploymentController.php#L27](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeDeploymentController.php#L27)
- [GetDeployableNodesRequest.php#L5](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Requests/Api/Application/Nodes/GetDeployableNodesRequest.php#L5)

## Get Node

### `GET /api/application/nodes/:id`

Returns a node by its `id` (number).

### Parameters

| Name    | Visibility | Type           | Allowed Values                 |
| ------- | ---------- | -------------- | ------------------------------ |
| include | optional   | array\[string] | allocations, location, servers |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The node was not found.     |

### Example Response

```json
{
  "object": "node",
  "attributes": {
    "allocated_resources": {
      "disk": 26512,
      "memory": 12368
    },
    "behind_proxy": false,
    "created_at": "2022-01-03T09:25:00+00:00",
    "daemon_base": "/var/lib/pterodactyl/volumes",
    "daemon_listen": 7373,
    "daemon_sftp": 3033,
    "description": "ptero test node",
    "disk": 72000,
    "disk_overallocate": -1,
    "fqdn": "nodes.pterodactyl.test",
    "id": 1,
    "location_id": 1,
    "maintenance_mode": false,
    "memory": 16000,
    "memory_overallocate": -1,
    "name": "ID1",
    "public": true,
    "scheme": "https",
    "updated_at": "2022-08-25T10:49:25+00:00",
    "upload_size": 100,
    "uuid": "21412d5d-4f65-4ba8-8803-6e1754b9b4e6"
  }
}
```

### Sources

- [NodeController.php#L50](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeController.php#L50)

## Get Node Allocations

### `GET /api/application/nodes/:id/allocations`

Returns a list of allocations for a specified node.

### Parameters

| Name     | Visibility | Type           | Allowed Values                |
| -------- | ---------- | -------------- | ----------------------------- |
| filter   | optional   | \[key]=value   | ip, ip_alias, port, server_id |
| include  | optional   | array\[string] | node, server                  |
| page     | optional   | number         | >= 1                          |
| per_page | optional   | number         | >= 1                          |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The node was not found.     |

<!-- ### Example Response -->

### Sources

- [AllocationController.php#L34](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/AllocationController.php#L34)

## Create Node Allocation

### `POST /api/application/nodes/:id/allocations`

Creates an allocation on the node.

### Body

| Field | Visibility | Type           | Description                                        |
| ----- | ---------- | -------------- | -------------------------------------------------- |
| ip    | required   | string         | The IP to bind the allocation to.                  |
| alias | optional   | string         | The IP alias for the allocation.                   |
| ports | required   | array\[string] | A list of ports or port-ranges for the allocation. |

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 204  | The request was successful.          |
| 404  | The node was not found.              |
| 429  | One or more validation rules failed. |

### Sources

- [AllocationController.php#L65](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/AllocationController.php#L65)

## Delete Node Allocation

### `DELETE /api/application/nodes/:id/allocations/:id`

Deletes an allocation from the node by its `id` (number).

### Response

| Code | Description                           |
| ---- | ------------------------------------- |
| 204  | The request was successful.           |
| 404  | The node or allocation was not found. |

### Sources

- [AllocationController.php#L77](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/AllocationController.php#L77)

## Get Node Configuration

### `GET /nodes/:id/configuration`

Returns the configuration data of a specified node.

### Response

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |
| 404  | The node was not found.     |

<!-- ### Example Response -->

### Sources

- [NodeConfigurationController.php#L17](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeConfigurationController.php#L17)

## Create Node

### `POST /api/application/nodes`

Creates a node.

### Body

| Field               | Visibility | Type    | Description                                                     |
| ------------------- | ---------- | ------- | --------------------------------------------------------------- |
| behind_proxy        | required   | boolean | Whether the node is behind a proxy.                             |
| daemon_base         | required   | string  | The daemon base for the node.                                   |
| daemon_listen       | required   | number  | The port for the daemon to listen on.                           |
| daemon_sftp         | required   | number  | The SFTP port for the node.                                     |
| description         | optional   | string  | A description of the node.                                      |
| disk                | required   | string  | The disk space limit.                                           |
| disk_overallocate   | required   | string  | The overallocated disk space limit.                             |
| fqdn                | required   | string  | The FQDN of the node.                                           |
| location_id         | required   | number  | The location to create the node on.                             |
| maintenance_mode    | optional   | boolean | Whether the node should be under maintenance mode when created. |
| memory              | required   | number  | The memory usage limit.                                         |
| memory_overallocate | required   | string  | The overallocated memory limit.                                 |
| name                | required   | string  | The name of the node.                                           |
| public              | optional   | boolean | Whether the node is publicly accessible.                        |
| scheme              | required   | string  | The HTTP scheme for the node.                                   |
| upload_size         | optional   | number  | The upload size for the node.                                   |

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 201  | The request was successful.          |
| 429  | One or more validation rules failed. |

<!-- ### Example Response -->

### Sources

- [NodeController.php#L63](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeController.php#L63)

## Update Node

### `PATCH /api/application/nodes/:id`

Updates a node by its `id` (number).

### Body

| Field               | Visibility | Type    | Description                                                     |
| ------------------- | ---------- | ------- | --------------------------------------------------------------- |
| behind_proxy        | required   | boolean | Whether the node is behind a proxy.                             |
| daemon_base         | required   | string  | The daemon base for the node.                                   |
| daemon_listen       | required   | number  | The port for the daemon to listen on.                           |
| daemon_sftp         | required   | number  | The SFTP port for the node.                                     |
| description         | required   | string  | A description of the node.                                      |
| disk                | required   | string  | The disk space limit.                                           |
| disk_overallocate   | required   | string  | The overallocated disk space limit.                             |
| fqdn                | required   | string  | The FQDN of the node.                                           |
| location_id         | required   | number  | The location to create the node on.                             |
| maintenance_mode    | required   | boolean | Whether the node should be under maintenance mode when created. |
| memory              | required   | number  | The memory usage limit.                                         |
| memory_overallocate | required   | string  | The overallocated memory limit.                                 |
| name                | required   | string  | The name of the node.                                           |
| public              | required   | boolean | Whether the node is publicly accessible.                        |
| scheme              | required   | string  | The HTTP scheme for the node.                                   |
| upload_size         | required   | number  | The upload size for the node.                                   |

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 404  | The node was not found.              |
| 429  | One or more validation rules failed. |

### Sources

- [NodeController.php#L82](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeController.php#L82)

## Delete Node

### `DELETE /nodes/:id`

Deletes a node by its `id` (number).

### Response

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |
| 404  | The node was not found.     |

### Sources

- [NodeController.php#L101](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Nodes/NodeController.php#L101)

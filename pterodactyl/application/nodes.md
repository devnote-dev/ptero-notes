## Contents

- [Get Nodes]
- [Get Deployable Nodes]
- [Get Node]
- [Get Node Allocations]
- [Create Node Allocation]
- [Delete Node Allocation]
- [Get Node Configuration]
- [Create Node]
- [Update Node]
- [Delete Node]

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

## Delete Node Allocation

### `DELETE /api/application/nodes/:id/allocations/:id`

Deletes an allocation from the node by its `id` (number).

### Response

| Code | Description                           |
| ---- | ------------------------------------- |
| 204  | The request was successful.           |
| 404  | The node or allocation was not found. |

## Get Node Configuration

### `GET /nodes/:id/configuration`

Returns the configuration data of a specified node.

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 204  | The request was successful.          |
| 404  | The node was not found.              |

<!-- ### Example Response -->

## Create Node

### `POST /nodes`

Creates a node.

### Body

| Key                 | Required | Type      | Description                                                    |
| ------------------- | -------- | --------- | -------------------------------------------------------------- |
| behind_proxy        | ✅       | `boolean` | Whether the node is behind a proxy                             |
| daemon_base         | ✅       | `string`  | The daemon base for the node                                   |
| daemon_listen       | ✅       | `number`  | The port for the daemon to listen on                           |
| daemon_sftp         | ✅       | `number`  | The SFTP port for the node                                     |
| description         | ❌       | `string`  | A description of the node                                      |
| disk                | ✅       | `string`  | The disk space limit                                           |
| disk_overallocate   | ✅       | `string`  | The overallocated disk space limit                             |
| fqdn                | ✅       | `string`  | The FQDN of the node                                           |
| location_id         | ✅       | `number`  | The location to create the node on                             |
| maintenance_mode    | ❌       | `boolean` | Whether the node should be under maintenance mode when created |
| memory              | ✅       | `number`  | The memory usage limit                                         |
| memory_overallocate | ✅       | `string`  | The overallocated memory limit                                 |
| name                | ✅       | `string`  | The name of the node                                           |
| public              | ❌       | `boolean` | Whether the node is publicly accessible                        |
| scheme              | ✅       | `string`  | The HTTP scheme for the node                                   |
| upload_size         | ❌       | `number`  | The upload size for the node                                   |

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 429  | One or more validation rules failed. |

<!-- ### Example Response -->

## Update Node

### `PATCH /nodes/:id`

Updates a node by its `id` (number).

### Body

| Key                 | Required | Type      | Description                                                    |
| ------------------- | -------- | --------- | -------------------------------------------------------------- |
| behind_proxy        | ❌       | `boolean` | Whether the node is behind a proxy                             |
| daemon_base         | ❌       | `string`  | The daemon base for the node                                   |
| daemon_listen       | ❌       | `number`  | The port for the daemon to listen on                           |
| daemon_sftp         | ❌       | `number`  | The SFTP port for the node                                     |
| description         | ❌       | `string`  | A description of the node                                      |
| disk                | ❌       | `string`  | The disk space limit                                           |
| disk_overallocate   | ❌       | `string`  | The overallocated disk space limit                             |
| fqdn                | ❌       | `string`  | The FQDN of the node                                           |
| location_id         | ❌       | `number`  | The location to create the node on                             |
| maintenance_mode    | ❌       | `boolean` | Whether the node should be under maintenance mode when created |
| memory              | ❌       | `number`  | The memory usage limit                                         |
| memory_overallocate | ❌       | `string`  | The overallocated memory limit                                 |
| name                | ❌       | `string`  | The name of the node                                           |
| public              | ❌       | `boolean` | Whether the node is publicly accessible                        |
| scheme              | ❌       | `string`  | The HTTP scheme for the node                                   |
| upload_size         | ❌       | `number`  | The upload size for the node                                   |

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 404  | The node was not found.              |
| 429  | One or more validation rules failed. |

## Delete Node

### `DELETE /nodes/:id`

Deletes a node by its `id` (number).

### Response

| Code | Description                          |
| ---- | ------------------------------------ |
| 204  | The request was successful.          |
| 404  | The node was not found.              |

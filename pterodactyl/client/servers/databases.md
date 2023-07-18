### `GET /api/client/servers/:serverId/databases`

Returns all the databases that belong to the given server.

### Responses

| Code | Description       |
| ---- | ----------------- |
| 200  | List of databases |

### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "object": "server_database",
      "attributes": {
        "id": "bEY4yAD5",
        "host": {
          "address": "127.0.0.1",
          "port": 3306
        },
        "name": "s5_perms",
        "username": "u5_QsIAp1jhvS",
        "connections_from": "%",
        "max_connections": 0
      }
    }
  ]
}
```

### `POST /api/client/servers/:serverId/databases`

Creates a new database for the given server and return it.

### Body

| Name     | Visibility | Type   | Description         |
| -------- | ---------- | ------ | ------------------- |
| database | Required   | string | Database name       |
| remote   | Required   | string | Database remote URL |

### Responses

| Code | Description      |
| ---- | ---------------- |
| 200  | Created database |

### Example Response

```json
{
  "object": "server_database",
  "attributes": {
    "id": "y9YVxO4V",
    "host": {
      "address": "127.0.0.1",
      "port": 3306
    },
    "name": "s5_punishments",
    "username": "u5_aeZqbGdCM9",
    "connections_from": "%",
    "max_connections": 0,
    "relationships": {
      "password": {
        "object": "database_password",
        "attributes": {
          "password": "=lR2orDOcwfKkM=BXb.BVF.C"
        }
      }
    }
  }
}
```

### `POST /api/client/servers/:serverId/databases/:databaseId/rotate-password`

Rotates the password on a database instance. If the user does not have the `view_password` permission they will not see the updated password.

### Responses

| Code | Description      |
| ---- | ---------------- |
| 200  | Password rotated |

### Example Response

```json
{
  "object": "server_database",
  "attributes": {
    "id": "y9YVxO4V",
    "host": {
      "address": "127.0.0.1",
      "port": 3306
    },
    "name": "s5_punishments",
    "username": "u5_aeZqbGdCM9",
    "connections_from": "%",
    "max_connections": 0,
    "relationships": {
      "password": {
        "object": "database_password",
        "attributes": {
          "password": "=lR2orDOcwfKkM=BXb.BVF.C"
        }
      }
    }
  }
}
```

### `DELETE /api/client/servers/:serverId/databases/:databaseId`

Removes a specified database from the server.

### Responses

| Code | Description      |
| ---- | ---------------- |
| 204  | Database deleted |

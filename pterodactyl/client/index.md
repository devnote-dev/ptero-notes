### `GET /api/client`

Returns all the servers available to the client making the API request, including servers the user has access to as a subuser.

### Body

| Name | Visibility | Type   | Description                                                 |
| ---- | ---------- | ------ | ----------------------------------------------------------- |
| type | Optional   | string | The type of user. Possible values: admin, admin-all, owner. |

### Responses

| Code | Description                    |
| ---- | ------------------------------ |
| 200  | The list of servers.           |
| 422  | The request query was invalid. |

### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "object": "server",
      "attributes": {
        "server_owner": true,
        "identifier": "1a7ce997",
        "uuid": "1a7ce997-259b-452e-8b4e-cecc464142ca",
        "name": "Gaming",
        "node": "Test",
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
          "cpu": 0
        },
        "feature_limits": {
          "databases": 5,
          "allocations": 5,
          "backups": 2
        },
        "is_suspended": false,
        "is_installing": false,
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
      }
    }
  ],
  "meta": {
    "pagination": {
      "total": 1,
      "count": 1,
      "per_page": 50,
      "current_page": 1,
      "total_pages": 1,
      "links": {}
    }
  }
}
```

### `GET /api/client/permissions`

Returns all the subuser permissions available on the system.

### Responses

| Code | Description                      |
| ---- | -------------------------------- |
| 200  | The list of subuser permissions. |

### Example Response

```json
{
  "object": "subuser_permission",
  "attributes": {
    "permissions": {
      "websocket": {
        "description": "Allows the user to connect to the server websocket, giving them access to view console output and realtime server stats.",
        "keys": {
          "connect": "Allows a user to connect to the websocket instance for a server to stream the console."
        }
      },
      "control": {
        "description": "Permissions that control a user's ability to control the power state of a server, or send commands.",
        "keys": {
          "console": "Allows a user to send commands to the server instance via the console.",
          "start": "Allows a user to start the server if it is stopped.",
          "stop": "Allows a user to stop a server if it is running.",
          "restart": "Allows a user to perform a server restart. This allows them to start the server if it is offline, but not put the server in a completely stopped state."
        }
      },
      "user": {
        "description": "Permissions that allow a user to manage other subusers on a server. They will never be able to edit their own account, or assign permissions they do not have themselves.",
        "keys": {
          "create": "Allows a user to create new subusers for the server.",
          "read": "Allows the user to view subusers and their permissions for the server.",
          "update": "Allows a user to modify other subusers.",
          "delete": "Allows a user to delete a subuser from the server."
        }
      },
      // ... (other permissions)
    }
  }
}

```

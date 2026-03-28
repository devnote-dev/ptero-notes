## Contents

- [Get Remote Servers](#get-remote-servers)
- [Reset Remote Servers](#reset-remote-servers)
- [Add Remote Server Activities](#add-remote-server-activities)

---

## Get Remote Servers

### `GET /api/remote/servers`

Lists all servers with their configurations that are assigned to the requesting node.

### Parameters

| Name     | Visibility | Description                    |
| -------- | ---------- | ------------------------------ |
| page     | optional   | The page to list.              |
| per_page | optional   | The amount of servers to list. |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |

### Example Response

```json
{
  "data": [
    {
      "uuid": "0a123456-bcd7-8901-e234-567fgh890ij1",
      "settings": {
        "uuid": "0a123456-bcd7-8901-e234-567fgh890ij1",
        "meta": {
          "name": "My server",
          "description": ""
        },
        "suspended": false,
        "environment": {
          "SERVER_JARFILE": "server.jar",
          "MC_VERSION": "latest",
          "BUILD_TYPE": "recommended",
          "FORGE_VERSION": "",
          "STARTUP": "java -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true $( [[  ! -f unix_args.txt ]] && printf %s \"-jar {{SERVER_JARFILE}}\" || printf %s \"@unix_args.txt\" )",
          "P_SERVER_LOCATION": "home",
          "P_SERVER_UUID": "0a123456-bcd7-8901-e234-567fgh890ij1",
          "P_SERVER_ALLOCATION_LIMIT": 0
        },
        "invocation": "java -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true $( [[  ! -f unix_args.txt ]] && printf %s \"-jar {{SERVER_JARFILE}}\" || printf %s \"@unix_args.txt\" )",
        "skip_egg_scripts": false,
        "build": {
          "memory_limit": 0,
          "swap": 0,
          "io_weight": 500,
          "cpu_limit": 0,
          "threads": null,
          "disk_space": 0,
          "oom_disabled": true
        },
        "container": {
          "image": "ghcr.io/pterodactyl/yolks:java_8",
          "oom_disabled": true,
          "requires_rebuild": false
        },
        "allocations": {
          "force_outgoing_ip": false,
          "default": {
            "ip": "192.168.228.1",
            "port": 25565
          },
          "mappings": {
            "192.168.228.1": [25565]
          }
        },
        "mounts": [
          {
            "source": "/root/mnt",
            "target": "/root/mnt",
            "read_only": false
          }
        ],
        "egg": {
          "id": "b3e7a6b9-1cc9-4d3e-9372-88b6d96c6b0f",
          "file_denylist": []
        }
      },
      "process_configuration": {
        "startup": {
          "done": [")! For help, type "],
          "user_interaction": [],
          "strip_ansi": false
        },
        "stop": {
          "type": "command",
          "value": "stop"
        },
        "configs": [
          {
            "parser": "properties",
            "file": "server.properties",
            "replace": [
              {
                "match": "server-ip",
                "replace_with": "0.0.0.0"
              },
              {
                "match": "server-port",
                "replace_with": "25565"
              },
              {
                "match": "query.port",
                "replace_with": "25565"
              }
            ]
          }
        ]
      }
    }
  ],
  "links": {
    "first": "http://127.0.0.1/api/remote/servers?page=1",
    "last": "http://127.0.0.1/api/remote/servers?page=3",
    "prev": null,
    "next": "http://127.0.0.1/api/remote/servers?page=2"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 3,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "http://127.0.0.1/api/remote/servers?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "http://127.0.0.1/api/remote/servers?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "http://127.0.0.1/api/remote/servers?page=3",
        "label": "3",
        "active": false
      },
      {
        "url": "http://127.0.0.1/api/remote/servers?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "http://127.0.0.1/api/remote/servers",
    "per_page": 1,
    "to": 1,
    "total": 3
  }
}
```

> [!TIP]
> The `mounts` field can also be defined as an array of objects with the fields `source` (string), `target` (string) and `read_only` (boolean).

### Sources

- [ServerDetailsController.php#L48](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L48)

## Reset Remote Servers

### `POST /api/remote/servers/reset`

Resets the state of all servers on the node to be normal.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |

### Sources

- [ServerDetailsController.php#L72](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L72)

## Add Remote Server Activities

### `POST /api/remote/activity`

<!-- TODO: no description?? -->

### Body

| Name | Visibility | Type  | Description                             |
| ---- | ---------- | ----- | --------------------------------------- |
| data | required   | array | An array with all server activity data. |

### Example Body

```json
{
  "data": [
    {
      "server": "a1bc2345-678d-9e01-2f3g-4hijk5l6m789",
      "event": "server:sftp.write",
      "timestamp": "1968-01-01T00:00:00.000000000Z",
      "metadata": {
        "files": ["/fake.log"]
      },
      "ip": "0.0.0.0",
      "user": "abcde1fg-2345-6789-012h-ij34kl5m6789"
    }
  ]
}
```

<!-- TODO: fix this
- `metadata` depends on the event. It can be null, a string, or a json blob with event specific metadata.
- `ip` has to be an IP address or empty string.
- `user` has to be a user UUID or undefined.
- `events` are activity events. You can find a list of them by [clicking here](activity_events.md).
-->

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 422  | One or more validation rules failed. |

### Sources

- [ActivityProcessingController.php#L20](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/ActivityProcessingController.php#L20)

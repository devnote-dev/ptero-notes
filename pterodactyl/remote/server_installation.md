### `GET /api/remote/servers/:uuid`

Returns details about the server that allows Wings to self-recover and ensure that the state of the server matches the Panel at all times.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The server was not found.   |

### Response example

```json
{
  "settings": {
    "uuid": "1abc23d4-567e-8f9g-9h01-2ij34k56lmno",
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
      "P_SERVER_UUID": "1abc23d4-567e-8f9g-9h01-2ij34k56lmno",
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
        "ip": "127.0.0.1",
        "port": 25565
      },
      "mappings": {
        "127.0.0.1": [25565]
      }
    },
    "mounts": [],
    "egg": {
      "id": "a1b2c3d4-5ef6-7g8h-9012-34i5j67k8l9m",
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
```

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L35](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L35)

---

### `GET /api/remote/servers/:uuid/install`

Returns installation information for a server.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The server was not found.   |

### Response example

```json
{
  "body": {
    "container_image": "openjdk:8-jdk-slim",
    "entrypoint": "bash",
    "script": "# Installation script here"
  }
}
```

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L30](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L30)

---

### `POST /api/remote/servers/:uuid/install`

Updates the installation state of a server.

### Body

| Name       | Visibility | Type    | Description                                                    |
| ---------- | ---------- | ------- | -------------------------------------------------------------- |
| successful | required   | boolean | Notifies if the server has completed the installation process. |
| reinstall  | required   | boolean | The state of the server.                                       |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |
| 404  | The server was not found.   |

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L48](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L48)

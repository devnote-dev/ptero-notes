### `GET /api/remote/servers`

Lists all servers with their configurations that are assigned to the requesting node.

### Parameters

| Name      | Visibility | Description                    |
| --------- | ---------- | ------------------------------ |
| page      | optional   | The page to list.              |
| per_page  | optional   | The amount of servers to list. |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |

### Response example

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
            "192.168.228.1": [
              25565
            ]
          }
        },
        "mounts": [],
        "egg": {
          "id": "b3e7a6b9-1cc9-4d3e-9372-88b6d96c6b0f",
          "file_denylist": []
        }
      },
      "process_configuration": {
        "startup": {
          "done": [
            ")! For help, type "
          ],
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

Sources

- [https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L49](app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L49)

---

### `POST /api/remote/servers/reset`

Resets the state of all servers on the node to be normal.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L72](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L72)

---

### `POST /api/remote/activity`

### Body

| Name  | Visibility | Type   | Description                                  |
| ----- | ---------- | ------ | -------------------------------------------- |
| data  | required   | array  | An array with all server activity data.      |

### Example Body

```json
{
  "data": [
    {
      "server": "a1bc2345-678d-9e01-2f3g-4hijk5l6m789",
      "event": "server:sftp.write",
      "timestamp": "1968-01-01T00:00:00.000000000Z",
      "metadata": {
        "files": [ "/fake.log" ],
      },
      "ip": "0.0.0.0",
      "user": "abcde1fg-2345-6789-012h-ij34kl5m6789"
    }
  ]
}
```

Notes

- Here is a list of all possible values for `event`.

```text
server.backup.restore-failed
server:allocation.create
server:allocation.delete
server:allocation.notes
server:allocation.primary
server:backup.complete
server:backup.delete
server:backup.download
server:backup.fail
server:backup.lock
server:backup.restore
server:backup.restore-complete
server:backup.restore-failed
server:backup.restore-started
server:backup.start
server:backup.unlock
server:console.command
server:console.command
server:database.create
server:database.delete
server:database.rotate-password
server:file.compress
server:file.copy
server:file.create-directory
server:file.decompress
server:file.delete
server:file.download
server:file.pull
server:file.read
server:file.rename
server:file.uploaded
server:file.write
server:power.kill
server:power.restart
server:power.start
server:power.stop
server:reinstall
server:schedule.create
server:schedule.delete
server:schedule.execute
server:schedule.update
server:settings.description
server:settings.rename
server:sftp.create
server:sftp.create-directory
server:sftp.delete
server:sftp.denied
server:sftp.rename
server:sftp.write
server:startup.edit
server:startup.image
server:subuser.create
server:subuser.delete
server:subuser.update
server:task.create
server:task.delete
server:task.update

* If there are any missing events, feel free to open a pull request.
```

- `metadata` depends on the event. It can be null, a string, or a json blob with event specific metadata.
- `ip` has to be an IP address or empty string.
- `user` has to be a user UUID or undefined.

### Responses

WIP.

Sources

- [app/Http/Controllers/Api/Remote/ActivityProcessingController.php#L20](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/ActivityProcessingController.php#L20)

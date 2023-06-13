### `GET /api/remote/servers`

Lists all servers with their configurations that are assigned to the requesting node.

### Parameters

| Name      | Visibility | Description                    |
| --------- | ---------- | ------------------------------ |
| page      | optional   | The page to list.              |
| per_page  | optional   | The amount of servers to list. |

### Responses

WIP.

Sources

- [https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L49](app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L49)

---

### `POST /api/remote/servers/reset`

Resets the state of all servers on the node to be normal.

### Responses

WIP.

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

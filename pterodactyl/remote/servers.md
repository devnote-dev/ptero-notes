### `GET /api/remote/servers`

Lists all servers with their configurations that are assigned to the requesting node.

### Parameters

| Name      | Visibility | Description                     |
| --------- | ---------- | ------------------------------- |
| page | optional | The page to list. |
| per_page | optional | The amount of servers to list. |

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
| data | required | array | An array with all server activity data. |

### Example Body

```json
{
  data: [
    {
      server: string,
      event: string,
      timestamp: string, // timestamp
      metadata: , // null, string or json blob with event specific metadata (it depends)
      ip: string, // ip address or empty string
      user: string, // user uuid or empty string
    },
    ...
  ]
}
```

### Responses

WIP.

Sources

- [app/Http/Controllers/Api/Remote/ActivityProcessingController.php#L20](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/ActivityProcessingController.php#L20)

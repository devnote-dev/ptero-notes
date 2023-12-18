## Contents

- [Get Server Startup](#get-server-startup)
- [Update Server Startup Variable](#update-server-startup-variable)

---

## Get Server Startup

### `GET /api/client/servers/:id/startup`

Retrieves the startup information for a server, including all the variables.

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
      "object": "egg_variable",
      "attributes": {
        "name": "Server Jar File",
        "description": "The name of the server jarfile to run the server with.",
        "env_variable": "SERVER_JARFILE",
        "default_value": "server.jar",
        "server_value": "server.jar",
        "is_editable": true,
        "rules": "required|regex:/^([\\w\\d._-]+)(\\.jar)$/"
      }
    }
  ],
  "meta": {
    "startup_command": "java -Xms128M -Xmx512M -jar server.jar",
    "raw_startup_command": "java -Xms128M -Xmx{{ SERVER_MEMORY }}M -jar {{ SERVER_JARFILE }",
    "docker_images": []
  }
}
```

### Sources

- [StartupController.php#L30](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Controllers/Api/Client/Servers/StartupController.php#L30)

## Update Server Startup Variable

### `PUT /api/client/servers/:id/startup/variable`

Updates a single variable for a server's startup.

### Body

| Name  | Visibility | Type   | Description                            |
| ----- | ---------- | ------ | -------------------------------------- |
| key   | required   | string | The key of the variable to be updated. |
| value | required   | string | The new value of the variable.         |

### Responses

| Code | Description                           |
| ---- | ------------------------------------- |
| 200  | The request was successful.           |
| 400  | The request body was invalid.         |
| 404  | The server or variable was not found. |

### Sources

- [StartupController.php#L53](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Controllers/Api/Client/Servers/StartupController.php#L53)
- [UpdateStartupVariableRequest.php#L8](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Requests/Api/Client/Servers/Startup/UpdateStartupVariableRequest.php#L8)

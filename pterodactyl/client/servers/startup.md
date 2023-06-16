### `GET /api/client/servers/:serverId/startup`

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

### `PUT /api/client/servers/:serverId/startup/variable`

Updates a single variable for a server's startup.

### Body

| Name  | Visibility | Type   | Description                            |
| ----- | ---------- | ------ | -------------------------------------- |
| key   | Required   | string | The key of the variable to be updated. |
| value | Required   | string | The new value of the variable.         |

### Responses

| Code | Description                           |
| ---- | ------------------------------------- |
| 200  | The variable was updated.             |
| 400  | The request body was invalid.         |
| 404  | The server or variable was not found. |

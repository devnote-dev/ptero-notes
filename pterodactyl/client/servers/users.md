### `GET /api/client/servers/:serverId/users`

Returns a list of all users associated with a server.

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | List of users associated with server |

### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "object": "server_subuser",
      "attributes": {
        "uuid": "73f233ca-99e0-47a9-bd46-efd3296d7ad9",
        "username": "subuser1uxk",
        "email": "subuser1@example.com",
        "image": "https://gravatar.com/avatar/c0da5391b64449c1ecbfd4349184377c",
        "2fa_enabled": false,
        "created_at": "2020-06-12T23:18:43+01:00"
      }
    }
  ]
}
```

### `GET /api/client/servers/:serverId/users/:userId`

Returns information about a specific subuser associated with a server.

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | Information about the specified user |

### Example Response

```json
{
  "object": "server_subuser",
  "attributes": {
    "uuid": "60a7aec3-e17d-4aa9-abb3-56d944d204b4",
    "username": "subuser2jvc",
    "email": "subuser2@example.com",
    "image": "https://gravatar.com/avatar/3bb1c751a8b3488f4a4c70eddfe898d8",
    "2fa_enabled": false,
    "created_at": "2020-06-12T23:31:41+01:00",
    "permissions": ["control.console", "control.start", "websocket.connect"]
  }
}
```

### `POST /api/client/servers/:serverId/users`

Creates a new subuser for the given server.

### Body

| Name        | Visibility | Type     | Description       |
| ----------- | ---------- | -------- | ----------------- |
| email       | required   | string   | Email of the user |
| permissions | required   | string[] | Permissions array |

### Responses

| Code | Description                |
| ---- | -------------------------- |
| 200  | Created subuser for server |

### `POST /api/client/servers/:serverId/users/:userId`

Updates a specific subuser associated with a server.

### Request Body

| Name        | Visibility | Type     | Description       |
| ----------- | ---------- | -------- | ----------------- |
| permissions | required   | string[] | Permissions array |

### Responses

| Code | Description                |
| ---- | -------------------------- |
| 200  | Updated subuser for server |

### `DELETE /api/client/servers/:serverId/users/:userId`

Deletes a specific subuser associated with a server.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | Subuser deleted from server |

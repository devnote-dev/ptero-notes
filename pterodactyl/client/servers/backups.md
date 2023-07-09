### `GET /api/client/servers/:serverId/backups`

Retrieves a paginated list of backups for a given server.

### Response

| Code | Description        |
| ---- | ------------------ |
| 200  | Request successful |

### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "object": "backup",
      "attributes": {
        "uuid": "123e4567-e89b-12d3-a456-426614174000",
        "is_successful": true,
        "is_locked": false,
        "name": "backup-20210611",
        "ignored_files": [],
        "checksum": null,
        "bytes": 102400,
        "created_at": "2023-06-11T12:34:56Z",
        "completed_at": "2023-06-11T13:45:00Z"
      }
    }
  ],
  "meta": {
    "pagination": {
      "total": 2,
      "count": 2,
      "per_page": 20,
      "current_page": 1,
      "total_pages": 1,
      "links": {}
    }
  }
}
```

### `POST /api/client/servers/:serverId/backups`

Creates a new backup for a server.

### Body

| Name      | Visibility | Type    | Description                                  |
| --------- | ---------- | ------- | -------------------------------------------- |
| name      | Required   | string  | The name of the backup.                      |
| ignored   | Optional   | string  | A list of ignored files separated by commas. |
| is_locked | Optional   | boolean | Indicates if the backup should be locked.    |

### Response

| Code | Description        |
| ---- | ------------------ |
| 200  | Request successful |

### `GET /api/client/servers/:serverId/backups/:backupId`

Retrieves information about a specific backup.

### Response

| Code | Description        |
| ---- | ------------------ |
| 200  | Request successful |

### Example Response

```json
{
  "object": "backup",
  "attributes": {
    "uuid": "123e4567-e89b-12d3-a456-426614174000",
    "is_successful": true,
    "is_locked": false,
    "name": "backup-20210611",
    "ignored_files": [],
    "checksum": null,
    "bytes": 102400,
    "created_at": "2023-06-11T12:34:56Z",
    "completed_at": "2023-06-11T13:45:00Z"
  }
}
```

### `GET /api/client/servers/:serverId/backups/:backupId/download`

Downloads server backups. For local daemon files, the backup will be streamed through the Panel. For AWS S3 files, a signed URL will be generated for user redirection.

### Response

| Code | Description              |
| ---- | ------------------------ |
| 200  | Request successful       |
| 400  | Unknown disk driver type |

### Example Response

```json
{
  "object": "signed_url",
  "attributes": {
    "url": "https://example.com/backup.zip"
  }
}
```

### `POST /api/client/servers/:serverId/backups/:backupId/lock`

Toggles the lock status of a specific backup.

### Response

| Code | Description        |
| ---- | ------------------ |
| 200  | Request successful |

### `POST /api/client/servers/:serverId/backups/:backupId/restore`

Restores a specific backup.

### Body

| Name     | Visibility | Type    | Description                                            |
| -------- | ---------- | ------- | ------------------------------------------------------ |
| truncate | Optional   | boolean | Indicates if files should be deleted before restoring. |

### Response

| Code | Description                    |
| ---- | ------------------------------ |
| 204  | Request successful             |
| 400  | This backup cannot be restored |

### `DELETE /api/client/servers/:serverId/backups/:backupId`

Deletes a backup from the panel as well as the remote source where it is currently
being stored.

### Response

| Code | Description        |
| ---- | ------------------ |
| 204  | Request successful |

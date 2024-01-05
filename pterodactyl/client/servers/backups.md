## Contents

- [Get Server Backups](#get-server-backups)
- [Get Server Backup](#get-server-backup)
- [Get Server Backup Download](#get-server-backup-download)
- [Create Server Backup](#create-server-backup)
- [Lock Server Backup](#create-server-backup)
- [Restore Server Backup](#restore-server-backup)
- [Delete Server Backup](#delete-server-backup)

---

## Get Server Backups

### `GET /api/client/servers/:server_id/backups`

Returns a list of backups for a given server.

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

## Get Server Backup

### `GET /api/client/servers/:server_id/backups/:id`

Gets information about the specified backup.

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

## Get Server Backup Download

### `GET /api/client/servers/:server_id/backups/:id/download`

Generates a one-time token with a link that can be used to download the specified backup.

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

## Create Server Backup

### `POST /api/client/servers/:server_id/backups`

Creates a new backup for a server.

### Body

| Name      | Visibility | Type    | Description                                  |
| --------- | ---------- | ------- | -------------------------------------------- |
| name      | required   | string  | The name of the backup.                      |
| ignored   | optional   | string  | A list of ignored files separated by commas. |
| is_locked | optional   | boolean | Indicates if the backup should be locked.    |

### Response

| Code | Description        |
| ---- | ------------------ |
| 200  | Request successful |

## Lock Server Backup

### `POST /api/client/servers/:server_id/backups/:id/lock`

Toggles the lock status of the specified backup.

### Response

| Code | Description        |
| ---- | ------------------ |
| 200  | Request successful |

## Restore Server Backup

### `POST /api/client/servers/:server_id/backups/:id/restore`

Restores the specified backup.

### Body

| Name     | Visibility | Type    | Description                                            |
| -------- | ---------- | ------- | ------------------------------------------------------ |
| truncate | optional   | boolean | Indicates if files should be deleted before restoring. |

### Response

| Code | Description                    |
| ---- | ------------------------------ |
| 204  | Request successful             |
| 400  | This backup cannot be restored |

## Delete Server Backup

### `DELETE /api/client/servers/:server_id/backups/:id`

Deletes a backup from the panel as well as the remote source where it is currently
being stored.

### Response

| Code | Description        |
| ---- | ------------------ |
| 204  | Request successful |

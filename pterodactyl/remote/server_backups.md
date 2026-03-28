## Contents

- [Get Remote Server Backups](#get-remote-server-backups)
- [Update Remote Server Backup](#update-remote-server-backup)
- [Restore Remote Server Backup](#restore-remote-server-backup)

---

## Get Remote Server Backups

### `GET /api/remote/backups/:backup`

Returns the required presigned urls to upload a backup to S3 cloud storage.

### Parameters

| Name | Visibility | Type   | Description           |
| ---- | ---------- | ------ | --------------------- |
| size | required   | number | The backup file size. |

### Responses

| Code | Description                                                    |
| ---- | -------------------------------------------------------------- |
| 200  | The response was successful.                                   |
| 400  | The configured backup adapter is not an S3 compatible adapter. |
| 404  | The backup was not found.                                      |
| 409  | The backup is already in completed state.                      |

### Example Response

```json
{
  "parts": [
    "https://example.com/s3_url_here"    
  ],
  "part_size": 1234
}
```

### Sources

- [BackupRemoteUploadController.php#L33](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/Backups/BackupRemoteUploadController.php#L33)

## Update Remote Server Backup

### `POST /api/remote/backups/:backup`

Handles updating the state of a backup.

### Body

| Name                | Visibility                  | Type    | Description                                                 |
| ------------------- | --------------------------- | ------- | ----------------------------------------------------------- |
| successful          | required                    | boolean | The success state of the backup.                            |
| checksum            | required if success is true | string  | The checksum.                                               |
| checksum_type       | required if success is true | string  | The checksum type.                                          |
| size                | required if success is true | number  | The size of the backup.                                     |
| parts               | optional                    | array   | An array containing the etag and part number for each part. |
| parts[].etag        | required                    | string  | The entity tag of an upload part. (for S3)                  |
| parts[].part_number | required                    | number  | The part number of an upload part. (for S3)                 |

### Example Body

```json
{
  "checksum": "a0b124c3def45g67890h12i3j4567k8l9mn01234",
  "checksum_type": "sha1",
  "size": 1234,
  "successful": true,
  "parts": [
    {
      "etag": "\"fad65ead865d78b768d313644d411c16\"",
      "part_number": 1
    }
  ]
}
```

> [!TIP]
> The `parts` field can also be defined as an array of objects with the fields `etag` (string) and and `part_number` (number).

### Responses

| Code | Description                               |
| ---- | ----------------------------------------- |
| 204  | The request was successful.               |
| 400  | The backup is already in completed state. |
| 404  | The backup was not found.                 |

### Sources

- [BackupStatusController.php#L31](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/Backups/BackupStatusController.php#L31)

## Restore Remote Server Backup

### `POST /api/remote/backups/:backup/restore`

Handles toggling the restoration status of a server.

### Body

| Name       | Visibility | Type    | Description                                  |
| ---------- | ---------- | ------- | -------------------------------------------- |
| successful | required   | boolean | The success state of the backup restoration. |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |
| 404  | The backup was not found.   |

### Sources

- [BackupStatusController.php#L78](https://github.com/pterodactyl/panel/blob/43f7c106172a68f9d81c84af34735373dc900395/app/Http/Controllers/Api/Remote/Backups/BackupStatusController.php#L78)

### `GET /api/remote/backups/:backup`

Returns the required presigned urls to upload a backup to S3 cloud storage.

### Parameters

| Name      | Visibility | Description                        |
| --------- | ---------- | ---------------------------------- |
| size      | optional   | The amount of backup URLs to give. |

### Responses

| Code | Description                                                    |
| ---- | -------------------------------------------------------------- |
| 200  | The response was successful.                                   |
| 400  | The configured backup adapter is not an S3 compatible adapter. |
| 404  | The backup was not found.                                      |
| 409  | The backup is already in completed state.                      |

### Response examples

WIP. Add example data for 'parts'. (note: the response example below was not tested, and manually written based on the panel code.)

```json
{
  "parts": [],
  "part_size": 5368709120 
}
```

Sources

- [app/Http/Controllers/Api/Remote/Backups/BackupRemoteUpl2oadController.php#L33](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Backups/BackupRemoteUploadController.php#L33)

---

### `POST /api/remote/backups/:backup`

Handles updating the state of a backup.

### Body

| Name  | Visibility | Type   | Description                                                                                            |
| ----- | ---------- | ------ | ------------------------------------------------------------------------------------------------------ |
| data  | required   | object | An object containing the checksum, checksum type, backup size, success state, and parts of the backup. |

### Example Body

```json
{
  "data": {
    "checksum": "a0b124c3def45g67890h12i3j4567k8l9mn01234",
    "checksum_type": "sha1",
    "size": 1234,
    "successful": true,
    "parts": [
      {
        "etag": string,
        "part_number": number,
      }
    ]
  }
}
```

Note: `parts` can also be defined as `null`.

### Responses

| Code | Description                               |
| ---- | ----------------------------------------- |
| 202  | The response was successful.              |
| 204  | No content.                               |
| 400  | The backup is already in completed state. |
| 404  | The backup was not found.                 |

### Response example

WIP. Is there even any?

Sources

- [app/Http/Controllers/Api/Remote/Backups/BackupStatusController.php#L31](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Backups/BackupStatusController.php#L31)

---

### `POST /api/remote/backups/:backup/restore`

Handles toggling the restoration status of a server.

### Body

| Name       | Visibility | Type    | Description                                  |
| ---------- | ---------- | ------- | -------------------------------------------- |
| successful | required   | boolean | The success state of the backup restoration. |

### Responses

| Code | Description                  |
| ---- | ---------------------------- |
| 204  | The response was successful. |
| 404  | The backup was not found.    |

Sources

- [app/Http/Controllers/Api/Remote/Backups/BackupStatusController.php#L78](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Backups/BackupStatusController.php#L78)

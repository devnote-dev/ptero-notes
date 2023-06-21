### `GET /api/client/servers/:serverId/files/list`

Returns a list of files in a given directory. If the directory is not provided, it defaults to the home directory `/home/container`.

### Body

| Name      | Visibility | Type   | Description                      |
| --------- | ---------- | ------ | -------------------------------- |
| directory | Optional   | string | The directory to list files from |

### Responses

| Code | Description                    |
| ---- | ------------------------------ |
| 200  | List of files in the directory |

### Example Response

```json
{
  "data": [
    {
      "object": "file_object",
      "attributes": {
        "name": "example_file.txt",
        "mode": "755",
        "mode_bits": "rwxr-xr-x",
        "size": 1024,
        "is_file": true,
        "is_symlink": false,
        "mimetype": "text/plain",
        "created_at": "2023-06-10T08:30:00Z",
        "modified_at": "2023-06-10T10:15:00Z"
      }
    }
  ]
}
```

### `GET /api/client/servers/:serverId/files/contents`

Returns the contents of a specified file for the user.

> **Note**
> The content type of the response will always be in the `text/plain` format.

### Body

| Name | Visibility | Type   | Description      |
| ---- | ---------- | ------ | ---------------- |
| file | Required   | string | Path to the file |

### Responses

| Code | Description  |
| ---- | ------------ |
| 200  | File content |

### `GET /api/client/servers/:serverId/files/download`

Generates a one-time token with a link that the user can use to download a given file.

### Body

| Name | Visibility | Type   | Description      |
| ---- | ---------- | ------ | ---------------- |
| file | Required   | string | Path to the file |

### Responses

| Code | Description                  |
| ---- | ---------------------------- |
| 200  | Signed URL for file download |

### Example Response

```json
{
  "object": "signed_url",
  "attributes": {
    "url": "https://pterodactyl.file.properties:3000/download/file?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmaWxlX3BhdGgiOiJkZXNrdG9wL3Rlc3QucGRmIiwic2VydmVyX3V1aWQiOiJ1c2VyLWlkIn0.u6Ln6vZDP1Z8fxSoZ7i7J9RTx69R5_Hn6mIF5xGm4O8"
  }
}
```

### `PUT /api/client/servers/:serverId/files/rename`

Renames one or more files on the remote machine.

### Body

| Name    | Visibility | Type          | Description                |
| ------- | ---------- | ------------- | -------------------------- |
| root    | Required   | string        | Root directory             |
| files[] | Required   | array[object] | Files to rename (multiple) |

### Example Body

```json
{
  "root": "/",
  "files": [
    {
      "from": "bungeecord.jar",
      "to": "server.jar"
    }
  ]
}
```

### Responses

| Code | Description  |
| ---- | ------------ |
| 204  | File renamed |

### `POST /api/client/servers/:serverId/files/copy`

Copies a file on the server.

### Body

| Name     | Visibility | Type   | Description          |
| -------- | ---------- | ------ | -------------------- |
| location | Required   | string | Location of the file |

### Responses

| Code | Description |
| ---- | ----------- |
| 204  | File copied |

### `POST /api/client/servers/:serverId/files/write`

Writes the contents of the specified file to the server.

### Request Parameters

| Name | Type   | Description                          |
| ---- | ------ | ------------------------------------ |
| file | string | URL encoded path to the desired file |

### Body

| Name | Visibility | Type       | Description                       |
| ---- | ---------- | ---------- | --------------------------------- |
| -    | Required   | text/plain | Content of the file to be written |

**Note**

> The request body contains the content that will be written to the file. It can be provided in any format, although the `text/plain` format is commonly used.

### Example Body

```
  This is the content of a file with a .txt extension.
```

### Responses

| Code | Description  |
| ---- | ------------ |
| 204  | File written |

### `POST /api/client/servers/:serverId/files/compress`

Compresses files on the server.

### Body

| Name    | Visibility | Type          | Description                    |
| ------- | ---------- | ------------- | ------------------------------ |
| root    | Required   | string        | Root directory for compression |
| files[] | Required   | array[string] | Files to compress (multiple)   |

### Example Body

```json
{
  "root": "/",
  "files": [
    "bungeecord.jar",
    "config.yml"
  ]
  ]
}
```

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | Compressed file information |

### `POST /api/client/servers/:serverId/files/decompress`

Decompresses a file on the server.

### Body

| Name | Visibility | Type   | Description                    |
| ---- | ---------- | ------ | ------------------------------ |
| root | Required   | string | Root directory for compression |
| file | Required   | string | The file to decompress         |


### Responses

| Code | Description        |
| ---- | ------------------ |
| 204  | Files decompressed |

### `POST /api/client/servers/:serverId/files/delete`

Deletes files or folders on the server.

### Body

| Name    | Visibility | Type          | Description                |
| ------- | ---------- | ------------- | -------------------------- |
| root    | Required   | string        | Root directory             |
| files[] | Required   | array[string] | Files to delete (multiple) |


### Responses

| Code | Description   |
| ---- | ------------- |
| 204  | Files deleted |

### `POST /api/client/servers/:serverId/files/create-folder`

Creates a new folder on the server. If the root directory is not provided it defaults to `/`.

### Body

| Name | Visibility | Type   | Description                   |
| ---- | ---------- | ------ | ----------------------------- |
| name | Required   | string | Name of the folder            |
| root | Optional   | string | Root directory (default: '/') |

### Responses

| Code | Description    |
| ---- | -------------- |
| 204  | Folder created |

### `POST /api/client/servers/:serverId/files/chmod`

Updates file permissions for file(s) on the server.

### Body

| Name  | Visibility | Type          | Description                 |
| ----- | ---------- | ------------- | --------------------------- |
| root  | Required   | string        | Root directory              |
| files | Required   | array[string] | Files to change permissions |

### Responses

| Code | Description              |
| ---- | ------------------------ |
| 204  | File permissions updated |

---

### `POST /api/client/servers/:serverId/files/pull`

Requests that a file be downloaded from a remote location by Wings.

### Body

| Name       | Visibility | Type   | Description                 |
| ---------- | ---------- | ------ | --------------------------- |
| url        | Required   | string | URL of the file to download |
| directory  | Required   | string | Destination directory       |
| filename   | Optional   | string | Filename                    |
| use_header | Optional   | bool   | Use header                  |
| foreground | Optional   | bool   | Foreground                  |

### Responses

| Code | Description |
| ---- | ----------- |
| 204  | File pulled |

### `GET /api/client/servers/:serverId/files/upload`

Returns a signed URL where files can be uploaded to.

### Responses

| Code | Description            |
| ---- | ---------------------- |
| 200  | Signed URL information |

### Example Response

```json
{
  "object": "signed_url",
  "attributes": {
    "url": "https://upload.example.com/upload/file?token={TOKEN}"
  }
}
```

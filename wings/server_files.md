### `GET /api/servers/:uuid/files/contents`

Returns the file contents of a specified file in the server's volume. The `Content-Length` header will be set to the size of the file according to its stat information, and the `X-Mime-Type` header will reflect the file's MIME type. If the `download` query parameter is included (e.g. `?download=true`), the `Content-Disposition` header will be set, and the `Content-Type` header will be set to "application/octet-stream".

### Parameters

| Name     | Visibility | Description                                                       |
| -------- | ---------- | ----------------------------------------------------------------- |
| download | optional   | Whether the file content should be returned as a download stream. |
| file     | required   | The URL-encoded file path.                                        |

### Responses

| Code | Description                        |
| ---- | ---------------------------------- |
| 200  | The request was successful.        |
| 400  | The file type could not be opened. |
| 404  | The file was not found.            |

Sources:

- [router/router_server_files.go#L31](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L31)

### `GET /api/servers/:uuid/files/list-directory`

Returns a list of file objects in the directory of the server's volume.

### Parameters

| Name      | Visibility | Description                     |
| --------- | ---------- | ------------------------------- |
| directory | required   | The URL-encoded directory path. |

### Responses

| Code | Description                      |
| ---- | -------------------------------- |
| 200  | The request was successful.      |
| 400  | The directory could not be read. |
| 404  | The directory was not found.     |

Sources:

- [router/router_server_files.go#L78](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L78)

### `PUT /api/servers/:uuid/files/rename`

Renames one or more files in the server's volume.

### Body

| Name  | Visibility | Type   | Description                                  |
| ----- | ---------- | ------ | -------------------------------------------- |
| files | required   | object | An object containing the from-to name pairs. |
| root  | required   | string | The root directory of the files.             |

### Example Body

```json
{
  "root": "/",
  "files": [
    {
      "from": "bungee.jar",
      "to": "bungeecord.jar"
    }
  ]
}
```

### Responses

| Code | Description                                                                      |
| ---- | -------------------------------------------------------------------------------- |
| 204  | The request was accepted.                                                        |
| 400  | The request body could not be parsed, or one of the destinations already exists. |
| 422  | The from-to name pairs in the request was empty.                                 |

Sources:

- [router/router_server_files.go#L94](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L94)

### `POST /api/servers/:uuid/files/copy`

Creates a copy of the file at the given location in the server volume.

### Body

| Field    | Visibility | Type   | Description                  |
| -------- | ---------- | ------ | ---------------------------- |
| location | required   | string | The file path (not encoded). |

### Responses

| Code | Description                                                                                               |
| ---- | --------------------------------------------------------------------------------------------------------- |
| 204  | The request was accepted.                                                                                 |
| 400  | The request body could not be parsed, the file is ignored by the system, or the file could not be copied. |

Sources:

- [router/router_server_files.go#L163](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L163)

### `POST /api/servers/:uuid/files/write`

Writes the given file content into a file in the server's volume. If the file does not exist, it is created instead. Unlike other panel and Wings endpoints, this endpoint takes a plain text body rather than a JSON string body, and should be used with the appropriate `Content-Type` header: "text/plain". No additional metadata is used by this endpoint, so if you want the file's MIME type and other attributes to be used, you should request the [upload file](./public.md#get-uploadfile) endpoint with the full file.

### Parameters

| Name | Visibility | Description                |
| ---- | ---------- | -------------------------- |
| file | required   | The URL-encoded file path. |

### Responses

| Code | Description                                                                                         |
| ---- | --------------------------------------------------------------------------------------------------- |
| 204  | The request was accepted.                                                                           |
| 400  | The file path is ignored, or the file path conflicts with an existing directory with the same name. |

Sources:

- [router/router_server_files.go#L232](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L232)

### `POST /api/servers/:uuid/files/create-directory`

Creates a directory at a given path in the server's volume.

### Body

| Field | Visibility | Type   | Description                                            |
| ----- | ---------- | ------ | ------------------------------------------------------ |
| name  | required   | string | The name of the directory.                             |
| path  | required   | string | The root path that the directory should be created in. |

### Responses

| Code | Description                                                        |
| ---- | ------------------------------------------------------------------ |
| 204  | The request was accepted.                                          |
| 400  | The request body could not be parsed, or the root path is invalid. |

Sources:

- [router/router_server_files.go#L363](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L363)

### `POST /api/servers/:uuid/files/delete`

Deletes one or more files from the server's volume. Note that if one of the files fail to be deleted, the request is aborted.

### Body

| Field | Visibility | Type            | Description                      |
| ----- | ---------- | --------------- | -------------------------------- |
| files | required   | array of string | A list of file names.            |
| root  | required   | string          | The root directory of the files. |

### Responses

| Code | Description                                   |
| ---- | --------------------------------------------- |
| 204  | The request was accepted.                     |
| 400  | The request body could not be parsed.         |
| 422  | The files list in the request body was empty. |

Sources:

- [router/router_server_files.go#L187](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L187)

### `POST /api/servers/:uuid/files/compress`

Compresses one or more files into a single archive in the server's volume, and returned the file object of the new archive.

### Body

| Field | Visibility | Type            | Description                      |
| ----- | ---------- | --------------- | -------------------------------- |
| files | required   | array of string | A list of file names.            |
| root  | required   | string          | The root directory of the files. |

### Responses

| Code | Description                                   |
| ---- | --------------------------------------------- |
| 200  | The request was successful.                   |
| 400  | The request body could not be parsed.         |
| 422  | The files list in the request body was empty. |

Sources:

- [router/router_server_files.go#L390](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L390)

### `POST /api/servers/:uuid/files/decompress`

Decompresses an archive file into the server's volume.

### Body

| Field | Visibility | Type   | Description                     |
| ----- | ---------- | ------ | ------------------------------- |
| file  | required   | string | The name of the archive file.   |
| root  | required   | string | The root directory of the file. |

### Responses

| Code | Description                                                                                                                   |
| ---- | ----------------------------------------------------------------------------------------------------------------------------- |
| 204  | The request was accepted.                                                                                                     |
| 400  | The request body could not be parsed, the archive could not be processed, or the file is currently in use by another process. |

Sources:

- [router/router_server_files.go#L431](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L431)

### `POST /api/servers/:uuid/files/chmod`

Changes the permissions of a file in the server's volume.

### Body

| Field | Visibility | Type   | Description                      |
| ----- | ---------- | ------ | -------------------------------- |
| files | required   | array  | A list of file-mode pairs.       |
| root  | required   | string | The root directory of the files. |

### Example Body

```json
{
  "root": "/",
  "files": [
    {
      "file": "bungeecord.jar",
      "mode": 493
    }
  ]
}
```

### Responses

| Code | Description                                                         |
| ---- | ------------------------------------------------------------------- |
| 204  | The request was accepted.                                           |
| 400  | The request body could not be parsed, or a file's mode was invalid. |
| 422  | The file-mode pairs in the request body was empty.                  |

Sources:

- [router/router_server_files.go#L479](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L479)

### `GET /api/servers/:uuid/files/pull`

Returns an object containing a list of download objects for in-progress downloads.

Sources:

- [router/router_server_files.go#L261](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L261)

### `POST /api/servers/:uuid/files/pull`

Pulls a file from a remote location and downloads it into the server's volume. All servers are limited to 3 simultaneous downloads at a time, if a server reaches this limit, the request is cancelled immediately. Note that synchronous downloads (ones using the `foreground` field in the request) will keep the request connection open until the download is complete or fails. If the `foreground` field is not specified, the endpoint will return the download's identifier and will continue the download in the background.

### Body

> **Warning** The `directory` field in the request body is deprecated, use the `root` field instead.

| Field      | Visibility | Type    | Description                                             |
| ---------- | ---------- | ------- | ------------------------------------------------------- |
| url        | required   | string  | The URL of the file to download.                        |
| directory  | optional   | string  | The root directory to download the file into.           |
| file_name  | optional   | string  | The name to save the file as.                           |
| foreground | optional   | boolean | Whether the request should be downloaded synchronously. |
| root       | required   | string  | The root path to download the file to.                  |
| use_header | optional   | boolean | Use the remote file header for file information.        |

### Responses

| Code | Description                                                                                                         |
| ---- | ------------------------------------------------------------------------------------------------------------------- |
| 200  | The request was successful.                                                                                         |
| 204  | The request was accepted.                                                                                           |
| 400  | The request body could not be parsed, the remote URL could not be parsed, or the server reached the download limit. |

Sources:

- [router/router_server_files.go#L269](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L269)
- [downloader/downloader.go](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/downloader/downloader.go)

### `DELETE /api/servers/:uuid/files/pull/:id`

Deletes an in-progress remote file download.

Sources:

- [router/router_server_files.go#L354](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L354)

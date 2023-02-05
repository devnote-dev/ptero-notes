> **Note** All of the endpoints listed in this document use custom authorization methods which are specified under each endpoint.

### `GET /download/backup`

Returns a multipart form-data response containing the volume files for a server backup. The `token` query parameter is required for this endpoint. It is a JWT token comprised of the following claims:

- `server_uuid`: the UUID of the server in the panel
- `backup_uuid`: the UUID of the backup to download
- `unique_id`: a randomly generated string

Sources:

- [DownloadLinkService.php](https://github.com/pterodactyl/panel/blob/release/v1.11.3/app/Services/Backups/DownloadLinkService.php)
- [tokens/backup.go](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/tokens/backup.go)

### `GET /download/file`

Returns a multipart form-data response containing a file from a server volume. The `token` query parameter is required for this endpoint. It is a JWT token comprised of the following claims:

- `file_path`: the URL-decoded file path
- `server_uuid`: the UUID of the server in the panel
- `unique_id`: a randomly generated string

Sources:

- [FileController.php#L77](https://github.com/pterodactyl/panel/blob/release/v1.11.3/app/Http/Controllers/Api/Client/Servers/FileController.php#L77)
- [tokens/file.go](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/tokens/file.go)

### `GET /upload/file`

Uploads the given file(s) to a server matching the identifiers set in the required `token` query parameter. It is a JWT token comprised of the following claims:

- `server_uuid`: the UUID of the server in the panel
- `user_uuid`: the UUID of the user in the panel
- `unique_id`: a randomly generated string

### Parameters

| Name      | Visibility | Description                                                    |
| --------- | ---------- | -------------------------------------------------------------- |
| directory | optional   | The directory path to upload the file(s) to (defaults to "/"). |
| token     | required   | The JWT token containing the required claims.                  |

Unlike other panel and Wings endpoints, this endpoint takes a multipart form-data body rather than a JSON string body, and should be used with the appropriate Content-Type header: "multipart/form-data" (plus additional multipart metadata).

The form-data files must be encoded under the "**files**" header, NOT "**file**". Each file must include:

- the file name; and
- the file contents

You can optionally include:

- the file type
- the file size

### Responses

| Code | Description                                                                                         |
| ---- | --------------------------------------------------------------------------------------------------- |
| 200  | The request was successful.                                                                         |
| 400  | The form-data could not be extracted from the request, or there were no files found in the request. |
| 404  | The server was not found.                                                                           |

Sources:

- [FileUploadController.php#L40](https://github.com/pterodactyl/panel/blob/release/v1.11.3/app/Http/Controllers/Api/Client/Servers/FileUploadController.php#L40)
- [router_server_files.go#L543](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_server_files.go#L543)
- [tokens/upload.go](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/tokens/upload.go)

### `GET /api/servers/:uuid/ws`

Initializes a websocket connection to the specified server (see [websocket](/wings/websocket.md) for more information).

### `POST /api/transfers`

> **Warning** this endpoint is only meant to be used by other Wings instances, and can be potentially damaging. The documentation for this endpoint is for learning purposes only.

Handles the incoming transfer request from another Wings instance (the source node). In summary, the process goes as follows:

1. The request is authenticated using a bearer token in the `Authorization` header – this is a standard JWT token with no additional claims
2. The file(s) are extracted from the request form-data and written into the destination node's volumes
3. The checksum is computed and compared with the one received from the source node

Sources:

- [router_transfer.go](https://github.com/pterodactyl/wings/blob/release/v1.11.2/router/router_transfer.go)

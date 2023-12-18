## Contents

- [Rename Server](#rename-server)
- [Reinstall Server](#reinstall-server)
- [Update Server Docker Image](#update-server-docker-image)

---

## Rename Server

### `POST /api/client/servers/:id/settings/rename`

Renames a server.

### Body

| Name        | Visibility | Type   | Description                         |
| ----------- | ---------- | ------ | ----------------------------------- |
| name        | required   | string | The new name for the server.        |
| description | optional   | string | The new description for the server. |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 204  | The request was successful.          |
| 422  | One or more validation rules failed. |

### Sources

- [SettingsController.php#L35](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Controllers/Api/Client/Servers/SettingsController.php#L35)
- [RenameServerRequest.php#L10](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Requests/Api/Client/Servers/Settings/RenameServerRequest.php#L10)

## Reinstall Server

### `POST /api/client/servers/:id/settings/reinstall`

Reinstalls the server on the daemon.

### Responses

| Code | Description               |
| ---- | ------------------------- |
| 202  | The request was accepted. |

### Sources

- [SettingsController.php#L64](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Controllers/Api/Client/Servers/SettingsController.php#L64)

## Update Server Docker Image

### `PUT /api/client/servers/:id/settings/docker-image`

Changes the Docker image in use by the server.

### Body

| Name         | Visibility | Type   | Description                          |
| ------------ | ---------- | ------ | ------------------------------------ |
| docker_image | required   | string | The new Docker image for the server. |

### Responses

| Code | Description                     |
| ---- | ------------------------------- |
| 204  | The request was successful.     |
| 400  | The provided image was invalid. |

### Sources

- [SettingsController.php#L78](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Controllers/Api/Client/Servers/SettingsController.php#L78)
- [SetDockerImageRequest.php#L12](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Http/Requests/Api/Client/Servers/Settings/SetDockerImageRequest.php#L12)

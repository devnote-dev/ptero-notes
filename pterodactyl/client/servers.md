### `GET /servers/:identifier`
Returns a server by its `identifier` (string). The `allocations` and `variables` include parameters are returned by default.

### Parameters
Name | Supported | Allowed Values
-----|-----------|---------------
filter | ❌ |
include | ✅ | allocations, eggs, subusers, variables
sort | ❌ |
page | ✅ | Any number
per_page | ✅ | Any number

### `GET /servers/:identifier/websocket`
Returns the websocket authentication details for a server. This includes the socket URL and JWT authentication token. See the [wings/websockets](../../wings/websocket.md) page for more information.

### `GET /servers/:identifier/resources`
Returns the current resource usage for a server, including the status and uptime.

### `GET /servers/:identifier/activity`
Returns a list of activity objects recorded on the server.

### `POST /servers/:identifier/command`
Sends a command to the server console.

### Body
Key | Required | Type | Description
----|----------|------|------------
command | ✅ | `string` | The command to send

### Responses
Code | Description
-----|------------
204  | The request was accepted
409  | The server is unavailable (installing/transferring/restoring backup)

### `POST /servers/:identifier/power`
Sends a signal request to change the power state of the server. Accepted power states are "start", "stop", "restart", and "kill".

### Body
Code | Description
-----|------------
204  | The request was accepted
400  | An invalid power state was sent
409  | The server is unavailable (installing/transferring/restoring backup)

### `GET /servers/:identifier/files/list`
Returns a list of file objects in a specified directory or the root directory (`/home/container`).

### Parameters
Name | Supported | Allowed Values
-----|-----------|---------------
filter | ❌ |
include | ❌ |
sort | ❌ |
page | ✅ | Any number
per-page | ✅ | Any number
directory | ✅ | Directory path

### `GET /servers/:identifier/files/contents`
Returns the contents of a file specified by the `?file=` parameter (e.g. `?file=%2Fconfig.yml`). The file path does not need to be URL-encoded but it is recommended to do so. The response content type will always be "text/plain", however, the actual MIME type of the file is specified in the file object (see [list files](#get-serversidentifierfileslist)).

### `POST /servers/:identifier/files/rename`
Renames a list of files specified in the request body. Returns a 204 status on success.

### Body
Key | Required | Type | Description
----|----------|------|------------
root | ✅ | `string` | The root directory of the files
files | ✅ | `object[]` | An array of from-to objects (see below)
from | ✅ | `string` | The original name of the file
to | ✅ | `string` | The new name of the file

### `POST /servers/:identifier/files/copy`
Copies a file to a new location specified in the request body. Returns a 204 status on success.

### Body
Key | Required | Type | Description
----|----------|------|------------
location | ✅ | `string` | The location of the file to copy

### `POST /servers/:identifier/files/write`
Writes the request body contents to the location specified by the `?file=` parameter. If the file path does not exist it will be created, otherwise the existing file is overwritten. An empty request body can be sent which will cause Wings to create an empty file at the file path. The `Content-Type` header MUST be set to "text/plain" for the request to be accepted. Returns a 204 status on success.

### `POST /servers/:identifier/files/compress`
Compresses a list of files specified in the request body into a single archive (using `.tar.gz` format). Returns a 204 status on success.

### Body
Key | Required | Type | Description
----|----------|------|------------
root | ✅ | `string` | The root directory of the files
files | ✅ | `string[]` | The names of the files

### `POST /servers/:identifier/files/decompress`
Decompresses an archive file specified in the request body, restoring all files and directories in that location. This only works with archives in the `.tar.gz` format. Returns a 204 status on success.

### Body
Key | Required | Type | Description
----|----------|------|------------
root | ✅ | `string` | The root directory of the file
file | ✅ | `string` | The name of the file

# Wings API - JWT specifications

This page lists the JWT specifications for Wings API.

### All Wings API routes that use JWTS

`GET /download/backup`

- Include `backup_uuid` and `server_uuid` in the JWT.

`GET /download/file`

- Include `server_uuid` and `file_path` in the JWT.

`POST /api/servers/:uuid/transfer`

- Include `sub` as the server UUID in the JWT.
- Token expires in 15 minutes.

`POST /upload/file`

- Include `server_uuid` in the JWT.
- Token is in the parameters, even though it's a POST request.

`WS /api/servers/:uuid/ws`

- Include `server_uuid` and `permissions` in the JWT.
- `permissions` has be an array of strings, which are [permissions](https://github.com/pterodactyl/panel/blob/develop/app/Models/Permission.php).
- After connecting to the WebSocket, you have to send `{ "event": "auth", "args": ["token here"] }`.
- Also, tokens expires in 20 minutes.

### Notes

- Tokens typically require in 5 minutes with few exceptions.
- Most tokens require `server_uuid` with the exception of `POST /api/servers/:uuid/transfer`, which uses `sub` instead.
- JWTs use the `HS256` algorithm.
- All JWTs require these values: **Note: Make sure to include the other required values based on the route you're making a JWT for.**

```json
{
  "iss": "The value for 'remote' in config.json. This is the panel's url.",
  "aud": [ "The FQDN value, which is the Wings url." ],
  "unique_id": "A random value. This can be anything.",
  "jti": "MD5 encryption of either the value of 'server_uuid' (in most cases) or 'sub' (for POST /api/servers/:uuid/transfer)."
}
```

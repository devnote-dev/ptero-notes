# JWT specifications

This page lists the JWT specifications for Wings API.

## Signing the token

Make sure to sign the token using the `token` value from the node configuration.

## Header format

- Tokens typically expire in 5 minutes with few exceptions.
- JWTs use the `HS256` algorithm.

## Payload format

**Make sure to include the other required values based on the route the JWT is for.**

| Field      | Type     | Description                                                                                                            |
| ---------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| iss        | string   | The value for `remote` in config.yml. This is the panel's url.                                                        |
| aud        | string[] | An array containing a value of the the FQDN value, which is the Wings url.                                             |
| unique_id  | string   | A random value. This can be anything.                                                                                  |
| jti        | string   | MD5 encryption of either the value of `server_uuid` (in most cases) or `sub` (for `POST /api/servers/:uuid/transfer`). |

Don't forget that most tokens require `server_uuid` in the JWT as well with the exception of `POST /api/servers/:uuid/transfer`, which uses `sub` instead.

### Example JWT payload

This JWT comes from [`GET /download/file`.](https://github.com/devnote-dev/ptero-notes/blob/8f8c6ae86d6c3445faf68d5e55f60953daac4bb0/wings/public.md#get-downloadfile)

```eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIsImp0aSI6IjFhMjM0NTY3ODliMGNkZTEyM2Y0NTZnNzhoOTAxMjM0In0.eyJpc3MiOiJodHRwOi8vMTI3LjAuMC4xIiwiYXVkIjpbImh0dHA6Ly8xMjcuMC4wLjE6ODA4MCJdLCJqdGkiOiIxYTIzNDU2Nzg5YjBjZGUxMjNmNDU2Zzc4aDkwMTIzNCIsImlhdCI6MTY4Njc5NzQzNCwibmJmIjoxNjg2Nzk3MTM0LCJleHAiOjE2ODY3OTgzMzQsImZpbGVfcGF0aCI6Ii9zZXJ2ZXIucHJvcGVydGllcyIsInNlcnZlcl91dWlkIjoiMTIzNGE1NjctODliMC0xY2QyLTM0NTYtNzg5MGVmMTIzNDVnIiwidXNlcl91dWlkIjoiMWEyYmMzNGQtNTY3ZS04ZjkwLWcxaGktMjM0ajU2a2w3OG1uIiwidXNlcl9pZCI6MSwidW5pcXVlX2lkIjoiQ3lwZmZMcDB3RTBXdjAwNCJ9.zQkWBDuk05cuKZlmE5mfCdJSCZ4TY48siRFXZYLkpjY
```

**Header**

```json
{
  "typ": "JWT",
  "alg": "HS256",
  "jti": "1a23456789b0cde123f456g78h901234"
}
```

**Payload**

```json
{
  "iss": "http://127.0.0.1",
  "aud": [
    "http://127.0.0.1:8080"
  ],
  "jti": "1a23456789b0cde123f456g78h901234",
  "iat": 1686797434,
  "nbf": 1686797134,
  "exp": 1686798334,
  "file_path": "/server.properties",
  "server_uuid": "1234a567-89b0-1cd2-3456-7890ef12345g",
  "user_uuid": "1a2bc34d-567e-8f90-g1hi-234j56kl78mn",
  "user_id": 1,
  "unique_id": "CypffLp0wE0Wv004"
}
```

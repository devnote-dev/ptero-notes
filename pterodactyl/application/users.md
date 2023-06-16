### Example Model

```json
{
  "2fa": false,
  "created_at": "2022-09-15T17:33:34+00:00",
  "email": "example@example.com",
  "external_id": null,
  "first_name": "test",
  "id": 4,
  "language": "en",
  "last_name": "user",
  "root_admin": true,
  "updated_at": "2022-09-15T17:33:35+00:00",
  "username": "test-user",
  "uuid": "4c45016d-0148-4794-89b6-970e0b429b54"
}
```

### `GET /users`

Returns a list of user objects.

### Parameters

| Name     | Supported | Allowed Values                     |
| -------- | --------- | ---------------------------------- |
| filter   | ✅        | email, external_id, username, uuid |
| include  | ✅        | servers                            |
| sort     | ✅        | id, uuid                           |
| page     | ✅        | Any number                         |
| per_page | ✅        | Any number                         |

### `GET /users/:id`

Returns a user by its `id` (number). Supports the above "include" parameter.

### `GET /users/external/:external_id`

Return a user by its `external_id` (string). Supports the above "include" parameter.

### `POST /users`

Creates a user.

### Body

| Key         | Required | Type      | Description                                                                                      |
| ----------- | -------- | --------- | ------------------------------------------------------------------------------------------------ |
| email       | ✅       | `string`  | The account email                                                                                |
| external_id | ❌       | `string`  | An external identifier for the account                                                           |
| first_name  | ✅       | `string`  | The first name for the account                                                                   |
| language    | ❌       | `string`  | The language of the account                                                                      |
| last_name   | ✅       | `string`  | The last name for the account                                                                    |
| password    | ❌       | `string`  | The password for the account. Manual input by the account holder is required if this is not set. |
| root_admin  | ❌       | `boolean` | Whether the account will have administrative access                                              |
| username    | ✅       | `string`  | The account username                                                                             |

### `PATCH /users/:id`

Updates a user account by its `id` (number).

### Body

| Key         | Required | Type      | Description                                         |
| ----------- | -------- | --------- | --------------------------------------------------- |
| email       | ❌       | `string`  | The account email                                   |
| external_id | ❌       | `string`  | The external identifier for the account             |
| first_name  | ❌       | `string`  | The first name for the account                      |
| language    | ❌       | `string`  | The language of the account                         |
| last_name   | ❌       | `string`  | The last name of the account                        |
| password    | ❌       | `string`  | The password for the account                        |
| root_admin  | ❌       | `boolean` | Whether the account will have administrative access |
| username    | ❌       | `string`  | The account username                                |

### `DELETE /users/:id`

Deletes a user account by its `id` (number).

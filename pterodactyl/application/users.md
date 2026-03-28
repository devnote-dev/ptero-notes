## Contents

- [Get Users](#get-users)
- [Get User](#get-user)
- [Get External User](#get-external-user)
- [Create User](#create-user)
- [Update User](#update-user)
- [Delete User](#delete-user)

---

## Get Users

<!-- TODO: terminology clarification in spec -->

### `GET /api/application/users`

Returns a list of user objects.

### Parameters

<!-- TODO: make parameter tables distinct from object tables -->

| Name     | Visibility | Type           | Allowed Values                     |
| -------- | ---------- | -------------- | ---------------------------------- |
| filter   | optional   | \[key]=value   | email, external_id, username, uuid |
| include  | optional   | array\[string] | servers                            |
| sort     | optional   | string         | id, uuid                           |
| page     | optional   | number         | >= 1                               |
| per_page | optional   | number         | >= 1                               |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |

### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "object": "user",
      "attributes": {
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
    }
  ]
}
```

### Sources

- [UserController.php#L36](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Users/UserController.php#L36)

## Get User

### `GET /api/application/users/:id`

Returns a user by its `id` (number).

### Parameters

| Name    | Visibility | Type           | Allowed Values |
| ------- | ---------- | -------------- | -------------- |
| include | optional   | array\[string] | servers        |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The user was not found.     |

### Example Response

```json
{
  "object": "user",
  "attributes": {
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
}
```

### Sources

- [UserController.php#L52](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Users/UserController.php#L52)

## Get External User

### `GET /api/application/users/external/:external_id`

Return a user by its `external_id` (string).

### Parameters

| Name    | Visibility | Type           | Allowed Values |
| ------- | ---------- | -------------- | -------------- |
| include | optional   | array\[string] | servers        |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The user was not found.     |

### Sources

- [ExternalUserController.php#L15](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Users/ExternalUserController.php#L15)

## Create User

### `POST /api/application/users`

Creates a user.

### Body

| Field       | Visibility | Type    | Description                                                                                      |
| ----------- | ---------- | ------- | ------------------------------------------------------------------------------------------------ |
| email       | required   | string  | The account email.                                                                               |
| external_id | optional   | string  | An external identifier for the account.                                                          |
| first_name  | required   | string  | The first name for the account.                                                                  |
| language    | optional   | string  | The language identifier for the account.                                                         |
| last_name   | required   | string  | The last name for the account.                                                                   |
| password    | optional   | string  | The password for the account. Manual input by the account holder is required if this is not set. |
| root_admin  | optional   | boolean | Whether the account will have administrative access.                                             |
| username    | required   | string  | The account username.                                                                            |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 201  | The request was successful.          |
| 422  | One or more validation rules failed. |

### Sources

- [UserController.php#L88](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Users/UserController.php#L88)
- [UserCreationService.php#L32](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Services/Users/UserCreationService.php#L32)

## Update User

### `PATCH /api/application/users/:id`

Updates a user account by its `id` (number).

### Body

| Field       | Visibility | Type    | Description                                          |
| ----------- | ---------- | ------- | ---------------------------------------------------- |
| email       | required   | string  | The account email.                                   |
| external_id | optional   | string  | An external identifier for the account.              |
| first_name  | required   | string  | The first name for the account.                      |
| language    | optional   | string  | The language identifier for the account.             |
| last_name   | required   | string  | The last name for the account.                       |
| password    | optional   | string  | The password for the account.                        |
| root_admin  | optional   | boolean | Whether the account will have administrative access. |
| username    | required   | string  | The account username.                                |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 404  | The user was not found.              |
| 422  | One or more validation rules failed. |

### Sources

- [UserController.php#L70](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Users/UserController.php#L70)
- [UserUpdateService.php#L25](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Services/Users/UserUpdateService.php#L25)

## Delete User

### `DELETE /api/application/users/:id`

Deletes a user account by its `id` (number).

### Responses

| Code | Description                                      |
| ---- | ------------------------------------------------ |
| 200  | The request was successful.                      |
| 400  | There are servers connected to the user account. |
| 404  | The user was not found.                          |

### Sources

- [UserController.php#L108](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Users/UserController.php#L108)
- [UserDeletionService.php#L28](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Services/Users/UserDeletionService.php#L28)

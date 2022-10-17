### Example Model
```json
{
    "created_at": "2022-02-15T06:35:34+00:00",
    "id": 1,
    "long": "london",
    "short": "gb",
    "updated_at": "2022-02-15T06:58:30+00:00"
}
```

### `GET /locations`
Returns a list of location objects.

### Parameters
Name | Supported | Allowed Values
-----|-----------|---------------
filter | ✅ | short, long
include | ✅ | nodes, servers
sort | ✅ | id
page | ✅ | Any number
per_page | ✅ | Any number

### `GET /locations/:id`
Returns a location by its `id` (number). Supports the above "include" parameter.

### `POST /locations`
Creates a location.

### Body
Key | Required | Type | Description
----|----------|-------|------------
long | ❌ | `string` | The location description
short | ✅ | `string` | The location identifier

### `PATCH /locations/:id`
Updates a location by its `id` (number).

### Body
Key | Required | Type | Description
----|----------|-------|------------
long | ❌ | `string` | The location description
short | ❌ | `string` | The location identifier

### `DELETE /locations/:id`
Deletes a location by its `id` (number).

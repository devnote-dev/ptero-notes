## Contents

- [Get Locations](#get-locations)
- [Get Location](#get-location)
- [Create Location](#create-location)
- [Update Location](#update-location)
- [Delete Location](#delete-location)

---

## Get Locations

### `GET /locations`

Returns a list of location objects.

### Parameters

| Name     | Visibility | Type           | Allowed Values |
| -------- | ---------- | -------------- | -------------- |
| filter   | optional   | \[key]=value   | short, long    |
| include  | optional   | array\[string] | nodes, servers |
| sort     | optional   | string         | id             |
| page     | optional   | number         | >= 1           |
| per_page | optional   | number         | >= 1           |

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
      "object": "location",
      "attributes": {
        "created_at": "2022-02-15T06:35:34+00:00",
        "id": 1,
        "long": "london",
        "short": "gb",
        "updated_at": "2022-02-15T06:58:30+00:00"
      }
    }
  ]
}
```

### Sources

- [LocationController.php#L36](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Locations/LocationController.php#L36)

## Get Location

### `GET /locations/:id`

Returns a location by its `id` (number).

### Parameters

| Name    | Visibility | Type           | Allowed Values |
| ------- | ---------- | -------------- | -------------- |
| include | optional   | array\[string] | servers        |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The location was not found. |

### Example Response

```json
{
  "object": "location",
  "attributes": {
    "created_at": "2022-02-15T06:35:34+00:00",
    "id": 1,
    "long": "london",
    "short": "gb",
    "updated_at": "2022-02-15T06:58:30+00:00"
  }
}
```

### Sources

- [LocationController.php#L51](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Locations/LocationController.php#L51)

## Create Location

### `POST /locations`

Creates a location.

### Body

| Field | Visibility | Type   | Description               |
| ----- | ---------- | ------ | ------------------------- |
| long  | optional   | string | The location description. |
| short | required   | string | The location identifier.  |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 422  | One or more validation rules failed. |

### Sources

- [LocationController.php#L64](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Locations/LocationController.php#L64)
- [LocationCreationService.php#L22](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Services/Locations/LocationCreationService.php#L22)

## Update Location

### `PATCH /locations/:id`

Updates a location by its `id` (number).

### Body

| Field | Visibility | Type   | Description               |
| ----- | ---------- | ------ | ------------------------- |
| long  | optional   | string | The location description. |
| short | optional   | string | The location identifier.  |

### Responses

| Code | Description                          |
| ---- | ------------------------------------ |
| 200  | The request was successful.          |
| 404  | The location was not found.          |
| 422  | One or more validation rules failed. |

### Sources

- [LocationController.php#L84](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Locations/LocationController.php#L84)
- [LocationUpdateService.php#L23](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Services/Locations/LocationUpdateService.php#L23)

## Delete Location

### `DELETE /locations/:id`

Deletes a location by its `id` (number).

### Responses

| Code | Description                                  |
| ---- | -------------------------------------------- |
| 200  | The request was successful.                  |
| 400  | There are servers connected to the location. |
| 404  | The location was not found.                  |

### Sources

- [LocationController.php#L98](https://github.com/pterodactyl/panel/blob/8abf2d810666c360320cc25808167d08963bb9be/app/Http/Controllers/Api/Application/Locations/LocationController.php#L98)
- [LocationDeletionService.php#L27](https://github.com/pterodactyl/panel/blob/a9bdf7a1ef27a65f07ebbf71d8ea20285cdaf30f/app/Services/Locations/LocationDeletionService.php#L27)

### `GET /nests`
Returns a list of nest objects.

### Parameters
Name | Supported | Allowed Values
----------|-----------|---------------
filter | ❌ |
include | ✅ | eggs, servers
sort | ❌ |
page | ✅ | Any number
per_page | ✅ | Any number

### `GET /nests/:id`
Returns a nest by its `id` (number). Supports the above parameters.

### `GET /nests/:id/eggs`
Returns a list of eggs in the nest.

### Parameters
Name | Supported | Allowed Values
----------|-----------|---------------
filter | ❌ |
include | ✅ | config, nest, script, servers, variables
sort | ❌ |
page | ✅ | Any number
per_page | ✅ | Any number

### `GET /nests/:id/eggs/:id`
Returns an egg in a nest by its `id` (number). Supports the above parameters.

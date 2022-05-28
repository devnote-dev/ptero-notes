# Application API
This API is for managing a lot of the administrative side of the panel, ranging from control over users, nodes, servers, eggs, and more.

# Access
The `Authorization` header must be present in requests and must be prefixed with "Bearer " followed by the key. Application API keys can be generated in the admin side of the panel. `Content-Type` and `Accept` headers are also required for `POST`, `PATCH`, `PUT` requests.

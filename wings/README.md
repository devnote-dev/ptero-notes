# Wings API
This API is mainly for communication between the panel and Wings, so this section will only cover necessary endpoints.

# Access
The `Authorization` header must be present in the requests and must be prefixed with "Bearer " followed by the node token ID. The token can be obtained in the configuration page of a node in the admin panel, or from the [node configuration endpoint](/pterodactyl/application/nodes.md#get-nodesidconfiguration) in the application API.

The `Content-Type` and `Accept` headers are also required for `POST`, `PATCH` and `PUT` requests. Requests that require a body should be in the format of a **JSON string** unless otherwise specified (see endpoint specific information).

# Wings API

The Wings API is used for communicating to the panel and other Wings instances on the panel.

> [!IMPORTANT]
> The Wings API does not have any control over the literal server instances in the panel, only the Docker containers for said servers and the server volumes. Use the [application API](/pterodactyl/application/README.md) for server control.

## Access

The `Authorization` header must be present in the requests and must be prefixed with "Bearer " followed by the node's token (also known as the daemon token or master daemon key). The token can be obtained in the configuration page of a node in the admin panel, or from the [node configuration endpoint](/pterodactyl/application/nodes.md#get-nodesidconfiguration) in the application API. The `Accept` header must be set to "application/json" for requests, and the `Content-Type` must be set appropriately when making `POST`, `PATCH` or `PUT` requests.

# Websockets

Server websockets can provide a constant stream of information about the server to the client in real-time.

## Access

Make sure you have set the `allowed_origins` field in your Wings configuration to your Fully Qualified Domain Name (FQDN), IP address or `"*"` if you want to allow all origins. Alternatively, you can include the `Origin` header with your panel URL or an allowed origin when establishing the connection if the library you're using supports it.

> **Warning**
> The `allowed_origins` field does not support pattern matching, meaning that you cannot allow all routes of a particular domain or IP dynamically (e.g. `192.168.1.*`).

Once you have connected to the websocket you must authenticate it with the token received from the panel (see [events](#events)). If successful, you will recieve an "auth success" event.

## Supported Libraries

| Language    | Libraries                                                                      |
| ----------- | ------------------------------------------------------------------------------ |
| Dart        | https://api.dart.dev/stable/2.17.3/dart-io/WebSocket-class.html                |
| Go          | https://pkg.go.dev/nhooyr.io/websocket                                         |
| Java/Kotlin | https://square.github.io/okhttp/                                               |
| JS/TS       | https://www.npmjs.com/package/ws https://www.npmjs.com/package/websocket       |
| Python      | https://pypi.org/project/websockets/ https://pypi.org/project/python-socketio/ |
| Rust        | https://docs.rs/websocket/latest/websocket/                                    |

## Events

All events being sent or recieved from the websocket are in the following JSON object format:

```json
{
    "event":"<event name>",
    "args": [<event arguments>]
}
```

_Replace the values with `<>` accordingly._

Websocket payloads will always have the event name, but the event arguments can be empty or unset. When sending requests to the websocket, make sure the payload is in the above format. If the event requires arguments, they must be in string form.

### Events you can send

| Name         | Arguments                             | Description                               |
| ------------ | ------------------------------------- | ----------------------------------------- |
| auth         | the websocket auth token              | Authenticates the websocket connection.   |
| set state    | "start", "stop", "restart", or "kill" | Sets the power state of the server.       |
| send command | the command                           | Sends a command to the server console.    |
| send logs    |                                       | Requests the console logs for the server. |
| send stats   |                                       | Requests the server statistics.           |

### Events you can recieve

| Name                     | Arguments            | Description                                                |
| ------------------------ | -------------------- | ---------------------------------------------------------- |
| auth success             |                      | The authentication was successful.                         |
| backup complete          |                      | Sent when a backup is complete.                            |
| backup restore completed |                      | Sent when a backup has been restored to the server.        |
| console output           | the output message   | The output from the console (one line).                    |
| daemon error             | the error message    | The daemon recieved an error (usually with the websocket). |
| daemon message           | the message          | A message from the daemon.                                 |
| install completed        |                      | Sent when a server's installation process is complete.     |
| install output           | the output message   | The output from the installation process.                  |
| install started          |                      | Sent when a server's installation process starts.          |
| jwt error                | the error message    | An error occurred with the authentication token.           |
| stats                    | statistics JSON data | Current statistics about the server.                       |
| status                   | the power state      | The power state of the server.                             |
| token expired            |                      | The token expired; connection will be closed shortly.      |
| token expiring           |                      | Warning event: you should reauthenticate the connection.   |
| transfer logs            | the output log       | The logs from the transfer process.                        |
| transfer status          | the transfer state   | The current transfer status.                               |

## Heartbeating

Websocket tokens can last upto 20 minutes, with a "token expiring" event sent around 5 minutes prior to closing. In order to keep the websocket connection open, a new token needs to be sent before the connection closes. This process is commonly called heartbeating, and can be done with these 2 steps:

1. Request a new token from the panel ([websocket endpoint](/pterodactyl/client/servers.md#get-serversidentifierwebsocket))
2. Send an "auth" event with the new token

It's advised to reauthenticate the connection when you recieve the "token expiring" warning event, as the connection is not always kept open for the full 20 minutes.

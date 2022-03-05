---
description: A list of events you can receive from the server websocket.
---

# Events

## Request Events

These are events that you can send to the server for data or to perform an action.

### Auth

Sends an authentication request to the server (part of initialization and heartbeating). An [auth success event](events.md#auth-success) will be received on success.

| Key   | Value         | Description         |
| ----- | ------------- | ------------------- |
| event | `"auth"`      | The event name      |
| args  | `["<TOKEN>"]` | The websocket token |

### Send Statistics

Sends a request for server statistics. A [stats event](events.md#stats) will be received on success.

| Key   | Value          | Description           |
| ----- | -------------- | --------------------- |
| event | `"send stats"` | The event name        |
| args  | `[]`           | No arguments required |

### Send Logs

Sends a request for server logs.

|       |               |                       |
| ----- | ------------- | --------------------- |
| event | `"send logs"` | The event name        |
| args  | `[]`          | No arguments required |

### Send Command

Sends a command to the server console. A [status event](events.md#status) will be received on success.

|       |                  |                     |
| ----- | ---------------- | ------------------- |
| event | `"send command"` | The event name      |
| args  | `["<COMMAND>"]`  | The command to send |

### Set Power State

Sends a request to change the server power state. This can be "start", "stop", "restart", or "kill". A [status event](events.md#status) will be received on success.

|       |               |                        |
| ----- | ------------- | ---------------------- |
| event | `"set state"` | The event name         |
| args  | `["<STATE>`"] | The power state to set |

## Receive Events

These are events that the server can send you.

### Auth Success

This is received when an authentication event is successful. No arguments are included in this event.

### Console Output

This event is received when data is outputted to the console. It includes an array of the messages outputted.

### Stats

This event is received when stats are requested from the server. It includes a JSON string of statistic data.

### Status

This event is received when the status (power state) of the server is updated. It includes the updated state of the server.

### Token Expiring

This event is received 10-15 minutes after each successful authorization event to notify you that the token is expiring and will eventually close the websocket if no authorization event is sent within the next 5-10 minutes. Heatbeating is briefly explained [here](setting-up.md#3.-maintaining-connection). No arguments are included in this event.

### Token Expired

This event is received just before a websocket connection is closed. No arguments are included in this event.

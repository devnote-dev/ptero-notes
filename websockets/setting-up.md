---
description: Setting up Pterodactyl websocket connections.
---

# Setting Up

## Wings

Before attempting any kind of connection to Pterodactyl, make sure that the `allowed_origins` option in the Wings configuration file has whitelisted your (or all) IPs.

```yaml
allowed_origins:
  - "127.0.0.1" # allows a specific IP address
  - "*" # allows all IP addresses
```

Afterwards, restart Wings using `systemctl restart wings`, then you should be good to go!

## Initial Connection

Connecting to a server websocket requires a few steps before the actual initialization. Make sure you have a client API key available (see the getting [started page](../getting-started.md#client-api) on how to get one).

### 1. Fetch the websocket authorization

{% swagger method="get" path="/servers/{id}/websocket" baseUrl="https://pterodactyl.domain/api/client" summary="Fetches the websocket connection information for a specific server." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
The ID of the server.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "data": {
        "token": "fKMITGYhbiytydHJKJOdtgJYUFVHJNoyhbOHUYFYVBKmo4i4hiu6gjknoig8yu46",
        "socket": "wss://pterodactyl.domain:8080/api/servers/c020fc84-15bb-4d60-b639-6a2ab27b2dca/ws"
    }
}
```
{% endswagger-response %}
{% endswagger %}

### 2. Initialize the websocket

This initializes the connection but it does not keep the connection open, step 3 covers that process.

```javascript
const Websocket = require('ws');

const ws = new Websocket('wss://pterodactyl.domain:8080/api/servers/c020fc84-15bb-4d60-b639-6a2ab27b2dca/ws');
```

### 3. Maintaining connection

After initializing the websocket connection, an authentication event must be sent to authorize the connection and thus receive events from the server. All websocket event objects use the following format:

```json
{
    "auth": "<EVENT_NAME>",
    "args": [] // this can include information sent/received for that event
}
```

It is recommended to send the authorization event once the websocket is open/ready. You should receive an auth success event when it is completed.

```javascript
const myToken = '<TOKEN_FROM_API>';

ws.onopen = (event) => {
    ws.send({
        event: 'auth',
        args:[myToken]
    });
}
```

As an extra layer of security, server websocket connections require that an authentication event is sent every 15-20 minutes to keep the connection open. This process is known as "heartbeating", and ensures that the websocket connection is not kept open longer than needed.

## Handling Events

Well done on successfully connecting to your server's websocket! Check \[] for a list of events you can receive from the server. The next step is handling those events; you can view a range of event handlers in the \[] page.

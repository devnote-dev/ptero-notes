---
description: A list of template handlers for websocket events.
---

# Handlers

### JavaScript

```javascript
const Websocket = require('ws');

const ws = new Websocket('wss://pterodactyl.domain:8080/api/servers/c020fc84-15bb-4d60-b639-6a2ab27b2dca/ws');

ws.onopen = (event) => {
    console.log('connected to the server!');
    ws.send({
        event: 'auth',
        args:['fKMITGYhbiytydHJKJOdtgJYUFVHJNoyhbOHUYFYVBKmo4i4hiu6gjknoig8yu46']
    });
};

ws.onmessage = (event) => {
    switch (event.data.event) {
        case 'auth success':
            break;
        case 'auth expiring':
            ws.send({
                event: 'auth',
                args:['fKMITGYhbiytydHJKJOdtgJYUFVHJNoyhbOHUYFYVBKmo4i4hiu6gjknoig8yu46']
            });
            break;
        case 'token expired':
            return;
        default:
            console.log(`received event: ${event.data.event}`);
            console.log(event.data.args.join('\n'));
            break;
    }
}

ws.onerror = (event) => {
    console.log(`error received: ${event.message}`);
}

ws.onclose = (event) => {
    console.log('websocket closed');
}
```

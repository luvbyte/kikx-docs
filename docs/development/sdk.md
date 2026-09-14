# Connecting to the SDK

## Installation

Install the SDK using npm:

```bash
npm i kikx-sdk
```

## Import

#### NPM

```js
import { createApp, createAppClient } from "kikx-sdk";
```
#### CDN

```html
<script src="https://cdn.jsdelivr.net/npm/kikx-sdk/dist/kikx-sdk.umd.js" />
```

## Create an App

#### NPM

```js
import { createApp } from "kikx-sdk";

const app = createApp();
```

#### CDN

```html
<script>
  const { createApp } = kikxSdk;

  const app = createApp();
</script>
```

Initialize the app:

```js
await app.run();
```

You can also provide a callback:

```js
await app.run(info => {
  console.log("App started:", info);
});
```

## Create an App Client

Use `createAppClient()` when your application requires API functionality and a WebSocket connection.

```js
import { createAppClient } from "kikx-sdk";

const app = createAppClient();
```

Initialize the client:

```js
await app.run();
```

The client initializes the application and establishes the WebSocket connection.

## App vs App Client

| Feature | `createApp` | `createAppClient` |
|---|---|---|
| API access | Yes | Yes |
| App information | Yes | Yes |
| App events | Yes | Yes |
| WebSocket | No | Yes |
| Automatic reconnection | No | Yes |
| Realtime events | No | Yes |
| `sendEvent()` | No | Yes |

## API App

Use `createApp()` for API-only applications.

```js
import { createApp } from "kikx-sdk";

const app = createApp();

await app.run();
```

## Client App

Use `createAppClient()` for applications that need realtime communication.

```js
import { createAppClient } from "kikx-sdk";

const app = createAppClient();

await app.run();
```

## Singleton

The SDK maintains a single application instance.

Calling the same factory multiple times returns the existing instance.

```js
const app1 = createApp();
const app2 = createApp();

console.log(app1 === app2);
// true
```

The same applies to `createAppClient()`.

An API app and a client cannot be created at the same time.

```js
const app = createApp();

const client = createAppClient();
// Error
```

## Get Existing App

Use `getApp()` to retrieve the existing SDK instance.

```js
import { getApp } from "kikx-sdk";

const app = getApp();
```

## WebSocket Events

WebSocket events are available when using `createAppClient()`.

### Connection Open

```js
app.on("ws:open", event => {
  console.log("WebSocket connected");
});
```

### Message

```js
app.on("ws:onmessage", event => {
  console.log("WebSocket message:", event);
});
```

### Connection Closed

```js
app.on("ws:onclose", event => {
  console.log("WebSocket disconnected");
});
```

### Error

```js
app.on("ws:onerror", error => {
  console.error("WebSocket error:", error);
});
```

### Reconnection Failed

```js
app.on("ws:reconnect_failed", () => {
  console.error("WebSocket reconnection failed");
});
```

## Sending Events

Use `sendEvent()` to send an event through the WebSocket connection.

```js
app.sendEvent("event-name", {
  key: "value"
});
```

A payload is optional:

```js
app.sendEvent("ping");
```

You can also use `send()` directly:

```js
app.send({
  event: "event-name",
  payload: {
    key: "value"
  }
});
```

## Listening for Events

Use `on()` to listen for events.

```js
app.on("event-name", payload => {
  console.log("Received:", payload);
});
```

Use `once()` for a one-time listener.

```js
app.once("event-name", payload => {
  console.log("Received:", payload);
});
```

Remove a listener with `off()`.

```js
const handler = payload => {
  console.log(payload);
};

app.on("event-name", handler);
app.off("event-name", handler);
```

## Message Events

Listen for browser `postMessage` events using `onMessage()`.

```js
app.onMessage("CHECK_WS", payload => {
  console.log("Message received:", payload);
});
```

Use `onceMessage()` for a one-time listener.

```js
app.onceMessage("CHECK_WS", payload => {
  console.log(payload);
});
```

Remove a message listener with `offMessage()`.

```js
app.offMessage("CHECK_WS", handler);
```

## Complete API Example

```js
import { createApp } from "kikx-sdk";

const app = createApp();

await app.run(info => {
  console.log("Kikx App started");
  console.log(info);
});
```

## Complete Client Example

```js
import { createAppClient } from "kikx-sdk";

const app = createAppClient();

app.on("ws:open", () => {
  console.log("WebSocket connected");
});

app.on("ws:onclose", () => {
  console.log("WebSocket disconnected");
});

app.on("ws:reconnect_failed", () => {
  console.error("Unable to reconnect");
});

await app.run(info => {
  console.log("Kikx Client started");
  console.log(info);
});
```

## Quick Reference

### API-only

```js
import { createApp } from "kikx-sdk";

const app = createApp();

await app.run();
```

### API + WebSocket

```js
import { createAppClient } from "kikx-sdk";

const app = createAppClient();

await app.run();
```

### Existing instance

```js
import { getApp } from "kikx-sdk";

const app = getApp();
```

### Send event

```js
app.sendEvent("event-name", payload);
```

### Listen for event

```js
app.on("event-name", payload => {
  // Handle event
});
```

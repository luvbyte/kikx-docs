# Invoker Documentation

The `Invoker` class provides a streamlined wrapper for routing application requests, managing window states, invoking system actions, and interacting with the KIKX environment core.

## Initialization

```javascript
import { createApp, Invoker } from "kikx-sdk";

const app = createApp();
const invoker = new Invoker(app);
```

---

## Methods

### `openApp(name, options)`

Launches or opens a specified application within the environment.

* **Parameters:**
  * `name` (string): The name or identifier of the application to open.
  * `options` (object, optional): Configuration object containing:
    * `args` (array, optional): Application arguments. Default: `[]`.
    * `query` (object, optional): Query parameters. Default: `{}`.
* **Returns:** Promise resolving from `_invoke`.

---

### `share(item)`

Shares a specified item using the system action handler.

* **Parameters:**
  * `item` (any): The item or resource to share.
* **Returns:** Promise resolving from `action`.

---

### `setWallpaper(url)`

Updates the system user interface wallpaper.

* **Parameters:**
  * `url` (string): The URL or local file path (`/files...path`) for the wallpaper image.
* **Returns:** Promise resolving from `action`.

---

### `setTheme(name)`

Changes the current UI application theme.

* **Parameters:**
  * `name` (string): The theme name identifier.
* **Returns:** Promise resolving from `action`.

# Alerts and Alert Documentation

The `Alerts` and `Alert` modules provide a comprehensive framework for building, configuring, displaying, and managing application-level alerts within the KIKX environment.

## Initialization

```javascript
import { createApp, Alerts } from "kikx-sdk";

const app = createApp();
const alerts = new Alerts(app);
```

## Classes

### `Alert`

A builder class for configuring and displaying custom individual alerts.

* **Constructor:** `constructor(_alert)`
* **Properties & State:**
  * `uid` (string): Unique identifier generated via `generateUUID()`.
  * `onclick` (function | null): Callback function triggered when the alert is clicked.
* **Methods:**
  * `setSticky(value)`: Sets whether the alert is sticky. Default: `true` (parameter default in implementation evaluates boolean).
  * `setSilent(value)`: Sets whether the alert is silent. Default: `true` (parameter default in implementation evaluates boolean).
  * `setPriority(priority)`: Sets alert priority (`"less"`, `"normal"`, `"high"`). Throws an error if an invalid priority is provided. Default: `"normal"`.
  * `setLabel(label)`: Sets a custom label. Default: `null`.
  * `setExtra(key, value)`: Adds custom extra metadata fields.
  * `setIsCode(value)`: Sets the `isCode` extra flag (`setExtra("isCode", Boolean(value))`). Default: `true`.
  * `onClick(callback)`: Registers a click handler callback for the alert. Returns `this`.
  * `show(message, type)`: Displays the alert with a specified message and type (default: `"info"`). Passes payload including `uid`, `type`, `message`, `label`, `extra`, `silent`, `sticky`, and `priority`.
  * `hide()`: Hides the alert by passing an empty message (`""`).

---

### `Alerts`

A manager class responsible for creating, tracking, and clearing multiple `Alert` instances.

---

## Methods

### `createAlert()`

Create and track a new `Alert` builder instance.

* **Parameters:** None
* **Returns:** `Alert` instance.
* **Errors:** Throws an error if the manager has been destroyed (`this.destroyed === true`).

---

### `alert(message, options)`

Quickly create and invoke a system alert. *(Note: Delegates to `this.system.alert`)*

* **Parameters:**
  * `message` (string): The alert message content.
  * `options` (object, optional): Configuration options `{ type = "info", priority = "normal" }`.
* **Returns:** Result of the system alert call.

---

### `clearAlert(alert)`

Clear, delete, and hide a specific alert instance.

* **Parameters:**
  * `alert` (`Alert`): The alert instance to clear.
* **Returns:** None

---

### `clearAll()`

Clear and hide all tracked alert instances.

* **Parameters:** None
* **Returns:** None

---

### `cleanup()` / `destroy()`

Destroy the `Alerts` manager, remove event listeners, mark as destroyed, and clear all active alerts.

* **Parameters:** None
* **Returns:** None

---

## Properties

### `size`

Returns the current count of tracked active alerts (`this.alerts.size`).

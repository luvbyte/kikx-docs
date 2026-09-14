# SystemService Documentation

## Methods

### `appInfo()`

Retrieve information about the application.

* **Parameters:** None
* **Returns:** Promise resolving to app info.

---

### `getAppsList(extra)`

Get a list of applications.

* **Parameters:**
  * `extra` (boolean, optional): Include extra details if `true`. Default: `false`.
* **Returns:** Promise resolving to the apps list.

---

### `sessionsInfo()`

Get information regarding active sessions.

* **Parameters:** None
* **Returns:** Promise resolving to session data.

---

### `closeSession(sessionID)`

Close a specific session by ID.

* **Parameters:**
  * `sessionID` (string): The session identifier to close.
* **Returns:** Promise resolving upon closing.

---

### `alert(message, options)`

Quickly dispatch a system alert.

* **Parameters:**
  * `message` (string): Alert message.
  * `options` (Object, optional):
    * `type` (string): Alert type. Default: `"info"`.
    * `priority` (string): Alert priority. Default: `"normal"`.
* **Returns:** Promise resolving to alert response.

---

### `closeApp()`

Request application closure.

* **Parameters:** None
* **Returns:** Promise resolving upon closure trigger.

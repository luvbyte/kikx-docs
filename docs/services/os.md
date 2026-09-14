# OSService Documentation

The `OSService` class extends the base `Service` class to provide a complete interface for executing system operations, managing environment variables, and querying OS information within the KIKX environment backend.

## Initialization

```javascript
import { createApp, OSService } from "kikx-sdk";

const app = createApp();
const osService = new OSService(app);
```

---

## Methods

### `func(name, options)`

Dispatches a request to run an OS function and returns the structured result containing `{ data, error }`.

* **Parameters:**
  * `name` (string): The name of the OS function to execute.
  * `options` (object, optional): Execution options containing:
    * `args` (array, optional): Arguments to pass to the function. Default: `[]`.
    * `options` (object, optional): Additional function options. Default: `{}`.
* **Returns:** Promise resolving to the result object (`{ data, error }`).

---

### `run(name, options)`

Executes an OS function using the fetch method.

* **Parameters:**
  * `name` (string): The name of the OS function to execute.
  * `options` (object, optional): Execution options containing `args` and `options`. Default: `{}`.
* **Returns:** Promise resolving to the execution response.

---

### `username()`

Retrieves the current system username.

* **Parameters:** None
* **Returns:** Promise resolving to the username response.

---

### `getenv(key, defaultValue)`

Retrieves the value of a specified environment variable.

* **Parameters:**
  * `key` (string): The name of the environment variable.
  * `defaultValue` (any, optional): The default value to return if the environment variable is not found. Default: `null`.
* **Returns:** Promise resolving to the environment variable value.

---

### `setenv(key, value)`

Sets an environment variable to a specified value.

* **Parameters:**
  * `key` (string): The name of the environment variable.
  * `value` (string): The value to assign.
* **Returns:** Promise resolving to the set operation response.

---

### `unsetenv(key)`

Unsets or removes a specified environment variable.

* **Parameters:**
  * `key` (string): The name of the environment variable to remove.
* **Returns:** Promise resolving to the unset operation response.

---

### `environment()`

Retrieves the complete system environment variables list/object.

* **Parameters:** None
* **Returns:** Promise resolving to the environment collection.

---

### `info()`

Retrieves general system and operating system information.

* **Parameters:** None
* **Returns:** Promise resolving to the OS information response.

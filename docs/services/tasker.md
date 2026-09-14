# Tasker Documentation

The `Tasker` service provide a complete framework for creating, running, monitoring, managing, and cleaning up background execution tasks within the KIKX environment.

## Initialization

```javascript
import { createAppClient, Tasker } from "kikx-sdk";

const app = createAppClient();
const tasker = new Tasker(app);
```

## Classes

### `TaskHandler`

Manages event dispatching, data listeners, and state tracking for an individual task session.

* **Constructor:** `constructor()` - Generates a unique handler ID using `generateUUID()`, initializes tracking properties, and sets up default event handlers (`started`, `info`, `output`, `error`, `ended`).
* **Properties & State:**
  * `handlerID` (string): Unique UUID for the handler.
  * `running` (boolean): Execution state flag. Default: `false`.
  * `destroyed` (boolean): Destruction state flag. Default: `false`.
  * `events` (object): Lifecycle event mapping dictionary.
* **Methods:**
  * `onData(callback)`: Registers a data callback listener. Throws an error if destroyed or if the callback is not a function. Returns an unsubscription function.
  * `offData(callback)`: Removes a data callback listener.
  * `emit(payload)`: Broadcasts a payload to all registered data callbacks safely.
  * `clearListeners()`: Removes all custom listeners while retaining the internal event dispatcher.
  * `destroy()`: Marks the handler as destroyed, clears all listeners and callbacks, and resets state.

---

### `Task`

Builder and execution wrapper class for managing a specific command task lifecycle.

* **Constructor:** `constructor(cmd, once, request)`
* **Properties & State:**
  * `cmd` (string): The command string to execute.
  * `request` (function): Request dispatcher function.
  * `handler` (`TaskHandler`): Associated task handler instance.
  * `taskID` (string | null): Unique task identifier returned from the backend. Default: `null`.
  * `once` (boolean): Flag restricting re-execution if completed.
  * `running` (boolean), `completed` (boolean), `destroyed` (boolean): Lifecycle state flags.
* **Methods:**
  * `init(options)`: Initializes the task session via a `create` request (`{ canSudo, outputMode }`). Throws an error if destroyed or already initialized.
  * `run()`: Executes the initialized task via a `run` request. Throws an error if not ready, already running, or completed (when `once` is true).
  * `kill(remove)`: Terminates a running task via a `kill` request.
  * `cleanup()` / `destroy()`: Kills the task, marks it as destroyed, removes all listeners, and resets properties.
  * `send(inputText, force)`: Sends input data to the task session.
  * `getInfo()`: Retrieves current task info/status from the backend.
  * `getSavedOutput()`: Fetches saved output data for the task.
  * `clearSavedOutput()`: Clears saved output data.
  * `on(callback)` / `off(callback)`: Registers or unregisters event listeners.
  * State helpers: `isInitialized()`, `isRunning()`, `isCompleted()`, `isDestroyed()`.

---

### `Tasker`

Manager service extending the base `Service` class to create, track, run, and clean up multiple `Task` instances.

---

## Methods

### `init()`

Initializes the tasker service.

* **Parameters:** None
* **Returns:** Promise resolving from the `init` fetch call.

---

### `createTask(cmd, once)`

Creates and tracks a new `Task` instance.

* **Parameters:**
  * `cmd` (string): The command string to run.
  * `once` (boolean, optional): Restricts re-execution if completed. Default: `true`.
* **Returns:** `Task` instance.

---

### `removeTask(task)`

Removes a specific task from tracking and cleans it up.

* **Parameters:**
  * `task` (`Task`): The task instance to remove.
* **Returns:** Promise resolving when cleanup is complete.

---

### `removeAll()`

Removes and cleans up all tracked tasks.

* **Parameters:** None
* **Returns:** Promise resolving when all tasks are cleaned up.

---

### `doTask(cmd, callback, canSudo)`

Creates, initializes, runs a task, and automatically cleans it up upon completion or error.

* **Parameters:**
  * `cmd` (string): The command string to run.
  * `callback` (function, optional): Status/output callback function.
  * `canSudo` (boolean, optional): Whether sudo permissions are allowed. Default: `true`.
* **Returns:** Promise resolving to the `Task` instance.

---

### `runSaveTask(cmd, callback, delayCheck)`

Runs a task, polls/monitors progress, and returns saved output data in an array once complete.

* **Parameters:**
  * `cmd` (string): The command to run.
  * `callback` (function, optional): Live output stream callback. Default: `null`.
  * `delayCheck` (number, optional): Polling delay in milliseconds. Default: `5000`.
* **Returns:** Promise resolving to an object containing `{ data, error }`.

---

### `runTaskPolling(cmd, delayCheck)`

Runs a task and long-polls its execution status until completion, returning final results.

* **Parameters:**
  * `cmd` (string): The command to run.
  * `delayCheck` (number, optional): Polling delay in milliseconds. Default: `5000`.
* **Returns:** Promise resolving to an object containing `{ returncode, stdout, stderr }`.

---

### `quickRun(cmd, options)`

Quickly executes a command on the backend and returns the result.

* **Parameters:**
  * `cmd` (string): The command string.
  * `options` (object, optional): Configuration containing `canSudo` (boolean), `input` (array), and `timeout` (number/null).
* **Returns:** Promise resolving to the quick execution response.

---

### `cleanup()` / `destroy()`

Stops and cleans up all running tasks.

* **Parameters:** None
* **Returns:** Promise resolving when cleanup is complete.

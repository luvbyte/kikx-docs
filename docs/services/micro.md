# Micro and MicroService Documentation

The `Micro` and `MicroService` modules provide a framework for creating, controlling, managing, and interacting with microservices within the KIKX environment.

## Initialization

```javascript
import { createApp, MicroService } from "kikx-sdk";

const app = createApp();
const microService = new MicroService(app);
```

## Classes

### `Micro`

A representation and controller class for an individual microservice instance.

* **Constructor:** `constructor(name, manager)`
* **Properties & State:**
  * `name` (string): The identifier name of the microservice.
  * `manager` (`MicroService`): Reference to the parent manager service instance.
  * `destroyed` (boolean): Flag indicating whether the micro instance has been destroyed. Default: `false`.
* **Methods:**
  * `start()`: Starts the microservice via the manager. Throws an error if already destroyed.
  * `output()`: Retrieves the output for the microservice via the manager. Throws an error if already destroyed.
  * `send(data)`: Sends input data to the microservice via the manager. Throws an error if already destroyed.
  * `stop()`: Stops the microservice via the manager and sets `destroyed = true`. Safe to call if already destroyed.
  * `cleanup()` / `destroy()`: Stops the microservice and unlinks the manager reference by setting `manager = null` and `destroyed = true`.

---

### `MicroService`

Extends the base `Service` class to manage multiple `Micro` instances, track active services, and handle communication with the microservice API namespace (`"micro"`).

---

## Methods

### `list()`

Retrieves a list of active microservices.

* **Parameters:** None
* **Returns:** Promise resolving to the list response from the API (`list`).

---

### `start(name)`

Starts or retrieves an existing active `Micro` instance by name.

* **Parameters:**
  * `name` (string): The name of the microservice to start.
* **Returns:** Promise resolving to a `Micro` instance.
* **Errors:** Throws an error if the API request fails.

---

### `output(name)`

Retrieves output data from a specified microservice.

* **Parameters:**
  * `name` (string): The name of the microservice.
* **Returns:** Promise resolving to the output data response.

---

### `send(name, data)`

Sends input data to a specified microservice.

* **Parameters:**
  * `name` (string): The name of the microservice.
  * `data` (any): The data to send.
* **Returns:** Promise resolving to the send operation response.

---

### `stop(name)`

Stops a specific microservice and removes it from the active instances map.

* **Parameters:**
  * `name` (string): The name of the microservice to stop.
* **Returns:** Promise resolving to the stop operation response.

---

### `stopAll()`

Stops all microservices and clears the active instances map.

* **Parameters:** None
* **Returns:** Promise resolving to the stop-all response.

---

### `cleanup()` / `destroy()`

Cleans up all tracked microservice instances using `Promise.allSettled`, stops all services on the backend, and clears all tracking maps.

* **Parameters:** None
* **Returns:** Promise resolving when cleanup is complete.

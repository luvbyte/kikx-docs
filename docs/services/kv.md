# KVService Documentation

The `KVService` module extends the base `Service` class to provide a complete key-value storage and management framework within the KIKX environment.

## Initialization

```javascript
import { createApp, KVService } from "kikx-sdk";

const app = createApp();
const kv = new KVService(app);
```

---

## Methods

### `info()`

Retrieves collection information.

* **Parameters:** None
* **Returns:** Promise resolving to the collection info response from the API.

---

### `dump()`

Dumps all data from the collection.

* **Parameters:** None
* **Returns:** Promise resolving to the data dump response.

---

### `get(key)`

Retrieves a value by its key.

* **Parameters:**
  * `key` (string): The key to look up.
* **Returns:** Promise resolving to the key's value.

---

### `set(key, value)`

Sets a key-value pair.

* **Parameters:**
  * `key` (string): The key to set.
  * `value` (any): The value to assign to the key.
* **Returns:** Promise resolving to the API response.

---

### `exists(key)`

Checks whether a specific key exists in the collection.

* **Parameters:**
  * `key` (string): The key to check.
* **Returns:** Promise resolving to a boolean or existence status response.

---

### `getOrSet(key, value)`

Retrieves an existing value by key, or sets it to the specified default value if it does not exist.

* **Parameters:**
  * `key` (string): The key to check or set.
  * `value` (any): The default value to assign if the key does not exist.
* **Returns:** Promise resolving to the resulting value or API response.

---

### `pop(key)`

Removes a key-value pair and returns the deleted value.

* **Parameters:**
  * `key` (string): The key to pop.
* **Returns:** Promise resolving to the removed value.

---

### `save()`

Persists the current key-value collection state.

* **Parameters:** None
* **Returns:** Promise resolving to the save operation response.

---

### `reset()`

Resets the key-value collection.

* **Parameters:** None
* **Returns:** Promise resolving to the reset operation response.

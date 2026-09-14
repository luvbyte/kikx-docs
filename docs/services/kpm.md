# KPM and AppInstaller Documentation

The `Kpm` and `AppInstaller` modules provide a complete package management framework for preparing, installing, tracking, querying, and removing applications within the KIKX environment.

## Initialization

```javascript
import { createApp, Kpm } from "kikx-sdk";

const app = createApp();
const kpm = new Kpm(app);
```

## Classes

### `AppInstaller`

A builder and handler class for managing the lifecycle of an individual package installation session.

* **Constructor:** `constructor(app)`
* **Properties & State:**
  * `app` (object): Reference to the main application instance.
  * `appData` (object | null): Cached metadata/data returned from a prepared installation session.
  * `isGithub` (boolean): Flag indicating whether the package source is GitHub. Default: `false`.
* **Methods:**
  * `getTempID()`: Returns the temporary session identifier from `appData?.temp_id`.
  * `getPreviewUrl(file)`: Generates a preview URL for a specified file using `app.getUrl()`, incorporating the base URL, temp ID, and encoded filename.
  * `prepare(file)`: Prepares a local package file via `kpm/prepare-local` (POST request with FormData). Caches the result in `appData`. Throws an error if the request fails.
  * `storage(path)`: Prepares a package from a server storage path via `kpm/prepare-storage` (POST request with query params). Caches the result in `appData`. Throws an error if the request fails.
  * `github(url, tag)`: Prepares a package from a GitHub repository URL and optional tag via `kpm/prepare-github` (POST request with query params). Sets `isGithub = true` and caches the result. Throws an error if the request fails.
  * `install()`: Confirms and executes the installation of the prepared package via `kpm/confirm-install`. Requires a pre-existing session (`appData`). Throws an error if no session exists or if the request fails.

---

### `Kpm`

A manager class responsible for creating, tracking, retrieving, and cleaning up multiple `AppInstaller` instances, as well as handling application queries and uninstalls.

---

## Methods

### `createInstaller()`

Creates and returns a new independent `AppInstaller` instance.

* **Parameters:** None
* **Returns:** `AppInstaller` instance.

---

### `getInstaller(name)`

Retrieves an existing named installer from the manager or creates and caches a new one if it does not exist. If no name is provided, returns a fresh unmanaged installer.

* **Parameters:**
  * `name` (string, optional): The unique name/key of the installer.
* **Returns:** `AppInstaller` instance.

---

### `removeInstaller(name)`

Deletes a specific named installer from the manager tracking map.

* **Parameters:**
  * `name` (string): The name of the installer to remove.
* **Returns:** None

---

### `clearInstallers()`

Clears all tracked named installers from the manager.

* **Parameters:** None
* **Returns:** None

---

### `getInstalledApps()`

Retrieves the list of currently installed applications.

* **Parameters:** None
* **Returns:** Promise resolving to the installed apps response from `kpm/installed-apps`.

---

### `getAppInfo(name)`

Retrieves detailed information about a specific installed application.

* **Parameters:**
  * `name` (string): The application name identifier.
* **Returns:** Promise resolving to the app info response from `kpm/app-info`.

---

### `uninstallApp(name, keepData)`

Uninstalls a specified application.

* **Parameters:**
  * `name` (string): The name of the application to uninstall.
  * `keepData` (boolean, optional): Whether to retain application data during uninstallation. Default: `false`.
* **Returns:** Promise resolving to the uninstallation response.
* **Errors:** Throws an error if the request returns an error detail.

---

## Properties

### `installerCount`

Returns the current count of tracked named installers (`this._installers.size`).

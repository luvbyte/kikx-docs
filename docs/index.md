# KIKX Documentation

**Kikx** is as an application runtime environment where apps (built using HTML, CSS, and JavaScript) run inside isolated iframes, while the Kikx UI connects as a client to manage and launch them.

⚠️ Note: KIKX is currently under active development. Features may change, break, or be incomplete as the project evolves.

## 🚀 Quick Links

* [Installation Guide](getting-started/installation.md)
* [Getting Started](getting-started/first-app.md)
* [App Development](development/app-development.md)
* [Application SDK Guide](development/sdk.md)
* [Services Overview](services/overview.md)

---

## 🛠️ Core Architecture

KIKX provides a modular set of client-side service modules and background handlers to ensure seamless execution and secure sandboxing across applications:

* **[FS](services/fs.md):** File System service.
* **[KV](services/kv.md):** Key-Value service.
* **[ProxyService](services/proxy.md):** Non-CORS blocking network request proxy.
* **[OSService](services/os.md):** Useful Operating-System functions.
* **[Tasker](services/tasker.md):** App running process management.
* **[Micro](services/micro.md):** App Long-running process management.

* **[System](services/system.md):** Kikx system service for kpm, alerts, invoker, ...
* **[Alerts](services/alerts.md):** Notification and custom alert builder UI.
* **[Kpm](services/kpm.md):** Package manager and installer pipeline for local, storage, and GitHub apps.
* **[Invoker](services/invoker.md):** System action dispatcher for opening apps and modifying UI settings.

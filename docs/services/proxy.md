# ProxyService Documentation

The `ProxyService` class extends the base `Service` class to route and handle non-CORS blocking network requests through a designated proxy target within the KIKX environment.

## Initialization

```javascript
import { createApp, ProxyService } from "kikx-sdk";

const app = createApp();
const proxy = new ProxyService(app)
```

---

## Methods

### `proxyRequest(url, options)`

Execute a non-CORS blocking request via the proxy target.

* **Parameters:**
  * `url` (string): The target URL to proxy.
  * `options` (Object, optional):
    * `method` (string, optional): HTTP method. Default: `"GET"`.
    * `params` (Object, optional): Request query parameters. Default: `{}`.
    * `body` (any, optional): Request body payload. Default: `undefined`.
    * `headers` (Object, optional): Request headers. Default: `{}`.
    * `...options` (Object, optional): Additional request options passed down to the base service.
* **Returns:** Promise resolving to the proxy request response.

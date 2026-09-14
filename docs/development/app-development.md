# App Development Guide

This document outlines the standard architecture, manifest structure, and lifecycle guidelines for building third-party applications that run inside KIKX.

---

## 📦 Application Structure

Every KIKX application is packaged as a `.kikx` archive or folder containing a standardized directory layout:

```text
my-kikx-app/
├── app.json             # Manifest configuration file
├── www/
│   └── index.html       # Application entry point (frontend UI)
└── public/
    └── icon.png         # Application icon / thumbnail
```

---

## 📝 The `app.json` Manifest

The manifest file defines app metadata, versioning, permissions, and runtime security sandboxing rules.

```json
{
  "name": "my-app",
  "title": "My Application",
  "version": "1.0.0",
  "kikx_version": "0.4.0",
  "description": "An example application.",
  "author": "Developer",

  "iframe": {
    "allowfullscreen": false,
    "sandbox": ["allow-scripts"],
    "allow": [],
    "loading": "eager",
    "referrerpolicy": "no-referrer"
  },

  "services": ["fs", "proxy", "kv", "os", "micro", "tasker"],
  
  "service_config": {
    "fs": {
      "os": "read",
      "home": "read-write"
    },
    "micro": {
      "app": {
        "persistent": true
      }
    }
  },
  
  "system": {
    "access": ["alerts", "invoke", "sessions", "kpm"]
  },

  "icon": "icon.png",
  "splash": "splash.png",
  "category": "Example",

  "theme": "transparent"
}
```
---

# Connecting to the SDK

## Installation

Install the SDK using npm:

```bash
npm i kikx-sdk
```

## Import

#### NPM

```js
import { createApp, createAppClient } from "kikx-sdk";
```
#### CDN

```html
<script src="https://cdn.jsdelivr.net/npm/kikx-sdk/dist/kikx-sdk.umd.js" />
```

## Create an App

#### NPM

```js
import { createApp } from "kikx-sdk";

const app = createApp();
```

#### CDN

```html
<script>
  const { createApp } = kikxSdk;

  const app = createApp();
</script>
```

Initialize the app:

```js
await app.run();
```
# Creating Your First KIKX App

Building an application for the KIKX requires setting up a specific project structure, configuring the metadata, packaging the files, and installing the package through the KIKX App Store.

## 📁 1. Project Directory Structure

To start building an app, create an example project folder containing a configuration file, a web asset folder, and an icon.

* **`example/`** — The root folder for your application source files.
  * **`app.json`** — The main configuration and metadata manifest file.
  * **`www/`** — Directory containing the web application interface assets.
    * **`index.html`** — The entry point file that loads when the app is opened.
  * **`public/`** — Directory containing public static assets.
    * **`icon.png`** — The application icon graphic.

---

## 💻 2. Creating the Entry Point (`index.html`)

Create a `www` folder inside your project directory and add an `index.html` file. Set up a simple layout with a centered "Hello World" text block:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MyApp</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f3f4f6;
            font-family: system-ui, -apple-system, sans-serif;
        }
        h1 {
            color: #1f2937;
            font-size: 2rem;
        }
    </style>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

---

## 🎨 3. Adding the App Icon

Create a `public` folder inside your project directory and place your application icon image inside it named `icon.png`.

---

## ⚙️ 4. Configuring `app.json`

Create an `app.json` configuration file in the root of your project directory with the following manifest structure:

```json
{
  "name": "com.example.myapp",
  "title": "MyApp",
  "description": "My hello world app",
  "author": "nobody",
  "version": "0.1.0",
  "kikx_version": "0.4.0",
  "include": ["public", "www"],
  "iframe": {
    "sandbox": ["allow-scripts"]
  }
}
```

---

## 📦 5. Packaging and Installation

Once all files are in place, package and install your application through the following steps:

1. Compress your project folder into a standard ZIP archive.
2. Rename the archive extension from `.zip` to `.kikx` (resulting in `app.kikx` or your project's custom package name).
3. Open the **App Store** app in kikx.
4. Upload and install your newly created package.

# FileSystemService Documentation

The `FileSystemService` class extends the core `Service` class to provide a comprehensive API wrapper for interacting with a file system backend. It handles file operations, directory management, uploading, downloading, and file serving/exposure.

## Initialization

```javascript
import { createApp, FileSystemService } from "kikx-sdk";

const app = createApp();
const fs = new FileSystemService(app)
```

---

## Protocols

* App **app://**
* App Cache **cache://**
* App Data **data://**
* Home **home://**
* OS **os://**
* OS-ROOT **osr://**
* KIKX-ROOT **root://**

---

## Methods

### `listFiles(directory, options)`

List files in a directory with options for pagination, sorting, and thumbnails.

* **Parameters:**
  * `directory` (string): The path of the directory to list.
  * `options` (Object, optional):
    * `offset` (number): Starting offset for pagination. Default: `0`.
    * `limit` (number): Maximum number of files to return. Default: `-1` (all files).
    * `sort` (string): Field to sort by. Default: `"name"`.
    * `asc` (boolean): Sort ascending if `true`, descending if `false`. Default: `true`.
    * `thumbnails` (boolean): Include thumbnails in response. Default: `false`.
* **Returns:** Promise resolving to file listing response.

---

### `thumbnail(filename)`

Get the thumbnail for a specific file.

* **Parameters:**
  * `filename` (string): Path or name of the file.
* **Returns:** Promise resolving to thumbnail data.

---

### `readFile(filename)`

Read the content of a file.

* **Parameters:**
  * `filename` (string): Path of the file to read.
* **Returns:** Promise resolving to file content.

---

### `writeFile(filename, content, options)`

Write content to a file.

* **Parameters:**
  * `filename` (string): Path of the file.
  * `content` (any): Content to write.
  * `options` (Object, optional):
    * `mode` (string): Write mode (e.g., `"write"`). Default: `"write"`.
    * `ensureDir` (boolean): Ensure directory exists before writing. Default: `false`.
* **Returns:** Promise resolving upon successful write.

---

### `appendFile(filename, content)`

Append content to an existing file.

* **Parameters:**
  * `filename` (string): Path of the file.
  * `content` (any): Content to append.
* **Returns:** Promise resolving upon successful append.

---

### `deleteFile(filename)`

Delete a file.

* **Parameters:**
  * `filename` (string): Path of the file to delete.
* **Returns:** Promise resolving upon successful deletion.

---

### `uploadFile(file, dest)`

Upload a single file to a destination directory.

* **Parameters:**
  * `file` (File | Blob): The file object to upload.
  * `dest` (string): Destination path.
* **Returns:** Promise resolving to upload response.

---

### `downloadFile(path)`

Download a file from the given path.

* **Parameters:**
  * `path` (string): Path of the file to download.
* **Returns:** Promise resolving to the downloaded file stream/data.

---

### `uploadFiles(files, dest)`

Upload multiple files to a destination directory.

* **Parameters:**
  * `files` (Array<File | Blob>): Array of file objects to upload.
  * `dest` (string): Destination path.
* **Returns:** Promise resolving to upload response.

---

### `createFile(filename)`

Create an empty file.

* **Parameters:**
  * `filename` (string): Path of the file to create.
* **Returns:** Promise resolving upon creation.

---

### `createDirectory(dirname)`

Create a new directory.

* **Parameters:**
  * `dirname` (string): Path of the directory to create.
* **Returns:** Promise resolving upon creation.

---

### `deleteDirectory(dirname)`

Delete a directory.

* **Parameters:**
  * `dirname` (string): Path of the directory to delete.
* **Returns:** Promise resolving upon deletion.

---

### `deleteList(paths)`

Delete a list of files or directories.

* **Parameters:**
  * `paths` (Array<string>): Array of paths to delete.
* **Returns:** Promise resolving upon completion.

---

### `rename(source, new_name)`

Rename a file or directory.

* **Parameters:**
  * `source` (string): Current path/name.
  * `new_name` (string): New path/name.
* **Returns:** Promise resolving upon renaming.

---

### `info(path)`

Get metadata/information about a file or directory.

* **Parameters:**
  * `path` (string): Path to inspect.
* **Returns:** Promise resolving to info object.

---

### `copy(source, dest)`

Copy a file or directory.

* **Parameters:**
  * `source` (string): Source path.
  * `dest` (string): Destination path.
* **Returns:** Promise resolving upon completion.

---

### `copyFile(source, dest, options)`

Copy a file with override options.

* **Parameters:**
  * `source` (string): Source file path.
  * `dest` (string): Destination file path.
  * `options` (Object, optional):
    * `override` (boolean): Overwrite destination if it exists. Default: `false`.
* **Returns:** Promise resolving upon completion.

---

### `move(source, dest)`

Move a file or directory.

* **Parameters:**
  * `source` (string): Source path.
  * `dest` (string): Destination path.
* **Returns:** Promise resolving upon completion.

---

### `expose(path, expires)`

Expose a path for serving files publicly or with an expiration time.

* **Parameters:**
  * `path` (string): Path to expose.
  * `expires` (number | null, optional): Expiration timestamp or duration. Default: `null`.
* **Returns:** Promise resolving to expose UID/token details.

---

### `removeExpose(uid)`

Remove a previously exposed file/directory exposure.

* **Parameters:**
  * `uid` (string): Exposure unique ID.
* **Returns:** Promise resolving upon removal.

---

### `clearExpose()`

Clear all file exposures.

* **Returns:** Promise resolving upon completion.

---

### `getServeUrl(uid, path, absolute)`

Generate a serve URL for an exposed path.

* **Parameters:**
  * `uid` (string): Exposure UID.
  * `path` (string, optional): Subpath. Default: `""`.
  * `absolute` (boolean, optional): Return absolute URL if `true`. Default: `false`.
* **Returns:** `string` (URL)

---

### `getServeAbsUrl(uid, path)`

Get the absolute serve URL for an exposed path.

* **Parameters:**
  * `uid` (string): Exposure UID.
  * `path` (string, optional): Subpath. Default: `""`.
* **Returns:** `string` (Absolute URL)

---

### `getServeFile(uid, path)`

Fetch a served file by its exposure UID and subpath.

* **Parameters:**
  * `uid` (string): Exposure UID.
  * `path` (string, optional): Subpath. Default: `""`.
* **Returns:** Promise resolving to the served file response.

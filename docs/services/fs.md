# FileSystemService Documentation

The `FileSystemService` class extends the core `Service` class to provide a comprehensive API wrapper for interacting with a file system backend. It handles file operations, directory management, uploading, downloading, and file serving/exposure.

## Initialization

```javascript
import { createApp, FileSystemService } from "kikx-sdk";

const app = createApp();
const fs = new FileSystemService(app);
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

List files in a directory with advanced options for pagination, sorting, filtering, and thumbnails.

* **Parameters:**
  * `directory` (string): The path of the directory to list.
  * `options` (Object, optional):
    * `offset` (number): Starting offset for pagination. Default: `0`.
    * `limit` (number): Maximum number of files to return. Default: `-1` (all files).
    * `sort` (string): Field to sort by. Default: `"name"`.
    * `asc` (boolean): Sort ascending if `true`, descending if `false`. Default: `true`.
    * `filter` (string): Filter type (e.g., `"all"`). Default: `"all"`.
    * `extensions` (string): Filter by file extensions. Default: `""`.
    * `search` (string): Search query string. Default: `""`.
    * `thumbnails` (boolean): Include thumbnails in response. Default: `false`.
* **Returns:** Promise resolving to file listing response.

---

### `quickListFiles(directory, options)`

Quickly list files in a directory with simplified options.

* **Parameters:**
  * `directory` (string): The path of the directory to list.
  * `options` (Object, optional):
    * `sort` (string): Field to sort by. Default: `"name"`.
    * `asc` (boolean): Sort ascending if `true`, descending if `false`. Default: `true`.
    * `filter` (string): Filter type. Default: `"all"`.
    * `extensions` (string): Filter by file extensions. Default: `""`.
    * `search` (string): Search query string. Default: `""`.
    * `hidden` (boolean): Include hidden files. Default: `true`.
* **Returns:** Promise resolving to simplified file listing response.

---

### `searchFiles(directory, options)`

Search files recursively within a directory.

* **Parameters:**
  * `directory` (string): The path of the directory to search within.
  * `options` (Object, optional):
    * `search` (string): Search query string. Default: `""`.
    * `filter` (string): Filter type. Default: `"all"`.
    * `extensions` (string): Filter by file extensions. Default: `""`.
    * `hidden` (boolean): Include hidden files. Default: `true`.
    * `maxResults` (number): Maximum number of results to return. Default: `500`.
* **Returns:** Promise resolving to search results.

---

### `exists(path)`

Check if a path exists in the file system.

* **Parameters:**
  * `path` (string): Path to check.
* **Returns:** Promise resolving to a boolean or existence status.

---

### `stat(path)`

Get detailed file information.

* **Parameters:**
  * `path` (string): Path of the file.
* **Returns:** Promise resolving to file stats.

---

### `touch(path)`

Create a file or update its timestamp.

* **Parameters:**
  * `path` (string): Path of the file.
* **Returns:** Promise resolving upon successful execution.

---

### `diskUsage(path)`

Get disk usage statistics for a path.

* **Parameters:**
  * `path` (string): Path to inspect.
* **Returns:** Promise resolving to disk usage details.

---

### `tree(directory, options)`

Get a directory tree structure.

* **Parameters:**
  * `directory` (string): Root directory path.
  * `options` (Object, optional):
    * `depth` (number): Maximum tree depth. Default: `2`.
    * `hidden` (boolean): Include hidden files/directories. Default: `true`.
* **Returns:** Promise resolving to the directory tree.

---

### `mime(path)`

Get the MIME type of a file.

* **Parameters:**
  * `path` (string): Path of the file.
* **Returns:** Promise resolving to the MIME type string.

---

### `hash(path, algorithm)`

Calculate the file hash using a specified algorithm.

* **Parameters:**
  * `path` (string): Path of the file.
  * `algorithm` (string): Hash algorithm (e.g., `"sha256"`). Default: `"sha256"`.
* **Returns:** Promise resolving to the calculated hash.

---

### `checksum(path, algorithm)`

Calculate the checksum for a file.

* **Parameters:**
  * `path` (string): Path of the file.
  * `algorithm` (string): Checksum algorithm. Default: `"sha256"`.
* **Returns:** Promise resolving to the checksum.

---

### `chmod(path, mode)`

Change file or directory permissions.

* **Parameters:**
  * `path` (string): Path of the target.
  * `mode` (string): Permission mode.
* **Returns:** Promise resolving upon successful update.

---

### `batch(operations)`

Perform batch filesystem operations.

* **Parameters:**
  * `operations` (Array): Array of operations to execute.
* **Returns:** Promise resolving to batch results.

---

### `trash(path)`

Move a file or directory to the trash.

* **Parameters:**
  * `path` (string): Path to move to trash.
* **Returns:** Promise resolving upon completion.

---

### `restore(trashDirectory, trashId)`

Restore an item from the trash.

* **Parameters:**
  * `trashDirectory` (string): Trash directory path.
  * `trashId` (string): Unique identifier in the trash.
* **Returns:** Promise resolving upon successful restoration.

---

### `compress(source, destination, format)`

Compress a file or directory into an archive.

* **Parameters:**
  * `source` (string): Source path.
  * `destination` (string): Destination archive path.
  * `format` (string): Compression format (e.g., `"zip"`). Default: `"zip"`.
* **Returns:** Promise resolving upon completion.

---

### `extract(archive, destination)`

Extract an archive to a destination directory.

* **Parameters:**
  * `archive` (string): Path to the archive file.
  * `destination` (string): Destination directory path.
* **Returns:** Promise resolving upon completion.

---

### `watch(directory, options)`

Watch a directory for changes using Server-Sent Events (SSE).

* **Parameters:**
  * `directory` (string): Directory path to watch.
  * `options` (Object, optional):
    * `interval` (number): Polling or check interval. Default: `1`.
    * `pathType` (string): Path type (`"virtual"` or `"absolute"`). Default: `"virtual"`.
    * `onChange` (Function): Callback invoked on change events. Default: `null`.
    * `onError` (Function): Callback invoked on errors. Default: `null`.
    * `signal` (AbortSignal): Abort signal for cancelling the stream. Default: `null`.
* **Returns:** Promise resolving to an object with a `close()` method to stop watching.

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
    * `mode` (string): Write mode (e.g., `"write"`, `"append"`). Default: `"write"`.
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

---

### `convertPath(path, type)`

Convert a path between virtual and absolute representations.

* **Parameters:**
  * `path` (string): Path to convert.
  * `type` (string): Target type (`"virtual"` or `"absolute"`). Default: `"virtual"`.
* **Returns:** Promise resolving to the converted path.

---

### `toAbsolutePath(path)`

Convert a virtual path to an absolute path.

* **Parameters:**
  * `path` (string): Virtual path.
* **Returns:** Promise resolving to the absolute path.

---

### `toVirtualPath(path)`

Convert an absolute path to a virtual path.

* **Parameters:**
  * `path` (string): Absolute path.
* **Returns:** Promise resolving to the virtual path.

# Storage (storage) <!-- order: 3 -->

Handles media storage requests.

The storage `storage` API allows you to read/write files to the filesystem or S3 bucket.

---


### Storage Requests


Generally, these requests are made via custom handlers we've built, all you have to do is provide them to the action!

```javascript
// +page.server.js
export const actions = {
	upload: uploadFilesAction;
};
```


---


> [!NOTE]
> To fetch image details, you'll need to read the references from the database first using the [Database (db) API](/docs/api/db).


### Request Methods


###### Upload (create)

Uploads a new file into your selected storage option.

```javascript
// Example
storage.upload(file);
```

`file` - object *required* - A file object to upload.

---


###### Upload Multiple (create)

Uploads an array of new files.

```javascript
// Example
storage.uploadMultiple(files);
```

`files` - array *required* - An array of file objects to upload.

---


###### Get Metadata (read)

Gets the metadata of an uploaded file.

```javascript
// Example
storage.getMetadata(id);
```

`id` - string *required* - The ID of the entry.


---


###### Find Files (read)

Finds a file based on provided options.

```javascript
// Example
storage.findFiles(options);
```

`options` - object *optional* - An object of options to filter the results.

---


###### Find Files By Name (read)

Finds a file based on a provided filename.

```javascript
// Example
storage.findFilesByName(filename);
```

`filename` - string *required* - The cosmetic filename.

---


###### Update File (update)

Updates a file based on provided data fields.

```javascript
// Example
storage.updateFile(id, data);
```

`id` - string *required* - The ID of the entry.
`data` - object *required* - An object containing the updated data.


---


###### Serve File (read)

Fetches a link to the stored file.

```javascript
// Example
storage.serveFile(id); // Can also accept `filename` instead of `id`
```

`id` - string *required* - The ID of the entry.
`filename` - string *optional* - *Replaces `id`.* The cosmetic filename.

---


###### Delete (delete)

Deletes the specified file.

```javascript
// Example
storage.delete(id);
```

`id` - string *required* - The ID of the entry.

---


###### Count Files (read)

Counts the number of uploaded files currently in storage.

```javascript
// Example
storage.countFiles(filter);
```

`filter` - object *optional*

---
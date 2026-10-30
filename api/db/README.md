# Database (db) <!-- order: 2 -->

Handles general database requests.

The database `db` API is a fairly standard JavaScript object-based CRUD (create, read, update, delete) interface.

---


### Database Requests


##### Fetching Data

Fetch requests can be made to the server via standard SvelteKit server-side `load` functions.

The following example would output `data.updates` to your co-located `+page.svelte` file.

```javascript
// +page.server.js
export const load = async ({ locals }) => {
	const updates = await locals.comixCleric.db.find("updates");

	return { updates }; // `updates` is automatically appended to a `data` object
};

// Or...

export async function load({ locals }) {
	const updates = await locals.comixCleric.db.find("updates");

	return { updates };
};
```

Which can be retrieved in the page code by doing the following:

```svelte
<!-- +page.svelte -->
<script>
	let { data } = $props();

	let updates = data.updates;
<script>
```

##### Sending Data

To send data, we recommend using form actions. These allow you to use custom handlers for your form that give you the ability to trigger additional actions.


---


### Request Methods


###### Find (read)

Finds all entries in the collection based on the provided options.


```javascript
// Example
db.find(collection, options)
```

- `collection` - string *required*
- `options` - object *optional*


---


###### Find One (read)

Find a single entry in the collection based on the provided ID and options.

```javascript
// Example
db.findOne(collection, id, options)
```

- `collection` - string *required*
- `id`- string *required*
- `options` - object *optional*


---


###### Find One By (read)

Find a single entry in the collection based on the provided filter and options.

```javascript
// Example
db.findOneBy(collection, filter, options)
```

- `collection` - string *required*
- `filter` - object *required*
- `options` - object *optional*


---


###### Create

Creates a new entry in the collection using the provided data. (Data MUST be present.)

```javascript
// Example
db.create(<collection>, { <data> })
```

- `collection` - string *required*
- `id`- string *required*
- `data` - object *required*


---


###### Update

Find all entries in the collection based on the provided options.

```javascript
// Example
db.update(<collection>, <id>, { <data> })
```

- `collection` - string *required*
- `id` - string *required*


---


###### Delete

Find all entries in the collection based on the provided options.

```javascript
// Example
db.delete(collection, id)
```

- `collection` - string *required*
- `id` - string *required*


---


###### Count (read)

Find all entries in the collection based on the provided options.

```javascript
// Example
db.count(collection, filter)
```

- `collection` - string *required*
- `options` - object *optional*


---


###### Batch (any)

Find all entries in the collection based on the provided options.

```javascript
// Example
db.batch(queries)
```

- `queries` - object *required*


---


### Options

These provide additional parameters to further narrow-down results.

###### Filter

- `filter` - allows you narrow the returned entries by a matching set of values.

```javascript
// Example
db.find("my_collection", { // Open `options` object
	filter: { // Open the `filter` object
		slug: { // Match a value in `slug` field
			_eq: "value" // Use `_eq` (equals) operation to match an exact value
		}
	}
});
```


---


###### Sort

- `sort` - allows you return the entries in a specified order.

```javascript
// Example
db.find("my_collection", { // Open `options` object
	sort: [ // Open a `sort` array
		'title', // Would first sort by `title` field in ascending order (A-Z).
		'-date_published', // Would next sort entries by the date they were posted in descending order (Z-A).
	]
});
```


---


###### Fields

- `fields` - allows you explicitly request only specified fields from the collection.

```javascript
// Example
db.find("my_collection", { // Open `options` object
	fields: [ // Open `fields` array
		'title',
		'slug',
		'cover',
		'date_published',
	]
});
```


---


###### Limit

- `limit` - tells the API how many entries to return.

```javascript
// Example
db.find("my_collection", { // Open `options` object
	limit: 1, // Returns a single result (still as an array) 
});
```


---


###### Page

- `page` - tells the API how many entries to skip based on the provided `limit` *(default: 20)*.

```javascript
// Example
db.find("my_collection", { // Open `options` object
	page: 2, // Returns a single result (still as an array) 
});
```


---


###### Populate

- `populate` - allows you to choose which relational data to fetch with the entries.\n
Sometimes, data from other tables is stored as a relation ID so you don't have to keep a full record on every individual entry.\n
To use that ID to get related data without extra requests, you can enable the field in the `populate` object.

```javascript
// Example
db.find("my_collection", { // Open `options` object
	populate: { // Open the populate object
		cover: true, // Will return the full related data for the `cover` media object.
	}
});
```
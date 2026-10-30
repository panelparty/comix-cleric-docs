# Data Requests <!-- order: 1 -->

How to get data to and from the server safely.

---


### Conventions

This project is built using [SvelteKit](https://svelte.dev/docs/kit/load) and has made almost no modifications to how it handles requests.

When creating server-side requests for sending or fetching data (reccommended), you will need either a `+server.js`, `+page.server.js` or `+layout.server.js` depending on the context.

> [!TIP]
> We are working on a quick-start guide for SvelteKit, so keep an eye out for that!

If the request exists as an endpoint (something that doesn't need a page, it only returns data), use a `+server.js` file.

If the file needs to return data to a page or entire layout, use the `+page/+layout.server.js` files respectively.


##### Fetching data

More specific examples are provided in the respective API pages, but here is a broad overview of how to use SvelteKit to get data from a database.

We rely on standard SvelteKit `load` functions to fetch data from the server-side.

`locals` is part of a provided `event` object, which contains handy information and helpers, or even completely custom values!

In the following example, `comixCleric` is your access to the main API, `db` tells the API this is a database request, and `find` tells the database we're looking for something.

```javascript
// +layout/+page.server.js
export const load = async ({ locals }) => {
	// Store the response in a variable called `updates` or `posts`
	const updates = await locals.comixCleric.db.find("updates");

	return { updates }; // `updates` is appended to a returned `data` object
};

// Or...

export async function load({ locals }) {
	const updates = await locals.comixCleric.db.find("updates");

	return { updates };
};
```

Which can be retrieved in a page or layout by doing the following:

```svelte
<!-- +layout/+page.server.js -->
<script>
	// Props (`data` is automatically populated from the server.)
	let { data } = $props();

	// Destructure server data
	let updates = data.updates; // Get the values of `updates` we returned from the server.
<script>
```

It is typically safer to load data this way, as you can manipulate the incoming data before it ever reaches the user's browser.

So, if you need to make sure certain sensitive fields are scrubbed or that a user is authorized to access certain information, you can run checks within this load function first before allowing the request to complete.


##### Sending Data

We generally use forms and form actions to complete create/update/delete requests.

Forms can be standard HTML, as long as the `name` field is included on each input and unique within the form.

```html
<!-- Example -->

<form method="POST">
	<input type="email" name="email" />
	<button type="submit">Submit</button>
</form>

```

To get custom response messages and toast popups, we also use another SvelteKit utility called `enhance`. This will override the form default functionality and allow you to use a custom handler function.

```html
<!-- Example -->
<script>
	async function handleSubmit() {
		// Events are passed-in automatically
		return async ({ result }) => {
			// Do something on response (success/fail)
		};
	};

	// Or...

	const handleSubmit = async () => {
		return async ({ result }) => {};
	};
<script>

<form method="POST" use:enhance={handleSubmit} action="/api?/joinNewsletter">
	<input type="email" name="email" />
	<button type="submit">Submit</button>
</form>

```

The `action` attribute in the previous example is the URL where the action exists. This can be co-located in a `+page.server.js` file, or as an isolated endpoint (as we typically do) using the same convention. The question mark in the URL comes at the very end of the file where the action is located. If co-located, you'd just use `?/<action-name>`.

```javascript
// /api/+page.server.js

// Open an `actions` object
export const actions = {
	// Create your actions as async functions:
	joinNewsletter: async ({ request }) => {
		const data = await request.formData(); // Gets all provided input data from the form.
		const email = data.get("email"); // Gets `email` from the submitted form inputs.

		// Actions to perform with this data...

		// Return what you need after completion or failure.
		return {};
	},
};
```

In this case, because many actions for our API use repeating patterns and outputs, we created a custom wrapper called `formAction` you can import and use for more consistent and secure actions.

Just use this function to wrap your anonymous async function in the action:

```javascript
// /api/+page.server.js
import { formAction } from "$lib/utils/api/handler.js";

export const actions = {
	// Create your actions as async functions:
	joinNewsletter: formAction(async ({ data, db, locals }) => {
		// `data` eliminates the need to use `const data = await request.formData();`
		const email = data.get("email"); // Gets `email` from the submitted form inputs.

		// Actions to perform with this data...

		// Success/failure is returned automatically, so this return is for anything else.
		return {};
		// Means any user can perform this action
	},
	{ // Open the optional parameters object.
		admin: false, // Means the user does not have to be an admin (default: true)
		user: false, // Means the user does not have logged-in (default: true)
	}),
};
```

This also provides direct access to our `db`, `auth`, `storage`, and `email` APIs without needing to add `locals.comixCleric` in before them. Just add them into the function parameters and you can use them like this: `db.create();`.


###### `formAction()` Anatomy

```javascript
// Anatomy
formAction(async ({
	...event, // All Svelte-provided event params (locals, request, parent, etc.)
	data, // Form input data (should probably change this to formData)
	db, // Shorthand for `locals.comixCleric.db`
	auth, // Shorthand for `locals.comixCleric.auth`
	storage, // Shorthand for `locals.comixCleric.storage`
	email, // Shorthand for `locals.comixCleric.email`
	user, // Shorthand for `locals.user` - exists if user is logged-in
	isAdmin, // Shorthand for `locals.isAdmin` - exists if user is an admin
}) => {
	// Your action functionality
},
// Optional `options` object
{
	admin = true, // Throws error if user is not an admin
	user = true, // Throws error if the user is not logged-in
	sanitizeUser = true, // Removes all sensitive user data
	logs = true // Enables error logging
})
```

---

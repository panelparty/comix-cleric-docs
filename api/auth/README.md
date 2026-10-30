# Authentication (auth) <!-- order: 4 -->

Handles authentication-related requests.

The authentication `auth` API is based on [Better-Auth](https://better-auth.com/) and uses its existing conventions accessed via our own adapters.

---


### Request Methods


###### List Users (read)

Lists all users, can accept filters.

```javascript
// Example
auth.listUsers({
	filterField: "role", // Filters by the `role` field
	filterOperator: "eq", // Filters using `equals` (exact match)
	filterValue: "admin", // Filters by values matching `"admin"`
});
```

- `query` - object *(optional)* - A search query to filter results.


---


###### Get User (read)

Gets a single user based on a provided ID.

```javascript
// Example
auth.getUser(id);
```

- `id` - string *(required)* - The ID of the entry.


---


###### Sign Up Email (create)

Creates a new user account based on the provided credentials.

```javascript
// Example
auth.signUpEmail({
	email: "email@example.com",
	password: "Password1234!",
	role: "user",
	username: "a.username",
	name: "a.username", // Holdover requirement from Better-Auth
	displayname: "A Cool Displayname",
	project_role: "Creator",
})
```

- `email` - string *(required)* - A valid email address
- `password` - string *(required)* - Min: 8, max: 32, uppercase, lowercase, one number, one special character.
- `role` - string *(required)* - A value that determins user permissions. (Default: 'user')
- `username` - string *(required)* - A unique name for identifying an account.
- `name` - string *(required)* - Same as `username`. Required by Better-Auth.
- `displayname` - string *(required)* - A cosmetic name; can use any characters.
- `project_role` - string *(optional)* - A cosmetic role; can be anything.


---


###### Sign In Email (POST)

Creates a new auth session based on the provided user credentials. The credentials must already exist in the database.

```javascript
// Example
auth.signInEmail({
	email: "email@example.com",
	password: "Password1234!",
})
```

- `email` - string *(required)* - The user's previously entered email address.
- `password` - string *(required)* - The user's previously entered password.


---


###### Reset Password (POST)

Validates a password reset request.

```javascript
// Example
auth.resetPassword({
	token: "<verification-token>",
	newPassword: "Password1234!",
})
```

- `email` - string *(required)* - The user's previously entered email address.
- `password` - string *(required)* - The user's previously entered password.


---


###### Create User (create)

Creates a new user record in the database without sending a confirmation.

```javascript
// Example
auth.createUser({
	email: "email@example.com",
	password: "Password1234!",
	role: "user",
	username: "a.username",
	name: "a.username", // Holdover requirement from Better-Auth
	displayname: "A Cool Displayname",
	project_role: "Creator",
});
```

- `email` - string *(required)* - A valid email address
- `password` - string *(required)* - Min: 8, max: 32, uppercase, lowercase, one number, one special character.
- `role` - string *(required)* - A value that determins user permissions. (Default: 'user')
- `username` - string *(required)* - A unique name for identifying an account.
- `name` - string *(required)* - Same as `username`.
- `displayname` - string *(required)* - A cosmetic name; can use any characters.
- `project_role` - string *(optional)* - A cosmetic role; can be anything.


---


###### Update User (update)

Creates a new user record in the database without sending a confirmation.

```javascript
// Example
auth.updateUser(id, {
	email: "email@example.com",
	username: "a.username",
	role: "user",
	name: "a.username", // Holdover requirement from Better-Auth
	displayname: "A Cool Displayname",
	project_role: "Creator",
});
```

- `id` - string *(required)* - The ID of the entry.
- `email` - string *(required)* - A valid email address
- `password` - string *(required)* - Min: 8, max: 32, uppercase, lowercase, one number, one special character.
- `role` - string *(required)* - A value that determins user permissions. (Default: 'user')
- `username` - string *(required)* - A unique name for identifying an account.
- `name` - string *(required)* - Same as `username`.
- `displayname` - string *(required)* - A cosmetic name; can use any characters.
- `project_role` - string *(optional)* - A cosmetic role; can be anything.


---


###### Delete User (delete)

Creates a new user record in the database without sending a confirmation.

```javascript
// Example
auth.deleteUser(id);
```

- `id` - string *(required)* - The ID of the entry.


---


###### Delete User (delete)

Creates a new user record in the database without sending a confirmation.

```javascript
// Example
auth.deleteUser(id);
```

- `id` - string *(required)* - The ID of the entry.


---
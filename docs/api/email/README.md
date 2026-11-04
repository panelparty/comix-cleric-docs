# Email (email) <!-- order: 5 -->

Here how to use the email adapter.

---


### Request Methods

###### Send (POST)

Sends a new email to a provided address. Can include a callback URL and verification token.

```javascript
// Example
email.send({type, to, url, token})
```

- `type` - string *required* - The type of email to send.
- `to` - string *required* - Where to send the email.
- `url` - string *optional* - A callback URL/API endpoint.
- `token` - string *optional* - The tokek needed for the callback, if required.


---
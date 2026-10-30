# Adapters <!-- order: 2 -->

Learn about the current database, storage, and email adapters.

> [!NOTE]
> We will expand adapter selection once we are able.

> [!IMPORTANT]
> We are currently working on a guide to creating your own adapters.

---

### Database

We currently offer 2 options for database adapters:
- `local` - A custom [SQLite](https://sqlite.org/) adapter to keep everything local to your server.
- `mongo` - A custom [MongoDB](https://www.mongodb.com/) adapter for cloud database management.

---

### Storage

We currently offer 1 option for storage adapters:
- `local` - An adapter that stores all uploaded files to your local server.

---

### Email

We currently offer 1 option for email adapters:
- `resend` - Uses the [Resend](https://resend.com/) API to send email without opening server ports.
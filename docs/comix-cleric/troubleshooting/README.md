# Troubleshooting <!-- order: 999 -->

Here are some things to check if Comix Cleric isn't working!

---

### "Server Not Found / Offline" Error Page

This typically means either the connection to the host has been lost, or the app was never run through the setup process. This message simply indicates that it cannot contact the database.

> [!TIP]
> We will add better setup processes as we are able. At this time, the app or host has no way of knowing if it has been setup or not, only if it can find relevant data from the server.

**Self-hosting:**
If you are self-hosting, make sure that your .env or Docker config is properly setup. Missing API keys or database directory may lead to this issue being persistent. If you are using local-only options, make sure that the `database` and `uploads` folders have correct read/write permissions.

**Hosting Plans:**
If you are on one of our hosting plans, make sure you have run the setup from the link you should have received via email when it was created. This email will be sent to the email address you currently use for your ComixCleric.com account. Account for your instance are completely separate to ensure that all data related to your site stays with your site and you never lose access.

If this error persists, please report the issue on our Discord server.

---

### Setup failed

Setup should only fail if credentials provided for the initial admin account are invalid.

Please make that you are providing:

1. A valid email address.
2. A username that contains no spaces or special characters aside from periods.
3. A cosmetic display name
4. A secure password (min: 8, uppercase lowercase letters, numbers, special characters)

It is also possible something broke on our end during an update.

If this error persists, again, please report the issue on our Discord server.

---

### Media upload failures

Media can fail to upload for a number of reasons. Most rarely it's a connection issue to storage. Some common issues are:

**Unsupported format:**
- We only support common, web-supported file types at this point.
- Images: .png, .jpg, .jpeg, .svg, .webp, & .gif.
- Audio: .ogg, .mp3, .wav.

**Too many items:**
We only allow bulk uploads of 999 items at a time.

**Bulk upload too large:**
We only allow bulk uploads of up to 256MB at a time.

**Image(s) too large:**
Images have a hard-limit of 10,000 x 10,000 pixels in size. Please consider resizing or cutting the image into smaller chunks.

---

-# More details coming soon.
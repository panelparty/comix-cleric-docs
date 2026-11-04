# Email <!-- order: 4 -->

Learn how to configure your server's email options.

---

> [!NOTE]
> We only support the Resend email adapter at this time. We have no real preference for this service, we simply didn't have time to test or build for other services.
>
> Learn more about our [adapters](/docs/self-hosting/adapters).

## Configuration:

To add an email adapter to your Docker or Node.js app, simply add `EMAIL_API_KEY` and `EMAIL_SENDER` to your `compose.yml` or `.env` file.

We currently only have a Resend adapter, which uses the Resend API to send email without needing to forward ports from your server.

Unfortunately, it does require you to sign-up for their services, but they have a generous free tier and you can verify one domain.

Once you've done that, though, you can visit Resend's dashboard and find the "API Keys" link in the sidebar.

Here, click "Create API Key" and follow the steps to create a new key.

- Name: A cosmetic name that helps you discern between keys.
- Permission: Access level of the key. (Sending only is fine)
- Domain: What registered domains are allowed to use the key.

> [!IMPORTANT]
> Remember to save the key in a safe location, because you cannot see it again after closing the page.

Add the new API key value to `EMAIL_API_KEY: YOUR_API_KEY_HERE`. As well, you should set your `EMAIL_SENDER` value to something like `Comix Cleric <noreply@example.com>` (the domain must be the same as the one you registered in Resend).

###### Docker
```bash
# docker-compose.yml or compose.yml
services:
	# Other settings...
  sveltekit:
		# Other settings...
    environment:
      # Other settings...
			EMAIL_API_KEY: YOUR_API_KEY_HERE
			EMAIL_SENDER: Comix Cleric <noreply@example.com>
```

###### .env
```bash
# .env
# Other settings...
EMAIL_API_KEY="YOUR_API_KEY_HERE"
EMAIL_SENDER="Comix Cleric <noreply@example.com>"
```
# Using Cloudflare <!-- order: 5 -->

Here you'll see how to use Cloudflare to publish your self-hosted Comix Cleric site to the web!

This will allow other people to view your webcomic, as well as automatically dealing with HTTPS, DDOS protection, and a few other cool things!

## Prerequisites

- Comix Cleric server set up on your home computer
- A [Cloudflare](https://cloudflare.com) account (it's free!)

## Getting started

Go to [Cloudflare](https://dash.cloudflare.com) and select the labele "Domains," then "Add a domain."

You should come to a page labelled "Add a Site." If you already have a domain, select "Connect a domain", otherwise select "Buy a domain". If you buy a domain from Cloudflare you should be able to skip most of the next section.

### Connecting a domain

On the "Connect your domain" page, you'll need to type in your domain name (ie, "example.com"). You can also enable some AI scraping prevention things here, which is recommended. Once you've finished selecting your settings, press on the "Continue" button.

It will ask you to select a plan for your domain. The free tier will be just fine for most use cases. Select that and you can press 'continue.'

In your domain provider's settings, you will need to change the nameservers to Cloudflare's.

As this varies from company to company, here are a few relevant articles:

- Porkbun: [https://kb.porkbun.com/article/22-how-to-change-nameservers](https://kb.porkbun.com/article/22-how-to-change-nameservers)
- Namecheap: [https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain/](https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain/)
- Godaddy: [https://www.godaddy.com/help/change-my-domain-nameservers-664](https://www.godaddy.com/help/change-my-domain-nameservers-664)

If the website you purchased a domain from is not listed, using your favourite search engine is recommended.

Once you have changed your nameservers, press on "I updated my nameservers". It may take a little while to update, and you'll have to refresh the page for it to show as being updated.

## Adding a new tunnel

Now that you've added your domain to your Cloudflare account, you can now add a new tunnel! A tunnel is a bridge between your computer and the internet. It lets you have your instance of Comix Cleric talk to the outside world without you needing to mess with port forwarding.

Go back to [dash.cloudflare.com](https://dash.cloudflare.com), and in the search bar look for "Tunnels". Select it, and then press on "Create Tunnel" on the top right area of the page. Give it a name like "my cool comix cleric instance", and it will give you instructions to set it up. If you are unaware what operating system or architecture you are, it is safe to assume that it is Windows, and 64-bit for computers built in the last decade, 32-bit for those earlier.

### Using `docker-compose`

If you are utilizing docker compose for your server, you should add this to your `docker-compose.yml` file:

```yaml
  cloudflared:
    image: cloudflare/cloudflared:latest
    container_name: cloudflared
    restart: unless-stopped
    command: tunnel --no-autoupdate run
    environment:
      TUNNEL_TOKEN: ${TUNNEL_TOKEN}
```

Then, in your `.env` file, add a line like this:

```env
TUNNEL_TOKEN=xxxxxxxxxxxxx
```

You can get the token by copying the command from Cloudflare and extracting the token. It'll provide something like this:

```sh
docker run cloudflare/cloudflared:latest tunnel --no-autoupdate run --token xxxxxxxxxxxxx
```

Take the part after `--token` and set it as your TUNNEL_TOKEN.

## Connecting to Comix Cleric

Now that your tunnel is connected, it's time to connect up your server to the world!

Select the tab "Routes" at the top of the page for your tunnel. Then, press on "Add route", then on "Published application". The domain that you added earlier should show up. If you want `comic.example.com` instead of `example.com`, you can put `comic` in the field for "Subdomain", else it should be left blank. Under "Service URL", this should be the local address of your server (likely `http://localhost:3366`)

> [!IMPORTANT]
> If you are using Docker or Docker Compose, you should use your container name instead, ie `http://sveltekit:3366`, as it can connect over the Docker network rather than your personal network; this will usually work better.

And...

That's it! You can press on "Add Route" and Cloudflare should complete all the magic for you. Now, anyone can access your Comix Cleric site!
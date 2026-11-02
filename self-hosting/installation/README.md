# Installation <!-- order: 1 -->

Here you'll learn how to install and deploy a new Comix Cleric app instance!

> [!IMPORTANT]
> If you have a better idea or want to see another deployment method supported, reach out on [Discord](https://discord.gg/vh7s79y2a3)!

---

## Getting Started

At this time, Comix Cleric requires a server/VPS with [Docker](https://docs.docker.com/get-started/get-docker/) and/or [Node.js](https://nodejs.org/en/download#:~:text=Or%20get%20a%20prebuilt%20Node.js) installed.

**Bare Minimum Specs:**
- CPU: 0.5 core
- RAM: 512MB
- Storage: 1GB

**Recommended Minimum Specs:**
- CPU: 1 core
- RAM: 2GB
- Storage: 10GB

Log into your host's panel and make sure that you are able to either request a VPS with root access or the ability to upload files to a Docker/Node.js environment.

Some options are:
- Vercel
- Digital Ocean
- Hetzner
- Linode/Akamai
- Dreamhost
- Hostinger
- Bluehost
- *And many others...*

-# We are not sponsored or endorsed by any of these companies or brands and cannot vouch for their services.

---

## Docker Container

### Official Docker Image (quickest method)

Create and upload the following Docker compose file to your server to get Comix Cleric running as quickly as possible!

This is the minimal config to get started:
```yaml
# docker-compose.yml or compose.yml
services:
  init-perms:
    image: alpine
    command: chown -R 1000:1000 /app/data /app/uploads
    volumes:
      - ./data:/app/data
      - ./uploads:/app/uploads

  sveltekit:
    image: panelparty/comix-cleric:latest
    container_name: comix_cleric
    restart: unless-stopped
    depends_on:
      init-perms:
        condition: service_completed_successfully
    ports:
      - 3366:3366
    volumes:
      - ./data:/app/data
      - ./uploads:/app/uploads
    environment:
      NODE_ENV: production
      ORIGIN: https://comic.example.com
      PORT: 3366
      COMIX_CLERIC_SECRET: REPLACE_THIS_SECRET_VALUE
```

After configuring and uploading the file to an *empty* directory (Example: `/var/cc-app`), run `docker compose up -d`. The app should now be running on port `3366` by default. Follow the later sections on getting the app live on the internet.

> [!TIP]
> Some versions of Docker use `docker-compose` instead of `docker compose`.

#### Updating

We reccommend *always* using the `latest` image of Comix Cleric. It does not upgrade automatically, but gives you simple access to `docker compose pull` which will grab a fresh copy of the latest version.

To run an update, first stop the running container with `docker compose down`, then run the pull command.

Once the new image has finished downloading, you can run the same `docker compose up -d` command to start it again.

If you choose to use a specific image, like `1.0.0`, you can upgrade by altering your image version in the `compose.yml` config to the latest version `panelparty/comix-cleric:1.2.3-beta`, running `docker compose pull`, and starting the app again.

> [!IMPORTANT]
> If you have pulled many new images in the past, they may be taking up too much of your system storage.
> You can run `docker image prune` to remove images that are currently not in use on your system.

### Custom Docker Image

Visit our [downloads](https://comixcleric.com/downloads) page or the releases page on GitHub and choose the version of Comix Cleric you'd like to work with:

- `release.zip` - Contains only the files you need to deploy Comix Cleric.
- `source.zip` - Contains the full source code of Comix Cleric for development.

Clone or download the source code to your machine and setup the development environment by running `pnpm i` in the project folder.

Make your required edits and then run `pnpm build` to output a `build/` directory. This directory will contain all the app code you need.

Configure your `compose.yml` and run `docker compose up -d --build` to create a local Docker image.

In production, you'll upload the `build/`, `dockerfile`, `compose.yml`, `pnpm-lock.yml`, and `package.json` to a server/VPS and run the same `docker compose up -d --build` command to create your Docker container there.

#### Updating

Updating follows the same process described in "Custom Docker Image" and will require manually removing and rebuilding the files for a new container.

> [!NOTE]
> There is currently no way to automate updates for this method, as custom sites may make changes we cannot foresee or plan around.

---

## Node.JS Server

### Download Source Code

Visit our [downloads](https://comixcleric.com/downloads) page or the releases page on GitHub and choose the version of Comix Cleric you'd like to work with:

- `release.zip` - Contains only the files you need to deploy Comix Cleric.
- `source.zip` - Contains the full source code of Comix Cleric for development.

### Environment Variables

Just as Docker needed certain config values to exists, so does Node.js. We will instead use a `.env` file to store the required config.

Copy the included `.example.env` as `.env` or create a new one.

Minimal config to run the app:

```bash
# .env
# Comix Cleric Config
COMIX_CLERIC_SECRET="REPLACE_THIS_SECRET_VALUE" # Keeps your site safe/unique

# Node.js Config
NODE_ENV="production"
ORIGIN="https://comic.example.com"
```

---

### Making the App Live

> [!IMPORTANT]
> This is highly dependent on your host. We will provide additional details as they become available.

#### Nameservers and DNS

Regardless of how you deploy, you'll most likely need to change your nameservers in your domain registrar's admin panel.

This may look something like:

```bash
ns1.myhost.com
ns2.myhost.com
ns3.myhost.com # May be hidden/unused
ns4.myhost.com # May be hidden/unused
ns5.myhost.com # May be hidden/unused
```

Simply replace the values with the ones provided by your host to allow you to connect your domain to their server IP.

##### DNS Records

Next, you'll want to make sure your host knows which domains and sub-domains your app will run on. 

You can add new records in your host's admin panel.

There are a few configurations for hosting an app:

- As the main site - `example.com`
- As a sub-domain - `comic.example.com`

Decided which is best for you, then create the **A records** to match.

This should look something like:

| Record | Hostname          | IP          | TTL     |
| ------ | ----------------- | ----------- | ------- |
| A/AAAA | example.com       | 192.168.0.1 | Default |
| A/AAAA | comic.example.com | 192.168.0.1 | Default |

#### Reverse Proxy Configuration

##### nginx

If you are using `nginx` as your proxy, create a config that points your domain name to the port you've chosen.

Navigate to `/etc/nginx/sites-available` and either create a new `.conf` file, or edit an existing config.

> [!IMPORTANT]
> If you create a new config file from scratch, you will need to "symlink" it to `sites-enabled`.
>
> You can do this by running `ln -s /etc/nginx/sites-available/comic.conf /etc/nginx/sites-enabled`.

Configs can take many different forms, but a general config for something like this would look like:

```
# Comix Cleric
server {
  server_name comic.example.com;

  location / {
    proxy_pass http://localhost:3366;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
  }

  listen 443 ssl;
  # SSL cert references
}
```

> [!TIP]
> More information is coming soon. Please consider contributing additional guidance in the [documentation repo](https://github.com/panelparty/comix-cleric-docs).

#### SSL Certificates

##### Why You Need SSL Certificates

All sites on the internet require SSL cerificates to run the sercure `HTTPS` protocol. This encrypts traffic to your site and makes sure that any site you visit is *reasonably* safe.

You may have seen some sites on `HTTP` protocol stating "Hackers may be trying to steal your information."

To avoid this fate for your site, you need to request SSL certificats, or "certs" to let everyone know you're trying to operate legitimately.

##### Generating Certificates

Luckily, this generally doesn't cost anything except some time and an email address.

Depending on your host and reverse proxy, you may need to install an official certificate generation tool, like `certbot`.

This can vary wildly depending on your needs, but in some cases, like for nginx, we need to run something like `certbot --nginx`. This will look over your nginx configuration(s) and request certificates for any found domains or subdomains, then configure them for you after successfully registering them.

> [!TIP]
> If you want to manually update your configs, run `certbot certonly --nginx` instead.

##### Renewal

There are certainw ays you can enable auto-renewal, but in this guide, we'll just talk about doing it manually.

All you need to do is run `certbot renew` and it will look for any outdated certificates and generate new ones.

---

#### Next Steps:

**[App Customization & Development](./customization)**
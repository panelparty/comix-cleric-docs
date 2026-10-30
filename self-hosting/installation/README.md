# Installation <!-- order: 1 -->

Here you'll learn how to install and deploy a new Comix Cleric app instance!

> [!IMPORTANT]
> If you have a better idea or want to see another deployment method supported, reach out on [Discord](https://discord.gg/vh7s79y2a3)!

---

## Getting Started

At this time, Comix Cleric requires a server/VPS with [Docker](https://docs.docker.com/get-started/get-docker/) and/or [Node.js](https://nodejs.org/en/download#:~:text=Or%20get%20a%20prebuilt%20Node.js) installed.

**Minimum specs:**
- CPU: 0.5 core
- RAM: 512MB
- Storage: 1GB

**Recommended specs:**
- CPU: 1 core
- RAM: 2GB
- Storage: 10GB

Log into your host's panel and make sure that your are able to either request a VPS with root access or the ability to upload files to a Docker/Node.js environment.

Some options are:
- Vercel
- Digital Ocean
- Hetzner
- Linode/Akamai
- Dreamhost
- Hostinger
- Bluehost
- *And many others...*

-# We are not sponsored or endorsed by any of these companies or brands.

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

After configuring and uploading the file to an *empty* directory (Example: `~/cc-app`), run `docker compose up -d`. The app should now be running on port `3366` by default. Follow the later sections on getting the app live on the internet.

> [!TIP]
> Some versions of Docker use `docker-compose` instead of `docker compose`.

### Updating

We reccommend *always* using the `latest` image of Comix Cleric. It does not upgrade automatically, but gives you simple access to `docker compose pull` which will grab a fresh copy of the latest version.

If you choose to use a specific image, like `1.0.0`, you can upgrade by altering your image version in the config to the latest version `panelparty/comix-cleric:1.2.3-beta` and running `docker compose pull`.

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

### Starting the Reader & Admin Panel

> [!TIP]
> If you are testing locally, skip the first step.

1. In a terminal, open an `ssh` connection to your server. This normally looks like: `ssh root@myappdomain.com` or `ssh <user-id>@<server-ip>`.

2. Create and move into a new directory on your server. Example: `mkdir cc-app && cd cc-app`

3. Upload and unpack the files to a new directory. Example `my-cc-app`

4. Make sure that at least `package.json`, `pnpm-lock.yaml`, `dockerfile`, `compose.yml`, & `/build` exist there. Those are the core files needed to run Comix Cleric.

5. In the `dockerfile` & `docker-compose.yml`, you will find a few instances of a port number. The default is fine, assuming you don't have something using that port at the time. You can also change this to any port number you wish, also assuming that's it's not *already in use*.

> We also advise that you give your Docker container a unique name, just in case you want to run other types of applications.

> [!NOTE]
> Some environments differ. The following commands with either be `docker compose` or `docker-compose` depending on your installation. If one doesn't work, try the other.

6. Run `docker compose up -d --build` to start up the Comix Cleric reader and admin panel.

> A quick & dirty breakdown of this command is: `docker compose` (or `docker-compose`) initiates an operation with a `docker-compose.yml` file; `up` says you'd like to launch the container; `-d` tells the terminal process that you'd like it to continue in the background using the "default driver", & `--build` tells it that you need to build the container image (app) from the instructions in the `dockerfile`.

---

### Making the App Live

> [!IMPORTANT]
> This is highly dependent on your host. We will provide additional details as they become available.

##### Nameservers and DNS

Regardless of how you deploy, you'll most likely need to change your name servers in your domain registrar's admin panel.

This may look something like:

```bash
ns1.myhost.net
ns2.myhost.net
ns3.myhost.net # May be hidden/unused
ns4.myhost.net # May be hidden/unused
ns5.myhost.net # May be hidden/unused
```

##### DNS Records

Next, you'll want to make sure your host knows which domains and sub-domains your app will run on. 

You can add new records in your host's admin panel.

There are a few configurations for hosting an app:

- As the main site - `example.com`
- As a sub-domain - `comic.example.com`

Decided which is best for you, then create the A records to match.

##### Reverse Proxy Configuration

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
  client_max_body_size 1G;

  location / {
    proxy_pass http://localhost:3366;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_busy_buffers_size 512k;
    proxy_buffers 4 512k;
    proxy_buffer_size 256k;
  }

  listen 443 ssl;
  # SSL cert references
}
```

---

### Taking the App or Database Offline

In both cases, you will need to be either in the main app or api directory, and run `docker compose down`. This command will look for the container in the active directory and tell Docker to stop running it immediately. To stop both, you will have to run this command in each respective directory.

---

#### Next Steps:

**[App Customization & Development](./customization)**
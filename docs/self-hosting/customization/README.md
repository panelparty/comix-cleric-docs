# Customization <!-- order: 2 -->

Here is a basic overview of how to customize your Comix Cleric app via code!

---

### Basic Customization

Most of Comix Cleric's no-code / low-code customization options are found in the admin panel!
For a more comprehensive look at these features, check out the [Admin Panel](/docs/comix-cleric/admin-panel) docs!

---

### Developing with Comix Cleric

##### Requirements

###### Development Tools (IDE)

To start customizing Comix Cleric, we highly recommend using an <abbr class="underline decoration-dashed" title="Integrated Development Environment">IDE</abbr>, such as Visual Studio Code, Zed, or JetBrains. A normal text editor and system terminal would work, but that's a lot of manual typing!

> [!IMPORTANT]
> We are aware that many of these IDEs have AI integrations.
> To avoid this, Zed has a simple "Disable AI" toggle in their settings.
> VSCodium also provides binaries (executables) that are free of Microsoft's default "product configurations" (no Copilot by default).

###### Node.js & NPM

Because this app is mainly built using [SvelteKit](https://svelte.dev/docs/kit/introduction), you'll need to have [Node.js](https://nodejs.org/en/download/archive/v22.14.0) & [NPM](https://www.npmjs.com/) installed. NPM is normally packaged with the Node.js installer.

> Comix Cleric is currently built using Node.js v22.14.0

###### Source Code

You will also need to download and unpack the source code from the official Comix Cleric GitHub repo.

---

##### Starting Your Local Server

To begin developing Comix Cleric, open a terminal, either in your OS or IDE. Make sure that the terminal is open in the directory where you upacked the source files.

Run `pnpm i` (which is shorhand for `pnpm install`). This will begin downloading and installing the required dependencies.

> [!NOTE]
> These dependencies are only installed to the current working folder. Only things manually installed with the `-g` or "global" flag will be installed to a system folder.
>
> To remove all installed dependencies from your machine, simply delete the `node_modules` folder.

If the install was successful, you can now run `pnpm dev --open` to start a local development server.

At this stage, you will also need access to a data source. You can either use an existing API URL, such as a project you're already hosting, or you can install Docker and run a database instance locally.

> [!NOTE]
> There is no drawback to using the local server. Any changes made can be easily added to your server. We honestly advise that you pull a copy of your database and use it to develop locally, if possible, just to avoid catastrophy. Back-ups are important!

> [!IMPORTANT]
> Proper instructions for updating API URL coming soon.

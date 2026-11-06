# SvelteKit Quick-Start: Intro & Basic Syntax

This guide helps you dive deeper into the SvelteKit / Svelte 5 component syntax.

-# Written by: Kevin Grawlich

---

> [!IMPORTANT]
> This guide assumes you have prior knowledge of at least intermediate HTML, CSS, and JavaScript.

## What is SvelteKit?

[SvelteKit](https://svelte.dev/docs/kit/introduction) is a first-party web application framework for [Svelte](https://svelte.dev/docs/svelte/overview), a UI framework that makes templating, components, and JavaScript functionality in your HTML a breeze!

> ###### *"What is a framework...?"*
>
> A framework, generally speaking, is a collection or ecosystem of tools, code compilers, and other integrations that convert special syntax into functional native web code and applications.

It might sound like a pretty big topic, but at its core, it's just the HTML, CSS, and JavaScript you're used to, with some shortcuts to make connecting the dots easier.

It's *much* more than that, but doesn't have to be!

---

## How does it work?

SvelteKit uses Svelte as a UI framework, which has a simple syntax that gives you a ton of power over how you approach your site code.

Let's do a quick comparison to standard HTML, CSS, and JavaScript.

Here's a basic example of changing the inner text of HTML elements. In HTML & JavaScript, this can get a bit long-winded, especially if you need to target multiple different elements:

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
		<h1 class="main-heading">[USERNAME]'s Profile</h1>
		<p class="user-bio">[USERNAME]'s Bio</p>
		<h6 class="user-stats">[USERNAME]'s Stats</h6>

		<script src="./script.js"></script>
	</body>
</html>
```

```js
// script.js
// Get element references
const mainHeading = document.querySelector(".main-heading");
const userBio = document.querySelector(".user-bio");
const userStats = document.querySelector(".user-stats");

// Value to use
const username = "Steve";

// Helper to replace specific text when found
function replaceUsername(element) {
	element.innerText = element.innerText.replaceAll("[USERNAME]", username);
};

// Replace text on those elements
replaceUsername(mainHeading);
replaceUsername(userBio);
replaceUsername(userStats);
```

> [!NOTE]
> There are shorter ways to write the above example, but this is a simple approach we chose.

---

## Installation

> [!IMPORTANT]
> You must have [Node.js + NPM](https://nodejs.org/en/download#:~:text=Or%20get%20a%20prebuilt%20Node.js%C2%AE%20for) installed on the machine you plan to develop with.

Installing SvelteKit is as simple as:

1. Create a new project folder, like `my-app`
2. Open a terminal in that folder
3. Run `npx sv create` and follow the on-screen instructions
		- Template to install (SvelteKit minimal or demo)
		- Type checking options (your choice)
		- Addons you'd like to try (your choice)
		- Package manager to install dependencies (npm)
4. Run the development server with `npm run dev` and open a browser at `http://localhost:5173/`


## Basic Syntax

Svelte shortens the above example significantly by giving you something called "template syntax", which is just a set of curly braces (`{}`) with JavaScript in between! It effectively just converts the value of whatever you give it into plain text.

Converting the previous example to Svelte syntax would look like this:

```svelte
<!-- /src/routes/+page.svelte -->
<script>
	const username = "Steve";
</script>

<h1 class="main-heading">{username}'s Profile</h1>
<p class="user-bio">{username}'s Bio</p>
<h6 class="user-stats">{username}'s Stats</h6>
```

You are still able to use all those JavaScript concepts you learned, but you can trim out a lot of the tedious stuff, like targeting elements (although you still can, and it's *also* easier).

It is not limited to text, it only *outputs* text, so you can do math or any other complex JavaScript logic, so long as it returns a result.

Here's how I like to think about Svelte/SvelteKit:

It is as free-form as you want to be, as long as you're following their basic conventions. You are only really locked-in to using specific names for route files, which we'll talk about later.

Here are a few more examples:

```svelte
<!-- Copyright.svelte -->
<script>
	const yearEstablished = "1999";
	const yearCurrent = new Date().getFullYear();
</script>

<!-- Will insert the current year (2026) instead of just `new Date().getFullYear()` -->
<p class="copyright">My Site &copy; {yearEstablished} - {yearCurrent} My Name</p>
```

```svelte
<!-- Calculated.svelte -->
<script>
	const calculation = 256 * 8 - 13;
</script>

<!-- Will insert the result of the math operation, `2035` -->
<p class="math">Your number: {calculation}</p>
```

### Component Structure

Svelte is written using `.svelte` files, and can contain a `<script>` tag for local JavaScript, a `<style>` tag for local CSS, and *any number* of plain HTML elements and special Svelte tags and components. Also, those HTML tags do not need a wrapping element, unless you want one. They can just sit freely in file.

```svelte
<!-- Basic Svelte File Layout -->
<script>
	// JavaScript
</script>

<!-- Any HTML elements -->

<style>
	/* Local CSS styles */
</style>
```

But, a Svelte file can also just contain plain HTML markup and no script or styles.

```svelte
<!-- Minimal File Example -->
<!-- This is still valid for an entire .svelte file -->
<p>I'm just text!</p>
```

Notice that these `.svelte` files don't have the usual HTML boilerplate. Svelte works as something called a "component." It is a snippet of reusable code that can be imported throughout your app as needed. Svelte is typically used in conjuction with another app framework to make it most effective at its job.

SvelteKit was built as a direct way to use Svelte in its ideal environment. In SvelteKit, there is a single `/src/app.html` that is set up automatically to use the page, layout, and element components without copying boilerplate over and over.

### Project Structure

The basic project structure should look something like this:

```bash
# Basic Project Structure
├── src/
|  ├── app.html
|  ├── lib/
|  └── routes/
|     ├── +layout.svelte
|     └── +page.svelte
├── static/
├── jsconfig.json
├── package.json
├── README.md
└── vite.config.js
```

Mainly, we need to focus on what's inside the `/src` directory. That's where all your main site code will live.

Inside `/src`, you'll generally find 3 things:
- `/src/lib` - An asset *library* for any custom code, files, or components you need to import to other files.
- `/src/routes` - All your app pages will live here.
- `/src/app.html` - The basis of your app (you should not need to edit this, generally)

Don't let this worry you, though. SvelteKit is pretty flexible, and as long as you can give a correct path to your imports, they can kinda live anywhere you want, even *outside* the `/src` directory.

### Pages & Routing

To work with routes (or pages) in SvelteKit, you simply need to define your expected structure in the filesystem under the `/src/routes` directory.

For example, if you wanted to have an About page, you'd just need to add a `/src/routes/about/+page.svelte` file. SvelteKit will turn this into `example.com/about` automatically.

Beyond that, you tend to just write your pages as you normally would, with the exception that anything that needs to stay the same page-to-page should be placed inside a parent `+layout.svelte` file. Things like your header, footer, etc.

A basic SvelteKit page layout could look like this:

```svelte
<!-- /src/routes/+layout.svelte -->
<script>
	let { children } = $props();
</script>

<header></header>
<main>
	{@render children()}
</main>
<footer></footer>
```

The only things in there we haven't covered yet is `let { children } = $props();` and `{@render children()}`:

- `let { ... } = $props();` - This is how you define custom component properties, or "props." You can create as many as you need within the curly braces.
- `{@render ...}` - This is how you tell Svelte the prop should be rendered as element(s) instead of text values. It essentially creates a "slot" in your code.
- `children` is the default slot and is used by Svelte to say "anything nested directly in this component tag should show up here." So, in this case, adding any elements to a `+page.svelte` will pass those elements directly into the layout.

```svelte
<!-- Example -->
<script>
	import MyComponent from "./MyComponent.svelte";
</script>

<MyComponent>
	<p>I will appear in the `children` slot!</p>
	<p>I will, too!</p>
</MyComponent>
```

You can also name slots, and have them anywhere you need! (This is part of how we handle the reader navigation):

```svelte
<!-- MyComponent.svelte -->
<script>
	// Props
	let {
		children,
		header,
		navigation
	} = $props();
</script>

<!-- Wrapper -->
<div>
	<!-- Top navigation slot -->
	{@render navigation?.()}

	<!-- Header -->
	<header>
		<!-- Label slot -->
		{@render header?.()}
	</header>

	<!-- Inner wrapper -->
	<div>
		<!-- Default slot -->
		{@render children?.()}
	</div>

	<!-- Bottom navigation slot -->
	{@render navigation?.()}
</div>
```

You can just pass in the element using `{#snippet slotName()}`:

```svelte
<!-- Example -->
<script>
	import MyComponent from "./MyComponent.svelte";
</script>

<MyComponent>
	<!-- `children` -->
	<p>I will appear in the `children` slot!</p>
	<p>I will, too!</p>

	<!-- `navigation` -->
	{#snippet navigation()}
		<p>I will appear in all of the `navigation` slots!</p>
	{/snippet}

	<!-- `header` -->
	{#snippet header()}
		<p>The slots can be added in any order!</p>
	{/snippet}
</MyComponent>
```

### Importing CSS & JavaScript

We'll talk more about props soon, but for now, let's talk about importing CSS and other assets. We previously mentioned that you can use a `<style>` tag in your routes for adding CSS local to that file, but what about external CSS files?

Svelte tries to simplify this process by allowing you to just import it in the `<script>` tag and it is consumed automatically. For example, our layout from earlier can contain a reference to the global CSS file:

```svelte
<script>
	// Global CSS
	import '../app.css';

	// Props
	let { children } = $props();
</script>

<header></header>
<main>
	{@render children()}
</main>
<footer></footer>
```

And that's it! Just add the relative path to your CSS file in the base layout, and it is now available throughout your app!

External JavaScript is imported a similar way, but usually requires you to import something specific, like `import { myFunction } from "$lib/functions.js";`. This will not make it globally available, like the CSS, however. Installed NPM packages are also imported this way: `import { find } from "lodash-es";`

`$lib` is a shorthand/alias to access the `/src/lib` directory directly.

> [!IMPORTANT]
> In recent versions of SvelteKit, this was changed to `#lib` instead, so this convention will also change for us soon.

### Element Components

One of the last basic concepts we can cover is components. Now, I know we've already *kind of* covered them, since technically any `.svelte` file is a component. More specifically, I want to cover non-route components, or components that act more like HTML elements.

They are structurally exactly the same, but you can make them whatever you want. A button, form inputs, containers, text displays, even entire self-contained games.

Not everything *needs* a component, but if there's something you find yourself re-writing the exact same code or feel you could use a template for something, that's where components come in!

We can use all of our prior concepts to create a reusable button:

```svelte
<!-- /src/lib/components/Button.svelte -->
<script>
	let { children } = $props();
</script>

<button type="button" class="component-button">
	{@render children?.()}
</button>

<style>
	.component-button {
		background: skyblue;
		padding: 4px 8px;
		color: black;
		border: 1px solid black;
	}
</style>
```

> [!TIP]
> It is standard convention to name components in "Pascal case" or capitalize each starting letter, no spaces or punctuation: `ComponentName.svelte`

Also, we've added optional chaining `?.()` to the slot, which just tells SvelteKit that this component may or may not receive child elements. Without the `?.` it would throw an error if you did not nest anything inside the component when using it because SveltKit expects it to exist.

Now, if you import that button anywhere, it will look and work exactly as you styled it. To be fair, the above example could just be done in plain HTML and CSS, but you can do so much more!

Just for an advanced example I don't expect you to fully grasp at this stage, we can make this button into a pretty decent template:

```svelte
<!-- /src/lib/components/Button.svelte -->
<script>
	let {
		children,
		type = "button",
		class: className,
		preset = "default",
		...restProps
	} = $props();
</script>

<button {type} class="component-button {className}" data-preset={preset} {...restProps}>
	{@render children?.()}
</button>

<style>
	.component-button {
		padding: 4px 8px;
		color: black;
		border: 1px solid black;
	}
	.component-button[data-preset="default"] {
		background: skyblue;
	}
	.component-button[data-preset="danger"] {
		background: red;
	}
	.component-button[data-preset="warning"] {
		background: goldenrod;
	}
	.component-button[data-preset="success"] {
		background: springgreen;
	}
</style>
```

To simply explain some of these things:
- `type` is going to be passed as the HTML attribute `type` for button to use, defaults to `button`.
- `class: className` - The word `class` is reserved in JavaScript, so we have to "alias" it internally to something else, like `className`, so we can access it as `class` like a normal HTML element.
- `preset` - Is a custom data type that we can use to easily use style presets we define.
- `...restProps` - Just passes any other HTML attributes/props you give the component.
- `data-preset="..."` - Is a custom HTML attribute we can target with CSS. It is not Svelte-specific.

Another cool thing there is replacing `type="button"` with `{type}`. If a prop shares a name with another existing prop or HTML attribute, you can simply add it without the `attribute=` part. It saves you from writing `attribute={attribute}`.

> [!IMPORTANT]
> CSS provided directly to a component file is "scoped" will only ever affect the elements in this file. To make it affect any other elements in your app with the same class name, either place the CSS in your global stylesheet, or use `:global(.class-name) {}` in your component file.
>
>```svelte
><!-- Example --> 
><p class="caution-text">Danger!</p>
>
><style>
>   /* Will affect other .caution-text elements throughout the app */
>	 :global(.caution-text) {
>		  color: red;
>   }
></style>
>```

### Using Components

We've talked about building components, but what about *using* them? You just need to import them into the files where they are needed and use them like any other HTML element (notice the import does not have curly braces):

```svelte
<!-- Example -->
<script>
	// Components
	import Button from "$lib/components/Button.svelte";

	// Actions
	function buttonAction() {
		console.log("Action triggered!");
	}
</script>

<!-- Default button with text -->
<Button>Click Me!</Button>

<!-- Danger-style button -->
<Button preset="danger">Delete Post</Button>

<!-- Warning-style button with onclick event -->
<Button preset="warning" onclick={()=>{buttonAction()}}>Run action</Button>

<!-- Success-style button for form submissions -->
<Button type="submit" preset="success">Submit</Button>
```

The coolest part (to me anyway) is now if you need to update functionality for all the buttons, you just have to edit the main component file! This can be done for nearly any element you can imagine.

Generally, it is best to stick with semantic HTML conventions to maintain basic web accessibility.

---

#### Next Steps:

There is still much to cover, so head over to the [Intermediate](/docs/guides/sveltekit-quick-start-intermediate) guide for your next steps.
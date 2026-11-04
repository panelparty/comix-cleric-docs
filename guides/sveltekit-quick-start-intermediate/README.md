# SvelteKit Quick-Start: Basics

This guide serves as a crash-course in getting started with the SvelteKit / Svelte 5 syntax.

---

> [!IMPORTANT]
> This guide assumes you have prior knowledge of Svelte and/or have read the [Basics](/docs/guides/sveltekit-quick-start-intermediate) guide.

### Intermediate Syntax

Let's move onto slightly more advanced concepts, but still simple enough you'll use them quite often.

#### Conditionals & Loops

If you've worked with JavaScript for any amount of time, you may know about conditionals (if-statements) and loops (each, for, while, etc.).

Svelte has a way to handle these directly in HTML using template syntax.

Conditionals can be handled a couple of ways:
1. Using the `{#if}{:else}{/if}` template.
2. Using a "[ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator)" `{condition-value ? true : false}`.

What you'll want/need to use depends heavily on the context, but generally, conditional templates are used for showing/hiding things with JavaScript, and ternary operators are for one-line template values.

Template conditional:

```svelte
<!-- HideText.svelte -->
<script>
	let {
		show = false
	} = $props();
</script>

<!-- Simple show/hide -->
{#if show}
	<p>Element is showing!</p>
{/if}

<!-- Provide an alternative value -->
{#if show}
	<p>My email address: admin@example.com</p>
{:else}
	<p>You're not allowed to see this.</p>
{/if}
```

> [!NOTE]
> This also supports `{:else if condition}` to provide more checks than binary true/false.

Ternary conditional:

```svelte
<!-- HideText.svelte -->
<script>
	let {
		show = false
	} = $props();
</script>

<!-- Swaps text based on `show` value -->
<p>My email address: {show ? "admin@example.com" : "********"}</p>
```

As for loops, they work very similar. You'll use `{#each}{/each}` templates and place what you want rendered for each item inside:

```svelte
<!-- GreetingList.svelte -->
<script>
	const array = [
		"Hello!",
		"Good morning!",
		"Good day!",
		"Good afternoon!",
		"Good evening!",
		"Good night!"
		"Goodbye!"
	];
</script>

<!-- Renders a list of all greeting items in `array` -->
<ul>
	{#each array as item}
		<li>{item}</li>
	{/each}
</ul>
```

If you need access to the `index` (current item number) in the array, just provide a second output value like `i` or `index` to the loop, like `{#each array as item, i}`. `i` will then output its current position/number in the list. This is useful if you need to check where we are in the loop for things like skipping a specific item or giving it special treatment from other list elements.

You can also use loops without explicit array values by giving `{length: number}` as the array:

```svelte
<!-- Creates 4 boxes -->
{#each {length: 4}}
	<div class="box"></div>
{/each}
```

#### Rendering Text to HTML

You can use Svelte to parse text values into raw HTML for your site to show.

> [!CAUTION]
> Be aware that you should only provide safe values to this template. There is a **high risk** of XSS (cross-site scripting) attacks if you allow any user-generated HTML in your site without sanitizing (removing malicious patterns from) the values before rendering them.

Assuming you are the only person in control of your app contents, though, you can provide HTML as a string/text and use `{@html value}` to use it as plain HTML.

```svelte
<script>
	const textHTML = "<h1 class='heading-one'>Heading One</h1>";
</script>

<!-- Should render the text as HTML instead of plain text. -->
{@html textHTML}
```

> [!IMPORTANT]
> You cannot apply local CSS this way as Svelte doesn't technically know about the new HTML and can't scope the required styles. You must make it global as briefly mentioned earlier.

#### Reactive Variables

Something Svelte is widely known for at this point is being able to define reactive JavaScript, or values that can update automatically wherever they are used. Technically, JavaScript can already allow for changes to values via the `let` variable type, but in Svelte, you do have to be explicit about what values you expect to be updating throughout your application. To do that, you have a few options, the three main ones being:

- `$state()` - Defines a value that is expected to be updated.
- `$derived()` - Defines a value that depends on another value that could change and should update itself accordingly.
- `$derived.by()` - Similar to the previous, but allows you to provide a closure/function that returns a value based on other reactive values, also updates automatically.

The latter two are more important when we talk about loading data from outside the component.

To start with `$state()`, define a variable as you normally would with `let`, but wrap the initial value in `$state()`. This example is similar to the one before where we provided a `show` prop to control the visibility. We can do that again, but only use it within the component to track the value state.

> [!TIP]
> Component props are already reactive!

```svelte
<script>
	// Reactive value state
	let show = $state(false);
</script>

<!-- Flips the current value of `show` -->
<button onclick={()=>{show = !show}}>{show ? "Hide" : "Show"} Value</button>

<!-- Only displays if `show` is `true` -->
{#if show}
	<p>I am the toggled value!</p>
{/if}
```

`$derived()` is a bit more involved, but essentially just lets you tell Svelte that the value depends on another reactive/state value.

Like, a simple example provided by Svelte, is doubling the count of another value automatically as it changes:

```svelte
<script>
	let count = $state(0);
	let doubledCount = $derived(count * 2);
</script>

<p>Count: {count}</p>
<p>Doubled Count: {doubledCount}</p>
<button onclick={()=>{count++}}>Increase Count</button>
```

`$derived.by()` is the most complex of the three, but allows you to basically put an entire function inside the parenthesis:

```svelte
<script>
	let count = $state(0);
	let multipliedCount = $derived.by(()=>{
		const factor = 5;
		return count * factor;
	});
</script>

<p>Count: {count}</p>
<p>Multiplied Count: {multipliedCount}</p>
```

Now, these examples, to me, don't have a ton of practical uses, considering they are things that can be written more simply, like:

```svelte
<script>
	let count = $state(0);
</script>

<p>Count: {count}</p>
<p>Doubled Count: {count * 2}</p>
<button onclick={()=>{count++}}>Increase Count</button>
```

---

-# This guide is still being written, stay tuned for updates!
# Theme Settings <!-- order: 5 -->

Learn how to create and adjust custom app themes!

---

### Themes

This section allows you to preview/select a theme to apply globally!

##### Active Theme

This dropdown determines your active theme. You can select an item to preview it. The preview only runs in your browser, so a new theme is not applied until you save.

> [!TIP]
> If the dropdown is highlighted, but not opened, you can use your up/down arrow keys to quickly cycle through the theme previews!

##### Custom Themes

This is a list of custom themes currently in your database.

There should be an exiting theme by default when setting-up your app for the first time. You may use the "download", "edit", and "delete" buttons on each theme item to manage exiting themes.

This area also provides the option to add a theme you've already generated, or to open the integrated Theme Generator.

---

### Custom Themes

This sections displays all of your created custom themes. Each item can be downloaded, edited, or deleted via the buttons on the right-hand side.

##### Add New Theme

To create a new custom theme, click the "+ Add Theme" button next to the section label.

When creating a new theme, you should (now semi-integrated) Theme Generator in your app (typically found by going into your admin panel's themes page and clicking "open generator") to create a base theme.

Select from their presets, or otherwise have a `.css` file already generated matching the Skeleton theme patterns and import it.

View this [guide](https://comixcleric.com/docs/guides/create-theme) on how to effectively utilize the theme generator. We know it's not super simple to understand.

Since these themes are just CSS files, feel free to share them with others!

> [!WARNING]
> CSS can still contain arbitrary JavaScript code. We do our best to keep things secure, but always ensure that you are vetting your sources before blindly importing/applying a theme.

##### Customizing Themes

Since these are just CSS, you can technically overwrite any styles in the app! We are going to be improving support for this as time goes on. For now, direct options are quite limited to what is in the Skeleton CSS theme settings, but feel free to tinker!

> [!TIP]
> In the near future, this system will either be more fleshed-out or replaced entirely by something better. Keep an eye out for our community polls on Discord!

##### Custom Fonts

Font uploads are not supported at this time. For now, while not the most elegant solution, you can add an `@import` rule to pull a font from a source like [Google Fonts](https://fonts.google.com/) or [Bunny Fonts](https://fonts.bunny.net/) (I'd suggest the latter if you have concerns about Google's privacy issues.)

You can add it to the top of your theme and replace the `--base-font-family` to change the font for everything, or add it only to `--heading-font-family` to change only HTML heading tags or `--anchor-font-family` to change only link fonts. If you want everything to use the same global font, set the base fomt family, then set headings and anchor to `inherit`, which is a CSS feature that just looks at the last provided value from a parent element.

```css
@import url(https://fonts.bunny.net/css?family=akronim:400|balsamiq-sans:400,400i,700,700i);

[data-theme="my-theme"] {
  --text-scaling: 1;
  --base-font-color: var(--color-surface-950);
  --base-font-color-dark: var(--color-surface-50);
  --base-font-family: "Balsamiq Sans"; /* Add new base font here */
  --base-font-size: inherit;
  --base-line-height: inherit;
  --base-font-weight: normal;
  --base-font-style: normal;
  --base-letter-spacing: 0em;
  --heading-font-color: inherit;
  --heading-font-color-dark: inherit;
  --heading-font-family: "Akronim"; /* New heading font here */
  --heading-font-weight: bold;
  --heading-font-style: normal;
  --heading-letter-spacing: inherit;
  /* ... */
}
```

Bunny Fonts can be a little more obtuse to use when selecting font styles (weights), but there is a `+Fonts` button in the upper right of their UI that opens a drawer from the side. You may need to switch the first panel in the list to CSS instead of HTML to get the `@import` rule.

Google Fonts is much the same, but there is a handbag icon in the same upper-right location that takes you to your current font selections and has options to import/download on the right. Click "Get embed code" and in the right-hand panel, change the `<link>` option to `@import` to get the import rule you need.

> [!TIP]
> If you still want to use Google Fonts, but increase privacy for your users, replace `fonts.google.com` with `api.fonts.coollabs.io` which provides the fonts without allowing Google to gather data about your site.

It is recommended that you set fallbacks for your selected fonts in case they become temporarily or permenently unavailable. You can easily do this by comma-separating the family names:

```css
--base-font-family: "My Custom Font", "Poppins", system-ui, sans-serif;
```

You can set any number of fallbacks you'd like.

##### Deeper Styling

We are currently in the process of converting much of the Tailwind prototype code to plain CSS classes.

Some classes are made available directly from the components using the `:global()` selector. This is partially to keep the `app.css` as small as possible, but is also a requirement of the UI libraries we use, as any applied style must be globally available.

Svelte provides the `:global()` selector to make sure that the class can be modified from anywhere in the app as if it was imported from a global stylesheet.

If you are modifying these classes from your theme, you do not need to use the `:global()` selector, and can simply target the classes directly, as you normally would.

Example:
```css
[data-theme="my-theme"] {
  /*Theme code*/
}

/* Component styles */
.author-avatar {
  /* Customize author avatar styles */
}
```
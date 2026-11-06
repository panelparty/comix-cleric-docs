# Creating a Custom Theme

This guide covers creating a custom theme for your Comix Cleric app.

-# Written by: Kevin Grawlich

---


### Themes Overview

In the **Themes** page, you have the option to add edit and download your themes.

By default, you should have one custom theme registered and applied.

> [!WARNING]
> Built-in themes cannot be edited or downloaded at this time.

You can use the built-in text editor to directly modify the CSS code generated for the theme. You can either edit the CSS custom properties `--property-name` directly, or add custom CSS below the `[data-theme="theme-name"] {}` block.<br><br>

[Skeleton UI](https://www.skeleton.dev/) utilizes [Tailwind](https://tailwindcss.com/) for creating "utility classes" that we use throughout the app interface.

> [!TIP]
> We are working to make this experience easier overall, as the color output format is optimal for Tailwind, but not very easy to read or modify directly.

> [!NOTE]
> We are also working on converting much of the Tailwind to standard CSS classes to ease the pain of truly customizing your app.


---


### Quick Guide:

1. Visit the (now semi-integrated) Theme Generator in your app (typically found by going into your admin panel's themes page and clicking "open generator") and select a template under the `Import` tab or start editing the default set under `Build`.

2. Use the **Color Palette** menu on the right to adjust your colors, and the preview pane on the left to check your adjustments.

3. Use the other menus on the right for deeper control over the spacing, borders, and text/font of the theme.

4. When everything is looking how you want, click the **Code** button in the top right and copy/paste the code into a new theme in your admin panel or overwrite an existing one.

5. Set your active/current theme to the one you just made.

**Enjoy the new look!**


---


### Generating a New Theme

The easiest method of creating a theme for your site is to use the (now semi-integrated) Theme Generator in your app, typically found by going into your admin panel's themes page and clicking "open generator".

Here, you can access the import tab, and either import a CSS file you downloaded from the Admin Panel, or use one of their templates as a base!

Once you've imported your theme or selected a template, you should be taken directly the "Build" tab, where you'll make your actual adjustments.

The right-hand side is a preview window to show what your theme looks like applied to some of Skeleton's UI elements, which will be *relatively* similar to your app.

> [!TIP]
> We are actively working to improve the integration of the generator and give more accurate previews that pertain more to Comix Cleric.

**The left-hand sidebar contains your theme controls:**

##### Preview / Code

This is a toggle that changes between the theme preview and the code output. Set this to **Code** when you're ready to use your new theme.

##### Theme Name (Text Input)

This is an unlabelled field that contains the name of your theme. Skeleton automatically converts the title to something that plays well with HTML/CSS, so it may look different than what you've typed-out.

##### Color Palette

This menu provides access to all available theme colors for editing.

###### Clear All Palettes

Resets all colors to grey with default light-dark values.

###### Palettes

Each of the seven colors represent the midtone of each color set in the palette. Clicking these squares changes which color set is being edited.

###### Active Color Palette

The **"Seed"** button allows you to enter or paste a HEX value and output a new color set automatically.

The **"Random"** button allows you randomize the selected color set. It will always try to create colors light to dark within the same hue.

The **"All"** switch allows you to enable editing of individual colors in the set, rather than just the lightest, midtone, and darkest in the set.

**50** - Lightest color possible for the set.

**500** - The midtone, most likely the color you want the set based on.

**950** - Darkest color possible for the set.


---


### Customizing Color Sets

Generally, I choose my base (midtone) colors first. I sometimes use sites like [coolors.co](https://coolors.co/generate) to create palettes, but winging-it is also a perfectly viable option!

For starters, the **Surface** colors will influence the rest of the colors I choose because it's the main background set. Think about this as what will be your main light/dark mode background colors.

For this example, I'll choose something like `#02c39a` (a saturated mint green) for the Surface 500 (midtone).<br><br>

After that, I will set my lightest and darkest colors.

> [!NOTE]
> Note: Depending on the template you chose, the theme/preview might be using a different color than **Surface 50** for light or **Surface 950** for dark as the background colors and might make it seem like certain colors aren't changing.
>
> Quickly jump down to the "Backgrounds" section and set the two dropdowns to `surface-50` and `surface-950`, respectively.

Back in the "Color Palette" settings, you can now choose your preferred lightest and darkest Surface (background) colors. If it helps, you can use the light/dark mode toggle in the upper-right corner and the color previews (specifically the "Tonal" set) farther down the page, to get a better preview of your lightest and darkest colors in their expected context.

After some messing around, I landed on using a pale peach color for the lightest color and a dark blue for the darkest color, making our current Surface set:

###### Surface

**50**: `#fef8dc` *(pale peach/sand)*

**500**: `#02c39a` *(seafoam green)*

**950**: `#003557` *(deep blue)*

> [!TIP]
> The generator does not retain saturation well on low-saturation colors. If needed, click the "All" toggle and manually adjust the colors to your needs.

Now we create the rest of the colors in a similar way! I'd suggest choosing your **Primary**, **Secondary**, and **Tertiary** midtone colors next. This basically allows you a primary brand color and two additional accent colors. These can be whatever you like, but try to stick with the midtone guidelines mentioned previously.

You can also set them all to the same as the **Primary** set, if you only want that one color.

For the lightest/darkest colors in any set besides **Surface**, I choose to make them stand-out a bit, rather than trying to match the intensity. So, if your light background is close to white, choose light colors that have some slight color and contrast increase, but aren't extremely different. If you dark background is close to black, same rule applies, but the opposite: Make them slightly lighter than the background with more contrasted values.

In the case of this example, the dark background is fairly light, and the light background is fairly saturated, so we'll really just have to keep an eye on that **Tonal** preview to make sure they stand-out well enough.

The colors I've chosen are:

###### Primary

**50**: `#ffdba5`

**500**: `#fd6e2d` *(Feiry Coral)*

**950**: `#411b1b`

###### Secondary

**50**: `#ffc5c1`

**500**: `#ff6aa6` *(Standard/Pink Coral)*

**950**: `#3b1b31`

###### Tertiary

**50**: `#c6f1de`

**500**: `#2bb3ba` *(Sky Blue)*

**950**: `#002d39`

> [!NOTE]
> I used a more advanced trick to get the colors somewhat "blended" with the background. Basically, just try and shift the lightest/darkest color hues slightly toward the Surface lightest/darkest hue.

Last big step to finishing your color sets is the **Success**, **Warning**, and **Error** sets. These do serve a functional purpose, so I'd highly advise setting these to somewhere in the green, yellow/amber, and red hues, respectively.

These colors will be used in certain contexts to denote issues (or a lack thereof).

> [!TIP]
> **Success** indicates: "all good or no issues are present."

> [!WARNING]
> **Warning** indicates: "caution or potential issues are present."

> [!CAUTION]
> **Error** indicates: "an error is present, a task failed to complete, or a dangerous/permanent action is about to take place."

The colors I've chosen are:

###### Success

**50**: `#b7f9b8`

**500**: `#1fd97d` *(Mint Green)*

**950**: `#0a3021`

###### Warning

**50**: `#fff1ab`

**500**: `#f3d644` *(Yellow)*

**950**: `#3c2a0d`

###### Error

**50**: `#ffd8c7`

**500**: `#f3504f` *(Red-Orange)*

**950**: `#3e1921`

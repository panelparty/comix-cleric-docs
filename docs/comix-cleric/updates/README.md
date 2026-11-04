# Comic Updates <!-- order: 4 -->

These are your main comic posts!

---

### Create & Edit Updates


##### Required Fields:

###### Slug

Unique identifier text to locate the update without the exact database ID.

---

##### Important Fields

###### Title

The title or name of the update.

###### Update Type

There are several different types of updates that come setup in Comix Cleric by default:

- **Main Story** - Updates that are part of the main storyline of your comic.
- **Intermission** - Usually, one page breaks in a story that prepare for an immediate return.
- **Hiatus** - Updates to notify your readers that you'll be taking a break from the comic.
- **Notice** - General notice to deliver important information about the comic to your readers.
- **Snippet** - A short, readable section of an upcoming page.
- **Preview** - Similar to a snippet, but generally meant as a single promotional image.
- **Misc.** - Any other reason you may want to tell your users about something.

For most cases, you'll want to add the comic page as a ***"Main Story"*** update, as this gives you the ability to set the *Page Number, Volume, and Chapter* fields.

###### Number

-# ***Only for "Main Story" update type.***

Sets the sequential ordering of the pages. Number should automatically increment from last update, or start from 1. Numbers cannot be repeated.

> [!TIP]
> An option for cosmetic numbering (ex: `XII`, `1-32-B`, etc.) may become available. Request it on our Discord!

###### Volume

-# ***Optional; Only for "Main Story" update type.***

For grouping comic updates & chapters.<br>*A volume does not have to be created or selected to add a comic post.*

###### Chapter

-# ***Optional; Only for "Main Story" update type.***

For grouping comic updates.<br>*A chapter does not have to be created or selected to add a comic post.*

###### Blurb

A brief description of the update. Can be a small snippet of the full description, or just a funny little quip. This shouldn't be more than a couple of short sentences.

###### Full Description

A description of the update, or whatever you want! It features HTML/Markdown support, allowing you to write an entire blog post with images there, if you wanted!

> [!NOTE]
> We are actively working to improve the editing experience with formatting options and media importers.

###### Cover/Thumbnail

The image that will be displayed on links and previews of your comic update. Will be set automatically if missing.

###### Featured Media

This is where your main update image(s) will go. These images will appear in the reader and always try to fill the available space. We currently support most common image formats, but we recommend: .png, .jpg, .gif, .webp

You can add up to 128 images in a single update at this time.

- **New Item** - Will allow you to add a custom media block (media, text, YouTube video embed)
- **Add from Library** - Will allow you to select items that have already been uploaded.
- **Upload Files** - Will allow you to upload up to 128 images at once. (Order may not be as expected, simply drag and drop to re-order!)

> [!NOTE]
> We are working on improving support for wider, strip-style comics, as well as inferring media order upon upload (if possible).

###### Transcript

For providing a text-based, screen-reader friendly version of your update! It should describe the panels, actions, and dialogue!

###### Date Published

This defines the date the page is intended to be public. This can be used to back-date old updates when rebuilding a archive. Setting this value later than the current date will activate the scheduler. You do not have to schedule your posts, they can be published manually at any time.

If a time is not provided, it will be set to `00:00` (midnight).

---

##### Other Fields

###### Audio File

Select or upload an audio file to embed to the page.

> [!NOTE]
>We are working on a custom embedded audio player to fit the style of the site more closely.

###### Autoplay

Allows the audio to play automatically when navigating to this update.

> [!WARNING]
> Due to browser security, there are many cases where auto-playing media is blocked automatically. There is nothing we can do to circumvent this. Sites like YouTube are on a *very* short list of domains that are allowed to bypass this feature.

###### Loop Playback

Sets the audio to start playing again from the beginning after it ends. Useful for looping/ambient tracks.

###### Volume

Sets the default playback volume of the audio track. Just in case the audio is known to be louder than average.

---

##### Hidden Fields

###### ID

The primary unique identifier of your updates.

###### Date Created

A DateTime automatically set by the database when creating a new update.

###### Date Updated

A DateTime automatically set by the database when updateing an existing update.

###### User Created

A user account relation that is automatically set by the database when creating a new update.

###### User Updated

A user account relation that is automatically set by the database when updating an existing update.

###### Status

A value that determines the visiblity of an update to public viewers. Admin can view any update at any time.

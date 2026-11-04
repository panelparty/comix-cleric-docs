# Creating Comic Updates

In this guide, you'll learn all about creating basic comic posts!



---



#### First Things First

Before you start creating updates, decide if your story needs **Chapters** or **Volumes**. These are *<u>completely optional</u>* and only serve to further categorize your comic updates!

**Chapters** and **Volumes** are intended to work similar to how you'd probably expect:

###### Chapters
-# A collection of **Comic Updates** *(pages)* from the main story across a small plot arc.

###### Volumes
-# Contains a collection of **Chapters** across a larger plot arc.

We only recommend deciding early because changing things later becomes a bit more time-consuming.

If you decide you need **Chapter**/**Volume** catergories, we suggest you make your first entries before creating any **Comic Updates**.



---



### Creating a New Comic Update

First, access your admin panel and locate a "Create New Update" button. These can usually be found on the `Dashboard` page or the `Comic Updates` page. The label text may vary. You should be taken to a form page with many fields for you to utilize. 

***Not all fields are important or required to save the post.*** The only thing you actually need to fill-out is the `slug` field, as it is the primary look-up for your posts.

> Here is a rundown of the full [Comic Update](/docs/comix-cleric/updates) schema that tells you what each field is for.

To create a normal **Comic Update**, you generally just need to follow these steps:



##### 1. Set the Post Type

Set **Update Type** to `Main Story`, as this will make sure the page is cataloged as part of the main story of your series. This also reveals a **Number** field that is not available to other **Update Types**.



###### 1a. Numbering
If this is your first post, you should see the **Number** field already populated with `1`. This field tries to look back at your previous `Main Story` post and infer the next page number. So your next post should show `2` and so on.

> This system is not fool-proof, it can only work based on what it was provided in a prior Update.



###### 1b. Grouping by Volume & Chapter
**Volume** and **Chapter**, as previously mentioned, are optional fields for further categorizing your posts. Leaving these blank has no affect on the reader functionality, only what categories appear in the archive.

If a **Chapter** or **Volume** is present, the system will assume you intend to use them and will auto-populate if entries already exist.



##### 2. Set the Post Title & Slug

Now, you can add your **Update's** `Title` and `Slug`.

As in most other software, the `Title` is purely cosmetic and can contain special characters if you like. For example: `My Awesome Update #1 (The Real One!)` is a perfectly valid title.

> [!NOTE]
> Note: Any markup or code entered is rendered as-is. The title is not processed as HTML.

Your `Slug` is generally generated based on your `Title`. It cannot contain spaces or special characters, basically just lowercase letters, numbers, and hyphens. For example: `my-awesome-update-1-the-real-one` would be created from the previous example.

You are free to manually enter the value yourself, or click the generate button, which will take your `Title` value and automatically convert it to the expected formatting.

> [!IMPORTANT]
> We will try to expand to allow custom generation options in the future!



##### 3. Add Your Media

Skipping down a few fields, you'll find `Cover/Thumbnail` & `Featured Media`. We will return to your `Blurb` & `Full Description` fields a bit later.

Your `Cover/Thumbnail` fields can accept a single image. This image will be used as the thumbnail or cover of your **Comic Update** in the various archive sections and social media link previews.

The `Featured Media` field is a bit more complex, but for simple images, it's about the same. You can import multiple images at once using the `Upload Files` button. If you've already uploaded your images to `Media Files`, you can choose `Add from Library` instead.

`Featured Media` also has a *not-so-secret* tool: `New Item`

`New Item` simply allows you to create a custom media block; be it an image, YouTube video embed, or a wall of Markdown-supported text!



##### 4. Set the Update's Publish Date

`Date Published` is a date-picker component that allows you to choose the exact time and date a post was or should be published.

This field can be used for scheduling and back-dating posts to fit their original publish date. Even if a post is set for some time in the distant future, you can still choose to publish it immediately, we won't stop you! *Look out 2077, we're ready!*

You do get the option to `Schedule`, as long as the publish date is later than the current date and time.

> [!TIP]
> Scheduled posts are stored the same as any other post, so you don't have to worry about losing your schedule between server restarts!



##### 5. Add More Details

The last few fields to go over are: `Blurb`, `Full Description`, `Transcript`, `Contributors`, & `Audio PLaylist`.



###### Blurb

The post's `Blurb` is a shortened version of the decription, or anything else you might want to say. We suggest keeping it as short as possible. 1-3 sentences, max. The text is cut-off automatically (but not altered) if there is no room to show it in the archive.



###### Full Description

`Full Description`, as self-described, allows you to write out your full post description. This field has support for Markdown formatting. Some HTML is accepted, but most is removed for safety reasons.



###### Transcript

The `Transcript` input is a Markdown-supported field that allows you give visually-impaired readers a way to follow along! It's like alt-text, but... much much longer. The more detail, the better!

Example:
```md
### Panel #1

A description of what's happening in the first panel.

Character 1 - "Some *dialogue!*"
Character 2 - "**More** dialogue!"

### Panel #2

Etc...
```



###### Contributors

With this field, you can select existing accounts or create new guest entries to give credit to your co-creators and editors!

Read more about creating contributors here. (Coming soon!)



###### Audio

Lastly, you can add `Audio` to your **Update**! Import or upload a new audio file and you should see options for: `Autoplay`, `Loop Playback`, & `Volume`.

- `Autoplay` - If enabled, it directs the browser to start playing audio as soon as the page loads. *(There are several cases where this will be automatically blocked by the browser, we cannot change this security feature.)*
- `Loop Playback` - Tells the audio player component to restart the audio file once it has ended.
- `Volume` - Sets the default playback volume for the audio player. *(Useful if your track is very loud!)*
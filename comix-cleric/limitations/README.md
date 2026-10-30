# Known Limitations <!-- order: 7 -->

Comix Cleric is always improving, but there are some things you should know...

---

### Comix Cleric Local Accounts

All local user accounts are either "admin" or "user". While we work to expand role capabilities, all staff have the same permissions.

> [!WARNING]
> <u>**ONLY CREATE STAFF/ADMIN ACCOUNTS FOR PEOPLE YOU KNOW AND TRUST. They see and control the exact same things you can.**</u>

---

### Browser Support

At this time, Comix Cleric can only support modern browsers (2023 and newer) to ensure we can take advantage of many of the amazing new CSS features! There are currently no fallbacks that would allow similar functionality on older browsers.

We understand some people out there might want the nostalgia or just really like using their favorite old-school browser. We're not saying it *won't* work, but it's highly likely that just *can't* because of new features in JavaScript and CSS that are not backwards-compatible.

It is possible to add `@supports` fallbacks to the main CSS stylesheet, but we have no plans do so at this time. If you'd like to contribute backwards-compatible styles and JavaScript features, feel free *once the package goes public*!

---

### Batch Uploading/Editing

While we very much understand the need for the tools, there is a ton of variation in how different webcomic apps handle data.

The biggest issue isn't really getting things *into* Comix Cleric, it's making sure you can get your old data out of your previous site in an ethical way. Many providers don't offer downloading a copy of your existing data **at all** and many more would disallow scraping to take it back by-hand.

---

### Theme System

When Comix Cleric was conceived, its main goal was to majorly simplify the process of setting-up a custom webcomic site that had a responsive, ready-to-go UI, API, and database.

As this project grew, it became quite clear that a Tailwind-based theme system will not fit the needs of everyone. We are always doing our best to improve this app and better serve the creators of this community. That being said, replacing this with something better is non-trivial and while we have plans to enhance or do away with the Skeleton UI theme system, it will take some time and more planning.

If you want to be part of the decision-making process, join our Discord and get involved in the feature discussions!

---

### Pages & Components

Similar to the previous statement, Comix Cleric's original intent was to be as simple as possible to set-up and go! We wanted to first provide a solid, functional UI and API, with bigger improvements coming later-on.

For now, pages and their respective components are *mostly* hard-coded, but we also have plans and functional code for massively improving this as well!

Once again, join the Discord to let us know what you'd like to see it replaced with!

---

### Downgrading Hosting (Hub Site)

It is currently not possible to automatically down-grade your hosting plan. This is a limitation caused by having to decide what to do if a server is already utilizing more resources than would be provided by the new plan.

If you really must downgrade, please reach out to staff and we can try to work out a custom plan that allows you to keep certain resources while reducing the overall cost of hosting if a simple downgrade is not possible.

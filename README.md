# Site maintenance guide

## What's what

```
_config.yml              site-wide settings
assets/css/style.css     all visual styling — one file, colors at the top
_layouts/default.html    shell: nav, theme toggle, footer (wraps every page)
_layouts/page.html       article layout used by posts, notes, and standalone pages
index.html               homepage
blog/index.html          blog listing (auto-generated from _posts/)
notes/index.html         notes listing (auto-generated from _notes/)
tags/index.html          tag index (auto-generated from tags on posts/notes)
search/index.html        search page
search.json              search index (auto-generated, don't edit)
how-i-write/index.html   standalone page — your text goes here
```

## Adding a blog post

1. Create a new file inside a folder called `_posts/`.
2. Name it exactly `YYYY-MM-DD-a-short-slug.md` — the date is required and
   controls sort order; the slug becomes the URL.
3. Content:
   ```yaml
   ---
   title: Your post title
   tags: [algorithms]
   ---
   Your writing, in Markdown.
   ```
4. Commit. It now appears on the homepage and on `/blog/` automatically —
   nothing else needs to change.

## Adding a note

1. Create a new file inside a folder called `_notes/`.
2. Name it anything, e.g. `binary-search.md` (no date needed).
3. Content:
   ```yaml
   ---
   title: Your note title
   tags: [algorithms, math]
   ---
   Your writing, in Markdown.
   ```
4. Commit. It appears on `/notes/` automatically, sorted alphabetically by title.

## Tags

Tags come entirely from the `tags: [...]` line in a post's or note's front
matter — there's no separate place to register a tag. Add a tag to a post,
and it shows up on `/tags/` automatically, grouped with anything else that
shares it. Remove it from the front matter, and it disappears from
`/tags/` the next time the site builds. If a tag has zero posts or notes
using it, it simply won't appear — there's nothing to clean up.

## Search

`search.json` rebuilds itself from every post and note automatically, so
you never touch it directly. It picks up title, tags, and the first ~160
characters of content, which is what `/search/` matches against as you type.

## Editing a standalone page (like "How this is written")

Standalone pages aren't posts or notes — they're just a folder with an
`index.html` inside it, like `how-i-write/index.html`. To edit one:

1. Open the file on GitHub.
2. Click the pencil (edit) icon.
3. Everything above the second `---` is front matter (title, permalink) —
   leave that alone unless you're intentionally changing the URL or title.
4. Everything below the second `---` is your content — edit freely.
5. Commit.

To add a new standalone page (e.g. an "About" page), copy this same pattern:
a new folder, an `index.html` inside it with `layout: page` and a `permalink`,
your content below the front matter.

## Changing the look

Everything visual lives in `assets/css/style.css`. The two blocks at the
very top of the file are the only ones you're likely to touch:

```css
:root {
  --bg: #FAFAF8;        /* light mode background */
  --ink: #2B2B2B;        /* light mode text */
  --ink-soft: #8A8A85;   /* light mode secondary text */
  --hairline: #E8E8E4;   /* light mode dividers */
  --accent: #6B7FD7;     /* light mode link/highlight color */
}

[data-theme="dark"] {
  --bg: #1C1C1E;         /* dark mode background */
  --ink: #DEDEDA;        /* dark mode text */
  /* ...same idea */
}
```

Change a hex value, commit, refresh — that's the whole process. Font size
(`font-size: 18px` on `body`) and spacing are further down the same file if
you want to adjust density.

## Changing the navigation

The four nav links (Blog, Notes, Tags, Search) are hard-coded in
`_layouts/default.html`, near the top of the `<body>`. To add, remove, or
rename a link, edit that block directly — each link is one line.

## General workflow

Every change follows the same shape:
1. Open the file on GitHub (or edit it locally and push).
2. Make the edit.
3. Commit.
4. Wait ~1 minute — GitHub rebuilds the site automatically.
5. Refresh the live URL to confirm.

There's no build step you have to run yourself unless you're also using
Jekyll locally to preview before pushing (optional, not required).

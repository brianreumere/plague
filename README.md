# plague

plague is a [Minima](https://github.com/jekyll/minima)-inspired theme that might have some [IndieWeb](https://indieweb.org/) stuff like [microformats](https://microformats.org/) at some point. For now it's a work in progress.

## Examples

### Homepage

By default, the homepage is a standalone page that will render Markdown-formatted content from `content/_index.md`. For example:

```
Welcome to the homepage. This is a list:

* First list item
* Second list item

[Check out this link](https://example.com/).
```

### List of posts

If your site has a `content/posts` directory with blog posts, add an `_index.md` file that looks something like this:

```
---
title: posts
menu:
  main:
    weight: 1
---
```

You can set the menu weight higher or lower to control its position in the site's menu.

### Standalone page

For a standalone page (for example, a page with contact info), create `content/contact/index.md` that looks something like this:

```
---
layout: standalone
title: contact
menu:
  main:
    weight: 2
---

[email](mailto:someone@example.com)
```
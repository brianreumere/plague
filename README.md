# plague

plague is a [Minima](https://github.com/jekyll/minima)-inspired theme that might have some [IndieWeb](https://indieweb.org/) stuff like [microformats](https://microformats.org/) at some point. For now it's a work in progress. It also draws heavily from the [Indigo theme](https://github.com/AngeloStavrow/indigo).

Add the theme to your Hugo site by running the following command from your site directory:

```
git submodule add https://github.com/brianreumere/plague.git themes/plague
```

## IndieWeb

To show an [h-card](https://microformats.org/wiki/h-card) in the footer of every page, set `showHcard` to `true` in your site's `config.toml` file. For example:

```
[params]
  showHcard = true
```

To populate the h-card, create a `[params.indieWeb]` section in `config.toml` and populate it. Only some of the fields are required (will be documented more fully later, with all possible social handles too). For example:

```
[params.indieWeb]
    avatar = "images/avatar.jpg"
    fullName = "someone"
    nickname = "something"
    emailAddress = "someone@example.com"
    gitHubUsername = "something"
    twitterHandle = "something"

    [param.indieWeb.location]
      city = "somewhere"
      region = "somewhere"
      country = "somewhere"
```

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

## Sublicenses

The social icons are from the [Indigo theme](https://github.com/AngeloStavrow/indigo) by [AngeloStavrow](https://github.com/AngeloStavrow). [The MIT license for these is included here](LICENSE.indigo).
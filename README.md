# plague

plague is a [Minima](https://github.com/jekyll/minima)-inspired theme that has some [IndieWeb](https://indieweb.org/) stuff like [microformats](https://microformats.org/). It is a work in progress. It also draws heavily from the [Indigo theme](https://github.com/AngeloStavrow/indigo).

Add the theme to your Hugo site by running the following command from your site directory:

```
git submodule add https://github.com/brianreumere/plague.git themes/plague
```

## Accessibility

I'm not super familiar with web accessibility, but this theme does aim to be accessible to users who use the web with assistive technologies and devices.

The [WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org/) from [Web Accessibility in Mind (WebAIM)](https://webaim.org/) and the [MDN Accessibility documentation](https://developer.mozilla.org/en-US/docs/Web/Accessibility) were helpful to get to an initial baseline of accessibility. I'd also encourage you to read about writing accessible Markdown and documentation in general (some things I read are [Improving The Accessibility Of Your Markdown](https://www.smashingmagazine.com/2021/09/improving-accessibility-of-markdown/), [Writing accessible documentation](https://developers.google.com/style/accessibility), and [Alternative Text](https://webaim.org/techniques/alttext/)).

## Hugo shortcodes

There is a Hugo shortcode implemented to display a paragraph of text with a custom class name `callout` and [ARIA `note` role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/note_role). You can use this instead of the `> `  Markdown blockquote syntax, since technically blockquotes are supposed to be actual quotations and not notes, call-outs, alerts, etc. (the `<aside>` tag also doesn't seem appropriate for this use case since it's intended to be for content that ["could be considered separate \[from the content around the `aside` element\]](https://www.w3.org/TR/2011/WD-html5-author-20110809/the-aside-element.html)).

For example:

```
{{< callout >}}
Make sure to do some stuff! This is important to read.
{{< /callout >}}
```

I might add additional shortcodes for differently colored callouts in the future.

## Minimum config requirements

These are the minimum required settings in your site's `config.toml` file for this theme to function.

With [h-card](https://microformats.org/wiki/h-card):

```
baseURL = "https://example.com"
languageCode = "en-us"
defaultContentLanguage = "en"
title = "example.com"
theme = "plague"

[params]
  siteHeaderText = "some website"
  showHcard = true

  [params.hcard]
    fullName = "some name"
```

Without h-card:

```
baseURL = "https://example.com"
languageCode = "en-us"
defaultContentLanguage = "en"
title = "example.com"
theme = "plague"

[params]
  siteHeaderText = "some website"
```

## IndieWeb

### h-card

With `showHcard = true`, you can configure multiple additional values in `config.toml` to populate your h-card. With the exception of `fullName`, everything is optional. The order of values in the `social` array determines the order of the social icons displayed in the footer.

For any social icons you would like to display, you should put a `font-awesome-icons` directory in the root of your Hugo site directory that contains SVG icons. The icon filenames should match `<platform>.svg`, where platform is the value you specify in `config.toml` (see example below). You can download icons from [Font-Awesome here](https://github.com/FortAwesome/Font-Awesome/tree/master/svgs). The social platforms specified below are just examples; you can add any custom ones you want as long as there is an icon file available.

```
[params]
  siteHeaderText = "My Website Name"
  showHcard = true

  [params.hcard]
    avatar = "images/me.jpg"
    fullName = "some name"
    pronouns = [ "they", "them", "theirs" ]
    nickname = "some nickname"
    showLocation = true
    city = "some city"
    region = "some region/state/province"
    country = "some country"

    social = [
      { platform = "email", identity = "someone@example.com", url_pattern = "mailto:%s" },
      { platform = "flickr", identity = "some flickr username", url_pattern = "https://www.flickr.com/people/%s" },
      { platform = "github", identity = "some github username", url_pattern = "https://github.com/%s" },
      { platform = "gitlab", identity = "some gitlab username", url_pattern = "https://gitlab.com/%s" },
      { platform = "glitch", identity = "some glitch username", url_pattern = "https://glitch.com/@%s" },
      { platform = "microblog", identity = "some micro.blog username", url_pattern = "https://micro.blog/%s" },
      { platform = "tumblr", identity = "some tumblr username", url_pattern = "https://%s.tumblr.com" },
      { platform = "twitter", identity = "some twitter username", url_pattern = "https://twitter.com/%s" }
    ]
```

See [The Pronouns in my h-card](https://wiki.zegnat.net/microformats/pronoun) regarding the `pronoun` h-card property.

`showLocation` can be set to false or deleted (along with `city`, `region`, and `country`) to not include any location info in your h-card.

The format of the theme's default h-card is in `layouts/partials/hcard.html`. If you want to customize the format, you can create a custom partial template at `layouts/partials/hcard.html` in your Hugo site directory.

The social icons are also part of the h-card, and their links will have the `rel="me"` attribute included.

### h-entry

The `fullName` and `avatar` (if it exists) properties are used on pages that use the `single` layout (typically a single blog post or article).

## Non-IndieWeb customizations

### Additional footer text

This will render below the h-card. Markdown is supported. For example:

```
[params]
  siteFooterText = "Powered by [Hugo](https://gohugo.io/) and the [plague](https://github.com/brianreumere/plague) theme."
```

If you want multiple lines (see the [TOML site](https://toml.io/en/)):

```
[params]
  siteFooterText = """
Powered by [Hugo](https://gohugo.io/).

Styled with the [plague](https://github.com/brianreumere/plague) theme.
"""
```

## Example pages

### Homepage

By default, the homepage will render Markdown-formatted content from `content/_index.md`. For example:

```
Welcome to the homepage. This is a list:

* First list item
* Second list item

[Check out this link](https://example.com/).
```

### List of posts

If your site has a `content/posts` directory with blog posts, add a `content/posts/_index.md` file that looks something like this:

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
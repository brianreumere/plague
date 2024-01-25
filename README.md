# plague

## Overview

plague is a [Minima](https://github.com/jekyll/minima)-inspired theme that has some [IndieWeb](https://indieweb.org/) features like [microformats](https://microformats.org/). It also draws heavily from the [Indigo theme](https://github.com/AngeloStavrow/indigo).

## Installation

### Git submodule

Add the theme to your Hugo site by running the following command from your site directory and adding `theme = "plague"` to `hugo.toml`:

```sh
git submodule add https://github.com/brianreumere/plague.git themes/plague
```

### Hugo module

Alternately, initialize your repo for Hugo modules:

```sh
hugo mod init github.com/brianreumere/plague-demo-site
```

And import it as a module in `hugo.toml`:

```toml
[module]
  [[module.imports]]
    disable = false
    ignoreConfig = false
    ignoreImports = true
    path = "github.com/brianreumere/plague"  # Theme
```

## Colors

There are two built-in color themes, `default` and `gibson`. They will automatically set a dark or light variety based on a user's preference (via the `prefers-color-scheme` CSS media feature). To force the site to always use the light or dark variety of a theme, specify `default-light`, `default-dark`, `gibson-light`, or `gibson-dark` for the `colors` parameter.

### Default

[![A screenshot of a single example post titled Commonly Used Passwords, showing the default color theme. The left half of the screenshot shows the light variety with a light background and dark text. The right half of the screenshot shows the dark variety with a dark background and light text.](https://github.com/brianreumere/plague/blob/main/images/tn.png?raw=true)](https://github.com/brianreumere/plague/blob/main/images/screenshot.png)

### Gibson

[![A screenshot of a single example post titled Commonly Used Passwords, showing the Gibson color theme. The left half of the screenshot shows the light variety with a light background and dark text. The right half of the screenshot shows the dark variety with a dark background and light text. Both varieties have purple and green color highlights.](https://github.com/brianreumere/plague/blob/main/images/tn-gibson.png?raw=true)](https://github.com/brianreumere/plague/blob/main/images/screenshot-gibson.png)

## Accessibility

I'm not very experienced with web accessibility, but this theme does aim to be accessible to users who use the web with assistive technologies and devices. [Some accessibility resources that were helpful are listed in the Resources section](#resources).

## Minimum configuration

These are the minimum required settings in your site's `hugo.toml` file for this theme to function (this example assumes you used the Hugo module method from [the Installation section](#installation)):

```toml
baseURL = "https://example.net"
languageCode = "en-us"
title = "Ellingson Mineral Tech Blog"

[module]
  [[module.imports]]
    disable = false
    ignoreConfig = false
    ignoreImports = true
    path = "github.com/brianreumere/plague"  # Theme

[params]
  siteHeaderText = "Ellingson Mineral Tech Blog"

  colors = "default"

  [params.hcard]
    fullName = "Eugene Belford"
```

## IndieWeb

### h-card configuration

You can configure additional values in `hugo.toml` to populate your h-card. With the exception of `fullName`, everything is optional. The order of values in the `social` array determines the order of the social icons displayed in the footer.

For any social icons you would like to display, you need to store an SVG file in the `icons` directory at the root of your Hugo site. The icon filenames should match `<platform>.svg`, where `<platform>` is a value you specify in `hugo.toml` (see the example below). [You can download icons from Font Awesome here](https://github.com/FortAwesome/Font-Awesome/tree/master/svgs). The social platforms specified below are just examples; you can add arbitrary ones as long as there is an icon file available and you write a `url_pattern` that inclues `%s` to specify where your username/handle/identity should be substituted to form a valid link.

```toml
[params]
  siteHeaderText = "Ellingson Mineral Tech Blog"
  siteFooterText = "Powered by [Hugo](https://gohugo.io/) and the [plague](https://github.com/brianreumere/plague) theme. Hosted on the Gibson supercomputer ⌨️."

  [params.hcard]
    avatar = "images/i.jpg"
    fullName = "Eugene Belford"
    pronouns = [ "they", "them" ]
    nickname = "The Plague"
    showLocation = true
    city = "New York"
    region = "NY"
    country = "US"

    social = [
      { platform = "email", identity = "e.belford@example.net", url_pattern = "mailto:%s" },
      { platform = "github", identity = "brianreumere", url_pattern = "https://github.com/%s" }
    ]
```

See [The Pronouns in my h-card](https://wiki.zegnat.net/microformats/pronoun) regarding the `pronoun` h-card property.

`showLocation` can be set to false or deleted (along with `city`, `region`, and `country`) to not include any location info in your h-card.

The h-card is displayed in the site footer, and the default format of the h-card is in `layouts/partials/hcard.html`. If you want to customize the format, you can create a custom partial template at `layouts/partials/hcard.html` in your Hugo site directory.

The social icons are also part of the h-card, and their links will have the `rel="me"` attribute included.

### h-entry

The `fullName` and `avatar` (if it exists) properties are used on pages that use the `single` layout (typically a single blog post or article).

## Non-IndieWeb customizations

### Additional footer text

This will render in the right-hand footer column, next to the h-card. Markdown is supported. For example:

```toml
[params]
  siteFooterText = "Powered by [Hugo](https://gohugo.io/) and the [plague](https://github.com/brianreumere/plague) theme."
```

If you want multiple lines (see the [TOML site](https://toml.io/en/)):

```toml
[params]
  siteFooterText = """
Powered by [Hugo](https://gohugo.io/).

Styled with the [plague](https://github.com/brianreumere/plague) theme.
"""
```

## Pages

### Homepage

By default, the homepage will render Markdown-formatted content from `content/_index.md`. For example:

```md
Welcome to the homepage. This is a list:

* First list item
* Second list item

[Check out this link](https://example.com/).
```

### List of posts

If your site has a `content/posts` directory with blog posts, add a `content/posts/_index.md` file that looks something like this:

```md
---
title: posts
menu:
  main:
    weight: 1
---
```

You can set the menu weight higher or lower to control its position in the site's menu. You may also want to source post dates from filenames by including the following in `hugo.toml`:

```toml
[frontmatter]
  date = [':filename', ':default']
```

### Standalone page

For a standalone page (for example, a page with contact info), create `content/contact/index.md` that looks something like this:

```md
---
layout: standalone
title: contact
menu:
  main:
    weight: 2
---

[email](mailto:someone@example.com)
```

## Hugo shortcodes

### SVG icon

If you download an SVG icon (e.g., from Font Awesome) and place it in the `icons` directory at the root of your Hugo site repo (**not** in the `content` or `static` directories), you can use it inline with your Markdown content by using the `fa` shortcode. The parameter is the name of the icon file (without the `.svg` file extension). The SVG will have the `aria-hidden="true"` attribute added so it [isn't included in the accessibility tree](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-hidden_attribute), so do not use it for any interactive functionality; it should be purely decorative.

```
{{< fa "github" >}}
```

### Callout

There is a Hugo shortcode implemented to display a paragraph of text with a custom class name `callout` and an [ARIA `note` role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/note_role). You can use this instead of the `> `  Markdown blockquote syntax, since technically blockquotes are supposed to be actual quotations and not notes, call-outs, alerts, etc. (the `<aside>` tag also doesn't seem appropriate for this use case since it's intended to be for content that ["could be considered separate \[from the content around the `aside` element\]](https://www.w3.org/TR/2011/WD-html5-author-20110809/the-aside-element.html)).

For example:

```
{{< callout >}}
Make sure to do some stuff! This is important to read.
{{< /callout >}}
```

I might add additional shortcodes for differently colored callouts in the future.

## Resources

The [WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org/) from [Web Accessibility in Mind (WebAIM)](https://webaim.org/) and the [MDN Accessibility documentation](https://developer.mozilla.org/en-US/docs/Web/Accessibility) were helpful to get to an initial baseline of accessibility. I'd also encourage you to read about writing accessible Markdown and documentation in general (some things I read are [Improving The Accessibility Of Your Markdown](https://www.smashingmagazine.com/2021/09/improving-accessibility-of-markdown/), [Writing accessible documentation](https://developers.google.com/style/accessibility), and [Alternative Text](https://webaim.org/techniques/alttext/)).

The [Accessible SVG test page](https://weboverhauls.github.io/demos/svg/), [Making SVG Accessible](https://decks.tink.uk/2017/lws/index.html), [Introduction to ARIA - Accessible Rich Internet Applications](https://webaim.org/techniques/aria/), and [Using Font Awesome Icons in Hugo](https://www.client9.com/using-font-awesome-icons-in-hugo/) were helpful re: SVGs.

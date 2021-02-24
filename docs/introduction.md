# Introduction for 1.0

## Features

- **Flexible theme system based on CSS custom properties**<br>
  Theme settings are presented as a flat list of logically-named [CSS custom properties](customization). There's no need to navigate or modify complex CSS, allowing changes to be made quickly and confidently.

- **No packages to install or static files to build**<br>
  All processing is done in the browser, removing the need for CSS pre-processors and other build tools. Just link to a theme, then customize by setting [theme-related properties](customization). That's it.

- **Multiple themes available**<br>
  Use a theme as-is, or as a starting point for something completely new. All themes share the same customizable properties, making it easy mix styles from different themes.

- **Improved desktop and mobile experience**<br>
  Enhancements that are unique to docsify-themeable—along with docsify- and browser-related bug fixes—provide a more enjoyable and trouble-free experience for site authors and visitors.

  - [Extensive customization](customization)
  - [PrismJS theme compatibility](customization#prismjs)
  - [Module scale typography](customization#base)
  - [Plugin customization](customization#plugin-styles)
  - [Ready transition](options#readytransition)
  - [Responsive tables](options#responsivetables)

- **Legacy browser support (IE10+)**<br>
  Thoroughly tested and fully compatible with legacy browsers, including support for CSS custom properties (courtesy of a handy [ponyfill](https://github.com/jhildenbiddle/css-vars-ponyfill) developed specifically for docsify-themeable).

?> Like docsify-themeable? Be sure to check out [docsify-tabs](https://jhildenbiddle.github.io/docsify-tabs)!

## Offline access

You can run this documentation offline by using [Docsify](https://docsify.js.org/#/). Fork this repo, [install Docsify](https://docsify.js.org/#/quickstart) on your local machine, and then in the root folder of this repo, type `docsify serve`. The website will be served on port 3000 on your localhost: `localhost:3000`.

Alternatively you can use [Docker](https://github.com/littlstar/docker-docsify) to run locally...


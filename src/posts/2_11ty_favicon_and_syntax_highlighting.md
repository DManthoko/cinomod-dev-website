---
title: Syntax highlighting and favicon's in 11ty
description: How to add a Favicon and configure syntax highlighting in 11ty
date: 2022-07-31
tags:
  - 11ty
  - favicon
  - syntaxhighlighting
layout: layouts/post.njk
---

## Adding a Favicon

This blog is based of the [eleventy-base-blog](https://github.com/11ty/eleventy-base-blog). The base blog doesn't include a default favicon, thus, when creating my blog, I had to find  way to include a favicon.

Before specifying a favicon to use on my site, of course, I would first need to have a favicon that I can use. [favicon.io](https://favicon.io/) is a free Favicon generator site, which is what I used to create my favicons.

In my case, I used the **text -> ico** option to create my favicon. The site allows you to download the generated favicons as a zip file. The extracted folder would contain a favicon.ico file, and a few other png files. I copied the favicon.ico and related images to my src/img/favicon folder.

Although the images have been included in the src folder, they aren't automatically included in the output folder. In the [.eleventy.js](https://github.com/11ty/eleventy-base-blog/blob/main/.eleventy.js) file, you will see the following two lines:


```js
// Copy the `img` and `css` folders to the output
eleventyConfig.addPassthroughCopy("img");
eleventyConfig.addPassthroughCopy("css");
```

Using the [addPassthroughCopy](https://www.11ty.dev/docs/copy/) method, the above would take the contents of the *src/img* and *src/css* folders, and include them in the root of the output folder.

Now that the favicon images would be included in the output folder, the html that is generated still needs to know which favicon to use. 

The eleventy base blog uses Nunjucks for templates. The base template can be found in [_includes/layouts/base.njk](https://github.com/11ty/eleventy-base-blog/blob/main/_includes/layouts/base.njk). 

In the head element, I used the link element shown below to specify the path to the favicon.ico file. 

```html
<link 
    rel="shortcut icon" 
    type="image/x-icon" 
    href="/favicon.ico"
>
```

## Updating the Syntax highlighting theme

In addition to updating the favicon, I also wanted to modify the theme used for syntax highlighting. 

Referring back to the [base.njk](https://github.com/11ty/eleventy-base-blog/blob/main/_includes/layouts/base.njk) file, in the head element, the default theme used for syntax highlighting is */css/prism-base16-monokai.dark.css*. 

To change the syntax highlighting theme, all that I needed to do was download a new prism theme. The prism themes are available from the [prism-themes](https://github.com/PrismJS/prism-themes) GitHub repository.

In my case, I downloaded the Laserwave theme, and in the my css folder, replaced *prism-base16-monokai.dark.css* with *prism-laserwave.css*.
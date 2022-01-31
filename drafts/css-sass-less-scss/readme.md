---
title: Differences between CSS, SASS, LESS and SCSS
published: false
description: 
tags: ''
cover_image: ../../assets/cover.png
canonical_url: null
id: 
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

## Differences between CSS, SASS, LESS and SCSS

### Which one should I choose?

Short answer: SASS.

### CSS
### SASS

It's an opensource CSS preprocessor coded in Ruby. It can save your time reducing repetitions in CSS. It provides features to create stylesheets and help to maintain the code. 

### LESS

It's also a CSS preprocessor coded in JavaScript. You can customize, maintain, manage and reuse stylesheets. It's a dynamic language that helps to keep the code modular, readable and easy to change.

### SCSS

### Comparative table

|             | CSS         | SASS        | LESS        | SCSS        |
| ---         | ---         | ---         | ---         | ---         |
|             |             |             |             |             |

### Examples

We'll show you some examples here, but you can find more on the official documentation websites.
- [SASS](https://sass-lang.com/guide)

#### Nesting

```css
/* CSS SYNTAX */
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

```sass
/* SASS SYNTAX */
nav
  ul
    margin: 0
    padding: 0
    list-style: none

  li
    display: inline-block

  a
    display: block
    padding: 6px 12px
    text-decoration: none
```

```scss
/* SCSS SYNTAX */
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

```less
/* LESS SYNTAX */

```

#### Modules

```css
/* CSS SYNTAX */
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

.inverse {
  background-color: #333;
  color: white;
}
```

```sass
/* SASS SYNTAX */
// _base.sass
$font-stack: Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```sass
/* SASS SYNTAX */
// styles.sass
@use 'base'

.inverse
  background-color: base.$primary-color
  color: white
```

```scss
/* SCSS SYNTAX */
// _base.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```scss
/* SCSS SYNTAX */
// styles.scss
@use 'base';

.inverse {
  background-color: base.$primary-color;
  color: white;
}
```

```less
/* LESS SYNTAX */

```

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.
# Sass/SCSS Style Guide

An indepth style guide to aid in formatting Sass/SCSS used in projects.

## <a name="toc">Table of Contents</a>

1. [CSS Style Guide](#css-style-guide)
1. [File Structure](#file-structure)
1. [Selector Nesting](#selector-nesting)
1. [Properties/Rules Organization](#properties-organization)
1. [Resources](#resources)
1. [License](#license)

## <a name="css-style-guide">CSS Style Guide</a>

While the focus of this style guide is primarily Sass/SCSS, it's important to touch on a few basic CSS formatting rules that should carry over.

#### Indentation & Whitespace

Be consistent with indentation and whitespace. Soft tabs with a tab size of 2 is popular.

```css
/* Bad */
.class {
    background: #000;
  font-size: 13px;
  }

/* Good */
.class {
  background: #000;
  font-size: 13px;
}
```

#### Keep Properties Organized

Make sure your selector's properties follow some form of organization.

```css
/* Bad */
.class {
  font-size: 14px;
  display: block;
  color: #333;
  background: #fff;
}

/* Good - Alphabetical */
.class {
  background: #fff;
  color: #333;
  display: block;
  font-size: 14px;
}

/* Good - Grouped Properties */
.class {
  /* Box Model */
  display: block;

  /* Type */
  color: #333;
  font-size: 14px;
  
  /* Other */
  background: #fff;
}
```

#### Selector Naming Scheme

Keep selector names clear and following a structure. For example, if there is inner markup related to the parent, keep a naming scheme.

```css
.modal {}
.modal-header {}
.modal-content {}
.modal-footer {}
```

#### IDs

Don't use them for styling elements. Argument could be made to use them for a project's basic structure and JS hooks, but the specificity is too high to merit using them for styling.

## <a name="file-structure">File Structure</a>

How you organize your files can speed up development and make it more clear about what file applies where. Below is a basic structure for a small site.

```
css/
 |- main.css (compiled stylesheet)
 |- scss/
      |- main.scss
      |- global.scss
      |- _variables.scss
      |- modal.scss
      |- sections/
           |- contact.scss
           |- about.scss
```

Files can be broken down as much as the project needs. For example, if the project contained more shared global rules, a `global` directory could be created and `global.scss`, `variables.scss` and 'modal.scss' could be moved into there for even cleaning organization.

#### main.scss

The `main.scss` *(global.scss, style.scss, etc.)* should not have any selector rules present. It should act only as a *"Table of Contents"* using this structure:

1. Vendor Globals
2. Project Globals
3. Reusable Patterns (modals, tabs, etc)
4. Section Specific
5. [shame.css](http://csswizardry.com/2013/04/shame-css/)

```scss
//Vendor
@import "compass";

// Globals
@import "variables";
@import "global";

// Reusable Patterns
@import "modal.scss";

// Sections
@import "sections/about";
@import "sections/contact";

// Shame
@import "shame";
```

## <a name="selector-nesting">Selector Nesting</a>

The ability to nest selectors is great for visual organization of code, but can be abused if developers aren't thinking about the output they are creating. **The maximum nesting level should only be three levels deep**

You wouldn't write the following selector in pure css: `.block .block-header .block-inner h2 span {}`, so don't do it with Sass/SCSS!

```scss
// Bad - output will be overly specific selectors
.block {
  .block-header {
    .block-inner {
      h2 { 
        span {}
      }
      h3 {}
      p {}
    }
  }
}

// Good
.block {
  .block-header {
    h2 {}
  }
}
```

## <a name="properties-organization">Properties/Rules Organization</a>

Ordering properties/rules in Sass/SCSS can help keep things clear and easier to read.

1. @extend
2. Regular Rules
3. @includes
4. Nested Selectors

```scss
// Bad
.class {
  background: #fff;
  @extend %module;
  @include transition(background 0.2s ease);
  h3 { font-size: 24px; }
  color: #333;
  @include float(left);
}

// Good
.class {
  @extend %module;
  background: #fff;
  color: #333;
  @include float(left);
  @include transition(background 0.2s ease);

  h3 { font-size: 24px; }
}
```

Separating rules and nested selectors like so makes the code more clear and easier read. 

## <a name='resources'>Resources</a>

##### Libraries

* [Bourbon](http://bourbon.io/)
* [Compass](compass-style.org)

##### Books

* [Scalable and Modular Architecture for CSS](http://smacss.com/)

##### Articles

* [CSS Tricks - Sass Style Guide](http://css-tricks.com/sass-style-guide/)

## <a name='license'>License</a>

(The MIT License)

Copyright (c) 2013 Joshua Jones

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[↑](#toc)
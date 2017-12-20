# Front-End Coding Standards (HTML & CSS)

The following document outlines a reasonable style guide for CSS development.
These guidelines strongly encourage the use of existing, common, sensible
patterns. They should be adapted as needed to create your own style guide.

## Introduction

This is a living document of Best Practices and Code Standards for Front-End Development at O3 World. The Development Team is encouraged to test, discuss, and evolve what is documented here together as best practices change and new ideas are shared. **Please implement and enforce these agreed upon standards in your own builds and in code reviews at all times for all projects.**

> Well-formed markup is made up of part standards and part agreed upon preferences by a team of developers. Along with consistency, both are important in creating maintainable, readable code for everybody.

**An [.editorconfig](#editor-config) file is included with this documentation to aid in enforcing some of these standards.** A full breakdown of the current `.editorconfig` is provided later in this document.

The Table of Contents below will help jump you to the pertinent section of this Code Standards document:

## Table of Contents

* [Principles of Standardized Code](#principles-of-standardized-code)
  * [Readability and Minification](#readability-and-minification)
  * [Whitespace](#whitespace)
  * [Comments](#comments)
* [HTML](#html)
  * [File Naming and Organization](#html-file-naming-and-organization)
  * [Semantics](#semantics)
  * [Formatting](#formatting)
  * [HTML5 DOCTYPE](#html5-doctype)
  * [Language and Character Encoding](#language-and-character-encoding)
  * [CSS and JavaScript Includes](#css-and-javascript-includes)
  * [Attribute Order](#attribute-order)
  * [Boolean Attributes](#boolean-attributes)
  * [JavaScript-Generated Markup](#javascript-generated-markup)
  * [HTML Comments](#html-comments)
  * [Accessibility](#accessibility)
  * [Performance](#performance)
* [CSS/SCSS](#css-scss)
  * [File Naming and Organization](#scss-file-naming-and-organization)
  * [Rule Structure](#rule-structure)
  * [Rule/Selector/Property Formatting](#rule-selector-property-formatting)
  * [Property Declaration Order](#property-declaration-order)
  * [Pixels vs. EMs vs. REMs for Typography](#pixels-ems-rems-for-typography)
  * [Comments](#scss-comments)
  * [Class Naming Conventions](#class-naming-conventions)
  * [Block Element Modifier (BEM)](#block-element-modifier-bem)
  * [CSS and JavaScript](#css-and-javascript)
* [Images](#images)
* [Editor Config](#editor-config)
* [Sources](#sources)

<a name="principles-of-standardized-code"></a>
## Principles of Standardized Code

There are several guiding principles with Code Standards. These represent the core concepts of standardized code and why we use this document to guide development best practices.

* Code should be readable and understandable by all members of the team. This includes internal and external developers.
* All code, regardless of the project, should read as if it was developed by a single person regardless of how many individuals actually worked on it.
* The style of writing and implementation of these Code Standards is agreed upon and implemented by the team.
* Assist in developing well-formed, semantically correct, and mostly valid code.
* Aid in the onboarding of new development team members to new and existing projects.

<a name="readability-and-minification"></a>
### Readability and Minification

When developing, readability is preferred over compression. There is no need for a developer to purposefully (manually or automatically) compress HTML or CSS/SCSS, nor obfuscate JavaScript (more details provided in JavaScript Code Standards).

_[Gulp](https://gulpjs.com/) modules are used to combine and minify CSS and JavaScript assets as needed. **Verbosity is preferred in original source code.**_

<a name="whitespace"></a>
### Whitespace

* Always be consistent in your use of whitespace using it to improve code readability.
* Use soft tabs with four spaces.

_Our [.editorconfig](#editor-config) file helps with maintaining proper whitespace in different files._

<a name="comments"></a>
### Comments

Well commented code is extremely important. Take time to describe components, how they work, their limitations, and the way they are constructed. Don't leave others in the team guessing as to the purpose of uncommon or non-obvious code.

<a name="html"></a>
## HTML

HTML (Hyper Text Markup Language) acts as the Structure or skeleton for which our Presentation (Styles) and Functionality (JavaScript) are built on. This makes it the foundation of the other components of our Front-End. It’s semantics can have a either a positive, or negative, impact on:

* Browser Rendering Speed
* Search Engine Optimization (SEO)
* Accessibility (a11y)
* Validation
* Usability

<a name="html-file-naming-and-organization"></a>
## File Naming and Organization

Filenames should contain lowercase letters and words should be separated with a hyphen. The hyphen word separator (as opposed to an underscore or camelcase) is considered good practice for SEO reasons.

<a name="semantics"></a>
## Semantics

HTML5 provides us with lots of semantic elements aimed to describe precisely the content - take advantage of its rich vocabulary. Make sure you understand the semantics of the elements you're using.

**NOTE: It's worse to use a semantic element in a wrong way than staying neutral.**

> Good developers can write valid HTML markup that is formatted properly and easy to read. Great developers go beyond that and know when to use the appropriate element for the job.

<a name="formatting"></a>
## Formatting

* Attribute values, even numeric attributes, should be quoted. Even though quotes around attributes are optional, always put quotes around attributes for readability. Always use double quotes, never single quotes, on attributes.
* **DO NOT** include a trailing slash in self-closing elements - the HTML5 spec defines this as optional. These self-closing elements include:
  * `<hr>`
  * `<br>`
  * `<input>`
  * `<img>`
* **DO NOT** omit optional closing tags (e.g. `</li>` or `</body>`).
* Element and attribute names should all be lowercase.
* Nested elements should be indented once (four spaces).
* Classes are preferred over IDs when it comes to CSS references to avoid specificity issues. More details on [Class Naming Conventions](#class-naming-conventions) are below.

```html
<!-- bad -->
<body>
  <img src='../path/file' alt='Alternative Text' />
  <ul id='myList'>
    <li>
        This is the first part of some sample text before a break.
        <br />
        More text after the break.
    <li>Just another list item in the middle of two others.
    <li>The final list item.
  </ul>
  <hr />
  <form>
    <label>Form Label</label>
    <input type=text placeholder='Sample Input' />
    <input type=submit value='Submit' />
  </form>

<!-- good -->
<body>
    <img src="../path/file" alt="Alternative Text">
    <ul class="my-list">
        <li>
            This is the first part of some sample text before a break.
            <br />
            More text after the break.
        </li>
        <li>Just another list item in the middle of two others.</li>
        <li>The final list item.</li>
    </ul>
    <hr>
    <form>
        <label>Form Label</label>
        <input type="text" placeholder="Sample Input">
        <input type="submit" value="Submit">
    </form>
</body>
```

**All HTML code must be valid and well formed.** A validator can often help a developer track down styling or scripting bugs. Valid HTML also increases the likelihood that a page will be displayed correctly in current and future browsers.

_Tools such as [The W3C Markup Validation Service](https://validator.w3.org/) or [PowerMapper’s SortSite](https://www.powermapper.com/products/sortsite/) can be used to test code validation as well as other aspects of development._

<a name="html5-doctype"></a>
### HTML5 DOCTYPE

Enforce standards mode and more consistent rendering in every browser possible with this simple doctype at the beginning of every HTML page.

```html
<!DOCTYPE html>
<html>
    <head>
        ...
    </head>
</html>
```

<a name="language-and-character-encoding"></a>
### Language and Character Encoding

**From the HTML5 spec (`<html lang="en-us">`):**

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use as well as aids translation tools to determine what rules to use.

Quickly and easily ensure proper rendering of your content by declaring an explicit character encoding. When doing so, you may avoid using character entities in your HTML, provided their encoding matches that of the document (generally `<meta charset="UTF-8">`).

```html
<!DOCTYPE html>
<html lang="en-us">
    <head>
        <meta charset="UTF-8">
        ...
    </head>
</html>
```

_**Starting HTML5 markup is included with this documentation (based on [HTML5 Boilerplate](https://html5boilerplate.com/)) with a fully formed and valid skeleton for front-end development.**_

<a name="css-and-javascript-includes"></a>
### CSS and JavaScript Includes

Per the HTML5 spec, typically there is no need to specify a type when including CSS and JavaScript files as `text/css` and `text/javascript` are their respective defaults.

```html
<!-- external CSS -->
<link rel="stylesheet" href="my-styles.css">

<!-- in-document CSS -->
<style>
    /* ... */
</style>

<!-- javascript -->
<script src="my-javascript.js"></script>
```

<a name="attribute-order"></a>
### Attribute Order

HTML attributes should come in this particular order for easier reading of code.

* `src`, `for`, `type`, `href`, `value`
* `class`
* `id`, `name`
* `title`, `alt`
* `role`, `aria-*`
* `data-*`

```html
<a href="#" class="..." id="..." data-toggle="modal">
    Example Link
</a>

<input type="text" class="form-control">

<img src="..." class="..." alt="...">
```

As far as Identifiable information is concerned, Classes make for great reusable components, so they come first. IDs are more specific and should be used sparingly (e.g., for in-page bookmarks), so they come after Classes.

<a name="boolean-attributes"></a>
### Boolean Attributes

XHTML required you to declare a value, but HTML5 has no such requirement. **Many attributes, like `disabled` or `checked`, don’t require a value to be set so don’t set them.**

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```

<a name="javascript-generated-markup"></a>
### JavaScript-Generated Markup

Writing markup in a JavaScript file makes the content harder to find, harder to edit, and less performant. **Avoid it whenever possible.**

<a name="html-comments"></a>
### Comments

Insert an ending comment after the closing tag of a long HTML section. This helps to identify what named element is being closed. **DO NOT use a starting comment.**

```html
<div class="my-class">
    ...
</div>
<!-- /.my-class -->
```

<a name="accessibility"></a>
### Accessibility (a11y)

Basic accessibility principles should be adhered to when writing HTML - it shouldn't be an afterthought. You don't have to be a [WCAG](https://www.w3.org/WAI/intro/wcag) expert and different clients have different requirements for level of support, but **basic accessibility support can have a huge impact.**

* Use `H1` - `H6` to properly order and identify headings.
* In tables, use the `scope` attribute to associate header cells and data cells in data tables and use the `summary` attribute of the table element to give an overview of data tables.
* For forms, always provide a submit button, use `label` elements to associate text labels with form controls, and visually indicate required form controls.
* With image elements, always use `alt` attributes. Use an empty `alt` attribute on image elements that Assistive Technology should ignore.

_Tools such as [PowerMapper’s SortSite](https://www.powermapper.com/products/sortsite/) or [Chrome’s Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en) extension can be used to audit and correct basic accessibility issues._

<a name="performance"></a>
### Performance

Unless there's a valid reason for loading your scripts before your content (e.g. [Modernizr](https://modernizr.com/) or certain tracking scripts), don't block the rendering of your page by placing them in the `<head>`. Move as many as possible to the bottom of the markup right above the `</body>` or `async`/`defer` the load.

Individual SVG assets should be optimized using a tool such as [SVGOMG](https://jakearchibald.github.io/svgomg/). Image assets should be processed using a tool like [ImageOptim](https://imageoptim.com/mac). Both of these safely remove - without a noticeable change to the asset - redundant and useless information such as editor metadata, comments, hidden elements, default or non-optimal values which can have a significant impact on file size.

_The default Gulp setup has been configured to combine and minify CSS and JavaScript into as few files as possible, but it can be configured to suit the unique needs of individual projects._

<a name="css-scss"></a>
## CSS/SCSS

Representing the Presentation layer of our Front-End Development, it’s important that our CSS/SCSS is well organized and documented. One of CSS’ best features - cascading - can also be its biggest achilles.

<a name="scss-file-naming-and-organization"></a>
### File Naming and Organization

Filenames should contain lowercase letters and words should be separated with a hyphen.

* Within individual CSS/SCSS files, organize sections of code by component element.
* Maintain a consistent commenting hierarchy for each section of code.
* Use consistent white space to your advantage when separating sections of code for scanning larger documents.

#### Global and Section-Specific SCSS

The top-level SCSS should serve as a “Table of Contents” with no styles directly within it. Keep all styles organized into component parts. When ordering your partials within your “Table of Contents”, the ideal order/grouping is:

* Global
* Vendor
* Elements
* Patterns
* Sections
* Pages

Partials are named `_partial-name.scss` - with a "_" prefix - to indicate that this file isn't meant to be compiled by itself. Break CSS/SCSS down by component instead of page. Pages can be rearranged and components (re)moved.

There is no penalty to splitting into many small files. It’s much easier to jump to small specific files and navigate through them than fewer/larger ones.

```css
// global
@import "global/functions";
@import "global/variables";

// vendor
@import "vendor/bootstrap/bootstrap";

// elements
@import "partial/grid";
@import "partial/utility";

// patterns
@import "partial/tabs";
@import "partial/modals";

// sections
@import "partial/header";
@import "partial/footer";

// pages
@import "partial/contact-page";
```

#### Compile with Source Maps

Source Maps are produced as part of our Gulp build to more easily determine where particular SCSS partial rules are coming from to aid in visual debugging within the browser.

<a name="rule-structure"></a>
### Rule Structure

The overall structure of a SCSS rule should follow the below order:

* **Extends**
  * Always place `@extend` statements on the first lines of a declaration block.
  * Knowing right off the bat that this class inherits another set of rules from elsewhere is good and overriding styles for that inherited set of rules becomes much easier.
* **Regular Styles**
  * Adding our regular styles after `@extends` allows us to properly override those properties, if needed.
* **Pseudo Class’ and Elements**
  * Pseudo Class’ and Pseudo Elements directly relate to the element itself so we nest them first before other selectors.
  * Differentiate between Pseudo Elements and Pseudo Classes by using a double colon versus a single colon, respectively (`my-class::before { … }` versus `my-class:hover { … }`).
* **Nested Selectors**
  * This includes any modifiers and children of the class we’re working within.

```css
.my-module {
    @extend %module;
    background: #0f0;

    &:hover { background: #0c0; }

    &::before {
        display: block;
        content: "";
    }

    > h3 {
        border-bottom: 1px solid #fff;
        @include transform(rotate(90deg));
    }
}
```

As a rule of thumb, avoid unnecessary nesting in SCSS. **At most, aim for three levels.** If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting). This prevents overly-specific CSS selectors.

<a name="rule-selector-property-formatting"></a>
### Rule/Selector/Property Formatting

CSS/SCSS formatting decisions documented below are in place to ensure that code is: easy to read; easy to clearly comment; minimizes the chance of accidentally introducing errors; and results in useful diffs and blames:

* When grouping selectors, keep each selector to a single line.
* Include one space before the opening brace of declaration blocks for legibility.
* Place closing braces of declaration blocks on a new line.
* Include one space after the `:` for each declaration.
* Each declaration should appear on its own line for more accurate error reporting.
* End all declarations with a semicolon. The last declarations semicolon is optional, but your code is more error prone without it.
* Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
* Don't include spaces after commas within `rgb()`, `rgba()`, `hsl()`, `hsla()`, or `rect()` values. This helps differentiate multiple color values (comma, no space) from multiple property values (comma with space).
* Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
* If you need transparency, use `rgba()`. Otherwise, always use the hexadecimal format.
* Lowercase all hex values (e.g., `#fff`). Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
* Use shorthand hex values where available (e.g., `#fff` instead of `#ffffff`).
* Use double quotes consistently (e.g., `content: "";`).
* Quote attribute values in selectors (e.g., `input[type="text"]`). They’re only optional in some cases, and it’s a good practice for consistency.
* Avoid specifying units for zero values (e.g., `margin: 0;` instead of `margin: 0px;`).
* Separate each ruleset by a blank line.
* Don't make values and selectors hard to override. Minimize the use of id's and avoid `!important`.
* For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
    display: block;
    box-shadow: 0 1px 2px #ccc;
    background: #fff;
    background: linear-gradient(#fff, rgba(0,0,0, .8));
    font-family: helvetica, arial, sans-serif;
    color: #333;

    &::before {
        position: absolute;
        padding: 0;
        content: "";
    }
}

.selector-a { padding: (10px * 2) 5px; }

.selector-b,
.selector-c { padding: 10px; }
```

_Adding vendor prefixes for CSS properties is unnecessary since Gulp uses [Autoprefixer](https://github.com/postcss/autoprefixer) to only post-process vendor prefixes based on the declared browser support. The unique browsers supported can be updated on a project basic._

#### Exceptions and Slight Deviations to the Above Syntax Rules

Long, comma-separated property values - such as collections of gradients or shadows - can be arranged across multiple lines in an effort to improve readability and produce more useful diffs.

```css
.selector-1 {
    display: block;
    box-shadow: 0 1px 2px #ccc,
                inset 0 1px 0 #fff;
}
```

In instances where a rule set includes only one declaration, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

```css
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }
```

<a name="property-declaration-order"></a>
### Property Declaration Order

Related property declarations should be grouped together following the order:

* **Positioning**
  * `z-index`
  * `position`
  * `top`
  * `right`
  * `bottom`
  * `left`
* **Display and Box Model**
  * `display`
  * `overflow`
  * `float`
  * `margin`
  * `border-radius`
  * `border`
  * `padding`
  * `width`
  * `height`
  * `background-*`
* **Typography**
  * `text-*`
  * `line-height`
  * `font-*`
* **Miscellaneous**
  * `opacity`
  * `content`
  * `transform`
  * `transition`

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.

```css
.declaration-order {
    /* positioning */
    z-index: 100;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* display and box-model */
    display: block;
    overflow: hidden;
    float: right;
    margin: 0;
    border-radius: 50%;
    border: 1px solid #999;
    padding: 0;
    width: 100px;
    height: 100px;
    background-color: #f5f5f5;

    /* typography */
    text-align: center;
    line-height: 1.5;
    font: normal 13px "Helvetica Neue", sans-serif;
    font-size: 14px;
    color: #333;

    /* misc */
    opacity: 1;
    content: "";
    transform: translateX(10px);
    transition: color #f00;
}
```

<a name="pixels-ems-rems-for-typography"></a>
### Pixels vs. EMs vs. REMs for Typography

Use REMs with a pixel fallback for `font-size`, because it offers absolute control over text. Additionally, a unitless `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the `font-size`.

<a name="scss-comments"></a>
### Comments

Well commented code is extremely important. Take time to describe components, how they work, their limitations, and the way they are constructed. Don't leave others in the team guessing as to the purpose of uncommon or non-obvious code.

* Each SCSS partial should have a clear comment header to define the role of this section of code.
* Place comments on a new line above their subject.
* Keep line-length to a sensible maximum (e.g. 80 columns).
* Make liberal use of comments to break SCSS code into discrete sections.
* Use "sentence case" comments and consistent text indentation.

```css
/*
 * Comment Header
 *
 *****************************************************************************/

/*
 * Detailed Comment Header
 *
 * This is some text the describes, in detail, how the below SCSS works, any
 limitations, and the way it is constructed.
 *
 * 1. Targeted notations can be included as well if inline comments aren't
 sufficient to outline functionality
 *
 *****************************************************************************/

/*
 * Child Comment
 *
 *********************************************************/

/* Single line comment */
```

Pre-formatted comment chunks can be setup within most IDEs and tied to a keyboard shortcut to more easily apply consistent formatting.

<a name="class-naming-conventions"></a>
### Class Naming Conventions

* Avoid excessive and arbitrary shorthand notation. `.btn` is useful for button, but `.s` doesn't mean anything.
* Use meaningful names; use structural or purposeful names over presentational.
* It's also useful to apply many of these same rules when creating SCSS variable names.

<a name="block-element-modifier-bem"></a>
### Block Element Modifier (BEM)

[Block Element Modifier (BEM)](http://getbem.com/) is a highly useful, powerful, and simple naming convention that makes your front-end code easier to read and understand, easier to work with, easier to scale, more robust and explicit, and a lot more strict.

The BEM approach ensures that everyone who participates in the development of a website works with a single codebase and speaks the same language - exactly what we’re looking for! Using BEM’s proper naming convention will better prepare you for design changes made to your website.

The naming convention follows this pattern:

```css
.block { ... }
.block__element { ... }
.block--modifier { ... }
```

* `.block` represents the higher level of an abstraction or component.
* `.block__element` represents a descendent of `.block` that helps form `.block` as a whole.
* `.block--modifier` represents a different state or version of `.block`.

An analogy/model for how elements are related:

```css
.media { ... }
.media__img { ... }
.media__img--rev { ... }
.media__body { ... }
```

```html
<div class="media">
    <img src="logo.png" class="media__img  media__img--rev" alt="Foo Corp logo">
    <div class="media__body">
        <h3 class="alpha">Welcome to Foo Corp</h3>
        <p class="lede">Foo Corp is the best, seriously!</p>
    </div>
</div>
```

<a name="css-and-javascript"></a>
### CSS and JavaScript

CSS classes or IDs as references for JavaScript functionality should be avoided as much as possible to prevent conflicts where renaming or removing a class or ID name would break JavaScript functionality. Instead use `data-*` attributes to apply JavaScript functionality to elements and components.

#### State Classes

Use the `.is-*` prefix for state classes that are shared between CSS/SCSS and JavaScript to denote a temporary styling application.

```html
<div class="accordion-tab is-active" data-accordion="true">
    ...
</div>
```

<a name="images"></a>
## Images

An image that has informational value should be a part of the markup and include an appropriate `alt` attribute. If an image is purely decorative (such as a textured background) then a `background-image` is appropriate or an inline image with the appropriate ARIA and `role` attributes applied.

<a name="editor-config"></a>
## Editor Config

EditorConfig helps developers define and maintain consistent coding styles between different editors and IDEs. This will help avoid common code inconsistencies and dirty diffs due to differences in editor formatting..

A few items pre-set in the `.editorconfig` file:

* `root = true`
  * Says that this file represents the top-most .editorconfig file and settings here should be applied.
* `[*]` denotes that the following settings will be applied to all files:
  * `indent_style = space`
    * Use a soft space character for indents.
  * `indent_size = 4`
    * A single indent is equal to 4 spaces.
  * `end_of_line = lf`
    * Unix-style line breaks.
  * `charset = utf-8`
    * Use the UTF-8 character set.
  * `trim_trailing_whitespace = true`
    * Removes any whitespace characters at the end of each line.
  * `insert_final_newline = true`
    * Adds a new, blank line to the end of our file.
* `[*.md]` is specific to files with this extension
  * `trim_trailing_whitespace = false`
    * Do Not remove any trailing whitespace from lines.
* The indent size used in the `package.json` file cannot be changed, so we have specific settings for this file type:
  * `[{.travis.yml,package.json}]`
    * `indent_size = 2`
    * `indent_style = space`

```
# .editorconfig helps developers define and maintain consistent coding
# styles between different editors and IDEs

# for more information about the properties used in this file, please see
# the .editorconfig documentation: http://editorconfig.org/

# this is the top-most .editorconfig file; do not search parent directories
root = true

# applied to all files
[*]
indent_style = space
indent_size = 4
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

# the indent size used in the `package.json` file cannot be changed
# https://github.com/npm/npm/pull/3180#issuecomment-16336516
[{.travis.yml,package.json}]
indent_size = 2
indent_style = space
```

<a name="sources"></a>
## Sources

These Code Standards are the culmination of research into best practices as well as input from the Development team. Specifics are adapted from various sources, including:

* [Front-End Guidelines](https://github.com/bendc/frontend-guidelines)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [SASS Style Guide](https://css-tricks.com/sass-style-guide/)
* [Code Guide](http://codeguide.co/)

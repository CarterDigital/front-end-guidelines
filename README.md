# Front-end-guidelines
Coding practices at Carter

In working on large, long running projects with dozens of developers, it is
important that we all work in a unified way in order to, among other things:

- Keep stylesheets maintainable.
- Keep code transparent and readable.
- Keep stylesheets scalable.

No matter the document, we must always try and keep a common formatting. This
means consistent commenting, consistent syntax and consistent naming.

There are a variety of techniques we must employ in order to satisfy these
goals.

## Contents

- [Whitespace](#whitespace)
    - [80 characters wide](#80-characters-wide)
    - [Text editor configuration](#text-editor-configuration)
        - [Sublime Text](#sublime-text)
- [Formatting](#formatting)
    - [Formatting rules](#formatting-rules)
    - [Declaration order](#declaration-order)
    - [Exceptions and slight deviations](#exceptions-and-slight-deviations)
    - [Preprocessors: additional format considerations](#preprocessors-additional-format-considerations)
    - [Linting](#linting)
- [Naming conventions](#naming-conventions)
    - [BEM](#bem)
    - [Namespacing](#namespacing)
        - [CSS frameworks](#css-frameworks)
        - [State hooks](#state-hooks)
        - [JavaScript hooks](#javascript-hooks)
        - [Test and Tracking hooks](#test-and-tracking-hooks)
            - [Order of the above hooks](#order-of-the-above-hooks)
- [Comments](#comments)
  - [DocBlock-esque](#docblock-esque)
  - [Main title](#main-title)
  - [Intro block](#intro-block)
  - [Section titles](#section-titles)
  - [Sub titles](#sub-titles)
  - [Preprocessor comments](#preprocessor-comments)
  - [Component-Extension pointers](#component-extension-pointers)
  - [Number labelling](#number-labelling)
  - [BEM modifier comments](#bem-modifier-comments)
  - [Settings comments](#settings-comments)
  - [TODO comments](#todo-comments)
  - [Non-JavaScript comments](#non-javascript-comments)
  - [`!important` comments](#important-comments)
  - [Other](#other)
- [Architecture Overview](#architecture-overview)
  - [Breakdown](#breakdown)
- [Writing CSS](#writing-css)
- [Acknowledgements and Further Reading](#acknowledgements-and-further-reading)

---





## Whitespace

Here are our rules for managing whitespace in Sass files:

- Use tabs for indentation.
- **Never** mix spaces and tabs for indentation.
- Wrap at 80 characters wide.

### 80 characters wide

Where possible, limit CSS files’ width to 80 characters. Reasons for this include:

- The ability to have multiple files open side by side.
- Viewing CSS on sites like GitHub, or in terminal windows.
- Providing a comfortable line length for comments.

There will be unavoidable exceptions to this rule—such as URLs, or gradient syntax—which shouldn’t be worried about.

### Text editor configuration

Configure your text editor to adhere to the above. At the bare minimum configure your editor to "show invisibles" or to automatically remove end-of-line whitespace.

## Formatting

Our chosen CSS code formatting rules ensures that CSS code is:

- Easy to read.
- Easy to clearly comment.
- Minimises the chance of accidentally introducing errors.
- Results in useful diffs and blames.

For reference here is an anatomy of a rule set:

```
[selector] {
  [property]: [value];
  [<- Declaration ->]
}
```

### Formatting rules

- Class names to use BEM notation, see [Naming Conventions -> BEM](#bem), where BEM isn't used then hyphen delimited class names are to be used.
- Use one discrete selector per line in multi-selector rule sets.

  **Good**
  ```scss
  .error,
  .success {
    ...
  }
  ```
  
  **Bad**
  ```scss
  .error, .success {
    ...
  }
  ```
- Include a single space before the opening brace of a rule set.
  
  **Good**
  ```scss
  .error,
  .success {
    ...
  }
  ```
  
  **Bad**
  ```scss
  .error,
  .success{
    ...
  }
  ```
- Place the closing brace of a rule set in the same column as the first character of the rule set.

  **Good**
  ```scss
  .error,
  .success {
    ...
  }
  ```
  
  **Bad**
  ```scss
  .error,
  .success {
    ...}
  ```
- Properties within rule sets should each reside on their own line.

  **Good**
  ```scss
  p {
    margin: 0;
    padding: 0;
  }
  ```
  
  **Bad**
  ```scss
  p {margin: 0; padding: 0;}
  ```
- Use one level of indentation for each declaration.

  **Good**
  ```scss
  .error {
    border: 0;
    margin: 0;
  }
  ```
  
  **Bad**
  ```scss
  .error {
  border: 0;
  margin: 0;
  }
  ```
- Separate each rule set by a blank line.

  **Good**
  ```scss
  .error {
    border: 0;
    margin: 0;
  }

  .success {
    border: 0;
    margin: 0;
  }
  ```
  
  **Bad**
  ```scss
  .error {
    border: 0;
    margin: 0;
  }
  .success {
    border: 0;
    margin: 0;
  }
  ```
- Include a single space after the colon of a property.

  **Good**
  ```scss
  margin: 0;
  ```
  **Bad** 
  ```scss
  margin:0;
  ```
- Use lowercase and shorthand hex values.
  
  **Good**
  ```scss
  #aaa
  ```
  **Bad**
  ```scss
  #aaaaaa
  ```
- Always use the shortest shorthand form possible for properties that support it.

  **Good**
  ```scss
  margin: 1px;
  ```
  **Bad**
  ```scss
  margin: 1px 1px 1px 1px;
  ```
- Always use double quotes, specifically for:
    - String literals e.g. `content: "";`.
    - `url()` e.g. `background: url("img/logo.png");`.
    - Attribute values in selectors e.g. `input[type="checkbox"]`.
- Where allowed, avoid specifying units for zero-values.
  
  **Good**
  ```scss
  margin: 0;
  ```
  **Bad** 
  ```scss
  margin: 0px;
  ```
- Commas in lists should be followed by a space.

  **Good**
  ```scss
  color: rgba(0, 0, 0, 0.1);
  ```
  **Bad**
  ```scss
  color: rgba(0,0,0,0.1);
  ```
- Include a space before `!important` keyword.
  
  **Good**
  ```scss
  padding: 10px !important;
  ```
  **Bad**
  ```scss
  padding: 10px!important;
  ```
- Property values; `@extend`, `@include`, and `@import` directives; and variable declarations should always end with a semicolon.
  
  **Good**
  ```scss
  color: #fff;
  ```
  **Bad**
  ```scss
  color: #fff
  ```
- Parentheses should not be padded with spaces.
  
  **Good**
  ```scss
  box-shadow: 0 2px 2px rgba(0, 0, 0, .2);
  ```
  **Bad**
  ```scss
  box-shadow: 0 2px 2px rgba( 0, 0, 0, .2 );
  ```
- When a decimal mark is needed always include the zero.

  **Good**
  ```scss
  0.25rem
  ```
  **Bad**
  ```scss
  .25rem
  ```
- Don't write trailing zeros for numeric values with a decimal point.

  **Good**
  ```scss
  margin: 0.5em;
  ```
  **Bad**
  ```scss
  margin: 0.500em;
  ```
- `url`s should not contain protocols or domain names. 
 
  **Good**
  ```scss
  background: url('assets/image.png');
  ```
  **Bad**
  ```scss
  background: url('https://example.com/assets/image.png');
  ```

### Declaration order

Declarations should be ordered alphabetically (get used to hitting F5, it works a treat). Reason for this is there is no learning curve for newcomers.

Example:

```
.selector {
  background-color: #000;
  bottom: 0;
  box-sizing: border-box;
  color: #fff;
  display: inline-block;
  font-family: sans-serif;
  font-size: 1em;
  height: 100px;
  text-align: right;
  width: 100px;
}
```

### Exceptions and slight deviations

Long, comma-separated property values—such as collections of gradients or shadows can be arranged across multiple lines in an effort to improve readability and produce more useful diffs. Each value after the first should be indented so that it starts at the same level as the first value e.g.

```
.selector {
background-image: linear-gradient(#fff, #ccc),
                  linear-gradient(#f3c, #4ec);
box-shadow: 1px 1px 1px #000,
            2px 2px 1px 1px #ccc inset;
}
```

### Preprocessors: additional format considerations

All our CSS is written with the Sass preprocessor so our conventions should be extended to accommodate the particularities of Sass.

- Limit nesting to 1 level deep. Reassess any nesting more than 2 levels deep. This prevents overly-specific CSS selectors (see [Specificity](http://cssguidelin.es/#specificity)).
- Always use placeholder selectors in `@extend`. Using a class selector with the `@extend` statement statement usually results in more generated CSS than when using a placeholder selector.
- Do not use parent selector references (`&`) when they would otherwise be unnecessary, e.g.

  ```
  .foo {
    > .bar {}
  }
  ```
  *not*
  ```
  .foo {
    & > .bar {}
  }
  ```
- Rule sets should be ordered as follows:
  1. `@extend` declarations.
  2. `@include` declarations without inner `@content`.
  3. Properties.
  4. `@include` declarations with inner `@content`.
  5. Nested rule sets.

## Naming conventions

Always ensure classes are sensibly named; keep them as short as possible but as long as necessary. Ensure any utilities are very vaguely named (e.g. `.u-display-block`, `.u-divider`) to allow for greater reuse. Don’t worry about the amount or length of classes in your markup; gzip will compress well written code incredibly well.

**ID's cannot be used as style hooks**, [see](http://cssguidelin.es/#ids-in-css).

[Further reading](http://cssguidelin.es/#naming-conventions).

### BEMIT

We use the BEMIT (Block, Element, Modifier, Inverted Triangle - [see information here](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)) naming convention. When BEMIT is not used e.g. [JavaScript hooks](#javascript-hooks) then we use hyphen delimited classes e.g. `.foo-bar`, not `.foo_bar` or `.fooBar`.

BEM is a methodology for naming and classifying CSS selectors in a way to make them a lot more strict, transparent and informative.

The naming convention follows this pattern:

```
.block{}
.block__element{}
.block--modifier{}
```

- `.block` represents the higher level of an abstraction or component.
- `.block__element` represents a descendent of `.block` that helps form `.block` as a whole.
- `.block--modifier` represents a different state or version of `.block`.

[Further reading](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).

### Namespacing

* o-: Signify that something is an Object, and that it may be used in any number of unrelated contexts to the one you can currently see it in. Making modifications to these types of class could potentially have knock-on effects in a lot of other unrelated places. Tread carefully.
* c-: Signify that something is a Component. This is a concrete, implementation-specific piece of UI. All of the changes you make to its styles should be detectable in the context you’re currently looking at. Modifying these styles should be safe and have no side effects.
* u-: Signify that this class is a Utility class. It has a very specific role (often providing only one declaration) and should not be bound onto or changed. It can be reused and is not tied to any specific piece of UI. You will probably recognise this namespace from libraries and methodologies like SUIT.
* t-: Signify that a class is responsible for adding a Theme to a view. It lets us know that UI Components’ current cosmetic appearance may be due to the presence of a theme.
* s-: Signify that a class creates a new styling context or Scope. Similar to a Theme, but not necessarily cosmetic, these should be used sparingly—they can be open to abuse and lead to poor CSS if not used wisely.
* is-, has-: Signify that the piece of UI in question is currently styled a certain way because of a state or condition. This stateful namespace is gorgeous, and comes from SMACSS. It tells us that the DOM currently has a temporary, optional, or short-lived style applied to it due to a certain state being invoked.
* _: Signify that this class is the worst of the worst—a hack! Sometimes, although incredibly rarely, we need to add a class in our markup in order to force something to work. If we do this, we need to let others know that this class is less than ideal, and hopefully temporary (i.e. do not bind onto this).
* js-: Signify that this piece of the DOM has some behaviour acting upon it, and that JavaScript binds onto it to provide that behaviour. If you’re not a developer working with JavaScript, leave these well alone.
* qa-: Signify that a QA or Test Engineering team is running an automated UI test which needs to find or bind onto these parts of the DOM. Like the JavaScript namespace, this basically just reserves hooks in the DOM for non-CSS purposes.

[Further reading](http://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)

#### State hooks

Any type of style that is **state** based e.g. a navigation link may be in an active state, an accordion section may be in an expanded state, should be namespaced with `.is-`, e.g. `.is-active`, `.is-expanded`.

State styles 90% of the time have a JavaScript/server-side dependency e.g. to highlight the active link in some primary navigation we will append `.is-active` to the relevant `a` element via server-side code, to style a component differently based on whether it only has one list item we would write some JS to check for this and if it's true append `.is-only-item` to the parent component element.

To keep things consistent we use a set list of common state class names:

- `is-active`
- `is-loaded`
- `is-loading`
- `is-visible`
- `is-only-item`
- `is-only-items-x` - where *x* is the amount of items
- `is-disabled`
- `is-expanded`
- `is-collapsed`

Where possible use these names rather than creating your own and we can always use these names as state styles are always scoped to the thing they're being applied too.

**State hooks do not use BEM.**

#### JavaScript hooks

***Never use a CSS styling class as a JavaScript hook***. Attaching JS behaviour to a styling class means that we can never have one without the other.

If you need to bind to some markup use a JS specific CSS class which is namespaced with `.js-`. So the naming convention would be something like: `.js-[component]-[what-it's-doing/UI-it's-affecting]`, e.g. `.js-accordion-header`, `.js-drag-and-drop`, `.js-carousel-items`.

This means that we can attach both JS and CSS to classes in our markup but there will never be any troublesome overlap.

A common practice is to use data-* attributes as JS hooks, but this is incorrect. data-* attributes, as per the [spec](http://www.w3.org/TR/2011/WD-html5-20110525/elements.html#embedding-custom-non-visible-data-with-the-data-attributes), are used to store custom data private to the page or application (emphasis mine). data-* attributes are designed to store data, not be bound to.

**JS hooks do not use BEM.**

##### Order of the above hooks

The order of the above hooks, within the `class` attribute, should be:

1. Style hooks:
    1. Component hook (no namespace)
    2. Layout hook (`.l-`)
    3. Utility hook (`u-`)
2. JS hooks (`.js-`)

Example:

```
<div class="pagination l-container u-text-align-center js-paginate test-pagination ga-pagination">
```





## Comments

We should document and comment our code as much as we possibly can, what may seem or feel transparent and self explanatory to you may not be to another dev. Write a chunk of code then write about it.

[Further reading](http://cssguidelin.es/#commenting).

### DocBlock-esque

For most of our comments we use a [DocBlock](http://en.wikipedia.org/wiki/PHPDoc#DocBlock)*-esque* style comment e.g.

```
/**
 * Settings.
 */
```

A DocBlock comment begins with `/**` and has an `*` at the beginning of every line. Any line within a DocBlock that doesn't begin with a `*` will be ignored, this technique is primarily used when referencing code so that the code can easily be copied to the clipboard e.g.

```
/**
 * N.B. This utility requires that you remove the whitespace between `li`s
 * especially with the Spacing modifiers. One way to remove whitespace is by
 * inserting HTML comments between the opening and closing `li`s e.g.
 *
   <ul class="u-list-inline">
     <li>Lorem</li><!--
     --><li>Aliquam</li><!--
     --><li>Vestibulum</li>
   </ul>
 */
 ```

If you use Sublime Text editor then install [this package](https://sublime.wbond.net/packages/DocBlockr) which makes writing DocBlock style comments super easy.


### Intro block

After the [main title](#main-title) comes the intro block comments which consist of:

- A general description that provides an overview of what the file is doing exactly, be as detailed as you can.
- Any dependencies on other files which should always be prefixed with `N.B.`.
- Sub sections prefixed with `@`:
    - `@todo` - any outstanding tasks.
    - `@demo` - a URL to a demonstration page.
    - `@markup` - markup example(s).
    - `@credit` - URL(s) to credit where the idea came from.
    - `@consideration` - any things to consider.
    - `@example` - Sass code example(s).

Examples:

```
    /**
     * Place any two elements side-by-side, typically for an image- and text-like
     * content.
     *
     * N.B. this utility is dependant on the following utilities:
     *
     * - Clear fix.
     * - New block formatting context.
     *
     * @credit
     * http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code
     */
```

```
    /**
     * Apply percentage based width classes with the option to apply at all the
     * main breakpoints. All the classes are the same as the Width settings found
     * in: Core -> Settings -> Widths, so `$one-whole` would be `.u-one-whole`.
     *
     * N.B. by default we're applying to the Lap breakpoint.
     */
```

```
    /**
     * Creates blocky list items out of a `ul` or `ol` with the option to add a
     * keyline separator between the list items.
     *
     * @consideration
     * The spacer utilities could replace this?
     *
     * @credit
     * https://github.com/inuitcss/objects.list-block/blob/master/_objects.list-block.scss
     */
```

```
    /**
     * A generic drop down utility powered by some JavaScript which toggles a
     * class e.g. `is-visible` on the drop down trigger (the button that makes the
     * drop down visible and invisible) and the target (the actual drop down).
     * This class will be used to make the drop down target visible when the
     * trigger is selected. There is also a version for showing the drop down via
     * the `:hover` pseudo class which is turned off for touch devices.
     *
     * @markup
       <div class="u-drop-down">
         <!-- The trigger -->
         <button class="u-drop-down__trigger"> ... </button>
         <!-- The target -->
         <div class="u-drop-down__target"> ... </div>
       </div>
     */
```

```
    /**
     * Generate percentage classes with the option to apply at different
     * breakpoints e.g. `.u-one-whole` / `.u-lap-one-whole`. The percentage classes
     * are based off the widths defined here: Core -> Settings -> Widths.
     *
     * N.B. the application for this mixin is quite unique so it's only used in a
     * few places in the framework.
     *
     * @example
       @include generate-percentage-classes-at-breakpoints(
         $breakpoints-for-grid-push-classes,
         $scally-type: "l",
         $class-name: "push",
         $css-property: "left"
       );
     */
```

**2 blank lines should always come after an intro block comment.**

### Section titles

Section title comments are used to break up large `.scss` files into their own logical sections so they're easier to read, however because we use compact Sass partials so extensively they're rarely needed. A section title is formatted like this:

```
/* Section title here
   ========================================================================= */
```

**4 blank lines should be between these section titles.**

### Sub titles

Each major chunk of CSS in a file should begin with a sub title comment e.g.

```
/**
 * Grid container.
 */
```

A full stop (period) should end the sub title comment.

**2 blank lines should come before and 1 blank line should come after these sub title comments.**

### Preprocessor comments

Sass allows us to use less verbose CSS comments prefixed with two forward slashes, like so: `// Some comment` e.g.

```
h1, .h1 {
  @include font-size($font-size-heading-1);

  // This is needed to turn off the top margin set in normalize.css
  margin-top: 0;
}
```

This type of comment style is used for when you need to explain what some CSS is doing, when it isn't obvious from the code itself that is, and when none of the aformentioned comment styles are appropriate.

A space should always come after the two forward slashes and when it spans multiple lines then each line should always start with the two forward slashes e.g.

```
// When specifying one breakpoint with an explicit limit, it needs to be
// casted into a list of lists, otherwise the mixin assumes there is a
// breakpoint called 'max'
```

**No blank lines should come after these type of comments.**

### Number labelling

When you want to easily comment on a number of declarations in a rule set then use number labelling e.g.

```
/**
 * Images.
 *
 * 1. Make responsive.
 * 2. So that `alt` text is visually offset if images don't load.
 */

img {
  max-width: 100%; // [1]
  height: auto; // [1]
  font-style: italic; // [2]
}
```

This should only be used when standard inline comments won't work i.e. in the above example it wouldn't be as readable if you had two inline comments for the no.1 declarations e.g.

```
img {
  // Make responsive
  max-width: 100%;
  // Make responsive
  height: auto;
  // So that `alt` text is visually offset if images don't load
  font-style: italic;
}
```

### Component-Extension pointers

When working across multiple partials and in an OOCSS manner sometimes we need to make adjustments to a component that exists within another component. This should be avoided in favour of using a BEM modifier on the component itself so that you don't end up with many dependencies across your components however sometimes this isn't the most appriopiate way of handling things. So in this scenario we need to include a comment to highlight this so that other developers are aware of the relationship between the files.

This is the format to use:

```
/**
 * Extend `.[component class]` in Components -> [component name].
 */
```

### BEM modifier comments

Whenever you're using BEM and you declare a modifier (see [Naming conventions -> BEM](#bem)) you need to include a comment and if required provide a brief explanation as to what it's doing, e.g.

```
/**
 * Modifier: striped.
 *
 * Applies a background colour to every odd row.
 */

.u-table--striped {
  tbody tr:nth-of-type(odd) td {background-color: $u-table-striped-background-cell-colour;}
}
```

```
/**
 * Modifier: border.
 */

.u-table--border {
  th,
  td {@include to-rem(border, $u-table-border-thickness $u-table-border-style $u-table-border-colour);}
}
```

### Settings comments

Any settings (Sass variables) defined in your Sass partials should always be placed before all other CSS in the `.scss` file and include a comment e.g.

```
/**
 * Settings.
 */

// Apply at these breakpoints
$u-drop-down-breakpoints: $default-breakpoints !default;
```

### TODO comments

To leave reminders of outstanding work for yourself or other developers prefix the comment with `TODO:` e.g.

```
// TODO: `.btn-main-compact-icon` needs more work
```

*If you use Sublime Text editor it will highlight these for you.*

### Non-JavaScript comments

Whenever you write some styles for non-JavaScript users always include a comment like this:

```
// Non-JS users
.no-js .selector {position: static;}
```

### `!important` comments

Whenever you write some styles that needs to use the `!important` keyword always include a comment like this:

```
// N.B. it is okay to use `!important` here as we're doing it pre-emptively i.e. you know you will always want the rule it's applied too to take precedence.
```

It acts as a nice reminder to other devs that you aren't using it incorrectly i.e. reactively.

### Other

1. When commenting on specific declarations (i.e. lines) in a rule set always place the comment on a new line above the declaration (one exception to this is when using [Number labelling](#number-labelling)) e.g.

    ```
    // Left double quotation mark
    content: "\201C";
    content: open-quote;
    ```

    ***not***

    ```
    content: "\201C"; // Left double quotation mark
    content: open-quote;
    ```
2. Use backticks when referencing code e.g.

    ```
    // We need to change the `box-shadow` at this breakpoint
    ```
3. Prefix important attention grabbing comments with **N.B.** e.g.

    ```
    // N.B: have to increase the specificity by chaining the base `.btn` class to make it easy to override non-simple modifiers
    ```
4. When you end a Sass `@if` statement then follow the closing bracket with `// endif`.




---

## Writing CSS

All of the above is about how we structure and form our CSS; they are very quantifiable rules. For how to deal with our attitude and approach to writing CSS we'll link to another set of guidelines:

- [CSS Selectors](http://cssguidelin.es/#css-selectors)
- [Specificity](http://cssguidelin.es/#specificity)
- [Architectural Principles](http://cssguidelin.es/#architectural-principles)





---

## Acknowledgements and Further Reading

- [CSS guidelines](http://cssguidelin.es)
- [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [OOCSS code standards](https://github.com/stubbornella/oocss-code-standards)
- [inuitcss](https://github.com/csswizardry/inuit.css)
- [SUIT CSS](http://suitcss.github.io/)
- [SMACCS](http://smacss.com/)
- [SOLID CSS](http://blog.millermedeiros.com/solid-css/)
- [One Module or Two](http://snook.ca/archives/html_and_css/one-module-or-two)
- [Our (CSS) Best Practices Are Killing US](http://www.stubbornella.org/content/2011/04/28/our-best-practices-are-killing-us/)
- [Keep your CSS selectors short](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
- [The single responsibility principle applied to CSS](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
- [Principles for writing good CSS](http://blog.kaelig.fr/post/38377421139/principles-for-writing-good-css)

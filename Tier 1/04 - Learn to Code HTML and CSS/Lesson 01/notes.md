Note to self: I need to enclose HTML tags in backticks, or else Git will parse them as actual HTML

# Lesson 1: Building Your First Webpage
## What are HTML and CSS?
HTML and CSS should remain as separate as possible. HTML defines the semantic structure of a document, while CSS defines
its styling. It's possible to have inline CSS, but that's probably super-jank.

## Understanding Common HTML Terms
The three main terms I need to familiarize myself with are elements, tags, and attributes.

### Elements
These are the parts that comprise the HTML document – they're the building blocks. Most elements are made of three
parts:
1. The opening tag
2. The content
3. The closing tag

Though there exist self-closing tags, which basically roll (2) and (3) into the opening tag.

### Tags
This is what encloses HTML elements to give them semantic meaning. All of them are letters enclosed in angle brackets,
e.g. `<p>`, `<a>`, etc.

### Attributes
These provide additional information to elements. One of the more common attributes is `id`, which marks an element as
being unique in a page. That is, there will be no other HTML elements with that same ID. Other common attributes
include:
* `class` – Adds an element to a class (basically a grouping)
* `src` – Defines the source of embeddable content
* `href` – For hyperlinks to other web pages.

## Setting Up the HTML Document Structure
Never, ever try to create HTML files in rich text editors, as they'll embed extra information inside the document that
will interfere with its ability to render properly.

All HTML documents require a `<!DOCTYPE html>` declaration, as well as `<html>`, `<head>`, and `<body>` elements. 

It is also possible to nest HTML elements inside of each other. When you do, it's generally a good idea to indent the
inner element.

### `<head>`
This is where metadata for the document lives, as well as where most links to other files will be declared. The majority
of the information will not be output directly to the screen, but through linking the HTML page to CSS and JS files, the
`<head>` indirectly affects a lot of the web page's appearance.

### `<body>`
This is where all the content for that the user sees goes.

### Self-Closing Elements
This list isn't exhaustive, but here is a list of common self-closing elements:
* `<br>`
* `<img>`
* `<meta>`
* `<wbr>`
* `<embed>`
* `<embed>`
* `<input>`
* `<param>`
* `<hr>`
* `<link>`
* `<source>`

## Code Validation
Always use HTML and CSS code validators before you ship off code for production. The W3C offers their own, but I'm sure
there are others that interface with code editors.

## Understanding Common CSS Terms
With CSS, there are three main terms that you'll want to familiarize yourself with. These are:
* Selectors
* Properties
* Values

### Selectors
A selector is just that: it selects an HTML element so that style can be applied only to that selection. You can also
get more specific or more general by mixing qualifiers together inside that selector.

The more common types of selectors select by ID, class, or element type.

If you use something like `p { ... }`, then you will select **all** `<p>` elements.

### Properties
But selectors don't do anything if you don't put anything inside them. This is where properties come in. They change the
the appearance of HTML elements, allowing you to modify things like color, size, and even layout.

All selectors require values, and each is terminated by a semicolon `;`.

### Values
Values and properties cannot exist by themselves. They need to exist in pairs. If selectors define which elements you
want to modify, properties define which aspects you want to modify, and values define how you want to modify those
aspects.

Selectors, properties, and values all together:
```css
p
{
    font-size: 2rem;
}
```

## Working with Selectors
As mentioned earlier, there are several types of selectors, which allow you to select elements by their type, their ID,
their class, and more.

### Type Selectors
These select all elements of a given type. If you want to select all `<p>` elements, then you need to use:

```css
p
{
    /* Properties and values go here */
}
```

### Class Selectors
This allows you to select elements by their class, which is an attribute defined in HTML. Classes allow you to select
elements that would otherwise be unrelated and apply the same styling to them. All class names in CSS are denoted by
the prefix `.` (e.g., `.className`), even though they don't have them in HTML.

HTML to markup:
```html
<h1 class="example">...</h1>
<p class="example">...</p>
```

And the CSS that would style them:
```css
.example
{
    /* Code */
}
```

### ID Selectors
These are even more precise than class selectors are, as – provided that you coded your HTML properly – they'll only
select one element at a time. Since IDs must be unique in valid HTML, ID selectors allow you to apply unique styling
to an element that receives most of its style from other selector types. All ID selectors must be prefixed by `#` in
CSS.

ID Selector:
```css
#example
{
    /* Code */
}
```

### Additional Selectors
The three aforementioned selector types only scratch the surface of what CSS can do. There are many other selectors
that allow you to create much more nuanced selections.

## Referencing CSS
Now, you've got an HTML file, and a CSS file*. How do you connect them, so that the CSS changes the presentation of the
HTML?

\* You should almost always keep your HTML and CSS in separate files. It helps keep them more manageable.

You can link the two files together through the `<link>` element, which lives inside the `<head>`. Modern HTML and CSS
only require that you declare two attributes within the `<link>` element: the `rel` (relationship) and the `href`
(hyperlink reference).

How it'll actually look:
```html
<head>
    <link rel="stylesheet" href="location/style.css">
</head>
```

## CSS Resets
Now, the browser will, by default, give a web page a set of pre-defined styles. Luckily, each and every one of these
can be overwritten, especially when each browser adds different styling. Because developers want to support browsers
as much as possible, things called resets and normalizers have become common. Both affect the browsers to try to get
their styling within a workable range of similarity. A reset will tend to try making all browsers look exactly the same.
A normalizer, however, will be more okay with websites not looking the same browser-to-browser, so long as the
differences don't detract from the developer-defined styles. In either case, you're giving yourself a new baseline to
start building on top of.

Of course, since CSS cascades from top to bottom, you'll want to place your reset/normalization at the top of the code,
ideally inside its own CSS file.
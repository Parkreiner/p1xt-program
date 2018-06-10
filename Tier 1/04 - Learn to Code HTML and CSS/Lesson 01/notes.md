Note to self: I need to enclose HTML tags in backticks, or else they'll get parsed as actual HTML

# Lesson 1: Building Your First Webpage
## What are HTML and CSS?
HTML and CSS should remain as separate as possible. HTML defines the semantic structure of a document, while CSS defines its styling. It's possible to have inline CSS, but that's probably super-jank.

## Understanding Common HTML Terms
The three main terms I need to familiarize myself with are elements, tags, and attributes.

### Elements
These are the parts that comprise the HTML document – they're the building blocks. Most elements are made of three parts:
1. The opening tag
2. The content
3. The closing tag

Though there exist self-closing tags, which basically roll (2) and (3) into the opening tag.

### Tags
This is what encloses HTML elements to give them semantic meaning. All of them are letters enclosed in angle brackets, e.g. `<p>`, `<a>`, etc.

### Attributes
These provide additional information to elements. One of the more common attributes is `id`, which marks an element as being unique in a page. That is, there will be no other HTML elements with that same ID. Other common attributes include:
* `class` – Adds an element to a class
* `src` – Defines the source of embeddable content
* `href` – For hyperlinks to other web pages.

## Setting Up the HTML Document Structure
Never, ever try to create HTML files in rich text editors, as they'll embed extra information inside the document that will interfere with its ability to render properly.

All HTML documents require a `<!DOCTYPE html>` declaration, as well as `<html>`, `<head>`, and `<body>` elements.

### `<head>`
This is where metadata for the document lives, as well as where most links to other files will be declared. The majority of the information will not be output directly to the screen, but through linking the HTML page to CSS and JS files, the `<head>` indirectly affects a lot of the web page's appearance.

### `<body>`
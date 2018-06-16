# Lesson 04 – Opening the Box Model
The box model is key to understanding how to lay out elements in HTML and CSS. But to understand that, you need to
understand exactly how elements are displayed.

## How are elements displayed?
Just as a quick refresher, HTML allows for two main types of element: block-level elements and inline elements. Block-
level elements push everything else after them onto a new line by default, while inline elements don't. The former is
generally used for for the main structural components of an HTML document, while the latter is for smaller elements,
like emphasis.

But *how* are they displayed?

### The `display` property
The `display` property is what decides how elements get displayed. A block-level element might get displayed as a block
in CSS, but that's only because that's the default value of the property. The same goes for inline elements. This means
that it's possible to overwrite this behavior, turning block elements inline or inline elements into blocks. Also, the
`display` value of an element determines which properties affect it. Inline elements can't take a `width` property, for
example.

While CSS has added more display values over the years (most notably, `flex` and `grid`), there are four types that have
pretty much been present since the beginning:
* `block`
* `inline`
* `inline-block`
* `none`

#### `inline-block`
The `inline-block` element is for when you want an element to be able to use block-level properties, but you don't want
it to push content that comes afterwards to a new line.

Just note that `inline-block` elements behave like `inline` elements in terms of flow. That is, any sets of space
between elements in the HTML structure will be rendered as spaces on the user's screen. There are ways to circumvent
this, but they'll get covered in the next lesson.

#### `none`
Giving an element a property of `display: none` will not just turn it invisible, but remove it from the flow of the
document. It'll be as if though that element never existed.

## What is the box model?
The box model, again, defines how HTML elements are displayed. By its specification, all elements, whether they're
squares/rectangles, circles, or triangles, are treated as boxes. So, a circle element will basically be inscribed 
inside its box, with the cardinal diameters touching the edges of the box.

## Working with the box model
All elements in the box model have a size, which can be either explicit or implicit. A size is explicit if it's defined
via CSS properties like `width` and `height`. A size is implicit if it's defined only by the content inside it, be it
made of elements or text.

There are several explicit size properties:
* `width` – Determines the width of a property
* `height` – Determines the height of a property

And these allow you to select all four directions or just one:
* `margin` – For giving an element margins that push it away from other elements.
* `padding` – For giving an element extra room inside itself
* `border` – For giving an element borders outside its padding (if it's there) or its main content

The total width of an element in CSS is given as:
```css
margin-left + border-left + padding-left + width + padding-right + border-right + margin-right
```

The total height isn't that different:
```css
margin-top + border-top + padding-top + width + padding-bottom + border-bottom + margin-bottom
```

The box model can be somewhat confusing at first. You would assume a property like `width` would refer to the entire
element, or at least everything but the margins, but by default, it only refers to the core of the element. All the
other properties are additive.

### Width and Height
Every element in HTML has a default size in CSS, defined in terms of `width` and `height`. A lot of the time, they'll
just be `0`, but every element must have some kind of size.

#### Width
The default width of an element depends on whether it's a block-level element or an inline element. Block-level elements
have a default width of `100%`, while the width of an inline element depends on the content inside it. The inline
element will expand and contract to fit everything inside. And to reiterate, elements with the `display: inline`
property don't accept `width` and `height` properties. If you want an inline element that will, you need to use
`display: inline-block`.

#### Height
The height of an element is independent of whether it's a block or inline. No matter what, the element will expand or
contract to contain all the elements and text inside it.

### Margins and Padding
This is often what screws up browser parity. Each browser has a different idea of how much padding and margin each
element type needs. However, it seems that it's mainly text-based elements that get affected by this. Other elements
might not get any margins or padding added at all.

#### `margin`
The `margin` property gives an element margins – invisible spacing that helps push it away from other elements. They can
be used both to determine the rhythm of a page or to give an element more breathing room.

Just note that elements with `display: inline` don't accept  most `margin` properties, either. If you want to give an
element margins, you'll have to sets its `display` value to either `block` or `inline-block`.

#### `padding`
The `padding` property isn't that different from the `margin` property; the main difference is that padding for an
element goes inside its borders for padding and outside for margins.

However, `padding` does actually work on `inline` elements, but only vertically.

#### `margin` and `padding` with inline elements
Just to make things super clear, `inline` elements can interact with the `margin` and `padding` properties; it's just
that they don't accept all of them.

* `margin` – Only horizontal values work on inline elements
* `padding` – Only vertical values work on inline elements

#### Padding and margin declarations
Up until now, the guide has modified margin values with `margin` and padding values with `padding`. However, both of
these are shorthand – they target their respective HTML aspects in all four directions, but it's possible to get
more specific with what they target.

When you use just `margin` and `padding` with a single value, that value will be applied in all four directions.
```css
p
{
    margin: 20px;
    padding: 30px;
}
```

But when you give either two values, the first will be applied vertically, while the second will be applied
horizontally:
```css
div
{
    margin: 2% 5%;
    padding: 50px 100px;
}
```

Use three values, and the first will be applied to the top, the second will be applied horizontally, and the third will
be applied to the bottom:
```css
nav
{
    margin: 0.1em 0.5em 0.2em;
    padding: 2% 5% 8%;
}
```

All of the above cases are still considered shorthand. For the longhand version, you need to append one of these
suffixes:
* `-top`
* `-bottom`
* `-right`
* `-left`

```css
article
{
    padding-left: 5%;
    margin-top: 60px;
    padding-right: 5px;
    margin-bottom: 2em;
}
```

If you only need to target one specific property, it's better just to use the longhand version, so that things are
more explicit for code maintainability.

#### Margin and Padding colors
Both `margin` and `padding` are transparent, which is why they don't accept color values. The space they affect can
be colored, though. An element's margins will assume the background color of its parent element, while its padding
will assume the background color of its content.

### Borders
All borders go between the affected element's padding and margins. However, unlike `padding` and `margin`, border has
three aspects that you can modify: width, style, and color. And like the other sizing properties, it can be written
as shorthand or longhand, but there are two sets of suffixes. You can mix-and-match any one suffix from both groups.

Directional suffixes (must come first if you're also using an aspect suffix):
* `-top`
* `-bottom`
* `-left`
* `-right`

Aspect suffixes:
* `-width`
* `-style`
* `-color`

```css
p
{
    border: 2px solid #000;
    border-width: 3px;
    border-top: 5px dotted #f00;
    border-bottom-style: dashed;
}
```

Like `margin` and `padding`, the `border-width` property can have 1–4 values, depending on how you want sides to be
affected. However, this does not apply to `border`.
```css
p
{
    border-width: 10px; /* All four directions */
    border-width: 5px 5px; /* Vertical, then horizontal */
    border-width: 2px 2px 2px; /* Top, horizontal, then bottom */
    border-width: 1px 1px 1px 1px; /* Top, right, bottom, left */
}
```

### Border Radius
The border radius property, despite the name, is used to round the corners of an entire element, minus its margins. It
accepts both relative and absolute units, too. And like all the above properties, you can either use shorthand or
longhand. But since you're dealing with corners, you don't proceed through properties in the traditional "start at the
top and go clockwise" way. You still go clockwise, but you start with the top-left corner. Basically, pretend that your
selections have rotated –45°.

Shorthand:
```css
div
{
    border-radius: 10px; /* All four corners */
    border-radius: 5px 5px; /* Top-left and bottom-right, then top-right and bottom-left. */
    border-radius: 2px 2px 2px; /* Top-left, then top-right and bottom-left, then bottom-right */
    border-radius: 1px 1px 1px 1px; /* Top-left, top-right, bottom-right, bottom-left */
}
```

Longhand uses these modifiers. Note that they go between `border` and `-radius` (e.g., `border-top-left-radius`):
* `top-left`
* `top-right`
* `bottom-right`
* `bottom-left`

## Box Sizing
All the examples so far have used the default behavior of the box model: additive behavior. CSS3 introduced a way to
change that, though, through the `box-sizing` property. The property accepts three values:
* `content-box` (default)
* `border-box`
* `padding-box`

### `content-box`
This keeps things exactly the same compared to normal. Everything remains additive.

### `padding-box`
This basically includes the element's content and padding when calculating an element's width and height. Borders stay
additive, but padding becomes subtractive. So, if you have an element with a `width` of `100px` and give it 
`padding: 10px`, then that will subtract `10px` from the sides of the element, leaving the core content with `80px`.

**Of course, none of this matters anymore, because this property has been deprecated.**

### `border-box`
As of 2018, this is only value of `border-box` (other than the default) that's still supported. With it, both `padding`
and `border` are included in `width` and `height` calculations. This turns both padding and borders subtractive, while
keeping margins additive. And again, since you can't specify the width of the main content separately, any padding and
borders that you add will eat away from the main content.

### Picking a box size
In general, you want to use `border-box` as your default property. It makes calculating dimension values easier, and it
makes the box model more predictable.

In addition, `border-box` still supports multiple value types for each property. So, if you give an element a width of
`40%`, then you're free to define its padding and margin in terms of pixels; the overall width will remain `40%`.

Nowadays, it should be safe to treat `border-box` as the default, but you might still run into a few issues when you're
trying to support every browser possible. 

## Browser Prefixes
It seems that this is becoming less of a thing, because browser makers are realizing how much adding a bunch of prefixes
for every little feature harms development. But you still need to use these if you want to support older browsers. The
prefixes are as follows:
* `-webkit-` – For Chrome, Safari, and newer versions of Opera
* `-moz-` – For Firefox
* `-o-` – For older versions of Opera
* `-ms-` – For Internet Explorer and Microsoft Edge

## Developer Tools
All browsers come with what are called developer tools. These allow you to inspect the underlying code of a HTML page
being rendered to your browser. They let you see how the HTML is laid out, as well as what CSS properties are being
applied to a given element. You can even use the "Select an element in the page to inspect it" tool to select a specific
element and see how it was implemented in HTML.

## The universal selector
In CSS, you can select all elements (as in, every single one, unqualified) with `*`.
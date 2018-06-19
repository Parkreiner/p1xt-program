# Lesson 5 – Positioning Content
CSS offers a **lot** of options for positioning elements. This chapter is going to focus on how to create reusable
style sheets, as well as how to position unique elements.

## Positioning with Floats
The CSS `float` property allows you to remove an element from the main flow of a document, making all other elements
flow around it. However, you can only float elements to the left or to the right. If you float an image inside a text
element, then the text will wrap around the image.

Properties (there are only two):
* `left`
* `right`

### Using `float` on multiple elements at the same time
when you use `float` on multiple elements that are back-to-back at the same time, they will all float up to the same
level. Look at this code:

```html
<div class="test"></div>
<div class="test"></div>
<div class="test"></div>
```

```css
.test
{
    float: left;
}
```

This will remove all three elements from the flow, but place them next to each other horizontally, pushing elements
below only if there isn't enough horizontal space.

Also, when you remove an element from the flow with `float`, you will send it all the way up to the top of its parent
(if there is one) or to the top of the page (if there isn't). And when you float an element, it will take on the width
of its content, unless you explicitly define those values.

### Using `float` on multiple elements not at the same time but with different properties
Even when you don't apply a CSS property to multiple elements at the same time, it's possible to make them sit next to
each other by giving a different property to each.

```html
<article></article>
<aside></aside>
```

```css
article
{
    float: left;
}
aside
{
    float: right;
}
```

### Floats changing an element's display value
Whenever you apply the `float` property to an element, its `display` value will change to `block` if it isn't already.
Be careful about using the property; you don't want to be surprised by an implicit change. If an `inline` element gets
floated, then it will start accepting `width` and `height` properties, even if it isn't obvious that it is from the
code.

### Clearing and containing floats
Now, `float` isn't a bad property. There are now dedicated layout properties defined in CSS, but `float` was able to
carry its weight for more than a decade. But it shouldn't have needed to: `float` isn't a layout property, and it was
never intended to be used as one. It was only ever meant to be used with images and text, which is why you can run into
some issues when using the property for layout.

One problem is that removing an element from flow can negatively impact its parent or the elements that surround it. It
seems that this most commonly affects normal flow elements' margins and padding. The elements that are still in normal
flow might blend together with the floated element. Or they might wrap around it.

There are two solutions:
1. Clear the float
2. Contain the float

#### Clearing floats
To clear a float, you need to give the `clear` property to the element that you don't want to interact with a floated
element. The property can take a few values, but the three most common are `left`, `right`, and `both`. In general, it's
safe to just default to `both`.

Whenever you use this property, the affected element will be forced to return to normal flow.

#### Containing floats (aka, using a clearfix)
It seems that in most cases, this is just as effective as using the `clear` property on an element. However, it also
seems that it might be a little better about maintaining styles?

The basic idea behind this approach is that you place the element that you want to float inside a parent element. So,
you're still floating something, but it's contained inside another element that's part of the normal flow. From there,
you just need to add some CSS to the parent. In the below example, the `group` class is used for all parent elements of
the aforementioned type:

HTML:
```html
<header>...</header>
<div class="group">
    <section>...</section>
    <aside>...</aside>
</div>
<footer>...</footer>
```

CSS:
```css
.group:before, .group:after
{
    content: "";
    display: table;
}
.group:after
{
    clear: both;
}
.group
{
    clear: both;
    *zoom: 1;
}
section {
  float: left;
  margin: 0 1.5%;
  width: 63%;
}
aside {
  float: right;
  margin: 0 1.5%;
  width: 30%;
}
```

In the above code, the `*zoom` is an IE hack. Placing an `*` before a property name will cause a parsing error in most
web browsers, meaning that it will be ignored. IE7 is a little special, though. This means that the property will *only*
be read by IE with a version of 7 or lower.

As for what it's actually doing, `:before` and `:after` refer to elements that are dynamically generated when HTML code
is parsed. The `:after` elements clear themselves, returning them and any elements that follow to normal flow. But the
`.group` elements also clear themselves, to return themselves to normal flow, just in case they come after other floated
elements.

**This specific technique is also called a clearfix.** Some developers will even `clearfix` as their parent class name,
rather than `group`.

## Positioning with `inline-block`
`inline-block` is a possible value of the `display` property. It basically turns an element into an inline element, but
allows block-level properties to affect it. Most of the time, this will be used to render elements side-by-side.

Unfortunately, it can be a pain to work with. Because they're treated as inline elements in terms of layout, any spacing
(spaces, tabs, new lines) between each element will be rendered as a space in the document.

### Removing spaces between `inline-block` elements
There are a number of ways of circumventing this behavior, but the guide is only going to focus on the simplest ones,
all of which involve only HTML.

Solution 1: Place all elements on the same line
```html
<div>...</div><div>...</div><div>...</div>
```

Solution 2: Place the start of a new element at the end of the previous one
```html
<div>
    ...
</div><div>
    ...
</div><div>
    ...
</div>
```

Solution 3: Break up the element tags
```html
<div>...</div><
div>...</div><
div>...</div>
```

Solution 4: Place empty comments between them.
```html
<div>...</div><!--
--><div>...</div><!--
--><div>...</div>
```

### The decline of `inline-block` elements
The guide doesn't mention this (presumably because it was written a few years ago), but it seems that `inline-block`
elements are falling out of favor, because flexbox has eaten their lunch. Flexbox allows you to achieve very comparable
functionality, all while not having to deal with issues like whitespace.

## Creating reusable layouts
Regardless of what you use to create the layout of a website, you want to write your code so that you can reuse it. This
is obvious to some degree, as you want some uniformity between different pages of the same site. However, you should
be designing things as small components, making them as modular and reusable as possible. This way, you can mix and
match them as the situation requires.

## Additive Padding
Whenever you have two or more elements sitting next to each other, be careful of their horizontal padding. If both
elements have 15px of padding on their left and right, then the space between them will have 30px of padding. One way of
getting around this is by wrapping them in a container and giving that the same amount of padding on both sides. This
way, the padding for the left side of the container will add to the padding of the left side of the first element. The
right padding of the first element will then add to the left padding of the second element, and the right padding of the
second element will add to right padding of the container.

```
[]: Element
-: Container padding
*: Padding for left element
^: Padding for right element

-*[]*^[]^-

```

## Uniquely positioning elements

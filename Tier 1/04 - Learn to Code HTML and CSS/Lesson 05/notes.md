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

One problem is that removing an element from flow can negatively impact its parent or the elements that surround it.

**STILL ON THIS SECTION**
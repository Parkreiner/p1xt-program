# Lesson 8: Creating Lists
HTML provides three forms of lists: ordered lists, unordered lists, and description lists.

## Unordered Lists
An unordered list (indicated by the `<ul>` block-level element) is for a collection of items for which the order doesn't
matter. Each item in an unordered list uses the `<li>` element. The browser will then, by default, style each item by
placing a bullet point next to it and applying a `margin-left` value.

## Ordered Lists
Like unordered lists, ordered lists (represented by the `<ol>`) element indicate a thematically-tied collection of
items. Each item with the block element must also be wrapped inside an `<li>` element. However, as the name would
suggest, a `<ol>` element places semantic importance on the order in which the elements are placed inside it.

And since the order matters in this type of list, all elements, by default, are preceded by a number that increments by
1 with each element in the list.

### The `start` attribute
The `start` attribute allows you to define the starting number in an ordered list. However, it only accepts integer
values, even though ordered lists can be changed to use things like Roman numerals.

```html
<ol start="30">
    <li>Head North on N Halsted St.</li>
    <li>Turn right on W Diversity Pkwy</li>
    <li>Turn left on N Orchard St</li>
</ol>
```

### The `reversed` attribute
The `reversed` attribute was added in HTML5, which is what allows it to forego a value. Using this attribute indicates
that the list is written in reverse order, so the browser will prepend the first element in the list with a number equal
to the list's length. It'll then decrement by 1 until the last item.

If you use this attribute together with the `start` attribute, the list will start counting at the `start` attribute's
value and then decrement by 1 with each element.

## Using the `value` attribute on an `<li>` in an ordered list
This attribute can only be applied to individual `<li>` elements with an ordered list. It allows you to override the
value the list item would normally display. However, any following elements will start counting from the new value.

```html
<ol>
  <li>Head north on N Halsted St</li>
  <li value="9">Turn right on W Diversey Pkwy</li> <!-- Next item will have a 10 in front of it -->
  <li>Turn left on N Orchard St</li>
</ol>
```

## Description Lists
Description lists are used to organize definitions, such as in a glossary. They're also a little different compared to
the other two types. For one, they don't use `<li>` elements; instead, you need to use a combination of two elements
for each list item: `<dt>` (description term) and `<dd>` (description definition). It's also possible to have multiple
terms for a single definition, just as it's possible to have multiple definitions for a single term. However, any `<dt>`
elements must come before any `<dd>` elements.

By default, both `<dt>` and `<dd>` elements will have a `margin-left` value. Curiously, these elements don't have list
markers applied to them by default.

```html
<dl>
    <dt>Study</dt>
    <dd>The act of devoting time and attention to a subject to increase one's knowledge in it.</dd>
    
    <dt>Design</dt>
    <dd>The act of creating a plan for how something should look and/or function.</dd>
    <dd>The plan for how something should look or function</dd>

    <dt>Work</dt>
    <dd>A person's regular occupation, profession, or trade</dd>
    <dd>Effort or services rendered for some form of compensation.</dd>
</dl>
```

## Nesting Lists
HTML allows you to nest lists. All you need to do is place one list in an `<li>` of another list. You can even mix
ordered and unordered lists.

## `<li>` list items
The `<li>` element is unique in that it lets you place **any** block-level or inline elements inside it. So presumably,
you could throw things like blog posts inside an `<li>`, provided that there are enough to warrant putting them in a
list.

## List item styling
By default, each item in a list has a marker placed next to it. CSS lets you change the style of the marker, as well as
where it's placed.

### `list-style-type`
This property can be applied to `<ul>`, `<ol>`, and `<li>` elements. It allows you to place any kind of list marker next
to an element, regardless of the list type. So, you can give ordered markers to an unordered list, or you can give
unordered markers to an ordered list.

#### Common values for `list-style-type`
* `none` – Displays no marker
* `disc` – Basically a bullet
* `circle` – A hollow circle
* `square` – A filled square
* `decimal` – Decimal numbers
* `decimal-leading-zero` – Decimal numbers with leading zeroes for padding
* `lower-roman` – Lowercase roman numerals
* `upper-roman` – Uppercase roman numerals
* `lower-greek` – Lowercase greek letters, starting with α (**no uppercase version**)
* `lower-alpha` / `lower-latin` – Lowercase Latin letters
* `upper-alpha` / `upper-latin` – Uppercase Latin letters
* `armenian` – Traditional Armenian letters
* `georgian` – Traditional Georgian letters
* `hiragana` – Regular hiragana (あかさたな)
* `hiragana-iroha` – Hiragana ordered based on the iroha (いろはにほへと)
* `katakana` – Regular katakana

#### Using an image as a list marker
Back when this guide was written, the standard practice for using an image as a list item marker was removing any and
then using a combination of `background-image` and `padding-left` to fake a marker. Nowadays, though, you can do the
same thing with the `list-style-image` property. It takes a URL as its sole property.

### `list-style-position`
This property allows you to change where your list marker is placed. By default, it will be outside the element.
However, by setting this property's value to `inside`, you can bring the marker inside the element itself. Just note
that when a marker is set to outside, it's possible for it to be cut off, because the browser won't try to preserve the
markers the way it tries to for the main content. That's why browsers apply a `margin-left` value by default.

## Horizontal Lists
There are several reasons why you would want to display a list horizontally, from navigation lists to turning each item
into a column. There are a few ways of doing this (aside from Flexbox, which I'm pretty sure is what I should be using
nowadays).

### Changing the `display` property
One of the quickest ways of doing this was by changing the list items' display property to `inline-block` or even just
`inline`. Just note that you'll need to compensate for whitespace and that the elements will be incapable of displaying
list markers. Trying to set them will do nothing.

### Floating the items
Setting the display value of a set of list items to `inline-block` is easy, but sometimes, you do want to retain the
marker, then your only option (ignoring Flexbox) is to float the items. However, if you have your markers set to display
outside, then while the items won't overlap, the markers will. To solve this, you need to give the elements a `margin`
property.

## Navigational Lists
Navigational lists are very common in HTML. This is most often done by placing a `<ul>` inside a `<nav>` element.
However, some of the implementation has changed thanks to Flexbox. Navigation lists prior to Flexbox have to use
`inline-block` elements, using a ton of hacky nonsense to compensate for things like whitespace. Modern browsers,
though, don't have to worry about that; you just have to set the `<ul>` to `display: flex`.  So, the semantics haven't
changed at all, but the code has a little bit, both in the HTML and the CSS.

-------STOPPED AT ITEM 3 OF THE FIRST "IN PRACTICE"-------
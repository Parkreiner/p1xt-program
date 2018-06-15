# Lesson 3: Getting to Know CSS

## The Cascade
The cascade is key to understanding exactly how CSS works. In CSS, styles are read from top to bottom. In a lot of
cases, if there are conflicts between two styles, whatever style is physically lower will be used. This means that
when you have conflicts, the second style will generally overwrite the first.

In the below case, the second `p` selector overwrites the first. However, only the `background-color` property is
affected. The `font-size` declared in the first selector remains.
```css
p
{
    background-color: orange
    font-size: 24px;
}
p
{
    background-color: green;
}
```

### Cascading Properties
You can even cascade properties within the same selector, though I'm not sure why you would ever want to do that.

```css
p
{
    background-color: orange;
    background-color: green;
}
```

## Calculating Specificity
Unfortunately, things in CSS aren't always clear-cut. The above examples apply because the selectors were of the same
*specificity*. As mentioned in lesson 1, there are three main CSS selectors: type, class, and ID. Each of these is
weighted differently.

It's perhaps best to visualize specificity like so: 0-0-0.
* The type selector adds 0-0-1.
* The class selector add 0-1-0.
* The ID selector adds 1-0-0.

The weighting increases as you go from right to left. However, theres's a reason why the numbers are hyphenated. Sure,
001 is less than 100, but without the hyphens, the notation would imply that it's possible to roll over values. For
example, 10 type selectors do **not** equal one class selector. The former is 0-0-10, while the latter is just 0-1-0.
This also means that a single class selector will **always** have more precedence over an infinite number of type
selectors that have nothing else.

Take a look at this HTML:
```html
<p id="example"></p>
```

Now look at this CSS:
```css
#example
{
    background-color: blue;
}
p
{
    background-color: red;
}
```
Even though the `p` selector comes after the `#example` selector, it can't change anything. It doesn't have more
precedence. So, if you have an ID selector and a thousand type selectors, it doesn't matter where you place the ID
selector; it'll always take precedence.

Of course, these rules exist only to help resolve property conflicts. If the selectors change different properties,
then they'll be able to play along no problem.

## Combining Selectors
It's possible to get very specific with which HTML elements you select. For example, by combining a `.dog` class
selector with a `p` type selector, you can select all `<p>` elements that exist within the `.dog` element.

```html
<div class="dog">
    <p> ... </p>
    <p> ... </p>
    <p class="special"> ... </p>
</div>
```

```css
.dog p
{
    background-color: black;
}
.dog p.special
{
    background-color: yellow;
}
```

Now, when reading combined CSS selectors, you need to read them from right to left. The selector closest to the opening
brace is called the *key selector*, because it's the selector that actually determines which element gets targeted.
Everything else that comes before it just pre-qualifies the selection.

So, for the first selector, you've got two selections – `.dog` and `p`. `.dog` is a class selector, while `p` is a type
selector. `p` also happens to be the key selector. So, in effect, the combined selector selects all `p` elements, but
is then is pre-qualified to select only those that exist within `.dog` elements.

As for the second selector, you've got three selections – `.dog`, `p`, and `.special` – the –`p` and `.special` elements
just happen to be linked. So again, you start at the right – `.special` – which then gets qualified by `p` to target all
`p` elements with the `.special` class. Then that gets qualified by `.dog` so that you select all all `p` elements with
the `.special` class that live inside the `.dog` class. In this case, `.special` is the key selector.

### Spaces within selectors
Be extra careful with where you place spaces in your selectors, as they can change the meaning. When you combine a type
selector with a class or ID selector but don't use a space (`p#example` or `li#example`), that targets all elements that
have both that type and that class. But when you put a space between them, that means that you're looking for elements
nested within each other. So, something like `a #example` would target all elements with the `#example` class that are
nested within the `a` element.

Basically:
* Spaces – You're looking for the element that comes after the space inside the element that comes before the space
* No Spaces – You're looking for elements that have all the properties specified; you don't care about their inner content

## Specificity with Combined Selectors
When you combine multiple selectors into a single selector, that new selector has the total weighting of its parts. So,
say that you have a selector like `#blue p.red li#purple a`, that has two ID selectors, two type selectors, and a class
selector. That gives it a combined weight of 2-1-2. It will have precedence over all selectors that have less than two
IDs.

Just be extra, super careful with your specificity. If your specificity values get too high – or, more specifically, if
you need that level of specificity – that should be a clue that your code is getting out of hand.

## Layering Styles with Multiple Classes
One of the best ways of keeping specificity under control is by making everything modular. And the best way to do that
is by giving an element multiple classes.

Since elements can have multiple classes, you can create a style for a broad category of elements, and then create new
styles for specific kinds of those elements. 

```html
<a class="btn btn-danger"> ... </a>
<a class="btn btn-success"> ... </a>
```
```css
.btn
{
    font-size: 16px;
}
.btn-danger
{
    background-color: red;
}
.btn-success
{
    background-color: green;
}
```

In the above code, you define three classes. One of them (`.btn`) is effectively the baseline. It defines styles for
**all** buttons. From there, `.btn-danger` defines styles for a "danger" style of button, while `.btn-success` defines
styles for a "success" style of button. Because `.btn-danger` and `.btn-success` are placed after `.btn` in the CSS,
they'll win in any style conflicts, even though they all have the same level of precedence.

Unfortunately, this does require a bit of trigger discipline on your part. There is nothing stopping you from using the
`.btn-success` class on another, unrelated element. You're *choosing* to make `.btn-success` be a subset of `.btn`; that
choice is a construct.

## Common CSS Property Values

### Colors
There are multiple ways of specifying color in CSS:
* RGB and RGBa
* Hex
* HSL and HSLa (newer and not as widely-supported)
* Pre-defined color names

Here are examples of how to format each:
* RGB - rgb(0, 0, 0)
* RGBa - rgba(147, 255, 10, 1)
* Hex - #abfcd4 or #e3f
* HSL - hsl(250, 100%, 24%)
* HSLa - hsla(117, 25%, 100%, 0.75)

#### Alpha Chanels
Both HSL and RGBA have versions that support alpha channels. For both, the alpha value comes last, and it's a number
between 0 and 1 (both inclusive). 0 is fully transparent, while 1 is fully opaque.

### Lengths
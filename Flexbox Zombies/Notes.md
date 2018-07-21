
# Chapter 1: `flex-direction`

## Enabling Flexbox

To enable flexbox on a container element, all you need to do is give it the CSS property `display: flex`. By default,
this will also set its `flex-direction` property to `row`, making it display content from left to right.

## Changing Flex directions

But `flex-direction` can take multiple other values. For positioning content horizontally, you have `row` (left to
right) and `row-reverse` (right to left). For vertical positioning, you have `column` (top to bottom) and
`column-reverse` (bottom to top).

# Chapter 2: `justify-content`

## The `justify-content` property

Using `justify-content` is like justifying text, but for flexbox elements. Note that the word is "justify", not "align".
When you set text to justify left, every line except for the final one will span the entire width of its "container".
However, the final line, which won't have enough characters to reach the end, will start from the left and then leave
whatever space couldn't be filled empty.

Justified flex elements are the same. If you set the value of `justify-content` to `flex-start`, then content will start
from the beginning of the flex direction. If there's enough content to span multiple lines, then the content that breaks
onto the final line will also start from the flex direction. However, everything on all the other lines will become
fully justified, making them all evenly-spaced.

The property has a couple of values:

* `flex-start` - The items on all lines but the final one will be evenly-spaced. The content on the final one will start at the beginning of its flex flow.
* `flex-end` - The items on all lines but the final one will be evenly-spaced. The content on the final one will start from the end of its flex flow.
* `center` - The items on all lines but the final one will be evenly-spaced. The content on the final one will start from the center.
* `space-around` - Ensures that each element has an equal amount of spacing on its sides parallel to the flex direction. This means that the elements will have two "units" of spacing between them, but there will only be one "unit" between them and the container edges. The amount of space will remain evenly-distributed even if each element has different margins.
* `space-between` - Ensures that the content on **all** lines is evenly-spaced. If there are two elements, each will hug the edges of the line. If there is only one element, it will start at the beginning of its line's flex flow (e.g., a container with `flex-direction: column-reverse` will have the element start at the bottom).
* `space-evenly` - This is basically `space-between`, except that the outermost elments don't hug the edges of the container. This means that there is an equal amount of spacing between all elements. You don't get doubled spacing like you do with `space-around`.

### `space-around` vs `space-between`

The best way to remember the difference between these two is to take their names literally. `space-around` ensures that
there is an even amount of space **around** each element. Because the flex container doesn't take the spacing between
the elements into account, the elements will have two units of spacing between them. `space-between` ensures that there
is an even amount of space **between** each element, which is why it doesn't add any spacing to the elements that hug
the edges. There aren't any elements opposite those sides, so there's no need to add spacing.

# Chapter 3: `align-items`

# Chapter 4: `align-self`

# Chapter 5: `flex-grow`

# Chapter 6: `flex-shrink`

# Chapter 7: `flex-basis`

# Chapter 8: `order`

# Chapter 9: `flex-wrap`

# Chapter 10: `align-content`

# Chapter 11: `flex` and `flex-flow`
# Lesson 6: Working with Typography
I don't know how long it took before embedding typefaces became a thing, but I'm so glad that I don't have to deal with
such a limited palette.

## Adding Color to Text
Changing the color of text through CSS is easy. You just have to use the `color` property. It only accepts one value,
but like `background-color`, it can accept many different formats.

## Changing Font Properties
There are two main groups of properties for changing how text appears on a page: text-based properties and font-based
properties. The former will generally be prefixed by `text-`, while the latter will generally be prefixed by `font-`.

### `font-family`
This is the property that determines which font file gets used to render text to the screen, as well as what fonts to
use as fallbacks. When you use this property, you can also declare a font stack – a series of fonts and fallbacks
separated by commas. With it, the browser will read through the fonts one-by-one, starting from the left. If it detects
that the system has a font, it'll use it and stop looking. If it doesn't find it, though, it'll move to the font
directly to the right. If it manages to go through all the options and still can't find a font that's on the system,
then nothing will display.

There are a few more quirks, though. For one, all font names that consist of multiple words must be wrapped in quotation
marks. Second, CSS provides keywords for specific styles of fonts. When the browser encounters this keyword, it'll use
a system font in that style, though which get selected first depends on the system itself. The keywords are as follows:

* `serif`
* `sans-serif`
* `monospace`
* `script`
* `cursive`
* `fantasy` – Quirky faces like Impact and Papyrus
* `system-ui`

### `font-size`
This property lets you set the size of some text. You can define it in terms of pretty much all the common units of
measurement (`px`, `em`, `%`*, etc.). You can also use the `pt` unit of measurement, as well as keywords exclusive to
this property:

#### General keywords
* `xx-small`
* `x-small`
* `small`
* `medium`
* `large`
* `x-large`
* `xx-large`

#### Relative keywords
* `smaller` – Decreases size by one level
* `larger` – Increases size by one level

\* Note that it seems that the `%` unit will be based on the font-size of its parent. Presumably, it'll go up parent
levels until it finds one that has a font size defined.

### `font-style`
Allows you to change the font style of some text, shifting between related families within the same typeface. There are
four possible values (aside from the general global values):

* `normal` (roman)
* `italic`
* `oblique`
* `oblique <degrees>` (e.g., `oblique 20deg`)

I know the difference between italics and obliques, but I don't know how browsers handle the keywords. All I know is
that if you set a font to `italic` or `oblique`, and the corresponding family doesn't exist, the computer will generate
an oblique of its own. It's super-nasty for very dense non-western characters like kanji. If the characters are small
enough, then they'll be completely unreadable on your typical computer monitor. Phones tend to fare a little better.

### `font-variant`
I don't know why this property has this name, when it's used exclusively for small caps. Again, I don't know how well
browsers actually support this feature. All I know is that if you use this property on a face that doesn't have unique
characters, the browser will generate small caps of its own, which will often look straight-up jank.

#### There are two main properties
* `normal`
* `small-caps`

### `font-weight`
This is what determines the weight of a typeface, but again, I don't know how well it's supported. I'd imagine that
faces that use the standard names will work just fine, but there are some fonts that use unique names for their weights.
I have no idea how those would render. Knockout is a good example; I have no idea how "No. 27 Junior Lightweight" would
translate.

#### There are three main options for this property's value
* Font weight value ranging from `100` to `900`; values increment by 100
* `normal` (equivalent to `400`)
* `bold` (equivalent to `700`)

If you try using a weight that a font doesn't support, then the browser will go to the nearest weight. Luckily, the
browser's smart enough to know that it shouldn't try to generate a black weight from a normal weight.

### `line-height`
This property determines the leading of an element's text or child that contains text. However, it isn't quite leading
in the traditional sense. True leading is measured by the distance between baselines. In CSS, `line-height` refers to
the "padding" that gets added above and below a line. So, if you set the line-height of an element to `20px`, `10px`
will get added above and below the first line. The same will happen for all following lines. So, when you have two
lines, the `10px` from below the first line will add to the `10px` from above the second line, adding up to `20px`.

But because `line-height` adds spacing to the top of an element, it will change how a single line gets displayed, which
leading doesn't do. It also seems that `line-height` spacing is applied above the ascenders and below the descenders.

#### Using `line-height` to center text
This feels hacky, but because the `line-height` property adds spacing above and below, you can use it in conjunction
with `height` to center single lines of text.

```css
.btn
{
    height: 22px;
    line-height: 22px;
}
```

### The `font` shorthand property
You can use `font` as shorthand for all the font-based properties, including line-height. You need to place them in this
order from left to right:
1. `font-style` (optional)
2. `font-variant` (optional)
3. `font-weight` (optional)
4. `font-size` **(not optional)**
5. `line-height` (optional)
6. `font-family` **(not optional)**

**However**, the formatting is a little quirky. In general, all the properties are separated by spaces. But the
`font-family` property separates all fonts in its stack with commas. In addition, you need a `/` between the `font-size`
and `line-height` properties.

## Pseudo-Classes
Pseudo-classes allow you to define styles for various general states of a property. For example, `a:hover` will define
styles that should display when 

### Children of Pseudo-Classes
In CSS, you can select children of a pseudo-class. So, if you have a `<p>` element inside an `<a>` element, you could
use a `a p` selector, but you can also use a `a:hover p` selector. This means that the `<p>` element will only be
affected when the user hovers over the `<a>` element.

## Applying Text Properties
As great as the font-based properties are, they only account for half of the properties you can add to text. There are
still the text-based properties.

### `text-align`
This element is for determining the alignment of the text. There are five primary values:
* `left`
* `right`
* `center`
* `justify`
* `inherit`

However, you should not think that this property is similar to a float. Floating an element moves the container itself.
When you use `text-align`, the container will stay put, but the inner text will change positions. 

### `text-decoration`
This property basically allows you to create lines for your text, whether they be underlines, overlines, or
strike-through lines. However, this property is just shorthand for the `text-decoration-line`, `text-decoration-color`,
and `text-decoration-style` properties. When you use the shorthand, only the `text-decoration-line` value is required.

**However, this property wasn't always shorthand. Even now, not all browsers support the more specific versions.** 
Splitting the property up is actually a pretty recent change – Chrome only added it in early 2017. It might be best just
to use `text-decoration` for everything. 

#### `text-decoration-line`
Determines what kind of line gets used. Three primary values:
* `underline`
* `overline`
* `line-through`
* `none`

#### `text-decoration-color`
Takes any of the general color values (RGB, HSL, Hex, etc.)

#### `text-decoration-style`
Defines how the line is styled. Five primary values:
* `solid`
* `double`
* `dotted`
* `dashed`
* `wavy`

#### What to use when you want to support older browsers
If you want to support older browsers, then you're stuck with a very limited version of the property. Just use
`text-decoration` and only use the `text-decoration-line` property values.

### `text-indent`
This property is used to indent the first line of an element. All standard sizing units (px, em, %, etc.) are accepted.
You can also use postive and negative values. Use a big enough value, and the text will go off the page (without
causing any scrollbars to appear).

### `text-shadow`
This is basically a drop shadow for text. The property takes four values, in this order:
1. Horizontal offset
2. Vertical offset
3. Blur radius
4. Shadow color

So, if you use `text-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3)`, you'll create a shadow that is `5px` to the right of and
below the position of the element it affects. It will be blurred by 10px, and the shadow will be pure black with 30%
opacity. Had you used `–5px` for the first two values, it would've been offset to the left and up.

But what's most interesting is that the property allows you to define multiple shadows for the same property. All you
have to do is separate them with commas. Whenver you use multiple shadows, each one beyond the first will be placed
below the one that came before.

### `box-shadow`
This property is basically the same as `text-shadow`, except that it works on elements. However, it does accept two more
optional values. The first, `inset`, goes before everything else and places the shadow inside the element. The second
goes just before the color and affects the spread. The spread affects how much of the blur is filled with a solid color,
starting from the center.

#### The order
1. The `inset` keyword (optional)
2. Horizontal offset
3. Vertical offset
4. Blur radius
5. Spread (optional)
6. Shadow color

### `text-transform`
This is for applying case styles to your text without changing your HTML. There are five main values:
1. `capitalize` (capitalizes the first letter of each word)
2. `uppercase` (sets the entire text in all-caps)
3. `lowercase` (sets the entire text in purely lowercase characters)
4. `inherit`
5. `none`

### `letter-spacing`
This property affects a text element's tracking. 
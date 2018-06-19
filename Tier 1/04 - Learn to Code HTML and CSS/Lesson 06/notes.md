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
measurement (`px`, `em`, `%`, etc.). You can also use the `pt` unit of measurement, as well as keywords exclusive to
this property:

#### General keywords:
* `xx-small`
* `x-small`
* `small`
* ``
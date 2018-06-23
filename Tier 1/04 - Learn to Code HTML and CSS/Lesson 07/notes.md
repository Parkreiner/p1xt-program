# Lesson 7: Setting Backgrounds and Gradiants

## Adding a background color
The quickest way to give an element a background is by using either the `background` property or the `background-color`
property. `background` is just shorthand for all background-related properties, while `background-color` is specifically
for setting background colors.

When you're just setting a background color, you can use any of the standard color formats, including ones that support
alpha channels.

### Transparent backgrounds
This isn't as much of a problem nowadays, since most browsers support transparency, but it's still a good idea to
provide a fallback for when someone's browser doesn't support alpha color values. You can do this by defining the
fallback color, followed by the color you actually want to use.

When you do, the main color will be applied for all browsers, but then they'll try to process the color you actually
want to use. The browsers that don't support it will ignore it and move on, but all others will override the fallback.
Had you done things in reverse, the main color would be applied, but then modern browsers would've overridden it with
the fallback, making things jank for everyone.

```css
div {
    background-color: #b2b2b2;
    background-color: rgba(0, 0, 0, 0.3);
}
```

## Adding background images
You can also use an image as a background. But since images are of fixed size and won't always fill their element,
CSS provides a number of properties for compensating. Like with defining background color, you can either define the
image with the `background` shorthand property, or the more specific `background-image` property. Whichever you choose,
the image source is provided through the `url()` function.

```css
div {
    background-image: url("example.png");
}
```

By default, most browsers will tile their backgrounds, repeating them both vertically and horizontally. Also, adding
padding will not move the background image; it'll only move the main content.

### `background-repeat`
This property allows you to define how a background is repeated (by default, only horizontally, only vertically, or not
at all).

There are only four main values:
* `repeat`
* `repeat-x`
* `repeat-y`
* `no-repeat`

### `background-position`
By default, all background images (especially those that aren't tiled) will start in the upper-left corner. The
`background-repeat` property lets you offset the image relative to its starting point. However, there is a wide range of
values that this property supports. It supports all the basic measurement units, but it also supports specialized
keywords, all of which can be combined with themselves and the more general units.

The keywords:
* `center`
* `top`
* `left`
* `right`
* `bottom`

Used together:
```css
div {
    background-image: url("dumb.png");
    background-repeat: no-repeat;
    background-position: right bottom;
}
```

The above code will place the image to the bottom-right of the element it's being applied to. It's equivalent to
`background-position: 100% 100%`. Just be aware that the horizontal values are placed first, though. That's because the
first value is always horizontal, while the second value is always vertical.

If you give the `background-position` property only a single keyword, that's equivalent to `<horizontal value> center`
if you're using `left` or `right`, or `center <vertical value>` if you're using `top` or `bottom`. In either case, both
of the default values `left top` are going to get overridden.

## Using `background`
As mentioned earlier, all the background-related properties can be rolled up into a single shorthand called
`background`. In addition, it doesn't seem like there's a set order that the properties need to follow. Still, Howe says
that most developers will default to this order:

```
background: <color> <image> <position> <repeat>
```

```css
div {
    background: #000 url("black.png") 20px top no-repeat;
}
```

## Designing gradiant backgrounds
Gradiant backgrounds were added in CSS3, meaning that they're not supported by modern browsers. As how how they're
implemented, they're treated as background images, meaning that you can create them with the `background` and
`background-image` properties. Unfortunately, browsers only allow for linear and radial gradients (even though gradients
have been a part of the language for nearly a decade). Still, those two should be more than enough for most purposes.

### Vendor prefixes for gradient backgrounds
At this point, there shouldn't be much need to add vendor prefixes to gradient backgrounds, but they're still worth
considering if you're trying to support as many browsers as possibble.

### Linear gradient backgrounds
The introduction of linear gradient backgrounds put an end to an unfortunate practice that developers were forced to use
for years: creating gradients in image editors and using them as backgrounds. As the gradients were of a fixed size, you
often ran into banding and color issues when your gradient was smaller than the container. It was especially bad if you
needed to change the color of your gradient; you would have to export an entire new image for each adjustment.

Luckily, that's all a thing of the past. If you need to change a gradient, you can just change a single value.

To create a linear gradient for your background, just the value of one of the background properties to the 
`linear-gradient()` function. This function takes two values: a starting color and an ending color. It will then
calculate all the colors needed for the space between them. You can also give it an optional argument that defines its
direction. For example, to make a green-to-blue gradient start from the upper left and go to the lower right, you'd use
`background: linear-gradient(to right bottom, #648880, #293f50)`. The keywords are basically the same as the ones for
`background-position` (sans `center`); you just need to put a `to ` in front of them.

Now, it does seem that there are some quirks for when you apply gradients to non-square elements (or elements that
could be contained within a square). I don't have the time to fully understand it (it might not even be a thing
anymore), but there is an article on the subject of ["magic corners"](http://meyerweb.com/eric/thoughts/2012/04/26/lineargradient-keywords/).

Linear gradients also support the `deg` unit of measurement instead of one of the `to ` values. Each degree will affect
the direction the gradient progresses in.


### Radial gradient backgrounds
On the surface, radial gradients aren't that different from linear gradients. All you have to do is use the
`radial-gradient()` function. Like `linear-gradient()`, it'll take two values. The first will define the starting
point color (defined at the center), while the second will define the end point color (defined at the outer edges).
The function will then figure out all the values between.

But radial gradients actually have a lot more aspects that linear gradients don't. You can define things like location,
size, and radius.

### CSS3 Gradient Generators
When you're first learning how to work with gradients, you might want to consider using an online gradient generator to
help you get your bearings. They'll let you create a gradient using more intuitive tools like sliders and then output
the code needed to produce it naturally. Even the simpler linear gradient has a few settings that the guide hasn't
covered.

### Gradient Color Stops
CSS gradients also allow you to create multiple color stops, which will create three points for the a gradient function
to gradate between. To use them, you just need to keep adding more and more colors as arguments for either the
`linear-gradient()` funciton or the `radial-gradient()` function.

By default, the browser will space each stop point evenly. So, if you have three stops, the first will be at the
beginning, the second will be in the middle, and the third will be at the end. However, you can override this by
including percentage points after each color.

```css
.element {
    background: linear-gradient(to right, #f6f1d3, #648880 85%, #293f50);
}
```
The above code will transition, from left to right, between a bright desaturated yellow to a desaturated cyan to a dark
desaturated green. However, The yellow will be placed at the start, the cyan will be placed at the 85% point, and the
green will be placed at the end. As the percent stops for the first and last colors weren't defined, they were
implicitly assigned values of `0%` and `100%` respectively.

## Multiple Background images
As of CSS3, you can now use multiple background images for a single element. You just need to separate each reference to
a background with a comma. Each background you add will be placed below the one that came before. This all applies to
the `background` shorthand property, as well as all the individual `background-` properties.

Using them all at once:
```css
div {
    background: url("image1.png") 0 0 no-repeat, url("image2.png") center no-repeat, url("image3.png") top repeat-x;
}

/* Makes element green but also adds check mark through background property */
.practicalExample {
    background: url("tick.png") 20px 50% no-repeat, linear-gradient(#72c41f, #5c9e19);
    padding: 15px 20px 15px 50px;
}
```

And separately:
```css
div {
    background-image: url("image1.png"), url("image2.png"), url("image3.png");
    background-repeat: no-repeat, no-repeat, repeat-x;
    background-position: 0 0, center, top;
}
```

## Exploring new background properties
CSS3 has added four new background properties, though the last one was added more recently: `background-size`,
`background-clip`, `background-origin`, and `background-attachment`.

### `background-size`
This allows you to define the size of a background image. This size can be defined either through units of measurement
or through keywords. If you ellect to use percentages, know that the values will be based off the size of the parent
element, not the image itself (so `background-size: 10% 10%` isn't guaranteed to be proportional).

Also,  when you do use standard units of measurement, you can either use one value or two. Either way, the first value
will always refer to the width of the image. But if you choose two values, the second value will refer to the height. If
you choose one, then the height will automatically be set to preserve the image's aspect ratio. You can also use `auto`
as either value – the browser will scale the image proportionally no matter what.

### The `cover` and `contain` keyword values
There are two more keywords that the `background-image` property has access to: `cover` and `contain`.

When you use `cover` as the sole value of the property, the image will stretch to fill its entire element – while
preserving its aspect ratio. This will often mean that the image will get cut off in some way.

The `contain` keyword, on the other hand, is similar, but has one big difference. The keyword will make the image
stretch to fit the element – while preserving aspect ratio – but it'll stop growing once it fills either the
entire width or the entire height. So, if you were to use a 5:1 image for a 2:3 element, the image would scale until
the entire width would be covered. However, because the element would be taller than the image, there would be a portion
that wouldn't be covered.

Of course, either property can stretch a raster image well beyond its original size, so keeping the aspect ratio
shouldn't be the sole consideration.

### `background-clip` and `background-origin`
The `background-clip` and `background-origin` properties are related in that they affect how a background image
interacts with all three parts of its element (the content, the padding, and the border). However, I don't think that
they can be used together. Both can take one of three values:
* `content-box`
* `padding-box`
* `border-box`

`background-clip` affects what parts of the element the image covers. Set it to `content-box`, and it won't extend into
the padding or border. Set it to `border-box`, and it'll extend into everything, including the border (though it seems
that it'll be placed behind the border style).

`background-origin` determines where an image starts. Set it to `content-box`, and it'll start in the upper-left of the
content area. Set it to `border-box`, and it'll start at the upper left of the border (with the border style being on
top.)
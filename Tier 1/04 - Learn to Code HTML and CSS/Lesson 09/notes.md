
# Lesson 9: Adding Media

Apparently, it used to be much harder to embed media other than images inside HTML. Thank goodness HTML5 made that
process so much easier.

## Adding Images

Images can be added to HTML pages through the `<img>` element. This element is self-closing, and its content is defined
by the `src` attribute. The value of this attribute is **always** a URL. Specifically, it'll almost always be an image
that's hosted on your own server. You can also assign an `alt` attribute to the element, the value of which is text that
gets displayed when the image can't load. The text can also be read by screen readers, which is great for those with
vision impairments. Oh, and search engines can see the text, too.

### Sizing Images

It's important that you define the width and height of your images whenever possible. That way, the browser can reserve
space for it and then focus on loading everything else while waiting for the image to load. You could do this by
giving the `<img>` element `width` and `height` attributes, but you can also use `width` and `height` properties in CSS.
When you have both, the CSS properties are able to override the HTML element's attributes, so keep that in mind if you
start modifying the HTML.

By default, all images will scale proportionally when you modify only one property/attribute. For example, if you modify
the width, then the height will scale to keep the image proportional. The proportions can only drastically change if
you define both.

Now, using the `width` and `height` attributes does have some merits, as it should provide information about the
original image's size. But the problem is that doing that for each and every image can be hard to manage, particularly
for huge sites. So, while there technically is a benefit to using them, most developers don't bother to save themselves
the huge headache.

### Positioning images

By default, all images are inline elements. However, you're free to override this behavior by changing their `display`
properties. Even as inline elements, the elements fully support the `padding` and `margin` properties; the only that
doesn't work is vertical values for the `margin` property.

### Inline positioning images

Be careful about using images purely inline (which is how they display by default). If you throw it inside a text
element when its height is larger than the height of each text line, the image will push the line down and align the
text it shares a line with to its bottom. This is why it's not very common to put images inline the text. If anything,
you'll float the images to the side. You can overcome this behavior with the `vertical-align` property, but it's still
probably not worth it.

### Block positioning elements

When you set an image element to `display: block`, the image will appear on its own separate line, pushing all following
content to the line below it.

### Positioning elements flush left or flush right

Sometimes, though, you don't want your HTML to be inline or to behave entirely like a block. In such cases, you can
still float your image (after turning it into a `block` or `inline-block`, of course). In fact, this was the main
reason why floats were invented.

### Images as backgrounds vs images as elements

There are two main ways to add images to a webpage. You can either add it through the `<img>` element or by setting it
as some element's `background-image`. In general, you want to use `<img>` when the image you're adding has semantic
meaning and isn't just decoration. You don't want to use `background-image` when the image is part of the main content.

## Adding Audio

HTML5 has made it so much easier to add audio to a webpage, all thanks to the (at this point, not so) new `<audio>`
element. It's similar to the `<img>` element in that it takes a `src` attribute to define where the audio goes, but
unlike `<img>`, it isn't self-closing.

### `<audio>` attributes

Some of the more common attributes to add to `<audio>` elements are `loop`, `autoplay`, `controls`, and `preload`. All
except `preload` are boolean attributes, meaning that you don't need to give any a value. Just the presence of an
attribute will make the browser treat that attribute's value as true.

By default, `<audio>` elements aren't displayed. If you want to display a dedicated player, then you're going to need to
give it the `controls` attribute, which will cause player controls to appear. This control set will include things like
a seek bar, a play/pause button, and a volume controller. It doesn't seem like there's a way to style the player that
the browser uses by default beyond simple things like size, but you can create a custom player with something called the
`HTMLMediaElement` API.

The `autoplay` element will cause the audio to start playing the moment it gets loaded, regardless of whether there is
a player being displayed. `loop`, meanwhile, will cause the audio to repeat the moment it finishes.

As for `preload`, it defines text that gets displayed before the audio finishes loading. It can take three values:

* `none`
* `auto`
* `metadata`

On one side of the spectrum, `none` displays nothing. On the other, you have `auto`, which displays pretty much every
piece of information about the audio file. Then there's `metadata`, situated in the middle. This will display basic
information, such as the audio clip's length, but it won't go as far the `auto` attribute does. If you don't set the
`preload` value at all, the browser will default to `auto`, which can be bad for large files. The browser will pull much
more information than it needs, which will mess with bandwidth and load speeds. That's why it's a good idea to define
the element's `preload` value as either `none` or `metadata` as a defensive habit.

### Audio fallbacks and multiple sources

Browsers support different file formats (though I would assume that there's much more parity nowadays). At the time of
the guide's writing, the three most common formats were `ogg`, `mp3`, and `wav`. This is why `<audio>` elements aren't
self-closing: you can supply the element with multiple `<source>` elements. These also replace the `src` attribute. The
moment a browser recognizes one of the formats provided via `<source>`, it'll use it and stop looking at the other
sources.

In addition, you can also place other elments inside the `<audio>` element. These will get displayed if the browseer
processing it doesn't support the `<audio>` element at all. However, even if the audio can't be loaded, if the browser
does support the element, then none of the inner content will be displayed.

```html
<audio controls>
    <source src="jazz.ogg" type="audio/ogg">
    <source src="jazz.mp3" type="audio/mpeg">
    <source src="jazz.wav" type="audio/wav">
    Please <a href="jazz.mp3" download>download</a> the audio file.
</audio>
```

## Adding video with `<video>`

Adding video to HTML isn't that different compared to adding audio. You have to use `<video>` instead of `<audio>`, but
all the other attributes like `auto`, `none`, `controls`, and `preload` apply. You can also either use the `src`
attribute, or use a fallback system of multiple inner `<source>` elements.

Still, there is a slight difference when it comes to the `controls` attribute. When you don't use it for `<audio>`
elements, the audio simply won't appear. When you do the same for `<video>`, the video will appear – it's just that the
controls won't. If you want the user to be able to control the video, then, you'll want to specify the `controls`
attribute every single time. Though sometimes you don't, like when you're using the video as more of a decoration.

Since `<video>` elements, like `<img>` elements, always take up space in the browser, it's a good idea to specify their
width and height to help load all the content around it faster. It's probably more critical that you do, since videos
are bigger than images. You can do this either by specifying the `width` and `height` attributes of the element or by
defining the `width` and `height` via CSS. This also helps ensure that your video doesn't break out of your page layout.

### The `poster` attribute

The `poster` attribute allows you to define an image that gets displayed in the video player before the user plays the
video. Like `src`, its value is a URL.

```html
<video src="earth.ogv" controls poster="earth-video-screenshot.jpg"></video>
```

### Video fallbacks

The `<video>` element lets you define multiple video sources to act as fallbacks, just like with the `<audio>` element.
As always, you want to define multiple `<source>` elements, followed by some text element. The latter, of course, only
gets displayed if the user's browser doesn't support HTML5 video whatsoever. If the browser recognizes one of the
`<source>` elements early, then it'll stop looking through everything else.

## Customizing video and audio controls

Again, the style of the video and audio player created by the `<video>` and `<audio>` elements is determined by the
browser. If you want to customize their appearance, you have no choice but to use JavaScript.

## Adding inline frames

The `<iframe>` element lets you embed an HTML inside the current one. This element has one main attribute – `src` –
which takes the URL of an HTML page as its value. This element is most commonly used to embed content from websites
like Google Maps and YouTube.

It also has some default styling, such as a border and a base width and height. As a more legacy element, this can be
changed by using the `frameborder`, `width`, and `height` attributes, or by using the `border`, `width`, and `height`
properties.

Whenever you embed another webpage via `<iframe>`, that page will not be affected by your style sheets. The iframe
will use whatever CSS the document references in its own code. Also, whenever you click links in the iframe, they'll
be opened in that iframe. The user won't have their current page changed, nor will the link open a new tab (though I
don't know about when the link explicitly uses `target="_blank"`).

## Semantically identifying figures and captions

HTML5 added the `<figure>` and `<figcaption>` elements, which allow you to semantically define figures and captions for
those figures. Apparently the old way of implementing this functionality relied on using ordered lists, which sounds
really jank to me, so thank god we're out of the dark ages.

### The `<figure>` element

The `<figure>` element is used to designate any content that is illustrative but that isn't necessarily an illustration.
That is, it's basically for additional, self-contained media that enhances the main text. If you move the figure, it
shouldn't affect the main content at all.

These elements can include images, video, audio, and even code. You can also include multiple types of media within the
same `<figure>` element.

### The `<figcaption>` element

The `<figcaption>` element is a little interesting. It can be used **anywhere** within the `<figure>` element, but you
can only have one caption per figure, and the caption is to describe the entire figure, even if there are multiple
instances of media inside it.

```html
<figure>
    <img src="dog.jpg" alt="A dog wearing a kerchief around its neck">
    <figcaption>A beautiful black, brown, and white hound dog wearing kerchief.</figcaption>
</figure>
```
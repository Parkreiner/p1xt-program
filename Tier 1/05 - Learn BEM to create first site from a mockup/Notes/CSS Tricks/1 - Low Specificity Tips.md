# CSS Tricks: Strategies for Keeping CSS Specificity Low

You absolutely need to keep CSS specificity as low as possible. Having it balloon too high can make projects completely
unmanageable, as you struggle to keep increasing specificity for each new element, find yourself abusing the
`!important` modifier for property values, or god forbid, use inline styles.

But how is this possible?

## Give yourself the class you need

Sometimes you'll find yourself writing high-specificity selectors because you want to apply a separate style to a unique
specific instance of a class you already have written.

CSS

```css
.section-header {
    /* The general styling */
}
body.about-page .section-header {
    /* Unique styling for section header found in the "about" HTML page */
}
```

Now, this might not seem like a big deal, and by itself, it isn't. But the fact remains that you're increasing CSS
specificity when it could be avoided. What if you have to do something like this hundreds of times?

A better solution (though certainly not the only one) is to use server-side functions to inject the specific class(es)
you need into the HTML, while providing the styling for all those classes in the CSS.

HTML

```html
<header class="<%= header_class %>">
    Apparently this would let you create a function to insert the classes. You could either insert both and design them
    to be used together, or you could use them as alternate versions of each other.
</header>
```

CSS

```css
.section-header {
    /* Normal styling */
}
.about-section-header {
    /* Either override the previous selector but keep the same specificity or extend the previous selector */
}
```

## Be careful about the order you write your styles in

Look at this code:

```html
<header class="section-header section-header-about">
    Stuff
</header>
```

It's obvious from the way it's written here that `section-header-about` is meant to extend `section-header`, but the
two classes have the same specificity. If you place `.section-header-about` first, then the only way things will
cascade properly is if it doesn't override a single value inside `.section-header`.

To provide against this, it's probably a good idea to section your code into chunks, such that `section-header` would
be in a separate section that comes before the one for `section-header-about`. This is the example structure CSS Tricks
uses:

```scss
@import "third-party-and-libs-and-stuff";

@import "global-stuff";

@import "section-stuff";

@import "specific-things-and-potential-overrides";
```

## Reduce the specificity of the thing that you're overriding

Try to improve whatever code you're using. Remember: ID-based CSS selectors have the highest specificity rating of all,
any no selector that doesn't involve one will ever be able to override it. If you see any IDs in the code, see if you
can remove them, possibly replacing them with classes. Sometimes this won't be possible, as the IDs will be acting as
hooks for JS. Still, even in such cases, it might make sense to add a class and then modify the CSS to be based around
it.

## Don't be afraid of classes

Using more specialized selectors like the parent selector `>` is fine, but be careful if you decide to modify the child
to have a unique style.

Original code:

```css
.module > h2 {
    Stuff
}
```

```html
<div class="module">
    <h2 class="unique">
        Special Header
    </h2>
</div>
```

What are you going to do if you decide that you want to give that `<h2>` element a unique style? You could do this:

```css
.module > h2 {
    Stuff
}
.unique {
    Unique stuff
}
```

But it'll always lose out in specificity. The first selector has a class and a general element, while the second only
has a class.

You could do this:

```css
.module > h2 {
    Stuff
}
.module .unique {
    Unique stuff
}
```

Which does work, but it presents more specificity creep. This is why most developers recommend structuring your HTML to
be as "flat" as possible.

```html
<div class="module">
    <h2 class="module-header">
    </h2>
    <div class="module-content">
    </div>
</div>
```

It might seem tedious and needless, especially if you never write styles for some of these elements, but you'll thank
yourself whenever you need to style a specific element later on. You won't have to touch the HTML, and you can just
change the class, all while keeping specificity the same:

```css
.module-header {

}
```

## Use the cascade

CSS is called "cascading style sheets" for a reason. Use the fact that styles cascade to your advantage. Modifying a
low-specificity element to become high-specificity can have disastrous effects on your code. You could avoid this by
making your code so highly specific that it could only target a small set of elements, but that'll make maintaining the
code an absolute nightmare.

```css
#for .the[love] #of .god #dont .do #this {
    /* It just isn't worth it */
}
```

You absolutely want a good base to work from. If you have that, then the number of overrides should be very, very low.
To do this, you can use strategies like:

### Use a pattern library and/or style guide and/or atomic design

A pattern library (sometimes conflated with a style guide) is a pre-made set of styles you can use in a wide variety of
contexts. This can either come from a framework or from a buildup of styles you've found yourself reusing over time. But
regardless of the source, all the elements should have documentation, including things like what the pattern modules do,
what they look like, and how they are coded. A pattern library is especially invaluable for pages that are meant to look
cohesive, as you're guaranteed to be using the same styles across each one.

For inspiration, you can look at [Mail Chimp's pattern library](http://ux.mailchimp.com/patterns) or look through
[Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/), which is an entire guide book for how to make your
own libraries.

However, a pattern library is not a style guide. It's not a reusable set of code snippets, but a guideline for how code,
even new code, should be written. You can find out more [here](https://css-tricks.com/css-style-guides/).

### Consider opt-in typography

The basic idea of this is that you create a general text class that then has text-based element selectors nested within
it. On the surface, this goes against the idea of low specificity. But it actually keeps things much more organized and
contained, reducing the likelihood that you'll have to ramp up specificity later.

An example:

```scss

/* Resets all lists globally */
ul, ol, li {
    list-style: none;
    margin: 0;
    padding: 0;
}

/* Apply text styles only to containers that contain text */
.text-content {
    h1, h2, h3 {
        Stuff
    }
    p {
        More stuff
    }
    ul {
        Even more stuff
    }
    ol {
        More stuff still
    }
}

```

In this example, all the lists are set to a baseline set of styles. But then all lists within a `.text-content`
container get extended to apply even more styles. But why? Realistically, your lists are going to be used in a wide
range of cases, ranging from more UI-based elements (like navigation) to content-based elements (like a to-do list).
You're almost definitely not going to want to use the same styling for both groups, so organizing the elements like this
ensures that you keep styling for each separate. By breaking things apart from the beginning, you cut down on the number
of potential overrides.

## Outside-of-your-control issues

All of the above is great advice, but only to a point. At some point, you're going to find yourself using someone else's
code that either expects HTML formatted a specific way or that **adds** HTML formatted a specific way. There's only so
much you can do about this, but even so, you should try to keep specificity as low as possible. Sometimes, the best you
can do is to use `!important` modifiers and comment your code explaining why things are written the way they are. Of
course, you could also ask the developer of the weak code if they can improve it.

## If you need to up specificity, do so as lightly as possible and be sure to label your code properly

Sometimes, upping a selector's specificity will be the only way to make a design work. But before you spring for an ID
selector or `!important` (the CSS equivalents to a sledgehammer), trying using classes, which are lighter and more deft.

The smallest possible change you can do is a tag-class combination.

```css
ul.override {
    /* Override content */
}
.normal {
    /* Normal styling */
}
```

But it might be even better to just create a general `.override` class, so that you can define overrides for any
element. This seems a bit hack-y, but you can even use the same class multiple times to increase specificity while
keeping the selector's target the same.

```css
.nav.override {
    /* Override for nav elements */
}
.override {
    /* Styling for all overrides */
}
.override.override {
    /* Even stronger override */
}
.nav {
    /* General nav styling */
}
```

## Nesting doesn't mean specificity has to go up

Nesting selectors within SCSS is often discouraged because it can quickly lead to overly-specific selectors. But if
you're already creating compound selectors, nesting can make the code much more readable. At the same type, the `&`
symbol allows you to cut up class names, which is has zero drawbacks.

SCSS source:

```scss
.what {
    color: red;
    &-so {
        color: green;
        &-ever {
            color: blue;
        }
    }
}
```

CSS output:

```css
.what {
    color: red;
}
.what-so {
    color: green;
}
.what-so-ever {
    color: blue;
}
```

## The single-class wrapper

A really straightforward (but forceful) way of using overrides is by wrapping the content you want to be overriden
within a `<div>` element with an `.override` class. To use the override style, all you have to do is prefix it with
`.override [other stuff]`. This does increase specificity, but it does try to keep it contained.

## Rethink things if you're finding yourself override your overrides

In general, you should only ever need to override an element once. If you have to do it two or more times, that's
basically a guarantee that your code is in need of re-factoring.

## Try to do better each time

Even if you're at a point where you can't afford to deal with specificity problems, you should always try to take your
mistakes to heart, using them to keep specificity in other projects low. Maybe you'll never be able to fix your past
mistakes, but at least you can minimize the ones you make in the future.
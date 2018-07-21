# Lesson 12: Writing Your Best Code

## HTML Coding Practices

HTML coding practices, as with those for all other languages, emphasize keeping code lean, clean, and tidy. No matter
what, your goal should be to write code that's well-structured but also standards-compliant.

### Writing standards-compliant markup

Writing HTML and CSS is very forgiving, as the browsers that render the code have a very high tolerance for code that
just doesn't work. That means that having code that renders (possibly even exactly how it should) is good underneath the
hood. More often, though, poorly-written code will behave unpredictably and won't look anything like how you want it to.

In order to avoid this, you need to be diligent about your nesting, your classes and IDs, and basically every part of
the code. You should also validate your code, using the free online tool that W3C provides.

### Making good use of semantic elements

Never, under any circumstances, should you ignore semantics. HTML offers about 100 different elements, each tailored to
describing a different element that can go into a web page. While it can be hard at times to decide which element is the
most appropriate, using nothing or using an element with zero semantic info is much worse than making the wrong choice.
For no other reason, it helps screen readers, which in turn helps the vision-impaired.

God forbid you decide to section off a chunk of text by using a bunch of `<br />` elements instead of just using a `<p>`
element...

### Use the proper document structure

HTML doesn't need the following to render: `<!DOCTYPE html>`, `<html>`, `<head>`, or `<body>`. That doesn't mean you
should ever create a standalone page that doesn't have all of them. Omitting even just one of these can cause very big
problems when browsers try to render the page – including not rendering the page at all.

### Keep your syntax organized

HTML can be tricky to maintain, especially if the code just keeps growing. Luckily, there are a few basic practices that
help keep things under control:

* Use lowercase letters for element names, attributes, and attribute values.
* Indent nested elements
* Always use double quotes for the outer parts of your values
* Remove the forward slash at the end of self-closing elements (doesn't really apply anymore, thanks to JSX)
* Omit the implied values of all boolean attributes

### Use practical class and ID names

Under ideal circumstances, class and ID names should have semantic meaning in themselves. That is, they should describe
some sort of functionality, rather than be named after the style you plan to give the elements. Say you have multiple
guests for a web page that puts each guest inside an `<article>` element and want to give of those elements blue. Don't
give those elements a `blue` class; give them a `guest` class. Likewise, if you want to make an element into an alert
and want to make the alert red, give the element an `alert` class, not a `red` class.

### Always give images an `alt` attribute, especially on sites with a discrete number of pages

Screen readers need these to be able to tell the vision-impaired anything about an image. Computing isn't good enough
that image recognition can generate descriptions on the fly.

### Avoid using images if they're meta (like being part of the main UI) rather than being part of the content

If you need to add visual elements to a web page, but they're not related to the content of the page, then it's often
better to add them via CSS. I don't know if this is less practical with vectors, though.

### Keep style and content separate

Never, ever use inline styles within your HTML. It makes code harder to maintain and makes the code load slower. Use
external style sheets.

### Avoid bogging your code down with `<div>` elements

This just goes back to the point of favoring semantically-meaningful elements. If you want, you can use `<div>` elements
in place of most other elements. That's a really bad idea, though, but going one step further, you should try to have
just as many elements as you need.

### Keep refactoring your code

Web pages evolve over time. Sometimes it's not just because they've gained new content. Always be on the lookout for
ways you can streamline old code and remove bloat.

## CSS Coding Practices

Again, the goal with CSS, as with HTML, as with any other language, is to keep the code lean and mean.

### Organize code with comments

CSS files tend to balloon pretty quickly, making it harder to keep track of everything if you don't label every part
properly.

Bad code:

```css
header { ... }
article { ... }
.btn { ... }
```

Good code:

```css
/* Primary header */
header { ... }

/* Featured article */
article { ... }

/* Buttons */
.btn { ... }
```

It also doesn't hurt to make a table of contents for all the main styles and place it at the top of the file.

### Give your CSS plenty of whitespace

Proper use of indentation and line breaks is key for readable CSS. Never put a chunk of code on a single line, even if
you think it looks elegant; it'll be inconsistent with everything else and will be more annoying to add to later.

Bad code:

```css
a,.btn{background:#aaa;color:#f60;font-size:18px;padding:6px;}
```

Good code:

```css
a,
.btn {
    background: #aaa;
    color: #f60;
    font-size: 18px;
    padding: 6px;
}
```

**Honestly, though, you should apply this principle to all code you write, regardless of language.**

### Use proper class names

A good rule of thumb to follow for class names is to make them all-lowercase and to hyphenate classes that require
multiple words. As mentioned earlier, they should also describe the content that they modify as much as possible.

Bad Code:

```css
.Red_Box { ... }
```

Good Code:

```css
.alert-message { ... }
```

### Try to avoid putting two many elements in your CSS selectors

It's very easy to bog your CSS selectors with two many elements, making them unwieldy and hard to read. It also doesn't
help that adding a bunch of elements in the selector makes that selector more and more specific, which can screw with
how you expect the code to cascade. Likewise, you should almost never include IDs in a selector that contains more than
just that ID. The IDs can really mess with specificity and make code harder to debug.

Bad code:

```css
#aside #featured ul.news li a { ... }
#aside #featured ul.news li a em.special { ... }
```

Good code:

```css
.news a { ... }
.news .special { ... }
```

### Use specific classes when necessary

Even if you follow the advice from the previous point, there will come points when your selectors will get overly long
anyway. This can really hamper performance and mess with readability, so it's often better to short-circuit the problem
and create a class specifically for the element(s) you're trying to modify. Adding code to HTML doesn't hit performance
nearly as much as having a bunch of long selectors does.

Bad code:

```css
section aside h1 em { ... }
```

Good code:

```css
.text-offset { ... }
```

### Use shorthand properties and values

CSS is great because it often provides shorthand for a bunch of related properties. So, instead of using four
properties, you can roll them into just one. However, you should only use this shorthand when you're using multiple
related properties. If you're using just one, then it's better to use that specific property, to make it clear that
you're only modifying one value. It also provides against accidentally overwriting other CSS values.

Bad code:

```css
img {
    margin-top: 5px;
    margin-right: 10px;
    margin-bottom: 5px;
    margin-left: 10px;
}
button {
    padding: 0 0 0 20px;
}
```

Good code:

```css
img {
    margin: 5px 10px;
}
button {
    padding-left: 20px;
}
```

### Use shorthand hex colors when your colors can be collapsed

CSS lets you use three-character hex colors when the equivalent six-character hex color has its three colors each be
comprised of the same two characters. So, `#aabbcc` can become `#abc` because the red channel is `aa`, the green channel
is `bb`, and the blue channel is `cc`. However, `#aabbcd` cannot be collapsed, as the blue channel doesn't have the two
of the same character – it'd need to be either `cc` or `dd`.

### Omit units of measurement from `0` values

`0` represents nothingness – and nothingness doesn't need a unit of measurement, because there's nothing to be
measured. You can omit all units of measurement from all `0` values in CSS.

### Group and align vendor prefixes

Vendor prefixes are important; they allow you to support nascent features while helping to ensure that your code is
future-proof. That doesn't change that they can end up adding a lot of clutter, though. Your best shot an mitigating
these problems is by aligning the properties so that they're obviously part of a single set. How you align the
properties depends on whether you need to give the vendor prefix to the property or its value.

Bad code:

```css
div {
    background: -webkit-linear-gradient(#a1d3b0, #f6f1d3);
    background: -moz-linear-gradient(#a1d3b0, #f6f1d3);
    background: linear-gradient(#a1d3b0, #f6f1d3);
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}
```

Good code:

```css
div {
    background: -webkit-linear-gradient(#a1d3b0, #f6f1d3);
    background:    -moz-linear-gradient(#a1d3b0, #f6f1d3);
    background:         linear-gradient(#a1d3b0, #f6f1d3);
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
            box-sizing: border-box;
}
```

**But no matter what**, always place the un-prefixed properties at the end of the set.

### Make styles modular for reuse

CSS code, especially properties for class selectors, is designed to be reused over and over. There's no reason to keep
repeating the same properties over and over again, even if they are for different elements. If you have two elements
that take almost the same set of properties, save for 1–2, then split things up. There's no limit to the number of
classes you can give an element.

Bad code:

```css
.news {
  background: #eee;
  border: 1px solid #ccc;
  border-radius: 6px;
  background-color: #eee;
}
.events {
  background: #eee;
  border: 1px solid #ccc;
  border-radius: 6px;
  background-color: #555;
}
```

Good code:

```css
.feat-box {
    background: #eee;
  border: 1px solid #ccc;
  border-radius: 6px;
}
.news {
    background-color: #eee;
}
.events {
    background-color: #555;
}
```
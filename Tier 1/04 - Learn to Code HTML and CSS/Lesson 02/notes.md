# Lesson 2: Getting to know HTML

## Semantics Overview
Semantics just refers to giving content meaning – labeling it, so that you know what role each element plays inside
the webpage. Giving your web pages good semantics is in your best interests, because it not only helps you trend
better in Google search results, but it helps users accessing your page through screen readers.

## Identifying divisions and spans
However, HTML does have two elements that have *zero* semantic meaning. They exist only to make styling content through
selectors easier.

`<div>` elements are the main block-based container, while `<span>` elements are the main inline container. These two
are the two that you'll be giving class and ID names to, more than any other element. So, while they exist to make
styling easier, you still want to label the content they contain as semantically as possible. Never use class names
based on what style they're meant to apply; also name your classes based on what role the element plays within the
document.

### Block vs inline elements
In HTML and CSS, there are two main ways that elements can be displayed: as blocks or inline. Block elements tend to
have a set size, regardless of the content inside. For example, `<p>` elements will, by default, span the entire width
of the page, even if the element itself only contains one letter. Block elements can also nest within and stack on top
of each other. Basically, think of them as elements that push subsequent elements to a new line.

Inline elements, on the other hand, are exactly what their name would suggest: inline. By default, they will only occupy
just enough space to contain their content, and they won't push other content or elements to a new line. Also, I don't
think they allow you to place many elements inside them.

All elements can have their default display values overwritten through CSS, though. So while a `<p>` element might
default to a block, for example, you can have it display inline through CSS. But it's still treated as a block element.

Also, some elements are designed to be used only with block or inline elements, regardless of how they're displayed.
One example is `<a>`, which for the longest time, didn't allow you to wrap it around an entire block.

### HTML and CSS Comments
Unfortunately, neither HTML nor CSS allow for single-line comments. The only option for each is multi-line comments.
In HTML, these start with `<!--` and end with `-->`, while in CSS, they start with `/*` and end with `*/`.

## Using Text-Based Elements
It doesn't matter how much advertisers try to push for video; text is still king, and for the immediate future, it will
stay king. You need to know how to label it properly.

### Headings
HTML comes with six different heading elements, labeled from `<h1>` to `<h6>`. Not only do they help readers navigate
through content easier – as they should be sectioning the starts of new content – but they also help search engines
index your page.

Each of the numbered HTML headings refer to the amount of precedence content can have in a page. So, `<h1>` elements are
always the top-level headings – depending on the website, you might not ever have more than one. Everything else,
starting with `<h2>`, refers to progressively more specific subheadings. 

For the love of god, never use heading elements just to make text big.

### Paragraphs
The `<p>` element is used for paragraphs. However, they don't just mark off an area of space for paragraphs – you want
to wrap each paragraph in a different `<p>` element.

Unfortunately, there isn't a generic text element, but it sounds like `<p>` elements can be used when the other elements
aren't appropriate.

### Strong and bold text
The `<strong>` inline element is used when you want to emphasize a specific piece of text, making it stand out from
the surrounding text. By default, CSS will render strong elements in bold. There is a bold element called `<b>`, but
it's deprecated.

There is also a `<b>` element, and I'm not quite sure how it fits into modern web dev yet. For a while, it was
considered deprecated, because it basically just turned text bold – it was a stylistic element in a language that values
it less than semantics. In HTML5, though, it's back to being a proper element. Now, you want to use `<strong>` for
elements that you want to stress very, very much (such as warnings), but you want to use `<b>` for elements that you
want the user to be able to find easily (like headings for individual list elements).

### Emphasized text
To emphasize text without making it stand out against the rest of the surrounding text, use the `<em>` inline element.
By default, CSS will display such elements in italics.

There was also an element for giving text italic styling, and like `<b>`, it's gone from being out of style to finding
new life. Nowadays, you want to use `<i>` for inline text that you're not necessarily emphasizing, but want to label as
being distinct from the surrounding text. So, you could use it for purposes like:
* Taxonomic designations
* Maruquing text from one language that's being used inline the main text written in another language
* When you're referring to words themselves ("You said *brought*, not *broad*.")

### `<b>`, `<i>`, `<em>`, and `<strong>` recap
* `<em>` – Used when you want to emphasize some part of a text, and you want that emphasis to carry semantic meaning. Especially good when **not** having emphasis could change the entire meaning of a sentence.
* `<i>` – For when you want to bring attention to some part of text as being distinct from the text that surrounds it. Generally used in more academic contexts.
* `<strong>` – For when you want to make something ridiculously, incredibly clear to the reader (like in warnings)
* `<b>` – For when you want to make elements stand out in text, so that it's easier for readers to find them at a glance.

## Building Structure
For a very, very long time, `<div>`s were the only way to create structure in a webpage, and that's awful, because
`<div>`s themselves carry zero semantic meaning. Luckily, HTML5 has rectified this, introducing a number of new
structural elements.

A sampling of these new elements:
* `<header>`
* `<nav>`
* `<article>`
* `<section>`
* `<aside>`
* `<footer>`

None of the above elements have any implied position or styling, but they are all block elements.

### `<header>`
`<header>` elements are used to denote headers of a given piece of the website. You can have headers at the top of the
web page, at the top of an article, or at the top of an aside. `<header>` elements are able to hold headings, text
(usually introductory), and even navigation.

#### `<header>`s vs Headings
Just to be clear, there is a very big difference between the `<header>` element and all the head*ing* elements (`<h1>`
through `<h6>`).

`<header>` elements are structural, grouping elements into a specific role. Heading elements, on the other hand, are
used strictly for text. There are very few elements that you can place in a heading, but you have much more flexibility
with `<header>`s.

### Navigation
You can use the `<nav>` element to denote a section as containing major navigation links. This element should only be
used for major navigation, such as global navigation, previous/next links, or tables of contents.

Interestingly, it seems that in HTML5, it's valid to omit `<ul>` and `<li>` elements in your `<nav>`. In such a case,
you'd just have a series of `<a>` elements

'''css
<nav>
    <a href="index.html">Home</a>
    <a href="speakers.html">Speakers</a>
    <a href="schedule.html">Schedule</a>
    <a href="venue.html">Venue</a>
    <a href="register.html">Register</a>
</nav>
'''

### `<article>`
This one can be a little confusing, but the most general way of putting it is that an `<article>` elment represents an
article or unit of content, in a sense similar to an article of clothing. That is, the content inside must be able to
stand on its own, even when divorced from the rest of the site. It *can* refer to the type of article also found in
magazines and reports, but it encompasses so much more.

### `<section>`
This element is used to denote a grouping of content that share a thematic connection. `<section>` elements can start
with a `<header>`, but they don't have to.

### `<section>`s vs `<article>`s vs `<div>`s
There can be quite a bit of confusion between which element to use where, but it's not too hard to remember. As
mentioned earlier, `<article>` elements are used for articles of content – content that is self-contained and can stand
on its own. `<section>` elements are for sections – they're inherently supporting players that can't stand on their own
outside of things like excerpts. It's possible to have `<article>`s within `<section>`s, and vice-versa. It's also
possible to have `<article>`s within `<article>`s and `<section>`s within `<section>`s.

However, both carry semantic meaning, while `<div>` elements don't. If you're grouping elements together because it
provides extra information about the structure of the web page, then use either a `<section>` or an `<article>`. If not,
then just use a `<div>`.

### `<aside>`
The `<aside>` element is for holding things like sidebars, inserts, and brief explanations. Basically, it's for bonus
content; it's nice, but removing it doesn't affect the core content. Interestingly, you can also use `<aside>` elements
for things like author information within `<article>`s.

Just by convention, I think most people think of asides as existing in a sidebar, off to the side of the main content.
But that's not inherent to the element. It's a block-level element, meaning that it'll push all other content below it
to a new line.

### `<footer>`
`<footer>` elements are for denoting the end or closing part of an article, section, or even the entire webpage. Again,
like `<aside>`s, removing a footer shouldn't impact the core content much, but just make sure that the footer has some
thematic ties to the content it's closing out. At least in my mind, `<footer>` elements are a little more connected to
the content it's within than `<aside>`s are.

### `<small>`
One final element – *that the page neglected to mention at all but was fine with using in examples* – is `<small>`,
which is another case of an element getting repurposed with the switch to HTML5. In older versions of HTML, this element
was used to shift text size down one level. So, text that was set to CSS `medium` would change to CSS `small`, and
CSS `small` text would become `x-small`.

In HTML5, though, the element is used for what you'd basically write in small print. It's for things like copyright
information, legal text, and side comments.

### Encoded/escaped characters
HTML can mess things up if it has to process characters other than what's covered in basic ASCII. It's unlikely to
happen now, but just to be safe, it's a good idea to escape the characters. Unlke with proper programming languages,
there's no general form for escaping any character (e.g., `\t`). Instead, you need to find the specific HTML entity
for that character and type it in.

All HTML entities start with an `&` and end with a `;`. The inner part can be either a shorthand name for that character
(e.g., `&ndash;` for an en dash) or the specific encoding. The specific encoding has two forms of its own: you can use
decimal or hex. However, the hex form must be preceded by a `#x` (e.g., `&#x0224C;` for &#x0224C;), while the decimal
form only needs a `#`.

## Creating Hyperlinks
Perhaps the most essential part of HTML – it's even part of the name – is the ability to hyperlink. This allows
different web pages to link with each other, letting you navigate between them. You can create hyperlinks through the
`<a>` element, which are all treated as inline. However, as of HTML5, you can wrap an `<a>` element around inline or
block elements.

### Relative and Absolute Paths
There are two main types of hyperlinks:
* Links that connect to other pages within the same website
* Links that connect to pages for external websites.

What determines the type of hyperlink is the type of path that you place in the element's `href` attribute. To get the
former type of link, you need to use a relative path. These path types don't use full HTML addresses, neglecting parts
like `https://` and `.www`/`.org`/etc. Instead, the address just needs the file type at the end: `.html`. However, you
need to navigate to different folders if the file you need to reach isn't in the same directory. For example, if you
have an `about.html` file in a folder called `About`, which is in the same directory as the file you're using, you need
to navigate to `About/about.html`.

As for the latter type of link, you need an absolute path. This needs to be a full HTML address, though depending on
how the file works, it might not end in a `.html` file extension (and in fact, no site should).

### Linking to an email address
Sometimes you want to create a link, such that, when the user clicks it, the user's email client opens up, ready to
send something to the linked address. All addresses like this must start with `mailto:`, and then be followed by the
actual email address.

However, you can attach other information as well, pre-populating more fields of the email that the client will open up.
All very first parameter must be preceded by a `?`, but everything else must be preceded by an `&`. In addition, all
parameters are key-value pairs, separated by a `=`. Also, any characters that are general invalid programming characters
must be encoded. So, spaces must be rendered as `%20`, question marks are `%3f`, and line breaks are `%0A`. Just look up
URL encoding for help with this.

So, in order to send an email that opens up a new email for `shay@awesome.com`, with the subject `Reaching Out` and the
body text `How are you?`, you need to use `mailto:shay@awesome.com?subject=Reaching%20Out&body=How%20Are%20You%3F`.

### Opening Links in a New Window
To open an HTML page in a new window, you need to give your `<a>` element a `target` attribute with a value of `_blank`.
When a user clicks a link with this property, the browser will open the link in a new tab, though the user can configure
the browser to open it in a new window.

The `target` attribute isn't really used for any other purposes nowadays, but the other major value for the attribute is
`_self`, which is what the element does by default. So really, you're only ever going to use `target="_blank"` when you
need to use the element.

### Linking to parts of the same page
There is one other type of linking that you'll see somewhat frequently, but not to the degree of the other two. However,
using it requires a little more work than just plopping an `href` in an `<a>` attribute. The reason is that this type of
linking jumps to a specific ID.

In order to use this kind of linking, you need to give an element an ID, and then put that ID (preceded by a `#`) in
the `href`. So, to link back to the top of the page, you need to give the topmost element an ID like `top` and then have
an `<a>` element use it, like `<a href="#top"> ... </a>`.
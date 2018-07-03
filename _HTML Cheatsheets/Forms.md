
# `<form>` Cheatsheet

Notes about form elements. Note that it is valid HTML to use form controls outside a form (e.g., using a `<select>`
element to create a drop-down list).

## Relatively global form attributes

These are attributes that all form controls support. However, some types of input controls behave differently with them.

### `name`

Gives form control elements a name that can be referenced when the form gets submitted. Be sure to give the same name to
all radio buttons and check boxes within the same group; it seems to be the only way to indicate that they're supposed
to be together.

### `value`

For non-text-based elements only. Each element of this type must have this attribute. Associates a more meaningful value
to input options. When used on an `<input>` of the type `submit`, the value will determine what the input button says.

Example with checkboxes:

```html
<input type="checkbox" name="day" value="Friday" checked> Friday
<input type="checkbox" name="day" value="Saturday"> Saturday
<input type="checkbox" name="day" value="Sunday"> Sunday
```

### `autofocus` (Boolean)

Brings focus to the element that has this attribute the moment the page finishes loading. Only one element in the entire
page can have this attribute, even if the page has multiple `<form>` elements.

### `required` (Boolean)

Prevents the overall form from being submitted if this element is empty.

### `disabled` (Boolean)

Renders a form control or entire field set unusable. Controls disabled with this keyword won't be sent to the server
when the form is submitted.

### `autocomplete` (Technically a boolean, but it isn't used like most)

The `autocomplete` attribute controls whether a text field allows for its input to be autocompleted. Unlike most
boolean values, its default state is actually `on`, so just inserting the attribute name by itself doesn't do anything.
If you want to disable autocomplete, you'll have to use `autocomplete="off"`.

## `<form>`

This element is for creating forms that will be submitted to a server. All form controls that are part of the form must
be nested inside it.

### `<form>` Attributes

#### `action`

Defines the URL that the form gets sent to once the user tries to submit it.

#### `method`

Defines the HTTP method used to submit the information. The only two values are `get` and `post`.

## `<input>`

The `<input>` element is very versatile, allowing you to capture simple input from the user. However, it isn't suited
to long-form text input; use `<textarea>` for that instead.

### `<input>` Attributes

#### `type`

Defines the type of input being used. Can range from text-based inputs to radio buttons to check boxes. Text-based
values added in HTML5 will cause some phone browsers to display unique input methods once the field is tapped, instead
of just a keyboard. If an older browser encounters a input type it doesn't understand, it'll just default to using
`text`.

##### Text-Based Values

* `text`
* `password` - Displays password as asterisks
* `date`
* `datetime`
* `email`
* `month`
* `number`
* `range`
* `search`
* `tel`
* `time`
* `url`
* `week`

##### Pseudo-text-based values

* `color` - Even for desktop, displays color picker if browser supports it; otherwise has user input color as hex value text

##### Radio Buttons and Check Box Values

* `checkbox`
* `radio` - Only one button within a group can be ticked at a time

##### Submission values

* `submit` - Creates a button that, when clicked, submits the form.

#### Normally Inaccessible Values

* `hidden` - Doesn't appear in webpage but passes extra information when the form gets submitted. Still perfectly accessible by digging through the source code; don't use it for sensitive information.

#### File Values

* `file` - Creates button that, when clicked, brings up a file explorer for finding files to upload. Use it with `multiple` to enable uploading multiple files.

#### `multiple`

Allows user to supply multiple inputs to the same `<input>` element. Also works when element is set to upload files.

#### `placeholder`

Text-based inputs only. Displays its value inside the `<input>` whenever the input is empty. The moment the user starts
typing, the placeholder text disappears. Placeholder text can't be selected directly or copied.

#### `checked` (Boolean)

Radio buttons and check boxes only. Pre-checks the element for the user. If multiple radio buttons within the same
group have this value, then only the last one will be checked.

## `<textarea>`

This element is for getting more long-form text input from a user, such as a comment.

### `<textarea>` Attributes

Honestly, you probably shouldn't bother with these attributes. Just define the `<textarea>`'s width and height via the
`width` and `height` CSS properties.

#### `maxlength`

Lets you define a character limit for the element.

#### `minlength`

Lets you define a minimum amount of characters needed before an element can get submitted.

#### `col`

Defines the width of the text area. The width is calculated by multiplying the attribute's value by the average width of
the element's characters with the element's current text styling.

#### `row`

Defines the height of the text area. Height is calculated by multiplying the attribute's value by the the distance from
the element text's descenders to its ascenders.

#### `wrap`

I'm not sure if I fully understand this, but as I understand things, this attribute has control over two types of word
wrapping. The first is visual word-wrapping and the second is word-wrapping embedded into the string that gets submitted
with the rest of the form. There are two main values for this attribute:

* `soft` will only create visual word wrapping. This is the default.
* `hard` will enforce word-wrapping in the string, so that regardless of the element's visual size, a newline character will be inserted after so many characters. The amount of characters that causes newlines to be inserted is determined by the value of the `col` attribute.

## `<select>` and `<option>`

The `<select>` element allows you to create drop-down lists, which, by default, only allow for one input at a time.
This element is like a `<ul>` or `<ol>`: it serves as a container for the elements that can go inside it (in this case,
the `<option>` elements). By default, only one option can be selected at a time.

### `<select>` Attributes

#### `multiple` (boolean)

Configures the drop-down list to allow multiple values to be selected at a time. Most browsers will modify the
appearance of elements with this attribute to show more options at once, but you can always change things further with
CSS.

### `<option>` Attributes

#### `selected` (boolean)

Basically `checked`, but for `<option>` elements. Treats one `<option>` as the default.

## `<button>`

Even though it can be used elsewhere, the `<button>` element is very much a form control. By default, it's treated as if
it has `type="submit"`, meaning that you're free to omit that attribute in most cases.

The element is block-level, so you can nest text inside of it. And because of that, the contents of the button aren't
determined by the value of its `value` attribute.

However, `<button>` elements have absolutely zero meaning when used outside forms. So if you're having them do something
through JavaScript, then it might be a good idea to add the buttons through JavaScript, too. That way, the buttons only
appear when they can actually do something (i.e., when JavaScript can be run).

### `button` Attributes

#### `type`

The `<button>` element supports a few different types.

* `submit` - (Default) Submits a form.
* `reset` - Resets the entire contents of the form it's contained within

## `<label>`

This element provides a label for a specific form control. They also aren't self-closing. You can use these elements in
one of two ways:

1. Tie the `<label>` to a single element by giving the `<label>` a `for` attribute and the element an `id` attribute, both with the same value. The text within the `<label>` will then be treated as descriptive text for the linked element.
2. Wrap the `<label>` around a single element, also throwing plain text inside it. The plain text will be treated as a single label, regardless of where it's located.

Style 1:

```html
<label for="username">Username</label>
<input type="text" name="username" id="username">
```

Style 2:

```html
<label>
    Username <input type="text" name="username">
</label>
```

Unfortunately, nesting `<label>` elements inside each other isn't valid HTML, so if you want to provide a label to a set
of controls (such as a set of radio buttons), you'll have to use `<fieldset>` with `<legend>`. You also can't use `for`
together with `name`; it only works with `id`.

## `<fieldset>`

This element is used for grouping content within a form together. It's basically a `<div>` but for form controls. In a
lot of cases, attributes applied to this element will also be applied to the elements nested within it.

## `<legend>`

This is basically a header for a fieldset. It only takes text as its content, and it need to be the very first element
within a `<fieldset>`.

## Other attributes to be aware of (Shay Howe only barely mentioned them; I don't know which elements they apply to)

* `accept`
* `formaction`
* `formenctype` (Form Encryption Type)
* `formmethod`
* `formnovalidate` (Form no validate)
* `formtarget`
* `max`
* `min`
* `pattern`
* `readonly`
* `selectionDirection`
* `step`

# Lesson 10: Building Forms

As a developer, you have limited ways of capturing user input. You can use event listeners, but those are largely
reactive. They can't help you gather more nuanced information like usernames or passwords. That's what makes forms so
essential.

## Initializing a form

To create a form, all you need to do is use the `<form>` element. This serves as a container for your form, regardless
of what type you use. It's effectively a `<div>` for controls to get user input.

The two most common methods to give the `<form>` element are `action` and `method`. `action` defines the URL that the
form information will be sent to once it's submitted. The `method` attribute, on the other hand, defines the type of
HTTP request that should be used when the form is submitted – it defines the protocol the info will be sent through.

## The `<input>` element

One of the more common elements that you'll find when dealing with user input is the `<input>` element. This element is
both self-closing and incredibly versatile. It allows you to create multiple types of inputs, all by changing the value
of the `type` attribute.

## Text Fields and Text Areas

HTML provides two elements for getting text-based input from a user. These are text fields and text areas.

### Text Fields

Text fields are just that: they're fields that the user can type text into. To create one, all you need to do is use
the `<input>` element and set the value of its `type` attribute to `text`. It's also a good idea that you give the
element a `name` attribute as well, since that will give the input a name that can be referenced after the information
has been submitted.

However, there are more specific values that you can give to the `type` attribute. The other value that has been in the
language for a long time is `password`. I don't know if this can be overwritten, but it causes any text typed inside it
to appear as asterisks. In fact, a lot of solutions for creating a "show password" toggle just change the input's type
from `password` to `text`.

HTML5 added some more semantic type values, though. All of these values allow you to give the content that the user
types in more semantic meaning. In fact, there is zero reason not to use them. If older browsers don't recognize their
values, then they'll just use `text`. But phones will actually display different types of input depending on the value
of the `type` attribute. So, if the value is `date`, tapping it will display a calendar selector – it won't even bother
to display a keyboard.

#### The new HTML5 `type` values

* `color`
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

### Text Areas

Text areas are designed to capture large chunks of text, such as comments. You can add them with the `<textarea>`
element. Note that unlike `<input>`, this element isn't self-closing. However, you can place text inside the element
to provide starting text. This isn't the same as placeholder text, though; the text won't go away the moment you start
typing. If you want true placeholder text, you'll need to use the `placeholder` attribute, which is supported by both it
and the `<input>` elements configured for text.

You can define the `<textarea>` element's width and height through the `col` and `rows` attributes. `col` defines the
width by having the browser multiply `col`'s value by the average width of the typeface's characters. `rows` defines the
number of lines of text that you want displayed. However, it's much more common to define this element's width and
height through the `width` and `height` CSS properties.

## Multiple-Choice Inputs and Menus

HTML also allows users to submit information via radio buttons, check boxes, and drop-down lists.

### Radio Buttons

Radio buttons are ideal for when you only have a small amount of options that can be selected within a group. To create
one, all you have to do is use an `<input>` element and give it a `type` attribute with a value of `radio`. Only one
radio button within a group can be checked at a time, but the only way to indicate that multiple radio buttons are part
of the same group is by giving each the exact same `name` value.

Radio buttons also aren't that sophisticated. On their own, having one checked over another doesn't tell any computer
system much. That's where the `value` attribute comes in. It associates a value with each radio button, so that you can
tie more nuanced data to them. In fact, I don't think you can actually make a radio button without a value. It wouldn't
make sense. Say you have two radio buttons, but neither have values. Well, as far as the computer's concerned, what's
the difference between them? What's so important about them that only one can be selected at a time, despite their
appearing identical?

### Drop-Down Lists

Drop-down lists are great for giving users a large set of possible options while consolidating them within a small
space. If you have more than a few radio buttons, it really would be better for you to remake the control as a
drop-down list instead. Also, like radio buttons, drop-down lists only let you select one option per group at a time.
However, this is only by default; you can modify lists to allow for multiple selections.

To create a drop-down list, you just need to use the `<select>` element. This is a more container-based element, similar
to a `<ul>` or `<ol>`. Inside this element go `<option>` elements, with each option representing a possible choice for
the list. Because all the `<option>` elements are contained within the `<select>` element, you also don't need to give
each option a `name` attribute. You only need to give it to the `<select>` container. That's enough to group them.
However, each `<option>` element still needs a `value` attribute, just like how radio buttons do.

As for the `<option>` elements, they're not self-closing. But because of that, you can insert text inside them and
associate that text with just that element. You can't do that with radio buttons; you might have text right next to
them, but there's nothing semantically tying them together.

#### Multiple Selections

You can also configure drop-down lists to allow the user to select multiple options by giving it the `multiple` boolean
attribute. Most browsers will render this type of `<select>` as a longer list, but it's probably a good idea to use
CSS to show more options at once. And because this type of list is more uncommon, it might also be a good idea to
include a note saying that the user can select multiple options.

#### `selected`

You can give an `<option>` inside a `<select>` element the `selected` attribute. This will treat it as the default
selection. If you're just using the default form of drop-down lists, then you can only give the attribute to one
element. However, if you use it inside a `<select>` element configured to allow for multiple selections, then you can
give it to multiple `<option>` elements.

## Submitting a form

Forms are great and all, but they can't do much if they're not sent to a server. HTML offers two ways of doing this:
you can either use a `<input>` and give it the attribute-value pair of `type="submit"` or you can use the `<button>`
element. Unlike `<input>`, `<button>` is a block-level element that content can be nested inside, so you can get a
little more fancy if you opt for it.

And since the element can have text nested inside it, the text that gets displayed by the button isn't determined by
the value of its `value` attribute.

## Other Inputs

`<input>` support a few more values that give you control over your forms.

### Hidden Input

When you give an `<input>` element `type="hidden"`, you create an element that isn't displayed on the page but is sent
with all the other information when the form is sent. Just be sure to give it `name` and `value` attributes.

```html
<input type="hidden" name="tracking-code" value="SR-388">
```

### File Input

When you give an `<input>` element `type="file"`, the browser will render it as a button for uploading files. Sadly, all
of the browsers block you from styling most of the properties of this element. If you want to completely style them,
you'll have to use JavaScript.

## Organizing Form Elements

Supplying a `<form>` with inputs is only half the battle. You still need to label these elements, so that users know
what they refer to. This is where labels, field sets, and legends come in.

### Labels

This is basically what you should be using for all elements, even if they just let you use plain text. The `<label>`
element allows you to tie a set of descriptive text to a form control unambiguously. There are two ways of doing this:

1. Give the `<label>` element a `for` attribute that has a value equal to the `id` value of the element it's supposed to go with
2. Wrap the `<label>` element around the element you want the label to be for

Unfortunately, `for` doesn't work with the `name` attribute, so in a lot of cases, you're going to have elements that
have their `name` and `id` attributes set to the same value. Also, since you can't have multiple elements have the same
ID, you have to wrap things like radio buttons and checkboxes inside their `<label>`. Otherwise, you'd have, at best,
the label apply to just one of the options.

If you do decide to wrap a `<label>` around some set of elements, you don't need to use `for` or `id`, even for single
elements.

### Field Sets

The `<fieldset>` element is used to separate forms into distinct groups or sections. For example, you might have a
section for getting the user's information and another section for getting their feedback. Each of these would be
contained within a separate `<fieldset>` element.

```html
<fieldset>
  <label>
    Username
    <input type="text" name="username">
  </label>
  <label>
    Password
    <input type="text" name="password">
  </label>
</fieldset>
```

### Legends

The `<legend>` element is basically a label for a `<fieldset>`. That is, they're basically fieldset headings. Whenever
you do use this element, just be sure to place it as the very first element within the `<fieldset>`.

## More Form and Input Attributes

There are a lot of attributes designed specifically for forms, but here are some of the more commonly-used ones:

### `disabled` (Boolean)

This attribute renders a form control unusable. Disabled elements won't send any information to the server when the form
is submitted. You can apply `disabled` to individual elements or to entire `<fieldset>` groups. If you disable a
`<fieldset>` that contains a hidden input, then that input will be disabled, too.

### `placeholder`

This attribute defines text that gets displayed when an element is empty and doesn't have focus. This is different from
giving text-based inputs a `value` attribute, because the value given to that attribute doesn't go away when you click
it.

### `required` (Boolean)

The `required` attribute prevents a form from getting submitted if the element attached to it is empty. It'll also
display an error message by the element itself, though unfortunately, it seems that there are very, very few ways to
style them. You can change the message, but that's kinda it.

### Extra Attributes the Guide Doesn't Want to Get Into

* `accept`
* `autocomplete`
* `autofocus`
* `formaction`
* `formenctype` (Form Encryption Type)
* `formmethod`
* `formnovalidate` (Form no validate)
* `formtarget`
* `max`
* `maxlength`
* `min`
* `pattern`
* `readonly`
* `selectionDirection`
* `step`
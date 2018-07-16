# You Don't Know JS book 1, Chapter 1 – Into JavaScript

X.X.X - Main section number, sub-section number, sub-sub-section number

## 0.0 – Extra

### 0.0.1 – Loose equality documentation

[This is the link to the part of the JS documentation that describes how the `==` operator works.](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3)

### 0.0.2 – Good rule of thumb for when to use `==`

1. If at least one value in the comparison isn't always the same value each time – whether that's `true` or `false` – use `===`.
2. If either value is falsy (such as an empty array) and you don't want it coerced into `false`, use `===`.
3. Feel free to use `==` in all other cases

### 0.0.3 – `void 0`

In all modern-day versions of JS, it's perfectly fine to use `undefined` in your code. However, not all browsers
supported the keyword from the beginning, meaning that it will sometimes cause browsers to break. However, `undefined`
has existed in all versions of JS; it's just that back then, you had to use `void 0`* instead. Using it today won't cause
any problems in the code, but you might confuse someone who's never seen it before.

\* You can use any value after `void`; it's just that `void 0` only requires that you type one more character.

## 1 – Values and Types

### 1.1 – Overview

To reiterate, JS is loosely-typed. This means that the language supports a wide range of data types, but specific types
aren't immediately available. All JS variables use the same set of variable keywords.

#### 1.1.1 – JS' variable types

* Strings
* Numbers*
* Booleans
* Null and Undefined
* Object
* Symbol

\* JS does support integers and floats, but in the majority of cases, they're rolled into a single numerical value type
that's implemented as a 64-bit double.

#### 1.1.2 – The `typeof` operator

You can use the `typeof` operator to determine the type of a variable. Note that despite using actual letters, this is
an operator and not a function. It'll return a string for the type (for example, `typeof 2` will evaluate to
`"number"`).

However, something you should absolutely be careful about is what happens when you use `typeof null`. This expression
will evaluate to `object`, which was a glitch at one point. Sadly, too much legacy code depends on this behavior for it
to be safely patched out.

#### 1.1.3 – Declaring a variable with no value

When you declare a variable without giving it a value (`var a;`), that's equivalent to setting it initializing it to
`undefined` (`var a = undefined`).

### 1.2.1 – Objects

JS object properties and methods can be referenced with either dot (`object.property`) notation or bracket notation
(`object["property"]`). It's faster to use dot notation, but there are some cases when it just doesn't work. If an
object's name is multiple words or contains special characters, then you'll have to use brackets. Likewise, you'll have
to use brackets when you have the name of an object's key stored inside a separate variable.

```javascript
var obj = {
    a: "Hello, world!",
    b: 42
}
var b = "a";

obj[b]; // Equivalent to obj["a"]; evaluates to "Hello, world!"
obj["b"]; // 42
```

Pretty much everything in JS is represented as an object, though arrays and functions are more specialized forms.

#### 1.2.2 – Arrays

This is a really bad idea, but since arrays are just a type of object, you can overwrite their behavior, having them
index their values by letters rather than numbers. Similarly, you could use an object but have the trigger discipline to
give it nothing but numerical values. Again, a really bad idea. Arrays and objects are specialized for a reason; there's
no need to use them for anything other than their intended purposes.

Still, since arrays are objects, they have access to the `length` property. Plus, if you use `typeof` on one, you'll get
a return value of `"object"`.

### 1.2.3 – Functions

If you use the `typeof` operator on a function, you'll get `"function"` back, as opposed to `"object"`.

### 1.3 – Built-in type methods

Pretty much all possible value types have object properties that make using them more convenient. In the case of objects
like arrays and functions, these properties are built right in. However, primitives are a little different. Each
primitive has an associated object, with the primitive being lowercase and the object being uppercase (i.e., `number`
and `Number`). These accompanying objects are basically primitive wrappers, extending the primitive functionality to
become object-oriented.

## 1.4 – Comparing Values

There are two comparisons that are the bread and butter of any program: equality comparisons (which comprise equality
and non-equality) and inequality comparisons. All of these return either `true` or `false`.

### 1.4.2.1 – Truthy and falsy values

Truthy and falsy values are values that JS will coerce into either boolean `true` or boolean `false`. However, JS might
try coercing mismatched values into other types first, so some might never become booleans. I don't really get the rules
for that, though.

#### 1.4.2.2 – List of falsy values

* `""` (An empty string)
* `0`, `-0`, and `NaN`
* `null` and `undefined`
* `false`

#### 1.4.2.3 – List of truthy values

Literally everything else, but here are some less obvious examples:

* `[ ]` - An empty array
* `{ }` - An empty object
* Any function

### 1.4.3 – Equality operators

JS supports four equality operators: `==`, `===`, `!=`, and `!==`. The latter two are also called non-equality
operators. Most developers conceptualize the difference between `==` and `===` as `===` checking for value and type,
while `==` only checks for value. That will hold up in most cases, but it's not foolproof. In truth, `==` and `===` are
almost exactly the same; it's just that `===` doesn't allow for type coercion.

As an extra bonus, JS always follows the same set of rules when trying to compare two values with `==`. For example,
when the interpreter encounters `"42" == 42`, it will always turn it into `42 == 42`. It will never turn it into
`"42" == "42"`. Again, Simpson argues that `==` is a tool like any other. When you neglect it because you think that
`===` is safer and more predictable, you're limiting yourself because you can't be bothered to learn how the tool works.

For the above case, this is what happens:

1. The engine will check whether the values are of the same type. If so, it'll just compare them.
2. The engine will check whether the string is basically a number (`"42"` is basically `42` wrapped in quotes). If so, it'll turn it into a number. Otherwise, it will convert   the string into `NaN`.
3. The engine will then compare the values.

Still, if you're uncertain about what your code will do or don't understand how it interfaces with code written by
others, then `===` is still a decent bet. Though Simpson advocates for `==` being the default, `===` does have plenty of
uses. It's just that it tends to be overkill.

#### 1.4.3.2 – `NaN` Comparisons

`NaN` is a very unique value in JS. It has the distinction of being the only value in the language that is not equal to
itself. As such, literally any comparison involving `NaN` will evaluate to `false`.

### 1.4.4 – The inequality operators

The inequality operators `<`, `>`, `<=`, and `>=` all have more of a mathematical bent. They all test for quantitative
differences, rather than qualitative ones. The operators can be used with numbers, as you would expect, but they can
also be used with strings. When they are, the strings are compared lexicographically.

One curious omission, though, is that the operators don't have strict equivalents. In fact, while all the operators
behave similarly to `==`, they have some differences. So, if you have `41 <= "42"`, it'll turn into `41 <= 42`, which is
`true`. Of course, if you try comparing a number with something that obviously isn't a number (like `41 >= "Cat"`), the
string will become `NaN`, which will cause the comparison to yield `false`.

## 2.1 – Variables (4.0 in Google Notes)
# You Don't Know JS book 1, Chapter 1 – Into JavaScript

X.X.X - Main section number, sub-section number, sub-sub-section number

## 0.0 – Extra

### 0.1 – Loose equality documentation

[This is the link to the part of the JS documentation that describes how the `==` operator works.](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3)

### 0.2 – Good rule of thumb for when to use `==`

1. If at least one value in the comparison isn't always the same value each time – whether that's `true` or `false` – use `===`.
2. If either value is falsy (such as an empty array) and you don't want it coerced into `false`, use `===`.
3. Feel free to use `==` in all other cases

### 0.3 – `void 0`

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

When you declare a variable without giving it a value (`var a;`), that's equivalent to initializing it to `undefined`
(as in, it's the equivalent to `var a = undefined`).

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

## 2 – Variables

### 2.1 – Overview

JS variable names must all be valid identifiers. There is a simple set of rules for determining whether a name is valid,
but that's only for ASCII-based English characters. Obviously you can also use foreign language characters, and
apparently you can also use emoji. I don't know how they work, though.

As long as you're just using basic ASCII, though:

1. Identifiers cannot be reserved words – the words that JS uses to operate
2. Identifier must start with a letter, an `_` (underscore), or a `$`
3. For all characters other than the first, you can use letters, `_`, `$`, and any number

### 2.2 – Function Scopes

Whenever you use the `var` keyword to declare a variable, that variable will be accessible from anywhere from within the
function scope it was declared in. So, if you use `var` inside a loop, it will still exist and be accessible after it
ends. It will get garbage-collected eventually, but for at least some period of time, it'll be accessible out of
context.

If the keyword is used outside a function, then that variable will be treated as completely global.

#### 2.2.1 – Hoisting

The mechanism that allows variables to be accessible from anywhere within the scope they were declared is called
**hoisting**. It is absolutely important that you understand it, as a lot of developers end up getting tripped up by
not even knowing it exists.

The way it works is that it moves any instances of variable declaration to the very top of the scope. So, all cases
of statements like `var a;` will get moved all the way up. However, this is only for the declaration, not the
initialization. If you use a statement, like `var a = 2;`, the engine will basically break it into two statements:
`var a;` and `a = 2;` Only the former will be moved up, so if you try accessing `a` before it gets assigned a value,
you'll get `undefined`.

However, this isn't too useful when dealing with variables. You generally don't want to take advantage of hoisting for
variables, as it can make code very confusing to read. But functions are a different story. Hoisting also works on
function definitions, which is what allows them to be called before they're defined. Using hoisting to throw all your
function definitions at the bottom of your code is perfectly fine, and can even help make it more readable.

#### 2.2.2 – Nested Scopes

A variable is accessible from anywhere within the scope where it was declared, including scopes nested within that
scope. On the flip side, any variables declared within a scope is **inaccessible** by the scopes that contain that
scope. Trying to reference a variable's value before it's been initialized or assigned will result in a
`ReferenceError`.

Be extra careful about referencing variables that you haven't declared yet. By default, JS has an annoying behavior
whereby it will, upon finding an assignment for a variable that doesn't exist, create that variable as a global
variable. However, this doesn't happen if you set the entire program or even the scope where the assignment happens to
**strict** mode. In strict mode, such an occurrence will result in a `ReferenceError`.

#### 2.2.3 – Block-level scopes

ES6 introduced support for block-level scopes via the `let` and `const` keywords. Variables declared this way are only
accessible within their block and any blocks contained within it. Blocks, in this case, basically refers to anything
contained within a set of braces `{ }`, including functions, conditional blocks, and loops. This is very similar to a
technique that other languages allow, by which any variables contained within a set of braces is treated as being scoped
to the block they create. Those don't need dedicated keywords, but at least a huge oversight finally got mended. It just
took almost twenty years.

## 3 – Conditionals

This is an area where JS does better than Python. Unlike Python, JavaScript supports switch statements and a C-like
ternary operator. This makes makes conditionals a little more concise and their writing a little faster. Just be sure
not to forget that switch cases can cascade into each other; if you don't want that, you need to use the `break`
keyword.

```javascript
var a = 2;
switch (a) {
    case 1:
        console.log("a = 1");
        break;
    case 2:
    case 4:
        console.log("a % 2 = 0 and 0 < a < 5");
        break;
    default:
        console.log("a = 3 or a >= 5");
}
```

## 4 – Strict Mode

Okay, so the book doesn't delve into this too much, but apparently, it's not always a great idea to set an entire script
to strict mode, because it screws with how older browsers handle code that's written with the mode in mind. After all,
the mode was only added in ES5.

In strict mode, JS doesn't try to resolve any errors. This means that if you do things like assign a value to a variable
that hasn't been declared, it won't create that variable in the global namespace. Instead, it'll just break the script.
This has some trade-offs. In some cases, you don't want scripts to completely break and would like for them to power
through any bugs. At the same time, using strict mode actually provides a lot of performance increases and
optimizations.

To use strict mode, all you need to do is type `"use strict";` anywhere in the code. If placed at the very top, the
entire script will be set to strict mode. If placed within a function, all code in that function will be set to strict
mode. It doesn't seem that you can scope strict mode to a block, which I guess makes sense. Strict mode was added in
ES5, while major block-scoping support was added in ES6. ES6 had to create entirely different keywords and couldn't
modify `var` at all; I'm guessing `"use strict";` was similarly untouchable.

Curiously, strict mode disallows things like deleting variables, deleting functions, and using octal numbers. I'm not
sure why it bars octal numbers, but at least it completely neuters the `with` statement and the `eval()` function – the
two parts of the language that ignore lexical scoping rules.

## 5 – Functions as values

### 5.1 – Overview

Whenever you use the `function` keyword by itself to define a function, that function is basically being stored in a
variable. It doesn't matter whether you explicitly assign it to a variable, either.

This has some implications. This behavior means that you can assign a function as a return value and can even use them
as arguments. When you assign a function to a variable, that function can be either named or anonymous. If you do decide
to name the function, you cannot reference it by that name; you have to use the name of the variable that has the
function assigned to it.

### 5.2 – IIFEs: Immediately-Invoked Function Expressions

By default, defining a function doesn't call it. You need to do that in a separate expression. However, JS does offer a
way of calling a function the moment it gets defined: this is through IIFEs.

To make a IIFE, all you need to do is wrap a function definition inside a set of parentheses `( )` and then follow that
with another set of parentheses, which will contain the arguments. Basically, you're turning this...

```javascript
function x {
    console.log("Here's some text");
}
x();
```

...into this:

```javascript
(function x() {
    console.log("Here's some text");
})();
```

You're substituting the name in the function call for the function definition itself.

And since IIFEs are functions, this means that they each have their own scope. It's a good way to isolate a function
from the rest of the surrounding code when you need to support older browsers. The technique has started to fall by the
wayside thanks to ES6 introducing block scope, but IIFEs still have merits based on legacy support. They might be a
little on the older side at this point, but they still allow you to create variables without fear of creating any name
conflicts.

But since IIFEs are functions, that also means that they can have return values. You can set a variable to an IIFE that
returns a value, and it'll be set to that value.

Example of using IIFEs to avoid name conflicts:

```javascript
var a = 1;
(function() {
    var a = 2;
    console.log(a); // 2
})();
console.log(a); // 1
```

And an example of assigning them to a variable, only for the IIFE to return a value:

```javascript
var a = (function() {
    return 1;
})();
console.log(a); // 1
```

### 5.3 – Closures

### 5.3.1 – Closures Overview

Closures aren't going to be covered too much here, as there's an entire book in the series that's dedicated to the
topic. But basically, think of them as a function's ability to recall its original context, even after things like it
being returned as a value to a scope elsewhere in the code.

#### 5.3.2 – Modules

Modules are a common use case for closures, providing developers an easy way to create an API with only a portion of
its interface exposed. The basic idea is that you have a user call a function **x**. That function then returns another
function **y**. **y** is dependent on **x**, but you only give the user access to **y**. Thanks to closures, this means
that the user is restricted to using whatever values and variables exist within **y**, yet it can still access all the
values it needs within **x**.

## 6 – The `this` identifier

`this` is a keyword that exists in all object-oriented languages. However, JS' version of the keyword tends to be
misunderstood, because it doesn't quite work the way that it does in other languages. Basically, `this` can refer to a
lot of different things, where it would refer only to a smaller number of things in other languages.

There are four basic rules to keep in mind:

1. If you're not in strict mode, then using `this` will refer to the global object. But if you are, then this usage will
    break the script.
2. When you call the method of an object, using `this` within that method will refer to its object.
3. Whenever you call a function, you can override what `this` refers to by invoking that function's `.call()` method. I
    don't think this function has to be part of an object, either. Calling the same function multiple times but with a
    different object passed into it via `call` each time will produce different results.
4. Using `new` to call a function that uses `this` will make `this` refer to a brand new empty object

Here are examples of all four in action:

```javascript
function foo() {
    console.log( this.bar );
}

var bar = "global";

var obj1 = {
    bar: "obj1",
    foo: foo
};

var obj2 = {
    bar: "obj2"
};


foo();              // "global"
obj1.foo();         // "obj1"
foo.call( obj2 );   // "obj2"
new foo();          // undefined
```

Those are the only four rules, but that's still more than some other OO languages. You need to be aware of the context
in which `this` is being used to understand why, depending on the situation, it produces some values over others

## 7 – Prototypes

As with closures, there is an entire book dedicated to the subject of prototypes. For now, though, think of it as a set
of fallbacks for when the engine can't find a certain property or method. Basically, if an engine tries looking for a
property in an object and can't find it, it'll turn to the object's prototype. That prototype can itself have a
prototype, so the engine can keep going up levels of prototypes if it still can't find the property until it either
finds it or finds nothing.

An object is linked to a prototype the moment it's first created. Presumably, if you add to a new object properties
that have names that already exist in the prototype, the engine will just use the versions that were added. The engine
will only start looking when it can't find something.

## 8 – Old & New

### 8.1 – Overview

JavaScript comes with a host of problems that just don't exist for other languages. The biggest one is the need to
support a wide range of browsers, not all of which support the same functionality in the same way or are kept
up-to-date.

There are two main techniques for making this easier:

1. Polyfilling
2. Transpiling

### 8.2 – Polyfilling

Polyfilling is implementing a new feature of a language in code that's recognized by older versions of the language.
Basically, you just check to see if a feature exists within the user's version of the language (through something like
an `if` statement), and if it isn't, run the polyfill.

For example, all modern versions of JS support the `Number.isNaN()` method. With polyfills, you would check if the
method is supported. If not, you'll then add that method to the `Number` object, allowing you to use the same code for
both modern and older browsers. Now, doing this is easy for methods. It's a little harder when you're trying to
implement more low-level additions, like entire keywords.

Just be careful if you ever decide to write your own polyfills. Your tests need to be rigorous and test for every
possible case. For this reason, it's often best just to use someone else's polyfill. They'll be more likely to have been
tested with much more rigor. Two well-known examples of polyfills that are tried and true are the ES5 Shim and the ES6
Shim.

### 8.3.1 – Transpiling

As mentioned earlier, polyfills do have a big blind spot: it's very hard to add anything lower-level than methods. In
fact, it's next to impossible. That's where transpiling comes in, to save you from even bothering. The idea is that you
write code using all the newest syntax and tools available (possibly even using tools that haven't been added to any
major browsers yet), and then convert it into code that uses older syntax and tools. The modern browsers will still
support the old syntax, so the resulting code will be able to run in everything.

So, if you're going to convert everything into old syntax, why bother using the new syntax? There are a few reasons:

1. Newer syntax is often designed to be more readable. This helps make maintaining the code base far easier.
2. It's possible to serve the code that uses the new features to new browsers. This will often come with big performance boosts.
3. Doing this allows you to use new syntax the moment it comes out. If you ever run into any issues, you can file any problems with the design committee.

Basically, transpiling should be viewed as an essential part of modern JS development. It's one of the easiest ways of
ensuring that all users have a good experience, even if they are using older browsers.

#### 8.3.2 – Transpiling Example

As an example, modern JS supports default parameters – values for a function's parameters for when nothing gets passed
into it. It looks like this in modern browsers:

```javascript
function foo(a = 2) {
    console.log( a );
}

foo();      // 2
foo( 42 );  // 42
```

And this is what it looks like when transpiled:

```javascript
function foo() {
    var a = arguments[0] !== (void 0) ? arguments[0] : 2;
    console.log( a );
}
```

It just uses the ternary operator to check if `arguments[0]` is undefined. If not, it'll just use `arguments[0]`, but if
it is, then it'll use `2`.

## 9 – Non-JavaScript

JS is in a bit of a peculiar spot compared to other languages. Since the language was first designed to interface with
browsers, there's a lot of browser-specific functions and methods that can't be used in any other context. The biggest
example of this is the entire DOM API. It looks like an object, but that appearance is basically in interface in itself.
Objects like this – ones that use their object-ness as an interface for external functionality – are called
**host objects**.
# You Don't Know JS book 1, Chapter 1 – Into Programming

## 1.2 – Input

### 1.2.3 – Getting Input

At least as far as web development is concerned, the most common way of getting user input with JS is forms and fields.
However, much like other programming languages, JS also supports a function that lets the user type input directly. In
JS' case, it's called `prompt()`.

The function isn't perfect, though. For one, it creates an alert box, which can be annoying to the user, and for
another, if the code runs while the window that the code triggered in doesn't have focus, Chrome will suppress the
prompt.

## 1.4 – Values and Types

### 1.4.2 – Loose equality and converting between types

The `console.log()` method (and other similar methods) is only able to print strings. This means that if the interpreter
finds a non-string inside it, it will perform a conversion. Such behavior is called **implicit coercion**. But JS also
supports **explicit coercion**, which is done through functions such as `Number()`, `parseInt()`, and `parseFloat()`.

JS seems to be the **only** language that supports implicit coercion, though, so it also seems to be the only language
to offer two types of equality operators: `==` (the loose equality operator) and `===` (the strict equality operator).
The `===` operator is almost exactly like the `==` operator found in other languages. It checks that the values on
either side are equal not just in value but in type. If either doesn't match up, then the operation will return `false`.
However, JS' `==` operator is exactly the same, except that it allows for coercion. If there is a type mismatch, then JS
will try to convert the left-hand value's type into that of the right-hand value.

A lot of developers absolutely hate implicit coercion, but it's Simpson's stance that they only hate it because they
never bothered to learn the rules for it.

## 1.6 – Variables

### 1.6.1 – Variable intro

Every single variable within JS has dynamic typing. THis means that you never need to specify the type of any variable.

Just also be aware that JS doesn't offer direct access to specific numeric types. It knows what integers and floats are,
as it offers the `parseInt()` and `parseFloat()` functions. But it doesn't give you direct access to them; you're just
stuck with a catch-all `number` type.

### 1.6.2 – Constants

JS, as of ES6, also supports a dedicated constant keyword in the form of `const`. Like in most other languages, it's a
good idea to place these variables at the very top of the program, since they will never change. You can place them
within scopes, but most constants are relevant to the entire program. By convention, JS constants don't use camel case;
instead, they use all-lowercase, separating different words with underscores.

If you try modifying a constant in JS, one of two things will happen, depending on what mode you're in. If you're in
`strict mode`, then the attempt will cause the entire script to break. But if you do it outside of `strict mode`, then
the interpreter will just ignore the modifying statement.

### 1.6.3 – The `.toFixed()` method

The `.toFixed()` method is usable on any numeric value.

## 1.9 – Functions

### 1.9.2 – Scope

At any given time, a function only has access to the variables directly inside it or within the scopes that contain it.
So say that you have `function1`, `function2`, `function3`, and `function4`. They're arranged like so, with `function1`
and `function4` being top-level functions:

```javascript
function1() {
    function2() {
        function3() {
            function4();
        }
    }
}

function4() {
    ...
}
```

`function1` only access to the variables inside itself (but not in `function2`) and in the global scope. `function3`,
on the other hand, has access to the variables inside itself, and inside `function2`, `function1`, and the global scope.
`function4`, however, only has access to the variables inside itself, the global scope, and whatever variables were
passed from `function3`.

It does not have access to anything else, even though it was called from within `function3`, which itself is nested
within two other functions. JS doesn't care about how functions were called; it cares about where they're located –
particularly how they're nested within one another.
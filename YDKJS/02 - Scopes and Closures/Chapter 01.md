
# Chapter 1 – What is scope?

## 1 – Overview

Central to every programming language in existence is **state** – the ability to store information for later
reuse. Once state information is created, however, the languages follow a strict set of rules for retrieving it. This
set of rules is called **scope**.

## 2 – Compiler Theory

### 2.1.1 – Overview

Let's get this out of the way: JS is not an interpreted language; it's compiled. It's just that the compilation step
doesn't happen until the moment before the compiled code needs to be run. Technically, the compiled versions of the code
are specific to the device or context it was compiled for, but that doesn't really matter.

Anyhow, compilation in JS is basically a three-step process:

1. Tokenizing/lexing
2. Parsing
3. Code generation

However, the process can become more involved, requiring several more steps. This is all in service of things like
performance and optimization, so they're basically extras. Still, JS doesn't have the luxury of compiling code well in
advance, so these extra steps often become critical for making responsive code.

#### 2.1.2 – Tokenizing and Lexing

You'll find these terms used interchangeably in some cases, just because they're so similar, but they are different.
Still, both involve breaking code down into the smallest semantically-meaningful chunks possible. So `var a = 1;` might
be broken down into `var`, `a`, `=`, `1`, and `;`. Whitespace can also be broken down, but that only happens when the
whitespace holds semantic meaning (such as in tab-separated value files).

As for the difference between tokenizing and lexing, it's all based on state. If the breaking down happens based on
state, then you've got lexing. If not, then that's tokenizing.

#### 2.1.3 – Parsing

Parsing involves processing the tokens that were created by the previous step and using them to create a model of the
code's structure, represented as a series of nested structures. The model itself is a special tree called the
**Abstract Syntax Tree** or the **AST**. Basically, think of this as a sentence diagram for the code.

#### 2.1.4 – Code Generation

In this step, the AST is used to create machine-readable code. How this happens depends on a lot of factors, including
the language the source code was written in, and what platform the resulting code is to be run on.

## 3.1 – Understanding Scope

Understanding the steps involved with compiling is a good foundation, but to understand everything, you need to know
what carries out the process.

### 3.2 – The Cast

There are three main agents involved with compiling:

1. The engine – Oversees the compiling process from start to finish; executes compiled code once created
2. The compiler – This is what actually does the majority of the work in the compiling process
3. The scope – Keeps a list of all the identifiers used within the code and enforces rules for how they can be accessed

### 3.3 – Back and Forth

To gain a true understanding of how compiling works, you need to realize that some parts of the language might not be as
they appear. For example, most people would regard `var a = 2;` as a single statement. But as far as the engine is
concerned, it's two: `var a`, which the compiler handles at the compiling step, and `a = 2`, which the engine handles at
runtime.

For the first expression, `var a`, the compiler will consult the scope to see if `a` already exists within the current
nesting level. If it doesn't, then `a` will be added to the scope rules and will only be accessible in certain contexts.
But if it does, then the compiler will just ignore it.

For the second expression, `a = 2`, the compiler will just translate it into machine-readable code that the engine can
run after the code has finished compiling. Once the engine runs the code responsible for `a = 2`, it will consult the
scope to see if `a` exists. If it doesn't, then it'll start looking elsewhere, using the scope's rules to determine
where and how it can look. After looking through every legal place `a` could be and not being able to find it, the
engine will return an error. However, if the engine finds a legal `a` at any time during its search, then it'll stop
looking and set `a`'s value to `2`.

### 3.4 – Compiler Speak

When the engine needs to consult the scope to see if a given variable exists, it does so via a lookup operation. The
only problem is that there are two kinds: left-hand side operations (LHS) and right-hand side operations (RHS). Given
the expression, `var a = b`, `a` would be found via an LHS (since it's to the left of the `=`), while `b` would be found
via an RHS (since it's to the right of the `=`). However, there is a little more nuance to that; the names are partially
misnomers, as they happen even when there are no "sides" to speak of.

Basically, think of the operations as LHS and "not LHS" – any operation that either isn't on the left side or that
doesn't involve a left side at all. When you have code like `console.log(a)`, `a` is retrieved via an RHS.

If I understand things right, here's another way of conceptualizing LHS and RHS:

* LHS – For when you need to retrieve a variable
* RHS – For when you need to retrieve a variable's value

Look at this code. It involves a number of scope lookup operations:

```javascript
function foo(a) {
    console.log(a);
}
foo(6);
```

This is how the engine works through it:

1. The engine looks for the value of the `foo` function via RHS
2. Inside the function after it's been called, an LHS is done to find the parameter `a` and then assign `6` to it. As `6` is a simple value, no lookups are needed.
3. The `console` object is looked up via RHS. It's `log` method is then found via property resolution.
4. The instance of `a` inside the `console.log` is looked up via RHS
5. Inside the `console.log` method, the value of `a` is assigned as the method's parameter via LHS. There can then be multiple LHS and RHS operations inside `console.log`.

------------Stopped at the **Note**
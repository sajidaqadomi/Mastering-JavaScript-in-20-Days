# Day 13💻
## **[Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)** 🔥🔥

### Lexical:

> The idea that a compiler (a parser or a processor) is figuring out all those scopes ahead of time before being executed, that's what we mean by the concept of **lexical scopes**.

That's where that name even comes from, that **lex** shares the same root as the first stage of parsing, the **lexer**.

We have two type of **Scope** model:

- **Lexical Scope**: It's an author-time decision and all the **scopes** (where the `function` and `variables` written) create in **compile-time**. So when we talk about **Lexical Scope**, we think about something that is **fixed** at author-time and it's predictable, it is **not** affected by **run-time** conditions.

- **Dynamic Scope**: We know that **Dynamic Scope** exists in some languages, but it does not exist in JavaScript. So this is a _theoretical_ example.

> The idea of a **Dynamic Scope** is the idea that a `function`'s references to its `variables` are depended upon where that `function` was called from. The same `function` called from 100 different places ends up giving 100 different answers to what the `variables` are.

> So in **Dynamic Scope**, it is scope that is determined based upon the conditions at **run-time**, whereas **Lexical Scope** is determined at **author-time** (or **compile-time**).

> The JavaScript is absolutely, definitely, 100% **lexically scoped**.

The **Dynamic Scope** is not very common at all, we generally only see this in a few old academic languages and maybe some different modes.

### Usage of Function Scoping:

In the below, there is a **Name Collision**. And if for resolving the problem, we turn this code:

```JavaScript
var teacher = "Kyle";

// ..

var teacher = "Suzy";
cobsole.log(teacher);   // Suzy -- oops

// ..

cobsole.log(teacher);   // Suzy -- oops

// Function Scoping
```

Into this one:

```JavaScript
var teacher = "Kyle";

function anotherTeacher() {
  var teacher = "Suzy";
  console.log(teacher);   // Suzy
}

anotherTeacher();

cobsole.log(teacher);   // Kyle

// Function Scoping
```

We still have a **Naming Collision**, we just shifted it to a different variable name (`anotherTeacher`).

💡 **Name Collision:** When two different entities used the **same semantic name** in the **same scope**.

There's a principle within **Software Development**, it's called the principle of **least exposure** or the principle of **least privilege**, that says this:
_You should default to keeping everything private, and only exposing the minimal necessary._

That's one of the core principles of software engineering, because it essentially sets up a defensive posture. And we can solve **three** main problems by using this defensive posture:

- If we hide something within a scope, or hide something on a namespace or do some other sort of hiding, then we reduce the surface area for **name collisions**. (so number one, we solve naming **collision problems**.)
- If we hide something, it means that somebody else can't accidentally of intentionally misuse that thing. If we expose it publicly, everybody can use it. (so number two, if we hide something, then we prevent other from accessing it.)
- If we hide something, like one of those implementation details, or like a variable name, we protect ourself for future refactoring. (so the third one, and probably the most core and important reason for this principle, it's often overlooked.)

But, right now, this usage of a `function` is not really accomplishing that task, because the problem is that now we have a `function` that has a name in that scope.
It has the name `anotherTeacher`. So we didn't really fix the **naming collision** problem at all, we just shifted it to a different variable name.

## Immediately Invoked Function Expression (IIFE):

This is true that in the previous example, we have a new scope, and we could contain any assignments of that scope, but we still have a **naming collision** problem, so we need a better way of using our knowledge of scope.

We can resolve this problem by using `function expression`:

```JavaScript
var teacher = "Kyle";

(function anotherTeacher() {
  var teacher = "Suzy";
  console.log(teacher);   // Suzy
})();

cobsole.log(teacher);   // Kyle

// Function Scoping: IIFE
```

But probably we have seen this code with an `anonymous function expression` form.

Even if we put the called `function's name` inside the parentheses like this:

```JavaScript
(anotherTeacher)();
```

 we create **IIFE**. That's where this comes from, using a `function expression` to create a scope, and immediately invoking it. We only need it for that moment, just so we can have a scope. So it runs once and then it kinda goes away.

🤔🤔🤔❓❓
**Q:** Why is this not a `function declaration`?

**A:** Because the word `function` is not the first thing in the statement.

In the below example we make `named function expression` to `anonymous function expression` and just pass in a value to a parameter instead of making an assignment.

```JavaScript
var teacher = "Kyle";

(function (teacher) {
  console.log(teacher);   // Suzy
})("Suzy");

cobsole.log(teacher);   // Kyle

// Function Scoping: IIFE
```

## Block Scoping:

We can get the previous example (**function scope**) and turns it to **block scope** form.

```JavaScript
var teacher = "Kyle";

{
  let teacher = "Suzy";
  console.log(teacher);   // Suzy
};

cobsole.log(teacher);   // Kyle

// Block Scoping: encapsulation
```

The **Block Scoping**, it's scoping that's done with blocks (curly braces `{}`) instead of with `functions`.

When we use **Block Scoping**, same principle is gonna apply. We wanna put something inside of a block (instead of inside of the enclosing scope), because:

- We wanna hide it, so that it has fewer chances of **name collision**.
- We wanna protect a detail.
- We wanna protect future refactoring.

All the same principle applies. It's just the mechanism we use is now a **Block Scope** declaration instead of an **IIFE** (**`function` scope**), for example.

🗒 🖐️ ️We can't use `var` in this example, because of historically the difference between the **`var`** and **`let`** or **`const`**:

- The **`var`** has been attaching itself to the outer **`function` scope** or **`global scope`**.
- But with the **`let`** or **`const`** we can make a declaration inside of a block (curly braces `{}`) and it turns that block into a scope (or in other words, **`let`** and **`const`** attached themselves to their enclosing **block scope**).

> **Blocks** are not **Scopes** until they have a `let` or `const` inside of them and then that sort of implicitly makes them a **scope**.

### Choosing `let` or `var`:

This is an example that shows us where we should use `var` and where we should use `let`:

```JavaScript
function repeat(fn, n) {
    var result;

    for (let i = 0; i < n; i++) {
        result = fn(result, i);
    }

    return result;
}

// Block Scoping: let + var
```

**The `var`**: When we have a variable that belongs to the entire **`function` scope** or needs to escape an unintended block, we use **`var`**. The `var` hoists and attaches itself to the **`function` scope**. The `var` can be reused within a scope, but `let` can not.

**The `let`**: When we have something that is naturally **block scoped**, we use **`let`** (for example in `for` loop). Or we want to use a `variable` for a few lines of code we create a **block scope** for it and then we only use **`let`** inside it.

### Explicit `let` block:

When we're only going to use a `variable` for a few lines of code, and we should not just throw it into the top level of the scope. What we should do is create a scope for it:

```JavaScript
function formatStr(str) {
    { let prefix, rest;
        prefix = str.slice(0, 3);
        rest = str.slice(3);
        str = prefix.toUpperCase() + rest;
    }

    if (/^FOO:/.test(str)) {
        return str;
    }

    return str.slice(4);
}

// Block Scoping: explicit let block
```

Open up a curly brace pair `{}` and create a scope just for those three lines of code to use the `prefix` and the `rest` variable, and then don't let them exist for any other part of the `function`.

**Don't just say `let prefix`, and `rest` at the top of our `function`, open up a curly brace there.**

### The `const`:

This is an example that shows us, what happens when we declare a mutable value like an `array` with `const`. Mutating the value is totally allowed on line 8:

```JavaScript
var teacher = "Suzy";
teacher = "Kyle";                      // OK

const myTeacher = teacher;
myTeacher = "Suzy";                    // TypeError1

const teachers = ["Kyle", "Suzy"];
teachers[1] = "Brian";                 // Allowed!

// Block Scoping: const(antly confusing)
```

🗒️💡**The `const` does not mean that it doesn't change, it means a `variable` that can't be reassigned.**

It's better to use `const` when we're assigning a value that is already a **`primitive`** and therefore **immutable** like **`strings`**, **`booleans`**, **`numbers`**. It used as a semantic placeholder for those literals. That's what `constants` are supposed to be for. They're supposed to give semantic meaning as placeholders.

So we should default to using `var`.
Use `let` where it is helpful, use `const` sparingly only with **immutable** `primitive` values.

## Hoisting:

**The JavaScript engine does not hoist**, it does not move things around the way it is suggested with hoisting.

**Hoisting is an english language convention that we have made up to discuss the idea of lexical scope, without thinking about lexical scope.**

This very simple piece of code, proves to us why hoisting doesn't actually exist:

```JavaScript
student;                        // undefined
teacher;                        // undefined
var student = "you";
var teacher = "Kyle";

// Scope: hoisting
```

In **lexical scope** discussion we would first pass through this as the **compiler**, and then we would pass through it as an **execution**.


Which was that any time JavaScript's execution engine entered a scope, it magically looked ahead and found all of the declarations wherever they were in that scope, and made `variables` for them. So it says the JavaScript engine goes and finds those `variable` declarations and moves them to the top of the scope before **execution**.
That's literally how hoisting is described.

**JavaScript does not actually reorganize our code by moving `variable` declarations up to the top.**

**If you wanna find the `variable` declarations further down in the block, the only way you can do that is with parsing.**

Let see what happened in `function`:

```JavaScript
function teacher() {
    return "Kyle";
}
var otherTeacher;

teacher();                      // Kyle
otherTeacher();                 // TypeError

otherTeacher = function() {
    return "Suzy";
}

// Scope: hoisting
```

For the exact same reason it doesn't move `variables`, it doesn't move `functions`. It handles them during the **first pass**, and then it **executes**.

To use the form of `function` where we only assign it to properties or `variables` (It means `function expression`), we have to have all of our `functions` defined before we call them. Otherwise we get `TypeError` like above example.

**With using of `function declaration` we can simply put the executable code at the top, and put our `function declarations` at the bottom. But with `function expression` we can't do the same thing.**

> The difference between a **`function declaration`** and a **`function expression`** (including **arrow functions**) is **function declaration** hoisted but **`function expression`** did not.

**This is critical to know:**

> When we assign a `function expression` to a `variable`, the `variables` decoration itself hoisted, but the assignment is a **run-time** thing. Even we have a `function expression`, **compile-time** still handled that `function expression`. It didn't defer handling. What didn't happen is it didn't get at **compile-time**, associated with some `identifier` in the scope, but it still got compiled.
>
> All `functions` have a plan for their scope, until, and every time they get executed. So whether it was a `declaration` or an `expression`, when it gets executed is when that whole mapper plan becomes a real thing in memory, and every time it gets executed, that is the case.

### Hoisting Example:

This example can trick us if we're not used to thinking about hoisting as a two-pass system:

```JavaScript
var teacher = "Kyle";
otherTeacher();                 // undefined

function otherTeacher() {
    console.log(teacher);
    var teacher = "Suzy";
}

// Scope: hoisting
```

When should use hoisting and when not:

```JavaScript
// var hoisting?
// usually bad :/
teacher = "Kyle";
var teacher;

// function hoisting?
// IMO actually pretty useful
getTeacher();                   // Kyle

function getTeacher() {
    return teacher;
}

// Scope: hoisting
```

### Hoisting and `let`:

This example shows us if we use `variable` before it declared (only if it was `let` or `const`), we get a `TDZ error`:

```JavaScript
{
    teacher = "Kyle";           // TDZ error!
    let teacher;
}

// Hoisting: let gotcha
```

**If we use a `variable` before it declared (with `let` or `const`), we get a `TDZ error` (Temporal Dead Zone error).**

> This statement, "`let` doesn't hoist", is wrong.

This example proves to us, that `let` (and `const`) will be hoist too:

```JavaScript
1. var = teacher = "Kyle";
2.
3. {
4.     console.log(teacher);    // TDZ error!
5.     let teacher = "Suzy";
6. }

// Hoisting: let gotcha
```

In above code, if the `teacher` on line 5 did not host, then line 4 should print out `"Kyle"`. Because there is no `teacher` as of line 4 and it should go to the outer scosdfsdfpe and find the `variable` from line 1. But this code still throws a `TDZ error`, and the reason is because **`let` and `const` still hoist**.

**There is a difference between how `var` and `let` or `const` hoist:**

- **`let` and `const` only hoist to a block, whereas `var` hoists to a `function`.**
- **When `var` creates its `variable` in the compile-time, it initialize it to `undefined`, but when `let` and `const` hoist and create their `variables`, they do NOT initialize it. It is in an `uninitialized` state.**

**`Uninitialized` being different than `undefined`. `Uninitialized` meaning you can't touch it yet.
And it doesn't get initialized until in that block you run across the `let` or the `const` declaration.**

> So `let` and `cont` absolutely do **hoist**, which is why we still get a `TDZ error`, it's just that they don't get **initialized**.

### Closure

#### What is Closure?

> The **Closure** is when a **`function`** is able to **"remember"** and access its **`lexical scope`** (the `variables` outside of itself, so-called **free `variables`**), even when that `function` executes in a **different scope**.

**Important Note:** So this definition has **two part** (without these two parts, we don't have a closure. We have to have both of them.):

- The `function` is able to access its **lexical scope**: We already know that, this is **lexical scope** definition in itself! **lexical scope** is that a `function` can reference `variables` outside of itself and it just goes up the **scope chain** to find it.

- The second part is the critical part. Without the second part, it's just **lexical scope**. With the second part of this definition, which is, even when the `function` is executed in a **different scope**, now we start to see something interesting. Cuz when we take a `function` and we pass it as a callback, or we take a `function` and return it back, the scope that it was originally defined in (at least conceptually), has gone away. And we would think, normally, it's been **garbage collected**, it's done. But there's a `function` that survived that was defined within that scope. It turns out that the scope didn't go away at all. It turns out that this `function` is able to hold on to a reference to that scope, and wherever we pass the `function`, it continues to have access to that. That doesn't happen by accident. That's not magical, that's **closure**.

The preservation, the linkage back to the original scope where it was defined, no matter where we pass that value, no matter where it executes, it retains that value. It preserves that scope. That's called **closure**.

So let's take a look at some examples of closure:

```JavaScript
function ask(question) {
    setTimeout(function waitASec() {
        console.log(question);
    }, 100);
}

ask("What is closure?");   // What is colsure?

// Closure
```

At the time that `waitASec function` runs, the `ask function` has already finished, and the `variable question` which it's closed over should have gone away. But it didn't go away because closure preserved it, so-called the `waitASec function` is closed over the `variable question`. That's a **closure**.

Now, academically, they think about closure on a per **`variable-basis`**, meaning only the `variables` that we're closed over, those are the only ones that are preserved. But at least the latest information that we have, JavaScript engines essentially implement closure as a linkage to the **entire scope**, **not** on a per `variable-basis`.
So it's best to assume that closure, even though academically it's per `variable`, it's best to assume closure is a **scope-based** (a per scope basis) operation.

> To create a closure don't need to do something special, just have to access a `variable` outside and then we have to pass the `function` somewhere.

> If we're in a language that has **first-class `functions`** and **lexical scope**, we're gonna have **closure**, because if we didn't have closure we would pass the `function` somewhere, and all over sudden, it would forget about all its `variables` it wouldn't make sense not to.

Another example of closure:

```JavaScript
1.  function ask(question) {
2.      return function holdYourQuestion() {
3.          console.log(question);
4.      }
5.  }
6.
7.  var myQuestion = ask("What is closure?");
8.
9.  // ..
10.
11. myQuestion();   // What is closure

// Closure
```

Here is the exact same thing. If we returned a `function` here that is closed over the `question variable`, then even though the `ask function` has finished, by line 11, we still have access to that `variable`.

It's **Not a snapshot of the `variable`**, but the **actual `variable`** itself. That's called closure.

### Closing Over `Variables`:

We maybe think of closure, snapshoting a value, that we're capturing some value at some moment.
That is **NOT** what closure is. As a matter of fact, closure has not got anything to do with the values at all. We don't close over a value. There's no such thing as closing over a value, **we close over a `variable`**, which means we have a linkage to that `variable`. Means at the time we access it, we're seeing whatever value that `variable` has at that moment, not it had before.

Here's an example that shows us, the value is not a snapshot of `variable`:

```JavaScript
1. var teacher = "Kyle";
2.
3. var myTeacher = function() {
4.    console.log(teacher);
5. };
6.
7. teacher = "Suzy";
8.
9. myTeacher();       // Suzy

// Closure: NOT capturing a value
```

**Don't think of closure as capturing values, think of it as preserving access to `variables`, a live link to all the `variables` that we are closed over.**

This is an example of closure, that bites people the most (creating closures inside of a loop):

```JavaScript
for (var i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(`i: ${i}`);
    }, i * 1000);
}

// i: 4
// i: 4
// i: 4

// Closure: loops
```

This `function`, that is being created in each iteration, it has the appearance that what it's doing is closing over the `i` value in each iteration.

So we're expecting it to print out `1`, `2`, `3`, but when we run it, it prints out `4`, `4`, `4`. Why? Cuz there's only one `i variable`. There's an `i variable` on first line and there's only one of them, and we have three `functions`. If we wanted to have **3 separate values**, we need **3 separate `variables`**. And there's only one, so of course it can only have the one value. And in this case, it's gonna have the value that occurs at the end of the loop, which is the value `4`.

If we wanted to solve this problem, and we analyzed that, we need separate `variables`, we do this:

```JavaScript
for (var i = 1; i <= 3; i++) {
    let j = i;
    setTimeout(function() {
        console.log(`j: ${j}`);
    }, i * 1000);
}

// j: 1
// j: 2
// j: 3

// Closure: loops
```

So if we wanna create **more than one variable** with the **same name**, we need to make **new scopes**, right? So we could do an **IIFE** here, but the much more common way now that we have **block-scoping** (ES6), is to just stick a block-scoped declaration in the iteration. So now `let j` is going to run every time the `for` loop iterates. And it's gonna create a **whole new `j`** in that **whole new iteration of the loop**. There are three separate `j`s and therefore we get the values in them `1`, `2`, and `3`.

**In this loop example we can see, the difference between capturing a value and closing over a `variable`.**

But there's an even better way of solving this problem:

```JavaScript
for (let i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(`i: ${i}`);
    }, i * 1000);
}

// i: 1
// i: 2
// i: 3

// Closure: loops
```

Why don't we just go ahead and make it so that if we use a `let` on our `for` loop we'll automatically create a new `i` for each iteration. Instead of creating just one that belongs to the whole `for` loop, here there's gonna be a brand new `i` for each iteration. Which means the closure just magically works.

> The point is if we need multiple **different values** being closed over, we need to closed over multiple **different `variables`**, not try to capture values.

🤔🤔❓
**Q:** So, the `i` is defined actually inside, even though it's written this way, but is it actually then defined inside the block?

**A:** Yes, it is interpreted as if each iteration there's a new declaration of `i`, and JavaScript takes care of assigning it the value that its cousin had at the end of the previous iteration. It wires up all that stuff for you.

🖐️⚠️Just as a little tiny detail, not that many people are gonna run across this. But if we did try to use a **`const`** there, we're gonna get an **`error`** because that `i++` is trying to modify the `variable` (me: try to reassign it so we get `error`). So here we would need to use a `let`.

**So closure is a preservation of the linkage to a `variable`, not the capturing of the value.**

### Module Pattern:

> **Namespace**: Taking a set of `functions` and data and putting them inside of an `object` (putting them as properties instead of `variables`), it is effectively collecting them into a **namespace**.
> Not really a syntactic feature of the language, but it's an idiom that we make **namespaces** with `objects`. And for years, people use it as the primitive data structure.

> Nothing wrong with **namespace pattern**. But it is definitely, 100%, positively **not a Module**.

> **Why namespace pattern is not a module?**
>
> The reason it's not a module is that the module pattern requires the concept of **encapsulation**. All **encapsulation** really means is, not only have to collected data and behavior (methods) together, which is the **namespace** creates, but need some idea for information **hiding**, or some control over visibility.
>
> The idea of a **module**, is that there are things that are **public** (public API), and there are things that are **private**, that's things that nobody on the outside can touch.

**So if we wanna have a module, we gotta have encapsulation and data hiding.**

> **The Classic Module Pattern (Revealing Module Pattern):**
>
> Modules **Encapsulate** data and behavior (methods) together. The state (data) of a module is held by its methods via **Closure**. In other world classic module patterns, **Encapsulates** data and it does so with **Closure** (that's key).

So we can't have a **module**, if we don't have **closure**. It's just not possible. Even the _ES6 modules_, conceptually, we need to think about them as **closure**.

```JavaScript
1.  var workshop = (function Module(teacher) {
2.      var publicAPI = { ask, };
3.      return publicAPI;
4.
5.      // ***********
6.
7.      function ask(question) {
8.          console.log(teacher, question);
9.      }
10. })("Kyle");
11.
12  workshop.ask("It's a module, right?");   // Kyle It's a module, right?

// Classic/Revealing module pattern
```

> **Singleton is an object which can only be instantiated once.** A singleton pattern creates a new instance of the class if one doesn’t exist. If an instance already exists, it returns the reference to that `object`.
>
> Technically speaking, `object literals` in JavaScript are **singletons**. Think about it! An `object` occupies a unique memory location and once it is created, there can be no other `object` like this. Every time we call the `object`, we are essentially returning a reference to that `object`. Hence, a **singleton**!

The previous example had a module **`IIFE`** (also known as a **module singleton**), but that's not the only way to make modules:

```JavaScript
1.  function WorkshopModule(teacher) {
2.      var publicAPI = { ask, };
3.      return publicAPI;
4.
5.      // ***********
6.
7.      function ask(question) {
8.          console.log(teacher, question);
9.      }
10. }
11.
12. var workshop = WorkshopModule("Kyle");
13.
14. workshop.ask("It's a module, right?");   // Kyle It's a module, right?

// Module Factory
```

We can make just regular `functions` that can be called multiple times. And every time a `function` is called, it's gonna produce a new instance of our module. We lovingly refer to those as **Factory Functions**.

This is a `WorkshopModule` **factory function**. We can call it once, like we do on line 12, but we could call it a hundred other times and have a hundred other **separate instances** that all have their own state. They're all separate and they don't mix with each other.

> That is the **module pattern** in a nutshell. The idea that we take some behavior, and data that that behavior operates on, and **encapsulate** it into a data structure, **hide** what we don't need to show, and expose only the minimal necessary API. That's a module.

### ES6 Modules & Node.js:

```JavaScript
            workshop.mjs: (file name in node)

1. var teacher = "Kyle";
2.
3. export default function ask(question) {
4.     console.log(teacher, question);
5. };

// ES6 module pattern
```

**Somethings we should know about modules:**

- Everything we write inside on module is **privet** (all `variables` and `functions`).

- To make something **public** and accessible from outside, we use the **`export`** keyword.

- Modules are **file-based**. Which means **it is impossible to have more than one ES6 module in the same file.** So for example, without a build process, if we wanted to ship all the modules to a browser, we're gonna have to load a thousand separate files with all the performance implications thereof. People that are currently doing this today are using tools where they author in ES6 modules and they compile back to the old school style module and concatenate them into a file and ship it off.

- Modules are also **singletons**. No matter how many times we import this module into an application, **it only ever runs once**. And every other time that we import it, we just get **another reference to that same instance**. So if we want to have a **factory for our modules** (where people can make multiple instances), we're gonna have to expose on our API, a **factory function** to do that.

To create a module we open up a file and we just start making `variables` and `functions`. And that file, because it's gonna be loaded as a module, is assumed that everything is **private**. We don't need a syntactic wrapper. We can conceptually think of it is being wrapped in a big `function`.
Wrapped in a scope that is by default private. The way we make something **public** is we use the `export` keyword as we see on line 3. **So anything we export is public, everything that we don't export is private.**

## ES6 Module Syntax:

There's a bunch of variations import modules, but two major styles:

```JavaScript
1. import ask from "workshop.mjs";
2.
3. ask("It's a default import, right?");   // Kyle It's a default import, right?
4.
5. import * as workshop from "workshop.mjs";
6.
7. workshop.ask("It's a namespace import, right?");   // Kyle It's a namespace import, right?

// ES6 module pattern
```

There are **two major style of import modules**:

- One is called the **named import syntax** which we see on line 1. We exported it the `default function`, so technically its name is default from the outside, and then we decided to name that default import `ask` on line 1, which means now in our top level scope of where the import happened, we now have an `identifier` called `ask`, which is reference bound to the `ask function` inside of the module. That's what we sort of referred to as the Java style of import where import means literally to import `identifiers` into your scope.

- The second style is referred to generally as the **namespace import** (as we see on line 7), which is to say we wanna get this whole module and collect **all of its contents** onto a **single namespaced `variable`**, in this case called `workshop`.

---
## delieverables 👩‍💻🥳

## ADVANCED SCOPE:

### QUESTION #1

Given the following code snippet and **explain what's happening**.

```javascript
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log("value of [i] is: ", i);
    }, 100);
}
```

The current output is: "value of [i] is: 5" five times.

The output should be: 

"value of [i] is: ", 0 "value of [i] is: ", 1 "value of [i] is: ", 2 "value of
[i] is: ", 3 "value of [i] is: ", 4

Without changing anything in the for loop's code itself, provide a solution to
fix it.

**explain what's happening** 💁‍♀️

> there's only one `i variable`. There's an `i variable` on first line and there's only one of them, and we have 5 `functions`. If we wanted to have **5 separate values**, we need **5 separate `variables`**. And there's only one, so of course it can only have the one value. And in this case, it's gonna have the value that occurs at the end of the loop, which is the value `4`.


```javascript
for (let i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log("value of [i] is: ", i);
    }, 100);
}
```
**explain what's happening** 💁‍♀️

> I use a `let` on our `for` loop will automatically create a new `i` for each iteration. Instead >of creating just one that belongs to the whole `for` loop, here there's gonna be a brand new `i` >for each iteration. Which means the closure just magically works.
>

**So closure is a preservation of the linkage to a `variable`, not the capturing of the value.**

-------------------------------------------------------------------

### QUESTION #2

Given the following code snippet and **explain what's happening**. 

```javascript

for (let i = 0; i < 5; i++) {
   let array = [];
   array.push(i);
   console.log("Current array is: ", array)
}

```

The current output is: 

"Current array is: [ 0 ]" "Current array is: [ 1 ]" "Current array is: [ 2 ]"
"Current array is: [ 3 ]" "Current array is: [ 4 ]".

The output should be: "Current array is: [0, 1, 2, 3, 4]".

**explain what's happening** 💁‍♀️
> Array is re-declared every loop iteration

Provide a solution to fix it. 

```javascript
let  array = [];
for (let i = 0; i < 5; i++) {
   array.push(i);
   console.log("Current array is: ", array)
}

```

-------------------------------------------------------------------

### QUESTION #3

Given the following code snippet and **explain what's happening**. 

```javascript

let functions = [];

for (var i = 0; i < 5; i++) {
  functions.push(() => {
    console.log("Current value of i is:", i);
  });
}

functions.forEach((func) => func());

```

The current output is: 

"Current value of i is: 5" "Current value of i is: 5" "Current value of i is: 5"
"Current value of i is: 5" "Current value of i is: 5"

The output should be: 

"Current value of i is: 0" "Current value of i is: 1" "Current value of i is: 2"
"Current value of i is: 3" "Current value of i is: 4"


**explain what's happening** 💁‍♀️

> there's only one `i variable`. There's an `i variable` on first line and there's only one of them, and we have mre than one `functions`. If we wanted to have **separate values**, And there's only one, so of course it can only have the one value. And in this case, it's gonna have the value that occurs at the end of the loop, which is the value `5`.
> var has not blockscope

> I use a `let` on our `for` loop will automatically create a new `i` for each iteration. Instead >of creating just one that belongs to the whole `for` loop, here there's gonna be a brand new `i` >for each iteration. Which means the closure just magically works.
>

**So closure is a preservation of the linkage to a `variable`, not the capturing of the value.**

Provide a solution to fix it. 

```javascript

let functions = [];

for (let i = 0; i < 5; i++) {
  functions.push(() => {
    console.log("Current value of i is:", i);
  });
}

functions.forEach((func) => func());

```

---
WE 🥇 ARE 🥇 DONE 🥳🥳🥳💁‍♀️


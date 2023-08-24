# Day 12💻
## **[Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)** 🔥🔥
## Scope
> `Scope` is where to look for things.

Here in this example we're looking for `identifiers`:

```JavaScript
x = 42;
console.log(y);
```

Here you see an `x` that's being assigned to, or a `y` that's being a value retrieved from.

> **Identifiers and Reserved Words**
>
> An `identifier` is simply a name. In JavaScript, `identifiers` are used to name `variables` and `functions` and to provide labels for certain loops in JavaScript code. A JavaScript `identifier` must begin with a `letter`, an `underscore` (`_`), or a `dollar sign` (`$`). Subsequent characters can be `letters`, `digits`, `underscores`, or `dollar signs`. (`Digits` are not allowed as the first character so that JavaScript can easily distinguish `identifiers` from `numbers`.) These are all legal `identifiers`:
>
>
>
> ```JavaScript
>   var sí = true;
>   var π = 3.14;
> ```
>
> Like any language, JavaScript reserves certain `identifiers` for use by the language itself. These `“reserved words”` cannot be used as regular `identifiers`.
>

All `variables` are in one of those two roles in our program:

1. Receiving the assignment of some `value`
2. We are retrieving a `value` from the `variable`.

When the scope is being processed by the JavaScript engine, it's essentially asking two question, when it see this `variable`:

1. What position is it in?
2. What scope does it belong to?

In other words, this is basically like a game of matching marbles to their color-coded buckets. If you think about the way a JavaScript engine processes the code, it's going to find a `variable` and it's gonna say, hmm, this is a green marble so it goes in the green bucket. And this is a red marble, so it goes into the red bucket. So it's fundamentally a game of sorting colored marbles.

But this **processing** that we're talking about is an actual step within JavaScript. It's not simply inlined with the **execution**. It's extremely common for people to think about JavaScript as running top down, line by line, executing.

> Because when we think of **interpreted programs**, or **dynamic scripted programs**, we generally think of them as executing line by line, top down.
>
> But it turned out, JavaScript is not an **interpreted language**, but is in fact actually a **compiled language**, that may not fit with our whole mental model because we're probably used to thinking of line-by-line **JavaScript interpretation**.

**A compiled language is converted into machine code so that the processor can execute it. An interpreted language is a language in which the implementations execute instructions directly without earlier compiling a program into machine language. The compiled programs run faster than interpreted programs.**

> **Compiled Languages:**
>
> Compiled languages are converted directly into machine code that the processor can execute. As a result, they tend to be faster and more efficient to execute than interpreted languages. They also give the developer more control over hardware aspects, like memory management and CPU usage.
>
> Compiled languages need a “build” step - they need to be manually compiled first. You need to “rebuild” the program every time you need to make a change. In our hummus example, the entire translation is written before it gets to you. If the original author decided he wanted to use a different kind of olive oil, the entire recipe would need to be translated again and then sent to you.
>
> Examples of pure compiled languages are C, C++, Erlang, Haskell, Rust, and Go.
>
> **Interpreted Languages:**
>
> Interpreters will run through a program line by line and execute each command. Now, if the author decided he wanted to use a different kind of olive oil, he could scratch the old one out and add the new one. Your translator friend can then convey that change to you as it happens.
>
> Interpreted languages were once known to be significantly slower than compiled languages. But, with the development of just-in-time compilation, that gap is shrinking.
>
> So the JavaScript is, in fact, **compiled**, or at least, as we would say, it's **parsed**.
>
> There's some **processing step** that has to happen before **execution** has occurred.

So let me prove to you, if you have ever written a JavaScript, syntax error, left off a comma, had an extra parenthesis, or curly brace somewhere, and then you try to run the program, and you immediately got a syntax error.

That is, say you have a syntax error on line 10, but you immediately get that error reported to you before lines 1 through 9 have executed.

The question is: How is it possible that JavaScript knew about the syntax error on line 10 before executing lines 1 through 9, unless JavaScript actually went through a **processing step** first. As opposed to simply **executing** top down, there was some **processing step**.

What does that **processing step** look like?

**In compiler theory, there are essentially four stages to a compiler:**

(Sometimes the first two are combined into one stage, sometimes they're separate.)

1. There's **lexing** and **tokenization**.
2. There's **parsing** (which turns the stream of **tokens** into what's called an **abstract syntax tree**).
3. The last step is what's called **code generation** (taking an **abstract syntax tree** and producing some kind of other **executable** form of that program).

This is how our program gets processed from its **textual code** and our **source format** into some kind of representation that can be executed.

Now, a lot of people think, well, JavaScript can't be **compiled** because I don't run a **compiler** on my development machine and then ship off the `compiled code` to some other location.

So in other words, a lot of people think about this difference between **interpreted** and **compiled** as the distribution model for the binary. But that's not really the right axis to be thinking about. The right axis is, is the code processed before it is executed or not? We do have languages that exist which generally don't get **processing** before **execution**. for example, `Bash script`.

But in JavaScript, if you have a syntax error on line 10 nothing happens on lines 1 through 9. It has to be processed to check that it's a well-formed, correctly formed, program.

> We have to think about JavaScript as a two-pass system rather than a single-pass.
>
> We are gonna process (**compilation** or **parsing**) the code first, and set up the scopes, and then we are gonna execute it.

> JavaScript organizes **scopes** with **`functions`** and **blocks** (ES6).

So we have **functions** and you have **blocks**, those are the units of **scope**.

## Compilation & Scope

In this exercise we try to think more like JavaScript engine:

```JavaScript
1.  var teacher = "Kyle";         // Red
2.
3.  function otherClass() {       // Red
4.    var teacher = "Suzy";       // Green
5.    console.log("Welcome!");
6.  }
7.
8.  function ask() {              // Blue
9.    var question = "Why?";      // Blue
10.   console.log(question);      // Blue (question is blue)
11. }
12.
13. otherClass();                 // Welcome!
14. ask();                        // Why?

// scope
```

After we've set up all those plans
(**compilation** step which we have two actors on it, the **compiler** and **scope manager** ), then we'll come back and execute the code.

There's going to be two actors, two entities that are going to be talking. One is the **compiler**, the thing that's **processing** the JavaScript program.
The other one is the **scope manager**, that makes buckets, makes marbles, drops the marbles in. It's the **compiler** who says, hey, I have this thing, and it's the **scope manager** who says, I'm gonna make a plan for that, I'm gonna make a plan for a bucket and make a plan for a marble.

**Remember, in our **processing phase** (**compilation phase**), we have a **scope manager** and we have a **compiler**.**

> It (the `variable`) hadn't actually been created, that they don't get created for real until **execution**, but conceptually we're creating this plan from what we see in the program.
>
> Actually what we're (the **compiler**) doing is looking for these formal declarations.

> When the **compiler** realize a `function`, it knows `function` makes scopes (buckets). So when it sees a `function` create both marble and bucket.

> Having two `variables` with the same name at different scopes, that has a term, it's called **shadowing**.
>
> Because we have two `variables` with the same name there's no possible way that we can reference **lexically** the `variable` from out side a inner scope. It just limit us from what we can access. Because those `names`, it would match the nearest one (`identifier`).

 why did we skip over console.log in line 5?🤔❓

We didn't skip over it from the perspective of **compilation**. The **compiler** would have certainly handled line 5 and done a bunch of **compilation**. It doesn't have any impact on our scopes. So we've narrowed our focus of **compiler** theory to preparing our `identifiers` and our scopes. Doing our marble bucket sorting thing. So we're just skipping over the uninteresting details at this point. Since line 5 doesn't create or access any `variables` within our scopes, we don't need to worry about it.

> (the stage before **executing**), the **compiler** preparing our `identifiers` and our scopes.
>
>  we're just skipping over the uninteresting details at this point. Since it doesn't create or access any `variables` within our scopes, we don't need to worry about it.


> In the **compiler phase** we create a plan for all the scopes that exist and where all the `identifiers` fit into all of those scopes. Including references `identifiers`.
>
> That is then handed over as part of the **execution** plan so that the **virtual machine** (the JavaScript engine), can run this code.
>
> And when we execute the code, there's no more declarations for anything, because we figured that stuff out at **compile-time**.

**It is very important to know:**

> In a **lexically scoped language** (like JavaScript), all of the scopes (**lexical scopes**) and `identifiers`, that's all determined at **compile-time**. It's not determined at **run-time**. It is used at **run-time**, but it is determined at **compile-time**.

## Executing Code

We have all our plan set up. There's no more declaration code, so let's then execute this code:

```JavaScript
1.  var teacher = "Kyle";
2.
3.  function otherClass() {
4.    var teacher = "Suzy";
5.    console.log("Welcome!");
6.  }
7.
8.  function ask() {
9.    var question = "Why?";
10.   console.log(question);
11. }
12.
13. otherClass();                 // Welcome!
14. ask();                        // Why?

// scope
```

> So even though line 1 looks like one statement, it's actually two separate things. There's the `var teacher` part. That's what the **compiler** handles. And then there's the `teacher = "Kyle"` part, that's what the **execution engine's** gonna handle.

Now, remember there's only two roles that a `variable` can play. It can either be the **target** of an assignment, and we can see on line 1, the `teacher` is in that role, it is receiving an assignment, it's the **target**. The only other role that it can play is in the **source position**.
It's going to give up its `value`. We're going to **retrieve** the `value` from it. That's like what we see on line 10, `question` is in that position.

We used to refer to this  as a **left hand side**, an **LHS** and a **RHS**, a **right hand side**. As in left and right hand of an equals. Nowadays, you might call it an **L value**, an **R value**. Maybe just for simple purposes, let's call them **source** and **target**.

All `variables` can play two roles in our program:

1. Be the **target** of an assignment (receiving an assignment of `value`, or in an old school terminology: **left hand side** (**LHS**), as in left hand of an equals)
2. Be in the **source position** (retrieving the `value` from it, or in an old school terminology: **right hand side** (**RHS**), as in right hand of an equals).

**let's call position of `variables` simply source position and target position.**

Here on line 1, `teacher`'s in a **target position**. On line 10, `question`, is in a **source position**. That's a piece of information that the **compiler** picked up. Whenever it created that whole `abstract tree` and all that, it knew that each `identifier`, each marble, not only what color it was, but what position it was in.

> The **compiler** in **compile-time** (**processing** or **compilation** or **parsing phase**), whenever it created that whole **abstract tree** (**abstract syntax tree**), it knew that each `identifier` (each marble) not only what color it was (not only that it exist), but what position it was in.

It's critical to know that we're dealing with something that's receiving a `value`, it's a **target**, or we're gonna **retrieve** it's `value`.

So let's then execute this code the way the JavaScript engine would, with all that **execution** plan and scope stuff set up.
Each time we enter a scope, all of the plans for the buckets and the marbles will have been created, and so now we're ready to go ahead and execute.

> In **execution phase** we have two people talking, **scope manager**, cuz it's gotta hand out the `identifier` (marbles), and the **virtual machine** (it's the JavaScript engine that's executing code).

> In **run-time** (when we executing our code) if there were `identifiers`, we assign the `values` to `variables` (if they were in `receiving position` or **target**), or `retrieving` the `values` from it (if they were in **source position**).
>
> And also in **run-time** the `variables`, does not have a `var` on them anymore.
>
> That `identifier`, represents an area in memory that needs to get assignment of `value` (So, we're gonna take the `value` from the right hand side, and assign it to that location represented by that `identifier`).

Line 3 through 6, and line 8 through 11, those were declarations, they're not there anymore. They've been **compiled** away. So, execution would move to line 13. Let's talk about how line 13 `executes`.

> In **compile-time**, the **compiler** declared all `identifiers` in line 3 through 6, and line 8 through 11, so in **run-time** (**execution phase**) we move to line 13.

Don't skip just to how the `function` runs inside. We first have to ask how the line 13 itself `executes`. Cuz JavaScript has gotta figure out that and execute it.

> The `otherClass identifier` (what we see in `function` call line 13), is in **source position**.
> We're not assigning something to `otherClass`. So if we're not assigning to it, we are pulling a `value` out. We wanna know what is currently in the `identifier otherClass`. Because, in just a moment, we're about to turn the `executor`. So we need to go get it.


> When we see an `identifier` for a `function` in **run-time**, the `value`
> of that `identifier` is the `function`, that `identifier` was declared to point at.
>
> At **compile-time**, the `identifier`, was associated with that `function`. That reference to that `value` is there.
>
> In the **run-time** the `identifier` that was declared to poit at `function` (`otherClass()`) with those parentheses `()`, they execute the thing that we just pulled out of that `variable`.
> And if we pulled out of that `variable` something that wasn't a `function`, like, `null`, or `undefined`, we get an error called a `TypeError`, because we would have a `value` like `null`, or `undefined`, but that is not a `value` that is legal to execute as a `function`.
>
> So we're doing something illegal with that `type`, that's call the `TypeError`, a **run-time** error, where we're doing something with a `value` that's not allowed for that `type`.

> The `console.log` is an `identifier` (and it's in **source position**) that we didn't created, but it is an `identifier`. The JavaScript engine has that available to us as sort of like an `auto global` (it's already in `global scope`). And when it find it (in `global scope`), and look at the `value` of it, it's an `object`, it has a `method` call `log`, so it can `invoke` it.
>
> If JavaScript engine look up for `identifier`, first asks for it in current scope if it wasn't there, it goes up one level until it gets to `global scope`, that's call the **lexical scope**.

> When we reference a `variable` in a **source position**, we have to first look it up, and when you reference a `variable` in a **target position**, we also have to first look it up.
>
> So there is a look up process involved.

---

There is a very important takeaway that we should have:

> We discover the **source** versus **target** position at **compile-time**, but we don't use that information until **run-time**.
>
> Basically think of it like a plan (map), it's like a to do list for every scope, that's the **executable code** (what **compiler** outputs). And then when it runs is when it all actually comes into existence.
>
> Every time we execute a `function`, the environment is recreated from scratch.
>
> So the **compiler** output is not actually reserved **memory**, it's the plan for how to reserve **memory** and make `identifier` (marbles) and all that. And then every time we execute that plan is effected into **memory**.
>
>
> | ARGUMENT                                                                                                          | PARAMETER                                                                                                      |
> | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
> | When a `function` is called, the `values` that are passed in the call are called `arguments`.                     | The `values` which are written at the time of the `function` `prototype` and the definition of the `function`. |
> | These are used in `function` call statement to send `value` from the calling `function` to the called `function`. | These are used in `function` header of the called `function` to receive the `value` from the `arguments`.      |
> | During the time of call each `argument` is always assigned to the `parameter` in the `function` definition.       | `Parameters` are local `variables` which are assigned `value` of the `arguments` when the `function` is called |
> | They are also called `Actual Parameters`                                                                          | They are also called `Formal Parameters`                                                                       |
>
And in the end, it becomes something like this:

![Scope](https://user-images.githubusercontent.com/37678729/72377060-50abad00-3724-11ea-9d5c-408ee5c5cd76.png)

---

### Dynamic Global Variables:

Another example with corner cases:

```JavaScript
1.  var teacher = "Kyle";
2.
3.  function otherClass() {
4.    teacher = "Suzy";
5.    topic = "React";
6.    console.log("Welcome!");
7.  }
8.
9.  otherClass();                    // Welcome!
10.
11. teacher;                         // "Suzy"
12. topic;                           // "React"

// Scope
```

First Step: **compilation**

> In **compilation stage** we looking for formal declarations and create `identifiers` for them, but in **execution stage** we see that `identifiers` is in **source position** or **target position**.

> We will heard of `teacher` in **execution**. but in **compilation stage** we'd never heard of it.
👁️
> If in **compilation stage** there is `identifier`, but without formal declaration (such as `var` or `function`), the **scope manager** didn't create `identifier` for it.
>
> But in **execution stage** the JavaScript engine, will go up one level until it gets to `global scope` and if it didn't find it there too, it will `auto global`🖐️ it, which means it will create that `identifier` in `global scope`.

Second Step: **execution**

🦜 So we remember, there's no formal declarations but there are executable statements. Line 1 has an executable statement. And so the JavaScript engine says, hey, `global scope`, I have a **target reference** for `teacher`, ever heard of it? Yes, here's your red marble. So we take the `value` `"Kyle"`, we assign it into the red marble (`teacher`), and we are complete.

Now remember, `functions` are declarations, they don't really exist. At least, they're only here symbolically. So we're going to move from the `function` to the next execution line of code, which would be line 9.

> In **execution stage**, because `functions` and other kind of formal declarations aren't exist (they're only there symbolically), the JavaScript engine skip them.

![Scope and Corner Cases](https://user-images.githubusercontent.com/37678729/72376864-f3176080-3723-11ea-8057-f7f63011b6fc.png)

> If we try to assign to a `variable` that's never been formally declared (on that scope). Once we go up one level and arrive at the `global scope`, if there wasn't `variable` with that `identifier`, the `global scope`'s gonna created it for us (in a **run-time** or **execution phase**), we call this idea `auto global`.
>
> Even when we wrote that `identifier` in the first place inside another scope than `global scope`, because the `global scope` created and gives us that `variable`, it is a `global scope` variable (`red marble`).
>
> And we should keep it in mind creating a declaration at **compile-time** and creating it dynamically during the **run-time**, have differences. There are performance differences and other sorts of things but mechanically they are two `global variables` at this point.
>
> ⚠️ Never ever under any circumstances did you intentionally `auto-create global`'s like that. Always declare the `variables` that we want to use declare them in whatever scope we need them in, but don't `auto-create` them.
>
> But we should keep it in mind, if we have `non-declared variable` without assigning to some `value`, we still get `ReferenceError` when we execute the code.

🦜 So we've created an `auto global` called `topic` which that sounds terrible. But now there's a `global variable` called `topic` and when we get that red marble back and make the assignment on line 5, there's a `global variable` now with the value `"React"` in it.

🤔🤔🤔  ❓
**Q:** Do the `auto global` would occur also if `topic = "react"` were in the `global scope` under `variable` of `teacher` (for example it was in line 2)?

**A:** That's true, any assignment to a `variable` that is undeclared at that moment, not declared to any scope we have access to. Any undeclared variable is going to end up creating this `auto global`.

**Now, the reason why that happens is because we'll notice that this program is not running in `strict-mode`. But this is running in the `non-strict-mode` or sometimes called, `sloppy-mode`. We should be using `strict-mode`, and if we were using `strict-mode`, we wouldn't see this behavior. But since this code snip it isn't, that's what happens, as we end up creating a `global variable` called `topic`.**

> If we use `strict-mode` instead of using `non-strict-mode` (or sometimes called `sloppy-mode`), we wouldn't see this `auto-create global`.

We execute `console.log` the same way as we have before. So execution is then done in the `function`. Execution moves to line 11. So hey `global scope` (red bucket), I have a **source reference** to a `variable` called `teacher`, ever heard of it? Yes, so we go get that marble and we look for its `value`. And the `value` is `"Suzy"`. Because of line 4, we've overwritten the `value` in that `variable`. It's not a separate `variable` (marble).

So line 12 then, hey `global scope`, I have a **source reference** for `topic`, ever heard of `topic`? Yes, here's your red marble. and the value of that red marble is `"React"`.

🤔🤔🤔❓
**Q:** If line 11 was actually in line 8, `teacher` would still be `"Kyle"`?

**A:** Yes, it's correct.

**Q:** What would happen if line 12 was on line 8?

**A:** We will get `ReferenceError`. There would be no `identifier`. But because there is an `identifier` on line 12 the `function otherClass` auto created it by assigning to a `non-declared variable`.

### Strict Mode:

```JavaScript
1.  "use strict";
2.
3.  var teacher = "Kyle";
4.
5.  function otherClass() {
6.    teacher = "Suzy";
7.    topic = "React";           // ReferenceError
8.    console.log("Welcome!"):
9.  }
10.
11. otherClass();

// Scope
```

So now if we flip on `strict-mode`, which we do by putting this `strict-mode` fragment at the top of any scope, preferably at the top of our program, the top of our file, or at the top of any `function`.

If we turn on `strict-mode`, all the same processing is going to happen. But when we arrive at line 7 and we say, hey scope of `otherClass`, I have this **target reference**.

> Whenever we are in `non-strict-mode` (or `sloppy-mode`), and we have a **target reference** for a `non-declared variable`, we will `auto create` it (`auto global`) in **run-time**.
>
> And if in `non-strict-mode`, we try to get `non-declared variable` that is in a **source position**, `global scope` throw us a `ReferenceError`.

> If we have any kind of reference (**target** or **source**) for `non-declared variable` in **`strict-mode`**, `global scope` throw us a `ReferenceError` (instead of `auto create` it, if `non-declared variable` was in **target position**).

That's what we would like to happen all of the time. It now happens as the result of `strict-mode`, we get a `ReferenceError`. So one of the many, many reasons why it would be good for us to be using `strict-mode`. It will avoid mistakes like line 7, cuz it almost certainly a mistake, it should not be something we intentionally try to create `global`.

> The difference between `TypeErrors` and `ReferenceErrors` are , `TypeErrors` are when we found the `variable` and the `value` that it is currently holding, is not legal to do whatever we're trying to do with it. Like trying to execute or access a `property` on an `undefined` or `null`, things like that, that's `TypeError`.
> A `ReferenceError` is, when JavaScript engine couldn't find that `variable` on any scope that we have access to.

🤔🤔🤔❓❓
**Q:** Is `strict-mode` always pretty on `ES6`?

**A:** The `strict-mode` is not always on. It's true that tools like `babel` and other transpilers basically always put the `strict-mode` in there for us.
So if we're using transpired code, it was almost a virtual certainty that our code is running in `strict-mode`. But JavaScript is not default the `strict-mode` because then that would break a bunch of programs. So that were written 20 years ago or something. So because of backwards compatible, we will always have to opt into `strict-mode`.
Another little caveat inside of certain kinds of mechanisms within `ES6` and going forward, it is assumed to be in `strict-mode`. So we don't even type it, so inside of a `class`, or inside of `ES6 module`, inside of both of those, `strict-mode` is assumed, we don't even have to put the `strict-mode`, is just assume that, that code is running in `strict-mode`. But as a general rule for JavaScript itself, it's not in `strict-mode` unless we opt-in.

> In the `babel` and other transpilers, basically always put the `strict-mode` in there for us.
>
> By default `ES6 class` and `ES6 module` are executed in the `strict-mode`.

So in `stric mode`, we can't auto create `variables`, you have to declare them.

### Nested Scope:

This is an example of a nested scope:

```JavaScript
1.  var teacher = "Kyle";
2.
3.  function otherClass() {
4.    var teacher = "Suzy";
5.
6.    function ask(question) {
7.      console.log(teacher, question);
8.    }
9.
10.   ask("Why?");
11. }
12.
13. otherClass();                   // Suzy Why?
14. ask("???");                     // ReferenceError

// Scope
```

We start by looking at line 1, that's a formal declaration that makes a red marble. Line 3 is a formal declaration that also creates a red marble. Line 4 and 6 both are the formal declaration that create a blue marble.

And now, we are inside of `ask`, in line 7, there is no marbles, but there are reference to marbles. So on line 7 when we reference `teacher`, it's a blue marble. And the `question` in line 7, is a green marble. Because the `question` is a `variable` inside of the scope of the `function ask`.

> The `function declarations` make their `identifier` in their enclosing scope.

> We shoud know the `parameters` are `variables` inside of the scope of that `function`.
>
> Even though it doesn't have a `var` there, a `parameter` is formally creating an `identifier` in that scope.

> Whenever our `function` have `arguments`, the `values` of that `arguments` will be assigned to the `parameters` of that `function` first, and then the `function` itself will be executed.

What's gonna happen with line 14? How does line 14 execute?
Hey `global scope`, I have a **source reference** for an `identifier` called `ask`, ever heard of it? No, so we have a `ReferenceError`.🖐️

Even though `ask` exist within the program, it doesn't exist in any scope that we have access to at this moment. So it is therefore an `undeclared variable`. Because we're not in `strict-mode`, unlike `auto globals` which go ahead and create a marble for us, if we have a **source referenced** to a `variable` that is `undeclared`, it always throws a `ReferenceError`. That's why it's critical to understand the difference between a **target reference** and a **source reference**. At least if you're in `non-strict-mode`.
Once you go to `strict-mode`, they both behave exactly the same, so it stops mattering as much **target** versus **reference**.

> If in `non-strict-mode`, we have a **source referenced** to a `variable` that is `undeclared` (it doesn't exist in any scope that we have access to at that moment), it always throws a `ReferenceError`. And if the `variable` is in the **target reference**, the `global scope` will be auto created it (`auto global`).
>
> But in `strict-mode`, it doesn't matter `undeclared variable` is in the **source position** or the **target position**, the JavaScript engine will always throw us a `Reference Error`.

🤔🤔🤔❓❓
**Q:** When we're passing the `"Why?"` to `ask` on line 10, is there behind the scenes, is JavaScript saying `var question = "Why?"` at some point?

**A:** Sort of, I think conceptually it works to think about `arguments` being assigned to `parameters`. It's not technically that, but it's close enough that it works for this particular narrative exercise.

![Nested Scope](https://user-images.githubusercontent.com/37678729/72377177-818be200-3724-11ea-96ed-bc31666bec80.png)

---

### Undefined vs Undeclared:

What is the difference between `undefined` and `undeclared`?

**Undefined:** means a `variable` exists but at the moment it has no `value`. It may have never had a `value` or it might have used to have a `value` and it doesn't anymore but there is no other `value` and the vacuum of space it is `undefined`.

**Undeclared:** is actually never formally declared in any scope that we have accessed to (we do not have a marble for it). And in `strict-mode`, it always results in those `ReferenceErrors`.

---

## Scope & Function Expressions:

### Function Expressions:

We've been talking about `functions` in the **compilation phase**, adding their `identifier` (as a colored marble) in the enclosing scope.

```JavaScript
1. function teacher() { /* .. */ }
2.
3. var myTeacher = function anotherTeacher() {
4.    console.log(anotherTeacher);
5. };
6.
7. console.log(teacher);
8. console.log(myTeacher);
9. console.log(anotherTeacher);                   //ReferenceError

// Scope: which scope?
```

In this example `teacher` in line 1 (`function declaration`), creates a red marble but `anotherTeacher` in line 3 (`function expression`) creates a blue marble.

In line 3 `identifier` called `myTeacher` creates red marble. We do know that there's a `function` called `anotherTeacher` there, so we need to create a bucket for it at least. We need to make a blue bucket. But because that `function` is not a `declaration`, we're not gonna handle its marble color in the same way. The key difference here is that the `anotherTeacher identifier` (line 3), is going to end up as a marble at **compile-time** but it's gonna be a different colored marble than we expect. It's not a red marble, it's a blue marble. So the blue scope is where the blue marble `anotherTeacher` ends up.

> One if the key differences between `function declarations` and `function expressions`, is that `function declarations` add their name or `identifier` (they attach their marble), to the enclosing scope, whereas `function expressions` will add their name (marble) to their own scope.
>
> Another difference is `function declarations` are hoisted but `function expressions` did not hoisted.

That's why on line 4, we can reference in `anotherTeacher` because there is in fact a blue marble called `anotherTeacher`. But down on line 9, there is no `anotherTeacher`. so when we're out in the `global scope` and we asked `global scope` you ever heard of this red marble, it's gonna say nope, never heard of that red marble and what we're gonna get there, `ReferenceError`.

> So key difference, `function expressions`, put there `identifiers` into their own scope.
>
> There's a little, also, additional nuance which is not only does that blue marble show up in the blue scope but it's also read only.
> You cannot reassign `anotherTeacher` on line 4, to some other `value`.

### Named Function Expressions:

What is a named `function expression`? That means a `function expression` that's been given a name.

```JavaScript
1. var clickHandler = function() {
2.    // ...
3. };
4.
5. var keyHandler = function keyHandler() {
6.    // ...
7. };

// Named Function Expressions
```

Why line 1 is a `function expression`?
Because it's not a `function declaration`.

> How do we know someting is a `function declaration`?
>
> If the word `"function"` is literally the first thing in the statement.
> So if it's not the first thing in the statement, if there's a `variable` or an operator or parentheses or anything, then it's not a `declaration`, it is an `expression`.

So on line 1, we see a `function expression`, but we see no name. So that's called a `anonymous function expression`, whereas the one on line 5 is a `named function expression`.

> We should always, 100%, zero exception, prefer the `named function expression`, over the `anonymous function expression`.

**Why we sould always, always use `named function expressions`?**

- Reliable `function` self-reference (the name produces or creates a reliable self-reference to the `function` from inside of itself). That is useful if we're going to make the `function` recursive, or that `function` is an event handler of some sort and it needs to reference itself to unbind itself. or it's useful if we need to access any properties on that `function object` such as its `length` or its name or other thing of that sort. Anytime we might need a self-reference to the `function`, the single only right answer to that question is, it needs to have a name.
- More debuggable stack traces. So automatically by naming our functions, we make our code and stack traces more debuggable.
- More self-documenting code. If we have a `function` that is anonymous, and we look at that `function` to figure out what that `anonymous function` is doing, we have to read the `function` body and we also probably have to read where it's being parsed.

🤔🤔🤔❓❓
**Q:** Which one of those two would be the better self-reference?

**A:** The first one, the one that we own and that is read only is a more reliable self-reference. So if there's any possible chance remotely that you're gonna need a self-reference, it's best to go ahead and name it.
Even if you don't need it now, you might need it in the future, it's best to go ahead and name it.

**Q:** When we just name the `function expression` the same thing that we will name the `variable` of the scope above, is that a case of **shadowing**?

**A:** Yes, it is a case of **shadowing**.

**Q:** What happens if we assign an `anonymous function` to property, or to a `variable` or something, what happens to the name?

**A:** Well, it's still an `anonymous function`, it still doesn't have a **lexical self-reference** to itself. Could we reference the `variable` in the outer scope? Of course we can, but it's a little less reliable, a little less trustable, and a little less semantic.

> Every `function` that exists in our program, every single `function` has a purpose. And if every `function` has a purpose, it means every `function` has a name.
>
> If we can not come up with a name for the `function`, it probably means that we don't understand that `function` yet. It probably means, that `function` is too complex (means this `function` is doing too much), and needs to be broken down into smaller pieces until such a time as those names are completely self obvious, and then put them there.

> The `arrow functions` are `anonymous`.
>
> So Kyle Simpson think we shouldn't use `anonymous function expressions`. And because `arrow functionds` don't have name, the only way that we can figure out what that `arrow function` is doing, is to read it's `function` body. But the name of the `funciton` can tell us the purpose of that `function`.

We can put lots of more information in there that semantically tells the reader of our code what its purpose is, that would not be obvious in the code (names like getPersonId or defaultPersonId).

So don't use `arrow functions` for this purpose. Later we'll see the one and only one exception that we have to the `arrow functions` rule, which is their **lexical** this behavior. But Kyle Simpson does not endorse or recommend or suggest using them as a general replacement for any `function`.

> `(Named) Function Declaration` > `Named Function Expression` > `Anonymous Function Expression`
>
> So the `function declaration` has some benefits over the `named function expression`. But then `named function expressions` have huge benefits over the `anonymous function expressions`.
>
>
🥳🥳


---
## delieverables 👩‍💻🥳

 ### QUESTION #1
 
>Create a function called arrowHOF that takes an arrow function as input and returns a new arrow function that enhances the behavior of the input function.
>
>The enhanced function should accept additional arguments and execute the input function multiple times based on these arguments.

```javascript
const exampleNormalFunc1 = (a, b, c) => {
  return a * (b + c);
};

const exampleNormalFunc2 = (x, y) => {
  return x * y;
};

const exampleNormalFunc3 = (string) => {
  return string + " " + string + " " + string + "!";
};

const arrowHOF = (normalFunc) => {
  //   // write your code here;
  const enhanced = (...param) => {
    const repeatFunction = (time = 1) => {
      if (time === 1) {
        return normalFunc(...param);
      }
      return normalFunc(...param) + "" + repeatFunction(time - 1);
    };

    return repeatFunction;
  };
  return enhanced;
};

const hofNormalFunc1 = arrowHOF(exampleNormalFunc1);
const hofNormalFunc2 = arrowHOF(exampleNormalFunc2);
const hofNormalFunc3 = arrowHOF(exampleNormalFunc3);

console.log(hofNormalFunc1(3, 4, 5)(2)); // logs 27 twice
console.log(hofNormalFunc2(20, 35)(4)); // logs 700 four times
console.log(hofNormalFunc3("Meow")()); // logs "Meow Meow Meow!" once
```
---

### QUESTION #2

>Build a function called preserveThis that takes a function as input and returns a new arrow >function that behaves the same way as the input function but preserves the original this context >when used as a method of an object.

```javascript
// // Example object
const obj = {
  name: "John",
  greet: function (greeting) {
    console.log(`${greeting}, ${this.name}!`);
  },
};

const preserveThis = (func) => {
  // write your code here;
  const preserveContext = () => {
    return func.bind(obj);
  };
  //console.log(JSON.stringify())
  return preserveContext();
};

// // Wrap the greet function using preserveThis
const preservedGreet = preserveThis(obj.greet);
console.log(preservedGreet);
// Call the wrapped function as a method of the object
preservedGreet("Hello"); // Output: "Hello, John!"
```

---

###  QUESTION #3
 
>Consider the 2 following examples and distinguish the different output in each one with them >with a reasoning.

```javascript
// Example 1:

function outer1() {
  var x = 10;

  var inner1 = function () {
    console.log(x);
  };

  inner1();
}

// outer1(); // Output: 10
// Reasoning for example 1's output: Here inner X has Glopal scope since it not declear
// .................................................................................

// Example 2:

function outer2() {
  var x = 10;

  var inner2 = function () {
    var x = 20;
    console.log(x);
  };

  inner2();
}

// outer2(); // Output: 20
// Reasoning for example 2's output: inner x has function scope
/* Having two variables with the same name at different scopes, that has a term, it's called shadowing.
Because we have two variables(X) with the same name there's no possible way that we can reference lexically 
the variable from out side a inner scope. It just limit us from what we can access. Because those names, it would match the nearest one (identifier).*/
// .................................................................................
```

---
WE 🥇 ARE 🥇 DONE 🥳🥳🥳💁‍♀️


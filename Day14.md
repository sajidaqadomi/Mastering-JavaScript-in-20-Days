# Day 14💻
## **[Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)** 🔥🔥
# Object

### Objects Overview:

The **objects oriented system** is one of the important of three pillars of the language. The `objects`, the `this` keyword and the `prototypes`, those make up the **objects oriented system**.

**Objects (Oriented)**

- `this`
- `class {}`
- Prototypes
- "Inheritance" vs. "Behavior Delegation" (OO vs. OLOO)

We're deliberately saying **objects oriented** instead of **object oriented**, because this is **not** strictly a **class system**, there is classes that have been layered on top of it, but it is not **inherently a class system**.

## The `this` keyword:

The first step that needs to take for understanding `this` keyword, is to stop trying to make it like `this` keyword in other languages. Because maybe some other languages behavior holds us back, and make it so harder for us to understand or leverage JavaScript.

Well it turns out that `this` keyword is actually a bit more straightforward and powerful than we would imagine. It's just been explained and taught incorrectly.

> A `function`'s `this` references the **execution context** for that call (a context in which that call was being made), determined entirely by <u>how the `function` was called.</u>

**In other words, if we look at a `function` that has `this` keyword in it, it is assigned based upon how the `function` is called.**

Most people think that we could look at a `function`, and figure out what `this` keyword is gonna point out. But **the definition of the `function` doesn't matter at all**, to determining the `this` keyword. **The only thing that matters is how does that function get invoked.**

> A `this`-aware `function` can thus have a different context each time it's called, which makes it more flexible & reusable.

**So in other words, the `this` keyword is JavaScript's version of <u>dynamic scope</u>. If it's this way of having as flexible, reusable behavior.**

If we recall and remember that we had a `function` that was in a dynamically scoped language:

```JavaScript
1.  var teacher = "Kyle";
2.
3.  function ask(question) {
4.      console.log(teacher, question);
5.  }
6.
7.  function otherClass() {
8.      var teacher = "Suzy";
9.
10.     ask("Why?");
11. }
12.
13. otherClass();   // Output in Dynamically Scoped language: Suzy Why?

// Recall: dynamic scope
```

So here with **dynamically scoped language**, on line 4, when it references `teacher`, instead of trying to line 1 to get `teacher`, it goes to line 8.
Because `ask` was called from line 10 it was called from the `otherClass` scope, that's what dynamic scope does.

**In JavaScript we have something very similar (to dynamically scoped language), but it's not based upon scope boundaries, or where something's called from, it's based on <u>how the `function` was called.</u>**

So here we have a version of the `ask function` which is `this`-aware (it uses a `this` keyword, so it's `this`-aware):

```JavaScript
function ask(question) {
    console.log(this.teacher, question);
}

function otherClass() {
    var myContext = {
        teacher: "Suzy"
    };
    ask.call(myContext, "Why?");    // Suzy Why?
}

otherClass();

// Dynamic Context ~= JS's Dynamic Scope
```

We'll notice that we're calling `ask function` from some other location but (with `this` keyword) that doesn't matter where we call it from, it's how we call it.

If we use `ask.call` here, we're saying use this particular `object` as your `this` keyword, and invoke the `function` in that context. So the `this` keyword in this particular case, will end up pointing at `myContext`.

So we can see that sort of **dynamic flexibility** happening here. So we could call that same `ask function`, lots of different ways, and provide lots of different context `objects` for the `this` keyword point on, **that's the dynamic flexible reusability of the `this` keyword**. That's why it exists by the way, it exists so that we can invoke `functions` in these different contexts.

**In JavaScript there are 4 different ways to invoke a `function`, and each one of them is gonna answer the question, what is the `this` keyword, differently.**

In **lexical scope** land, we start at the current scope, and work our way up to the global scope. Well here (with `this` keyword) we are gonna have a different building involved. **We're gonna to start at the bottom of a building. But the real question is, which building?**

## Implicit & Explicit Binding:

So let's look at those four different ways to invoke a `function`.

### 1. Implicit binding:

The first of them we'll look at is called **implicit binding**.

In this example we called `workshop object` the **namespace pattern** and we're gonna ask how does the `this` keyword behave in that namespace pattern?

![implicit binding](https://user-images.githubusercontent.com/37678729/74843783-ab4ab100-5341-11ea-829f-2570391b1063.png)

When we get the `ask question` invoked, how does it figure out what the `this` keyword should point at? And the answer is **because of the call site**.

Because of the call site, the `this` keyword is gonna end up pointing at the `object` that is used to invoke it, which in this case on line 8 is the `workshop object`. The `workshop.ask` says invoke `ask` with the `this` keyword pointing at `workshop`. That's what the **implicit binding** rule says.

That's exactly how the `this` binding works in other languages. It decides (the `this` keyword inside) the `method` based upon what `object` we call it from.

Here we're defining just one `ask function`, but we're sharing the `ask function` across two different `objects`:

```JavaScript
1.  function ask(question) {
2.      console.log(this.teacher, question);
3.  }
4.
5.  var workshop1 = {
6.      teacher: "Kyle",
7.      ask: ask
8.  };
9.
10. var workshop2 = {
11.     teacher: "Suzy",
12.     ask: ask
13. };
14.
15. workshop1.ask("How do I share a method?");
16. // Kyle How do I share a method?
17.
18. workshop2.ask("How do I share a method?");
19. // Suzy How do I share a method?

// this: dynamic binding -> sharing
```

> The idea of having **implicit binding** is useful because this is how we share behavior among different contexts.

The `workshop1` and `workshop2` are two separate `objects` with two separate pieces of data in them. But because on line 7 and line 12 we have a reference to the `ask function` on it. When we use that reference to invoke the `ask function`, the **implicit binding** rule says invoke that one `function` in a different context each time. One `function` used in lots of different contexts.

> If we think back to how we described the idea of **lexical scope**, which was a very **fixed**, **predictable** thing. It's defined at **author-time**, and nothing about the run-time can ever change that.
>
> And here with **`this` keyword**, we have something which is **not fixed and predictable**, it's entirely **dynamic**, it's entirely determined at **run-time**. And the trade off here is not accidental, the trade off here is very intentional, that what we really are getting is we're getting the choice between **predictable** and **flexible**.

Here we benefit from the flexibility of being able to share one `function` across different contexts. But there are times when that flexibility is a downside and what we would prefer is to have predictability. It's not that one is right and the other's wrong, it's just that these are different tools and they have different benefits. Here we're seeing the flexibility benefit of the `this` keyword.

But **implicit binding** is only one of the four ways to invoke a `function`, and that's where the extra confusion can come in.

### 2. Explicit Binding:

There's another way to invoke `functions`:

```JavaScript
1.  function ask(question) {
2.      console.log(this.teacher, question);
3.  }
4.
5.  var workshop1 = {
6.      teacher: "Kyle",
7.  };
8.
9.  var workshop2 = {
10.     teacher: "Suzy",
11. };
12.
13. ask.call(workshop1, "Can I explicitly set context?");
14. // Kyle Can I explicitly set context?
15.
16. ask.call(workshop2, "Can I explicitly set context?");
17. // Suzy Can I explicitly set context?

// this: explicit binding
```

> The `.call` method along with it's cousin, `.apply` method, both of them take, as their first `argument`, a `this` keyword.

So on line 13, when we say `.call` and we pass in `workshop1`, it is saying invoke the `ask function` with the this context of `workshop1`. It's very similar to the previous slide, we are still sharing that `function`, **but here we're doing so explicitly rather than implicitly**. We're saying wherever this `function` comes from, invoke it in a particular context which we're going to specify.

> **So we can use `.call` and `.apply` to explicitly tell JavaScript which context to invoke it in.**

Now, we're gonna talk about a variation of **explicit binding**, this is the second of the rules that we're looking at. But this isn't a separate rule, but kind of a sub-rule or a sub-part of this rule, which is an extremely common scenario or phenomenon referred to as **losing your `this` binding**.

If we've ever worked with a `function` that we pass around, and all of a sudden, it used to have a `this` binding and now it doesn't have a `this` binding. It's very frustrating when we think of a `this` keyword as being predictable and then we find out oops, actually, **it's not predictable, it's flexible**.

#### 2.1. Hard Binding:

So variation of explicit binding is called **hard binding**. This is a sub-rule or a sub-part of **explicit binding** which is a second ways of calling a `function`.

```JavaScript
1.  var workshop = {
2.      teacher: "Kyle",
3.      ask(question) {
4.          console.log(this.teacher, question);
5.      }
6.  };
7.
8.  setTimeout(workshop.ask, 10, "Lost this?");
9.  // undefined "Lost this?"
10.
11. setTimeout(workshop.ask.bind(workshop, "Hard bound this?"), 10);
12. // Kyle Lost this?

// this: hard binding
```

Looking at line 8, if we passed in `workshop.ask`, that method is on the `workshop object`, but that **line 8 is not the call site**. We have to imagine in our head, what would the call site look like for the `function` whenever that timer ran ten milliseconds from now?
And that call site would look like cb(), or something like that. It's not going to look like `workshop.ask`, and because it doesn't look like that, it's not going to invoke `ask` in a `workshop` context. Which is we've lost our `this` binding, we end up getting `undefined`.

> Actually just as side note, technically, the `setTimeout` utility is defined by HTML, it's not evoking it just with the default call, it actually **explicitly** invokes it with a `.call` in the context of **global**.

So it would actually invoke `workshop.ask` by saying `cb.call(window)`. Invoking it in the **global object** context.

**Q:** Would this be unnecessary if `ask` were defined as an `arrow function`?

**A:** The `ask` here as an `arrow function` would **not** solve the problem.

So line 8, we're losing our `this` binding and it's actually getting rebound to something else, in this case the **global object**. That's not what we want. So a very common solution to this is line 11, passing a **hard-bound `function`**. **If we pass in a hard-bound `function` using the `.bind` method, it will take away that whole flexibility thing and force it to only use the `this` that we've specified on line 11.**
It says evoke this `function`, and no matter how you invoke it, always use `workshop` as it's this context.

> In other words the `.bind` method, **doesn't invoke the `function`**, it produces a **new `function`** which is bound to a particular specific `this` context.

So we see a trade-off here:

We see the predictable, flexible `this` binding, but then we see some scenarios where, it's kind of frustrating that it's flexible. And what I'd really like is for it to be super predictable.

**There's a tension here:**

If we were to go to all the trouble to define a bunch of `functions` on some **namespace object**, and have `this.` in front of every property reference and every method access. And then all of our `function` calls use the `.bind`, we would be cutting ourself off at the knees.

Because the whole purpose of this system, **the whole reason that we pay the tax of putting `this.` in front of everything is to get the dynamicism. And then we're going and taking that whole dynamic system and locking it down so that it's completely predictable.**

At that point, wouldn't we be better served simply writing a **module** that uses **closure** and has a **fixed**, **predictable behavior**?

So how do we deal with this tension? We like using the `this` keyword, it can be useful to us, but there are times when we need it to not be so flexible.
If we go to the trouble to write a `this`-aware set of code, and then most of our core sites are using the flexible dynamism, and every once in a while we have to do something like a **hard binding**. Then we're getting a lot of benefits out of that system, seems like a reasonable trade-off.

On the other hand, if we go to all the trouble to write a `this`-aware system and then everyone or most of our calls sites have to use `.bind`, that's a clue to ous we're doing this the hard way. **We should switch back and use the predictable lexical closure.**

> If we want **flexible dynamism**, use a **`this` keyword**, if we want **predictability**, use **lexical scope** (closures).

So just keep that in mind when we're using the `.bind` method.
Not that it is bad, not that it is evil, not that it is an anti-pattern. But if we find that happening more often than not, we're probably doing things the hard way.

### 3. The `new` Keyword:

The `new` keyword is the third way that we can invoke a `function`:

```JavaScript
                 "constructor calls"

function ask(question) {
    console.log(this.teacher, question);
}

var newEmptyObject = new ask("What is 'new' donig here?");
// undefined "What is 'new' donig here?"

// this: new binding
```

> We should know that the **`new` keyword** seems as if it has something to do with invoking **`class constructors`**, **but the `new` keyword has not got anything to do with `classes`.** It's just an unfortunate syntactic trick to make it look like it's dealing with `classes` when it really isn't.
>
> But the purpose of the **`new` keyword** is actually to **invoke a `function`** with a `this` keyword pointing at a whole **new empty `object`**.

So far the three ways to invoke a `function`:

- One way is, invoking `functions` and pointing them at a context `object`, like a `workshop.ask`.
- The second way is to invoke a `function` and givie it a specific `object` with `.call` or `.apply` or force it with `.bind` method.
- A third way is to invoke a `function` and use a whole **new empty `object`**. And the **`new` keyword** can accomplish that (it also does other stuff too). We can accomplish that same goal by saynig, `function.call({})`. Cuz that would invoke our `function` in the context of a brand new empty `object`.

So in other words, these two statements are equal:

```JavaScript
ask.call({}) ==== new ask();
```

So the `new` keyword isn't actually buying ous much except the syntactic sugar of, hey I want this `function` invoked with a new `this` content.

**The `new` keyword does four things when it's used to invoke `function` (or what we should call it with heavy air quotes a `"constructor"` call):**

- Create a brand **new empty `object`** (out of thin air).
- Link that `object` to another `object` (so it first creates a brand new `object` and then links it somewhere).
- It calls the `function` with its **`this` keyword pointed at the new `object`** (not the linked `object`, the new `object`).
- And fourth and finally, the `new` keyword after the `function` call is done, if that `function` does not return its own `object`, the `new` keyword assumes that you meant to **return `this` keyword**.

**So these four things happen every single time a `new` keyword is invoked with a `function`.**

**Q:** When we describe it this way, which of the two entities seems like it's doing all the work?
Does it seem like the `new` keyword is doing all the work?
Or does it seem like your `"constructor" function's` doing all the work?

**A:** It's really the `new` keyword, isn't it? As a matter of fact, if you put `new` in front of almost any `function`, **even a completely empty `function`**, all four of these things would happen. It’s almost as if the `function` doesn’t even matter. The `new` keyword is just sort of hijacking the `function` so that it can do these four things.

### 4. Default Binding:

And our fourth and final way of invoking a `function` is the fallback, if none of the other three match, which is called the **default binding**:

```JavaScript
1.  var teacher = "Kyle";
2.
3.  function ask(question) {
4.      console.log(this.teacher, question);
5.  }
6.
7.  function askAgain(question) {
8.      "use strict";
9.      console.log(this.teacher, question);
10. }
11.
12. ask("What's the non-strick-mode default?");
13. // Kyle What's the non-strick-mode default?
14.
15. askAgain("What's the strick-mode default?");
16. TypeError

// this: default binding
```

Here we have an `ask function`. And when we call it on line 12, we'll notice that on line 12, we don't have any context `object`. We don't have any `.call`, or a `bind`, or a `new`. It's just a normal `function` call. It doesn't match any of the other rules.

> So since it **doesn't match any of the other rules**, the fallback is defined in the spec as, in **non-strict-mode**, default to the **global**.

So it's why we print `"Kyle"` here, cuz there's a **global `variable`** called `teacher`, with a value `"Kyle"`.

But notice that the `askAgain function` is in **strict-mode**. And when we invoke it, we actually get a `TypeError`.

**Q:** Can anybody guess why there's a `TypeError`?

**A:** Specifically in **strict-mode**, when we invoke it with no other `this` bindings, the default behavior is to leave `this`, `undefined`. So we're now trying to access a property on the `undefined` value, which is a `TypeError`.

> In **strict-mode**, when we invoke a `function` with no other `this` bindings rules, the default behavior is to leave `this`, **`undefined`**.

Now, why do they chose in **strict-mode** to make `this`, `undefined`, so that it would create a `TypeError`?
It's because it is almost certainly an `error` on our part to define a `this`-aware `function`, and invoke it without it any `this`. That's a terrible idea, that's almost as bad as **auto-creating globals**. Which nobody would ever do, right? **That's a terrible idea to invoke a `this`-aware `function` using the default binding**.

And in **non-strict** (so-called **sloppy-mode**), it ends up using the **global object**, which is almost never what we would want, in exactly the same way that it's almost never the case that we wanna **auto-create globals**. But **strict-mode** fixes that up for us and it says, hey, you've made an `error`.

Our `error` is not that we're doing a `this.` reference. Our `error` is that we've invoked the `function` without giving it a `this`. We need to use one of the other three ways. Use a `new` keyword, use a `.call`, or `.apply`, or a `.bind`, or use a context `object`.

So there we go, four ways to invoke a `function`. Those are the only four ways, by the way. That's it, just those four.
**These four ways are all we need to learn to be able to understand how the `this` keyword get bound.** But let's reset our mind back. The question that we set out to ask is:

**Q:** If we have a `this`-aware `function`, how do we know what its `this` keyword points at?

**A:** And our strong temptation is, we wanna assume that we can just answer that by looking at the `function`. And what we've now seen is, **there's no way to look at the `function` to answer that question. We have to look at the call site. We have to look at how the function's being called.**
Because every time it gets called, the how of the call controls what the `this` keyboard will point at.

### **Summary:**

So far the three ways to invoke a `function`:

- One way is, invoking `functions` and pointing them at a **context `object`**, like a `workshop.ask` (**implicit binding**).
- The second way is to invoke a `function` and givie it a specific `object` with `.call` or `.apply` (**explicit binding**) or force it with `.bind` method (**hard binding:**).
- A third way is to invoke a `function` and use a whole **new empty `object`**. And the **`new` keyword** can accomplish that (it also does other stuff too). We can accomplish that same goal by saynig, `function.call({})`. Cuz that would invoke our `function` in the context of a brand new empty `object` (**the `new` keyword**).
- And our fourth and final way of invoking a `function` is the fallback, if none of the other three match, which is called the **default binding**. Since it doesn't match any of the other rules, `this` in **non-strict** (so-called **sloppy-mode**), ends up using the **global object**. But in **strict-mode** the default behavior is to leave `this`, **`undefined`**.

## Binding Precedence:

What if we have a really crazy call site like line 8?

```JavaScript
1. var workshop = {
2.     teacher: "Kyle",
3.     ask: function ask(question) {
4.     console.log(this.teacher, question);
5.     }
6. };
7.
8. new (workshop.ask.bind(workshop))("What does this do?");
9. // undefined "What does this do?"

// this: binding rule precedence?
```

On line 8, we have a `new` keyword, we have a `workshop.ask` (so we have a context `object`), and we have `.bind` (which under the covers, of course, using `apply`). We have three of our four rules matched on the same call site. By the way we should not ever write a call site like that, but it does actually work.

So from here forward, if we ever need to ask ourself what is our `this` keyword gonna point out, when this `function` gets invoked, this is how we determine that.

**This precedence that shows us, if we have more than one rule matches a call site, what is our `this` keyword gonna point out when the `function` gets invoked :**

1. **Is the `function` called by `new`? If so, the newly created `object` will be the `this` keyword.**
2. **Is the `function` called by `call` or `apply()`? (And by the way `bind()` is a sub of that rule because it also uses `apply()`). If so, the context `object` that is specified will be used.**
3. **Is the `function` called on a context `object` (like `workshop.ask`)? If so, use that `object`.**
4. **DEFAULT: global object (except strict mode), if none of those three have applied, then we fallback to the default.**

That's it, just those four rules in that order, and it'll perfectly and completely answer every question that we may have about what does my `this` keyword point at?

## Arrow Functions & Lexical `this`:

Let's examine the arrow `functions` within the context of what we've just discussed, which is the `this` keyword:

![this: arrow functions](https://user-images.githubusercontent.com/37678729/75470429-e7b38800-59a5-11ea-9ba3-2714a6e00f14.png)

Here we'll notice that the `this` keyword, when the arrow `function` is invoked, is correctly is pointing at the `workshop object`.

**This is what we refer to as lexical `this` behavior.**

So let's explain what **Lexical `this`** means:

> Many people have in their minds a mental model that a arrow `function` is essentially a hard-bound `function` to the parents `this`, **that is not accurate**.
>
> The proper way to think about what an arrow `function` is, **an arrow `function` does not define a `this` keyword at all. There is no such thing as a `this` keyword in an arrow `function`.**
>
> Which means if we put a **`this` keyword** inside of an **arrow `function`**, **it's gonna behave exactly like any other `variable`**. Which means it's going to **lexically** resolve to some enclosing scope that does define of `this` keyword.

So in this particular case, on line 5, when we say `this.` there is no `this` in that arrow `function` no matter how it gets invoked, so we lexically go up one level of scope which is, which `function`? The `ask function`.

It goes up from the callback `function` (the arrow `function`, that scope), to the enclosing scope, which is? `ask`. And what is `ask`s definition of the `this` keyword? What line of code controls what the `this` keyword will point out inside of `ask`? Line 10, because the `ask function`s `this` keyword gets set by the call site.

And then when that callback gets later invoked, it’s essentially closed over, that parent scope that had a `this` keyword pointing at the `workshop object`. That's what we mean by **lexical `this`**.

**Arrow `function` is not a hard-bound `function`. It's a `function` that doesn't have a `this` at all. And so it revolves lexically. That means if it had to go up, five levels because we had five nested arrow `functions`, it just keeps going and going and going up the building elevator until it finds a `function` that defines a `this` keyword.
And whatever the `this` keyword points at for that `function`, that's what it uses.**

> So this is **not the correct explanation**: An arrow `function` is `this-`bound (aka `.bind()`) to its parent `function`.

And here is the spec:

> ![ECMAScript](https://user-images.githubusercontent.com/37678729/75474747-c99d5600-59ac-11ea-8af7-1d672d0238aa.png)
>
> [ECMAScript](https://www.ecma-international.org/ecma-262/10.0/index.html#sec-arrow-function-definitions-runtime-semantics-evaluation)

### Resolving `this` in Arrow Functions:

Here's a place where it is perpetually frustrating that we have **overloaded operators**. We tend to think that curly braces `{}` must be scopes. They're blocks, they're `function` bodies, they must be scopes. But they're not!

What's gonna happen when we define an arrow `function` on line three?

![this: arrow functions](https://user-images.githubusercontent.com/37678729/75797114-e5787180-5d89-11ea-87c1-d019e39164e8.png)

What is the parent lexical scope from which that arrow `function` will go up one level to resolve the `this` keyword? It is the global.

It is not the `workshop object` because, guess what? Just cuz there's **curly braces `{}` around that `object` doesn't make it a scope. Objects are not scopes.** So this is a very common mistake that people have, where people are saying, why is the arrow `function` not getting my `workshop` as my content?
Well, **because `workshop object's` not a scope. We have to think about an `arrow` function as not having of `this` and resolving it lexically.** So what is the parent scope? There's only two scopes in this program. The scope of the `ask function`, which is an arrow, and the global scope. There's no intervening scope in between.

> It is unfortunate that we've overloaded the curly brace `{}` that confuses us into thinking it's a scope, but it isn't.

The downside is that arrow `functions` are anonymous and so they're a bit harder to debug at times, they don't explain themselves well. If we take the entire context, Kyle Simpson perception is that **the only time we should ever use an arrow `function` is when we're gonna benefit from lexical `this` behavior.**

Because the alternative to lexical `this` behavior is a hack like the `var self = this` this days. Let me just say, `var self = this` is the worst possible name anybody ever could have come up with. **Because `this` keyword never, ever, ever, under any circumstances, points at the `function` itself, it points at a context.**
**So if we absolutely must do the `var self = this` hack, we should do `var context = this`. Cuz that's what `this` keyword is, is a context.**

> But this arrow `function` lexical `this` behavior is a much better way of doing it than, a `var self = this`. And even better than doing the `function.bind()`.
>
> It is a much better way because it actually matches the mental model of what we want. We want the `this` keyword to behave lexically here. We don't want for the arrow `function` to have some magical `this` behavior to it. We want it to just adopt the `this` keyword of some parent scope.

**Q:** When we would be parsing this example, `workshop` is going into the red bucket, it’s getting the global scope. The `teacher` property, though, would be scoped to ...

**A:** Properties aren't scoped, properties aren't lexical identifiers. It's a member on an `object` value. It's not participating in lexical scope at all.

If we gonna use an arrow `function` to get our lexical `this`, we need to combat those three downsides that we talked about with anonymous `function`. We need to combat the downside that, anonymous `functions` don't have a self reference, in case we need to do recursion or unbinding.
We need to combat the fact that they don't have a name. Use it in some way so that it's gonna get a name inference, like, assign it to a `variable` or a property. Because it's gonna show up as anonymous otherwise.
And we need to have some way of making it clear and obvious to the reader. What is the purpose of this `function`? Don't make them read the `function` body to figure that out.

> The only thing we ever need to do to understand the `this` keyword is look for the call site of a `function` that defines the this keyword, and ask those four rules.

## ES6 `class` Keyword

> The `class` keyword is ostensibly **syntactic sugar** layered on top of the **prototype system**.
>
> By the way, this is a little know fact. `classes` don't have to be statements, `classes` can be **expressions**, and they can be **anonymous**.

The `classes` can be defined with or without an `extends` clause. Here, we're just defining a `class` that doesn't extend anything, so it's the top level `class`.

```JavaScript
1.  class Workshop {
2.      constructor(teacher) {
3.          this.teacher = teacher;
4.      }
5.      ask(question) {
6.          console.log(this.teacher, question);
7.      }
8.  }
9.
10. var deepJS = new Workshop("Kyle");
11. var reactJS = new Workshop("Suzy");
12.
13. deepJS.ask("Is 'class' a class?");
14. // Kyle Is 'class' a class?
15.
16. reactJS.ask("Is this class OK?");
17. // Suzy Is this class OK?

// ES6 class
```

We can choose to define a `constructor` if we want, like we're doing on line 2, and we can add methods.

And look on line 4, we don't even need commas in between them. They did a fantastic job of just dribbling all kinds of syntactic sugar on this feature. It's very attractive. Then we look at line 10, it looks exactly like instantiating classes in any other class-oriented language.

We just say `new`, capital W `Workshop`, and we get an instance. And we call `deepJS.ask` and the method call works. And there's a `this` context that works. So that's what the `class` syntax looks like.

**If we want to extend one `class` into another `class`, we use the `extends` clause**. Like here on line 10:

```JavaScript
1.  class Workshop {
2.      constructor(teacher) {
3.          this.teacher = teacher;
4.      }
5.      ask(question) {
6.          console.log(this.teacher, question);
7.      }
8.  }
9.
10. class AnotherWorkshop extends Workshop {
11.     speakUp(msg) {
12.         this.ask(msg);
13.     }
14. }
15.
16. var JSRecentParts = new AnotherWorkshop("Kyle");
17.
18. JSRecentParts.speakUp("Are classes getting better?");
19. // Kyle Are classes getting better?

// ES6 class: extends (inheritance)
```

We don't have to redefine any other methods that are already defined because they'll be so-called **inherited**. So we can define new methods like the `speakUp` method here on line 11 and when we instantiate that child `class`, we can invoke that method, `.speakUp` (line 18), exactly like it was on the `object`.

In the below, is a example of relative polymorphism in `classes`:

```JavaScript
1.  class Workshop {
2.      constructor(teacher) {
3.          this.teacher = teacher;
4.      }
5.      ask(question) {
6.          console.log(this.teacher, question);
7.      }
8.  }
9.
10. class AnotherWorkshop extends Workshop {
11.     ask(msg) {
12.         super.ask(msg.toUpperCase());
13.     }
14. }
15.
16. var JSRecentParts = new AnotherWorkshop("Kyle");
17.
18. JSRecentParts.ask("Are classes getting better?");
19. // Kyle ARE CLASSES GETTING BETTER?

// ES6 class: extends (relative polymorphism)
```

> The `class` system also now has a **`super` keyword** in it, which allows us to do **relative polymorphism**. If we have a child `class` that defines a method of the **same name** as a parent `class` (so-called **shadowing**), we can refer to the parent from the child by saying `super.` like we see on line 12.

**By the way, this is an example of extension beyond syntactic sugar because prior to ES6 `classes`, there was essentially no way to do relative polymorphism. There was no equivalent of the `super` keyword.**

Not saying that's a bad thing, just saying, when people say, it's just syntactic sugar anyway, no, it isn't. It's its whole own mechanism, with its own set of complexities. It's like a language within a language at this point, **`classes` are not just syntactic sugar**, but that is a useful, mental model for these simplest of examples.

It's need to say that even though there's a bunch of syntactic sugar, **they didn't change anything fundamentally about how `function` calls work and how that `this` keyword gets bound.** So, even if we define a method on a `class` instance, if we pass it into a `setTimeout`, guess what?
It's gonna lose its `this` binding.

```JavaScript
1.  class Workshop {
2.      constructor(teacher) {
3.          this.teacher = teacher;
4.      }
5.      ask(question) {
6.          console.log(this.teacher, question);
7.      }
8.  }
9.
10. var deepJS = new Workshop("Kyle");
11.
12. setTimeout(deepJS.ask, 100, "Still losing 'this'?");
13. // undefined "Still losing 'this'?"

// ES6 class: still dynamic this
```

They're not somehow magically auto bound. Those methods on `class` instances, behave just like any other `function`.

And that idea of having an autobound `this` method is why in this interim period for the last several years, we have seen an explosion of patterns where people want hardbound or autobound methods and they aren't automatically.

So what we see a lot happening is something like line 4 in below example:

```JavaScript
1.  class Workshop {
2.      constructor(teacher) {
3.          this.teacher = teacher;
4.          this.ask = question => {
5.              console.log(this.teacher, question);
6.          };
7.      }
8.  }
9.
10. var deepJS = new Workshop("Kyle");
11.
12. setTimeout(deepJS.ask, 100, "Is 'this' fixed?");
13. // Kyle Is 'this' fixed?

// ES6 class: "fixing" this?
```

**Where instead of defining a method on the `prototype`, we added into the `constructor` and use a hardbound method or use an arrow `function`.**

This deeply troubles to see this propagation of this idiom. This idea that it's got to be hard bound and don't want any dynamism to it all, so I'm gonna use a lexical `this` from an arrow `function` or I'm gonna use a hard bound `function` to accomplish that.

Because we are essentially betraying the entire system that `classes` has built upon. **The entire `class` system is built upon this idea that our methods don't exist on our instances, they exist on our prototypes.** And guess what happens when we say `this.ask` and we assign it a `function`? **It's no longer on the `prototype` anymore, it's on our instance. So every single time we instantiate a `function`, we're getting a whole separate copy of all those `functions` added to every single instance.**

---
WE 🥇 ARE 🥇 DONE 🥳🥳🥳💁‍



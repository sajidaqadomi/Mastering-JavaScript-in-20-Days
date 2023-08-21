
# Day 11💻
## **[Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)** 🔥🔥

## Equality 💁‍♀️

### Double & Triple Equals:

> JavaScript provides three different value-comparison operations:
>
> - `===` - `Strict Equality` Comparison ("`strict equality`", "`identity`", "`triple equals`")
> - `==` - `Abstract Equality` Comparison ("`loose equality`", "`double equals`")
> - `Object.is` provides SameValue (new in `ES2015`).
>
> Which operation you choose depends on what sort of comparison you are looking to perform. Briefly:
>
> - `double equals` (`==`) will perform a `type conversion` when comparing two things, and will handle `NaN`, `-0`, and `+0` (so `NaN != NaN`, and `-0 == +0`);
>
> - `triple equals` (`===`) will do the same comparison as `double equals` (including the special handling for `NaN`, `-0`, and `+0`) but without `type conversion`; if the types differ, `false` is returned.
>
> - `Object.is` does no type conversion and no special handling for NaN, -0, and +0 (giving it the same behavior as `===` except on those special numeric values).
>

> ![ECMAScript](https://user-images.githubusercontent.com/37678729/71779325-2262fa80-2fcb-11ea-835d-debd2bccb90f.png)
>
> [ECMAScript](https://www.ecma-international.org/ecma-262/10.0/index.html#sec-abstract-relational-comparison)

> This is not exactly the case:*The difference between `double equals` and `triple equals` is that `double equals` checks the value so called `loose equality` and `triple equals` checks the `value` and the `type` so called `strict equality`.*
>
> The `double equals` and the `triple equals` both checked the types, it's just that one does something different with that information than the other one.

> Essentially the real difference between `strict equality` and `loose equality` is whether or not we're going to to allow any coercion to occur.

> If the types are the same in `Strict Equality` (`===`), it's going to, return `false` if they're `NaNs`, because remember it's supposed to lie about `NaNs`. And it's gonna return `true` if there's a `-0` because it's supposed to lie about `-0`. But it only does the lies if the types already match.


We have two `objects`:

```JavaScript
var workshop1 = {
  name: "Deep JS Foundations"
};

var workshop2 = {
  name: "Deep JS Foundations"
};

if (workshop1 == workshop2) {
  // Nope
}

if (workshop1 === workshop2) {
  // Nope
}

// Equality: identity, not structure
```

We have two `objects`, they have the same structure and ostensibly and the same value. But they are not the same object.

> The Equality comparisons in JavaScript does `identity comparison` not `structure comparison`.

If workshop1 and workshop 2 pointed at literally the same `object reference` then their `identity` would be the same and you'd get `true`.

**So neither `==` nor `===` is gonna return a `true` because they are different objects.** ☹️

> The `==` is going to allow `coercion` when the `types` were different. And the `===` is going to disallow `coercion` when the `types` are the same.

### Coercive Equality:

> In the `double equals` if the `types` are `null` or `undefined` on either side, then return `true`.
>
> The `null` value and the `undefined` value are `coercively` equal to each other and to no other values in the language.
>
> So we have the option of treating `null` and `undefined` as indistinguishable (or pretend that they're interchangeable) through coercive equality.

Here is a example that it is better to treating `null` and `undefined` as indistinguishable:

```JavaScript
var workshop1 = { topic: null };
var workshop2 {};

if (
  (workshop1.topic === null || workshop1.topic === undefined) &&
  (workshop2.topic === null || workshop2.topic === undefined) &&
) {
  // ..
}

if (
  workshop1.topic == null &&
  workshop2.topic == null
) {
  // ..
}

// Coercive Equality: null == undefined
```

The reader has not gaining anything readability-wise by being `explicit` between two empty values.

The second one (`double equals`) says, whether they are `null` or `undefined`, tell us if they're empty or not. Tell us if they're one of those two empty values. And by the way, we just picked the shorter of the two cuz it's less to type.

### Double Equals Algorithm

If we're not talking about `nulls` and `undefines`, but we're talking about `strings`, `numbers` and `booleans`:

> For `strings`, `numbers` and `booleans` primitive values, the `Abstract Equality` (`double equals`) prefers to do numeric comparison (`toNumber`).

> The [ECMAScript](https://www.ecma-international.org/ecma-262/10.0/index.html#sec-abstract-relational-comparison) says if one of them is `number`, but the other one is `string`, then call `toNumber` on the `string`, so it can do a numeric comparison.
>
> If one of them's `boolean`, then do a `toNumber` on it, and make the comparison.

> The `double equals` prefers numeric comparison.

Here is a example of `string` and `number`:

```JavaScript
var workshopEnrollment1 = 16;
var workshopEnrollment2 = workshop2Elem.value;

if (Number(workshopEnrollment1) === Number(workshopEnrollment2)) {
  // ..
}

// Ask: what do we know about the types here?
if (workshopEnrollment1 == workshopEnrollment2) {
  // ..
}

// Coercive Equality: perfers numeric comparison
```

So the abstraction of the `double equals` is helpful there.

> But if they are both `strings`, that means they are both of the same `type` (literally `identical`), it does the `triple equals` (`===`).
>
> The `double equals` is going to allow `coercion` when the `types` are different.
>
> If we're in a scenario where the `types` are not different, where the types are the same, then it's not ever going to invoke `coercion`, ever.

> if we use a `double equals` with something that's not already a `primitive`, We invoke the `toPrimitive` abstract operation.

The `double equals` only compares `primitives`. If we use it with something that's not a `primitive`, it turn it into a `primitive`. The only time it does something useful with `non-primitives` is when they're the exact same type and then it just does the same value `triple equals` comparison. Otherwise it invokes `toPrimitive` abstract operation.

This is a example where `coercion` is a very bad thing for us:

```JavaScript
var workshop1Count = 42;
var workshop2Count = [42];

// 1- if (workshop1Count == workshop2Count)
// Because workshop2Count is non-primitive, algorithm invokes toPrimitive on it.
// (because of that weird array stringification that doesn’t include the brackets.
// And only accidentally working because there is only one value in the array.)

// 2- if (42 == "4")
// Now we have two different types, we have a number and a string. There's two options here.
// We could either make the number into a string and compare the strings,
// or make the string into a number and compare the numbers. The algorithm prefers numeric comparison.
// So the string becomes the number.

// 3- if (42 === 42)
// Because the types are now the same, it does a `triple equals` comparison.

if (true) {
  // Yep (hmm...)
}

// Coercive Equality: only primitives
```

> We should never use `double equals` to compares a `primitive` with `non-primitive` value.

### Summary:

This is summary of how `double equals` works:

- If the types are the same it's just gonna use `triple equals` (`===`).
- If both of them are `null` or `undefined`, they are equal.
- If there are `non-primitives` involved in the comparison, they are always gonna become `primitive` first.
- And then once we have `primitives`, prefer `toNumber`.

### Double Equals Corner Cases

How could something like an empty array somehow be coercively equal to the negation of itself?

```JavaScript
[] == ![];      // true WAT!?

// let's explain how it works. With an example:

var workshop1Students = [];
var workshop2Students = [];

1- if (workshop1Students == !workshop2Students) {
  // Yep, WAT!?

  // 1- if ([] == ![])
  // The workshop2Students is an array which is truthy. So if we negate (!) it it becomes false.

  // 2- if ([] == false)
  // Now, we have a non-primitive compared to a primitive.
  // So we need to turn that non-primitive (array) into a primitive. So it becomes the empty string.

  // 3- if ("" == false)
  // So now, We have two primitives but they are not of the same type.
  // The algorithm prefers that they both become numbers.

  // if (0 === 0)
  // if (true)
}


2- if (workshop1Students !== workshop2Students) {
  // Yep, WAT!?

  // if (!(workshop1Students == workshop2Students))
  // if (!(false))
  // if (true)
}

// == Corner Cases: WAT!?
```

Compare the first one in your mind to the more appropriate comparison (the second one), which is to say, I want to check to see if they're not the same `array`.

Those might look like the same thing (first one and second one), but these are entirely different approaches. One is saying I wanna see if it is coercively `equal` to its `negation` (`!`), and the other one is saying I wanna see if it is not coercively `equal`. Those are entirely different beasts.

In the second one, since they're both `arrays`, then what we're effectively doing is asking an `identity` question. We're saying, are they not the same `identity`?

And it would work `identically` if we use the `triple equals` version of them. It's a rational thing, and it has no difference in the rational case between double equals and triple equals.

### Corner Cases Booleans:

This is another example one of those corner cases that we shouldn't do:

```JavaScript
var workshopStudents = [];

1- if (workshopStudents) {
  // Yep

  // if (Boolean(workshopStudents))
  // if (true)
}

2- if (workshopStudents == true) {
  // Nope :(

  // if ([] == true)
  // We have a non-primitive which need to became primitive, so it becomes empty string.

  // if ("" == true)
  // We have an empty string and a true. These are not the same type, so they need to both become numbers.

  // if (0 === 1)
  // One of them becomes 0, (which should have been NaN), the other one becomes 1.

  // if (false)
}

3- if (workshopStudents == false) {
  // Yep :(

  // if ("" == false)
  // if (0 === 0)
  // if (true)


// == Corner Cases: booleans
}
```

If we wanna check and we want to allow the `boolean` coercion of an `array` to be `true`. In other words, we wanna say its `truthy` sort of construct.
There's one way of doing it (the first statement), which is just to do an if statement. Allow the if statement to invoke the `toBoolean` operation on the `array`, which in this case, is a lookup that says the `array` is not on the table, so, therefore, it's `true`. That's a perfectly rational implicit `toBoolean` coercion.

But if we try to get more clever and tricky with it and say, well, if it's `truthy`, then maybe what we want to do is do a `double equals` with `true`. Well, now all of a sudden it doesn't work. And by the way, it wouldn't work with `triple equals` either. There's no case where second and third statement are better. And there's a bunch of cases where they are worse, like these one.

So `implicit` is sometimes much better than `explicit`.

> Don't ever do a `double equals`, (or even in that case, `triple equals`) with `true` or a `double equals` with `false`.
>
> We don't need to `double equals` to `true`, or `double equals` to `false`, we should allow the `toBoolean` to happen `implicitly`.

Summary:

How to avoid corner cases with the `double equals`:

- Avoid the `double equals` when either side of them can be a `0`, or an `empty string`, or even one of those `strings` with only `whitespace` in it.
- Don't use it with `non-primitives`. Only use it for coercion among the `primitives`.
- Definitely don't use `double equals` to `true` or `double equals` to `false`. Essentially, just allow the `ToBoolean` to happen. And if we really can't allow that, if it really has to exactly `true` or exactly `false`, which sometimes it does, then use `triple equals`.

---

### The Case for Double Equals:

If we `know` the `type(s)` in a comparison:

- Whether the `types` match or not, `==` is the more sensible choice when we know the `types`.

If we `don't know` the `type(s)` in a comparison:

- If we can't or won't, use a style where we can know and have obvious `types`, the only thing that is sensible and reasonable is for us to use the `===`.

Making our `types` known and obvious just leads to better code. Knowing the `types` leads to better code and if the `types` are known, `==` is always best.
In every scenario `==` is best when the `types` are known and in any scenario where you can't you should fall back to `===`.

### Equality Exercise Solution 👩‍💻
> **Wrangling Equality**

In this exercise, you will define a `findAll(..)` function that searches an array and returns an array with all coercive matches.

> **Instructions**

1. The `findAll(..)` function takes a value and an array. It returns an array.

2. The coercive matching that is allowed:

	- exact matches (`Object.is(..)`)
	- strings (except "" or whitespace-only) can match numbers
	- numbers (except `NaN` and `+/- Infinity`) can match strings (hint: watch out for `-0`!)
	- `null` can match `undefined`, and vice versa
	- booleans can only match booleans
	- objects only match the exact same object
	
```
function findAll(match,arr) {
  var ret = [];
  for (let v of arr) {
    if (Object.is(match,v)) {
      ret.push(v);
    }
    else if (match == null && v == null) {
      ret.push(v);
    }
    else if (typeof match == "boolean") {
      if (match === v) {
        ret.push(v);
      }
    }
    else if (typeof match == "string" && match.trim() != "" && typeof v == "number" && !Object.is(-0,v)) {
      if (match == v) {
        ret.push(v);
      }
    }
    else if (typeof match == "number" && !Object.is(match,-0) && !Object.is(match,NaN) && !Object.is(match,Infinity) && !Object.is(match,-Infinity) && typeof v == "string" && v.trim() != "") {
      if (match == v) {
        ret.push(v);
      }
    }
  }
	return ret;
}


// tests:
var myObj = { a: 2 };

var values = [
	null, undefined, -0, 0, 13, 42, NaN, -Infinity, Infinity,
	"", "0", "42", "42hello", "true", "NaN", true, false, myObj
];

console.log(setsMatch(findAll(null,values),[null,undefined]) === true);
console.log(setsMatch(findAll(undefined,values),[null,undefined]) === true);
console.log(setsMatch(findAll(0,values),[0,"0"]) === true);
console.log(setsMatch(findAll(-0,values),[-0]) === true);
console.log(setsMatch(findAll(13,values),[13]) === true);
console.log(setsMatch(findAll(42,values),[42,"42"]) === true);
console.log(setsMatch(findAll(NaN,values),[NaN]) === true);
console.log(setsMatch(findAll(-Infinity,values),[-Infinity]) === true);
console.log(setsMatch(findAll(Infinity,values),[Infinity]) === true);
console.log(setsMatch(findAll("",values),[""]) === true);
console.log(setsMatch(findAll("0",values),[0,"0"]) === true);
console.log(setsMatch(findAll("42",values),[42,"42"]) === true);
console.log(setsMatch(findAll("42hello",values),["42hello"]) === true);
console.log(setsMatch(findAll("true",values),["true"]) === true);
console.log(setsMatch(findAll(true,values),[true]) === true);
console.log(setsMatch(findAll(false,values),[false]) === true);
console.log(setsMatch(findAll(myObj,values),[myObj]) === true);

console.log(setsMatch(findAll(null,values),[null,0]) === false);
console.log(setsMatch(findAll(undefined,values),[NaN,0]) === false);
console.log(setsMatch(findAll(0,values),[0,-0]) === false);
console.log(setsMatch(findAll(42,values),[42,"42hello"]) === false);
console.log(setsMatch(findAll(25,values),[25]) === false);
console.log(setsMatch(findAll(Infinity,values),[Infinity,-Infinity]) === false);
console.log(setsMatch(findAll("",values),["",0]) === false);
console.log(setsMatch(findAll("false",values),[false]) === false);
console.log(setsMatch(findAll(true,values),[true,"true"]) === false);
console.log(setsMatch(findAll(true,values),[true,1]) === false);
console.log(setsMatch(findAll(false,values),[false,0]) === false);

// ***************************

function setsMatch(arr1,arr2) {
	if (Array.isArray(arr1) && Array.isArray(arr2) && arr1.length == arr2.length) {
		for (let v of arr1) {
			if (!arr2.includes(v)) return false;
		}
		return true;
	}
	return false;
}

```

### Static Typing 💁‍♀️

#### Typecript & Flow:

let's look at what `TypeScript` and `Flow` can do for us.

**Benefits of Typecript & Flow:**

1. Catch type-related mistakes.
2. Communicate type intent. (because the typing is in the code.
   And it's gonna make our code more obvious.)
3. Provide IDE feedback. (maybe one of the biggest things is it get us an amazing amount of feedback through the tooling ecosystem that can show up live directly in our IDE.)

**Caveats:**

1. Inferencing is best-guess, not a guarantee.
2. The annotations are optional. (Which means the developers on our team, if they don't put an annotation on a variable, `TypeScript` will default to the any type unless we have that turned off. And then we're not getting any benefit out of it.)
3. Any part of the application that isn't typed, introduces uncertainty.

#### Inferencing:

So some examples of `TypeScript` and `Flow`, and these examples are actually identical between the two:

```JavaScript
var teacher = "Kyle";

// ..

teacher = { name: "Kyle"};
// Error: can't assin object to string


// Type-Awarw Linting: inferencing
```

> `Type inference` refers to the automatic detection of the `data type` of an expression in a programming language.
>

If we don't do any typing at all, both `TypeScript` and `Flow` by default will do some inferencing.

So here they're doing a `static types inference`, which means my intent (that they're guessing), is that we want `teacher` (the variable), to only ever hold `strings`. And when we later try to assign it something `non-string`, it throws us an error, and says, you're doing an assignment that you shouldn't do. That's their best guess.

But that's what we refer to as `static types`, inferring that the variable has a `type` based upon the value that goes into it. JavaScript `variables` don't have `types`, but we're layering on this extra requirement.

So that's when we don't annotate the `types`, but of course we can annotate the `types`:

```JavaScript
var teacher: string = "Kyle";

// ..

teacher = { name: "Kyle"};
// Error: can't assin object to string


// Type-Awarw Linting: annotating
```

We can say `teacher` is definitely a `string`. We're gonna get basically the same error, but here we're not guessing at the error. We're literally saying we intended for this thing to only ever hold `strings`, and now we're trying to put something `non-string` to it. In both cases `TypeScript` and `Flow` are gonna throw us an error and say, you're assigning something you shouldn't have.

#### Custom Types:

We can define custom types like this:

```JavaScript
type student = { name: string };

function getName(studentRec: student): string {
  return studentRec.name;
}

var firstStudent: student = { name: "Farank"};

var firstStudentName: string = getName(firstStudent);


// Type-Aware Linting: custom types & signatures
```

Here we're defining that an `object` of a `type` that has a property called `name` that is of type `string`, that is a `type`. And then we can pass values of that `type` as parameters. And we can receive values back as parameters. So here we are passing in `studentRec` of the type `student`. we're defining our own `type`. this program doesn't have any errors.

But most of the guarantee here is are things being assigned correctly.
A parameter to a `function` is a lot like a `variable`. If we're saying we wanna only be able to pass in `numbers`, then we're basically saying the same thing as we want this `variable` to only hold `numbers`.

Where I to uses something like `TypeScript` I probably would define many more of my parameters as say union `types`. Or I would say, you know what, I'm gonna allow `strings`, `numbers`, and `nulls`. Because it's rare that I want it to be so restrictive that it can only ever receive exactly this kind of structured `object` for example.

But nevertheless, it's able to do some very useful guarantees if the problems that you have are misassignments of types.

#### Validating Operand Types

In this particular case, `TypeSript/Flow` saying we can't subtract a `string` from a `number`:

```JavaScript
var studentName: string = "Frank";

var studentCount: number = 16 - studentName;
// error: can't substract string


// Type-Aware Linting: validating operand types
```

Because that particular preference is saying don't allow that `coercion`, and in this particular case, that would be a really useful help for us.

An undervalued part of what they do, Is that they are actually allowing us to check the operations that we're doing where most of our business logic is, and making sure that those operations are valid.

> It would be nice if `TypeScript` would have some mechanism by which we could allow some more `coercion` to occur.

Because there are plenty of places, where we'd like to be able to do `coercion` and other places we'd like to avoid it. It appears that `TypeScript` is kind of all or nothing. We opt into it or we don't opt into it.

#### Static Typing Pros and Cons

#### Pros:

- They make types more obvious in code.
- Familiarty: they look like other language's type systems.
- Extremely popular these days.
- They're **very** sophisticated and good at what they do.

#### Cons:

- They use "non-JS-standard" syntax (or code comments) (they chose to use a syntax that they had to layer on top of JavaScript.)
- They require\* a build process, which raises the barrier to entry.
- Their sophistication can be intimidating to those without prior formal types experience.
- They focus more on "static types" (variables, parameters, returns, properties, etc) than *value types*

These tools came out with a way that we can do their typing annotations using only code comments. So at least in that scenario, we haven't locked ourself into if we don't use this tool this code literally can't run. That's sort of an escape valve, and that's a good thing, but almost nobody's using the code comments. Everybody's using the inline syntax annotations.

---

**Summary:**

- JavaScript has a (`dynamic`) `type` system, which uses various forms of `coercion` for `value type` `conversion`, including `equality comparisons`.

- We simply cannot write quality `JS` programs without knowing the `types` involved in our operations.

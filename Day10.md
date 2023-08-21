
# Day 10💻
# **[Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)** 🔥🔥

## Data Types 💁‍♀️
### Primitive values

✅ String
✅  Number
✅  Bigint
✅  Boolean
✅  Undefined
✅  Null
✅  Symbol

> are known as being immutable data types because there is no way to change a primitive value once it gets created

```
var string = 'This is a string.';
string[1] = 'H'
console.log(string) // 'This is a string.
```

### Non-primitive values (object references)

✅ Object
> But what about functions and arrays? functions and arrays are subtype of the object type.

> Non-primitive values are mutable data types. The value of an object can be changed after it gets created.

```
var arr = [ 'one', 'two', 'three', 'four', 'five' ];
arr[1] = 'TWO';
console.log(arr) // [ 'one', 'TWO', 'three', 'four', 'five' ];
```
### Typeof Operator

> typeof operator to find the data type of a JavaScript variable

> In JavaScript, variables don't have types, values do.

```
typeof "John"                 // Returns "string"
typeof 3.14                   // Returns "number"
typeof NaN                    // Returns "number"
typeof false                  // Returns "boolean"
typeof [1,2,3,4]              // Returns "object"
typeof {name:'John', age:34}  // Returns "object"
typeof new Date()             // Returns "object"
typeof function () {}         // Returns "function"
typeof myCar                  // Returns "undefined" *
typeof null                   // Returns "object"

typeof 42n                   // bigint
```
> 🤔 Why **typeof null** returns object? This is a historical fact from ES1 which essentially indicated to developers that if you wanted to unset a regular value, like a number, you would use undefined. But if you wanted to unset an object reference, you would use null.

Remember, function is not an official type at the top level, in the most official sense. But it has its own return value here, the typeof operator returns as function. So it's useful that it returns to us function, but arrays, it doesn't. Arrays just returns object.

> `The Array.isArray() will tell you for sure or not whether you have an array.`

### undefined vs. undeclared vs. uninitialized

This is often confused between undefined and undeclared concept. And it's confused because developers, quite naturally, think of these words as sort of synonyms. They seem like they mean kind of almost the same thing. And in English, that's probably true. But in programming, it's entirely not true. In programming, and especially in JavaScript, these are two entirely different concepts.

> undefined and undeclared in JavaScript are two entirely different concepts.

When we said type of V, and we got back quote, undefined, V or whatever that variable is, didn't even exist. So how is it that I can get back quote undefined when something doesn't even exist? Well, that's another historical wart, JavaScript trying to pretend as if the absence of a declaration isn't that big a deal. It's not that big of a problem, you can work around it. In retrospect, they never should have done that. They should have just returned a string undeclared.

> The `undeclared` means it's never been created in any scope that we have access to.
>
> The `undefined` means there's definitely a variable, and at the moment, it has no value.
>
> the `uninitialized` or TDZ (Temporal Dead Zone) was introduced with ES6, and the best way to describe this is uninitialized. Meaning you can't touch it yet.

> The `typeof` operator is the only operator in existence that is able to reference a thing that doesn't exist and not throw an error.

The idea for `uninitialized` is that certain variables, never initially get set to undefined. When something is in an uninitialized state, it is off-limits. You're not allowed to touch it in any way, shape or form, or you'll get an error, and the error you get is the **TDZ error**.

We can have a variable that's never been initialized. We can have a variable that's been initialized that is undefined. Or we can have a variable that was never even created, and then it's undeclared.

### BigInt
### Kinds of Empitness
### NaN & isNAN
NaN:
The NaN is an invalid number.

```
var myAge = Number("0o46");       // 38
var myNextAge = Number("39");     // 39
var myCatsAge = Number("n/a");    // NaN
myAge - "my son's age";           // NaN

myCatsAge === myCatsAge;          // false   OOPS!

isNaN(myAge);                     // false
isNaN(myCatsAge);                 // true
isNaN("my son's age");            // true    OOPS!

Number.isNaN(myCatsAge);          // true
Number.isNaN("my son's age");     // false
```
> The NaN is the only value in JavaScript, that is not equal to itself. Even when we use the triple equals operator ( === ).

> The isNaN() function determines whether a value is NaN or not. But for The historical reason the isNaN utility coerces values to numbers before it checks for them to be NaN.
>
>The Number.isNaN() method (ES6) tells us defiantly for sure the passed value, is the NaN value or it's not.
>Note: This function differs from the global isNaN function in that it does not convert its argument to a Number before determining whether it is NaN.

SO

> isNaN() method returns true if a value is Not-a-Number.

> Number.isNaN() returns true if a number is Not-a-Number.

**type of a NaN is number. It's just an invalid number.**

### Negative Zero

> The -0 (Negative Zero) is essentially the zero value, but with the sign bit on. So it is the negative representation of a zero.

```
var trendRate = -0;
trendRate === -0;             // true

trendRate.toString();         // "0"    OOPS!
trendRate === 0;              // true   OOPS!
trendRate < 0;                // false
trendRate > 0;                // false

Object.is(trendRate, -0);     // true
Object.is(trendRate, 0);      //false
```
> Note: When we toString() the -0 we got 0.

> Note: The triple equals operator ( === ) again lies to us, cuz it says the -0 is equal to a 0.

> Note: the < (less than sign) and the > (greater than sign) , also lie to us.

**Until ES6 they added a utility called Object.is(), and it doesn't lie at all. So the best way to do this is to use this built-in checker and by the way, object.is can be used to check NaNs.**

>The Object.is() method (ES6) determines whether two values are the same value. And the best way to check if -0 and 0 are the same or not.

>Note: The Object.is() also can be useful to check NaNs.

### Object.is()

The Object.is() behaves like the === operator with two differences:

- -0 and +0
- NaN

**Negative zero**

> The === operator treats -0 and +0 are the same value:

```
let amount = +0,
    volume = -0;
console.log(volume === amount);
Code language: JavaScript (javascript)
```

Output:

true

> However, the Object.is() treats +0 and -0 as different values. For example:

```
let amount = +0,
    volume = -0;
console.log(Object.is(amount, volume));
```

Output

false

**NaN**

> The === operator considers NaN and NaN are different values. The NaN is the only number that does not equal itself. For example:

```
let quantity = NaN;
console.log(quantity === quantity);
```

Output:

false

> However, Object.is() treats NaN as the same value:

```
let quantity = NaN;

console.log(Object.is(quantity, quantity)); //true
```
### Math.sign()

> The Math.sign() method retuns whether a number is negative, positive or zero.

> Syntax: Math.sign(x)

> Parameters: x A number. If this argument is not a number, it is implicitly converted to one.

> Return value: A number representing the sign of the given argument:

- If the argument is positive, returns 1.
- If the argument is negative, returns -1.
- If the argument is positive zero, returns 0.
- If the argument is negative zero, returns -0.
- Otherwise, NaN is returned.

```
Math.sign(-3);         // -1
Math.sign(3);          // 1
Math.sign(-0);         // -0   WTF?
Math.sign(0);          //  0   WTF?

// "fix" Math.sign(..)
function sign(v) {
    return v !== 0 ? Math.sign(v) : Object.is(v, -0) ? -1 : 1;
}

sign(-3);              // -1
sign(3);               // 1
sign(-0);              // -1
sign(0);               // 1

// Special Values: -0
```

### Fundamental Objects

> Fundamental Objects aka Built-In Objects aka Native Functions.

> So these are the ones where you really should absolutely use the new keyword:
Usage of the new keyword:

- Object()
- Array()
- Function()
- Date()
- RegExp()
- Error()

> If you need to construct an object of that fundamental type, then use new Object(), or new Array(), or new Function(). Probably the most useful one that would be use is new Date().
> But there are other ones that are fundamental objects which could be used with new, but you should definitely **not use** them with new keyword:

**Don't use with new keyword:🖐️**

- String()
- Number()
- Boolean()

## Coercion 💁‍♀ 

### ToPrimitive:

> If we have a `non-primitive` value, and we need to make it into a `primitive`, there the `abstract operation` is going to be involved in doing that.

By the way, the **abstract operations** they're not like a function that could somehow be called. There may, in fact, be actual methods inside of a JavaScript engine or not, they're not like required to be actual things. But when we call them abstract, we mean they're a conceptual operation. So any time you have something that is not a `primitive` and it needs to become a `primitive`, conceptually, what we need to do is this set of algorithmic steps, and that's called `ToPrimitive`, as if it were a function that could be invoked.

So the `ToPrimitive` abstract operation takes an optional type hint. So in other words, it says, if you have something that is not a `primitive`, tell what kind of type you would like it to be.

> The `ToPrimitive` abstract operation takes an optional type hint.

If you're doing a numeric operation and it invokes `ToPrimitive`, guess what hint it's gonna send in? It's gonna say, I would like to have a `number`. That doesn't guarantee you a `number`, by the way. It's just a hint to say, the place that I'm using it, I would like it to be a `number`. If you're doing something `string` based, guess what hint it's going to send in? It's going to send in `string`.

Those are basically the only two hints. It can say, I would like it to be a `number`, I would like it to be a `string`, or I'm not going to tell you at all, so just give me whatever `primitive` you can.

Another thing you need to understand about the algorithms within JavaScript is that they are inherently recursive, which means that they define something, for example to `ToPrimitive`. If the return result from `ToPrimitive` is not a `primitive`, if it's another `non-primitive`, like another object, then it's gonna get evoked again, and it's gonna keep getting invoked until we can get something that's an actual `primitive`, or in some cases get an error.

> The Abstract Operation algorithms within JavaScript are inherently recursive.

So `ToPrimitive`, the way it works, essentially, boiling down the algorithm, is that there are two methods that can be available on any `non-primitive` (any `object`, `function`, `array`, whatever...). There are these two functions, The `valueOf()` function and the `toString()` function. And this algorithm says, if you've told me that the hint is `number`, then I'm going to first try to invoke the `valueOf()`, if it's there, and see what it gives me. And if it gives me a `primitive`, then we're done. If it doesn't give me a `primitive`, or it doesn't exist, then we try the `toString()`. And we either get a `primitive`or not. And if we tried both of those (functions), and we don't get a `primitive`, generally that's gonna end up resulting in an error.

That's if the hint was `number`. If the hint was `string`, they just reverse the order that they consult them in, but they still essentially consult both of them. So if the hint is `string`, we would ask for that that `non-primitives`, `toString()` method, and if it has it, use what it returns. And if it gives us legitimately a `primitive` like a `string`, which it should, then we'll just use that. And then we'll try to `valueOf()`.

> The way the `ToPrimitive` abstract operation works, is with two methods that available on any `non-primitive`.
>
> - The `valueOf()` function
> - The `toString()` function
>
> If we told this algorithm that the hint is `number`, it first invoke the `valueOf()`, if it gives us a `primitive`, then it's done, if it doesn't give us a `primitive`, then it invoke `toString()` to get `primitive`. and if it tried both of those functions, and don't get a `primitive`, then gonna end up resulting in an error.
>
> If the hint was `string`, it invoke `toString()` method on the `non-primitives`, if it gives us a `primitive` like a `string` (which it should) then we'll just use that. if it doesn't then it'll try `valueOf()`, and if we don't get a `primitive`, then we it's end up resulting in an error.

> The other object conversion function is called `valueOf()`. The job of this method is less well-defined: it is supposed to convert an `object` to a `primitive` value that represents the `object`, if any such `primitive` value exists. `Objects` are compound values, and most `objects` cannot really be represented by a single `primitive` value, so the default `valueOf()` method simply returns the `object` itself rather than returning a `primitive`. Wrapper classes define `valueOf()` methods that return the wrapped `primitive` value. `Arrays`, `functions`, and `regular expressions` simply inherit the default method. Calling `valueOf()` for instances of these types simply returns the `object` itself. The Date class defines a `valueOf()` method that returns the date in its internal representation: the number of milliseconds since January 1, 1970:
>
> ```JavaScript
> var d = new Date(2010, 0, 1);   // January 1st, 2010, (Pacific time)
> d.valueOf();                    // => 1262332800000
> ```
>
> [JavaScript: The Definitive Guide](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) ( Page 50 | Chapter 3: Types, Values, and Variables )

> **Description (`valueOf`):**
>
> JavaScript calls the `valueOf` method to convert an object to a primitive value. You rarely need to invoke the `valueOf` method yourself; JavaScript automatically invokes it when encountering an object where a primitive value is expected.
>
> By default, the `valueOf` method is inherited by every object descended from `Object`. Every built-in core object overrides this method to return an appropriate value. If an object has no primitive value, `valueOf` returns the object itself.
>
> You can use `valueOf` within your own code to convert a built-in object into a primitive value. When you create a custom object, you can override `Object.prototype.valueOf()` to call a custom method instead of the default `Object` method.
>
> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf#Description)

So just keep in mind, if we're gonna use something that is not a `primitive` in some place that definitely needs `primitives`, like math or concatenation. We should realize, it is going to end up coercing it through this `ToPrimitive` algorithm, and it's gonna end up either invoking the `valueOf()` or the `toString()`.

> Briefly summarized, when converting from Object-to-String, the following steps are taken:
>
> 1. If available, execute the toString method.
>    - If the result is a primitive, return result, else go to Step 2.
> 2. If available, execute the valueOf method.
>    - If the result is a primitive, return result, else go to Step 3.
> 3. Throw TypeError.

### ToString:

The next abstract operation is `toString`. The `toString` abstract operation does what it sounds like. It takes any value and gives us the representation of that value in `string` form. And almost every value that you can imagine has at least some kind of representation in `string` form.

> The `toString` abstract operation takes any value and gives us the representation of that value in `string` form.

Some examples of things and what they end up producing as a string representation:

```JavaScript
         null   "null"
    undefined   "undefined"
         true   "true"
        false   "false"
      3.14159   "3.14159"
            0   "0"
           -0   "0"   // *

// Abstract Operations: ToString
```

> The `toString` operation produces a quote zero for negative zero. That's one of the corner cases.

> If we call `toString` on an `object`, it's going to invoke the `toPrimitive` abstract operation with `string` hint. Which is going to call `toString` first and if it's present and then it's going to use `valueOf`.

 **ToString (object):**
> Abstract Operations: ToString(Array/Object)

So what's gonna look like on some particular `object` like an `array`?

```JavaScript
                    []   ""
             [1, 2, 3]   "1,2,3"
     [null, undefined]   ","
    [[[], [], []], []]   ",,,"
                [,,,,]   ",,,"

// Abstract Operations: ToString(Array)
```

Arrays have a default `toString`, which is strange serializes the representation of the `array`. Because they're leaving off the brackets.

> If we serialized a empty `array`, you get an empty `string`.
> The built-in `toString` on `arrays` leaves off the brackets.

> If we have an `array` with some contents in it, it'll show those contents unless they're `null` and `undefined`. So the `nulls` and `undefines`, when they show up in `arrays` just get left out.
>
> They're not represented as `nulls` and `undefines` the way `null` and `undefine` when `toString` do.

What about on an `objects`:

```
{}   //"[object Object]"
{a: 2}  // "[object Object]"
{ toString() { return "X"; }}   //"X"

// Abstract Operations: ToString(Object)
```

> The default `toString` on the `Object.prototype` is to do that whole the square brackets thing, it does a lower case `object` and then it puts in this thing which is called the string tag.

And it turns out you can actually override the string tag for any of your own custom `objects` using an ES6 symbol.

> So that (capital O Object) `Object` is the default string tag for all default `objects`. And then the `toString` method takes that string tag and wraps this around it.

If you override the `toString` method, you can completely control what you want the stringtification of your `object` to look like. In this case, we are making it turn, return just a string X.

### ToNumber:

The `ToNumber` is a bit more interesting cuz there's a lot more corner cases involved.

> Anytime we need to do something numeric and we don't have a `number`, we're gonna invoke the `ToNumber` abstract operation.

```
 ""   0   // The root of all evil in JavaScript. *
"0"   0
 "-0"   -0
" 009 "   9
"3.14159"   3.14159
"0."   0
".0"   0
"."   NaN
"Oxaf"   175

// Abstract Operations: ToNumber
```

```
false   0
true   1
null   0   // *
undefined   NaN

// Abstract Operations: ToNumber
```

When we use `ToNumber` on a `non-primitive` (not a `string`, `undefined`, `boolean` or whatever), when we use it in an `object`, remember it invokes the `ToPrimitive` with the `number` hint. That consults first the valueOf, and then it consults the toString.

**ToNumber (object):**

> Abstract Operations: ToNumber(Array/Object)

So what does that look like?

> ##### (for [] and {} by default):
>
> ### **valueOf() { return this; }**
>
> ### **toString()**
>
> Abstract Operations: ToNumber(Array/Object)

> For any `array` or `object`, by default, meaning you have not overridden these, the `valueOf` method essentially just returns itself (does this, `return this`). Which has the affect of just ignoring the `valueOf` and deferring to `toString`.
>
> So it doesn’t even matter that the hint was number. It just goes directly to the toString.

You can think of the numberification of an `object` as, essentially, the stringification of it. It's that it's gonna end up producing whatever `toString` or `valueOf` produces. That's a perplexing choice, but it's the choice nonetheless, is that it's gonna actually produce a `primitive` `string`.

So then in your various operations where you were expecting a `primitive`, but you wanted a `primitive` `number`, there's actually a `primitive` `string` there. And then further coercions will kick in. So we're gonna end up deferring to the `toString` and whatever the `toString` returns.

> So with `ToNumber` we're gonna end up deferring to the `ToString` and whatever the `ToString` returns.

```JavaScript
           [""]   0   // *
          ["0"]   0
         ["-0"]   -0
         [null]   0   // *
    [undefined]   0   // *
      [1, 2, 3]   NaN
       [[[[]]]]   0   // *

// Coercion: ToNumber(Array)
```

If the `array` has either `null` or `undefined`, it becomes 0. Because they first become empty `strings`, and then empty `string` becomes `0`. Remember, empty `string` is the root of all coercion evil.

And if you have an object

```
{ .. }   NaN   // means {} or for example {x: 5}
{ valueOf() { return 3;}}   3

// Coercion: ToNumber(Object)
```

And remember what a stringification of an `object` by default is, it's that `[object Object]` thing. Which is definitely not a representation of a number, so we get `NaN`. If you override the `valueOf` for some `object`, you can return whatever thing you want.

> The stringification of `object` by default is `[object Object]`, Which is definitely not a representation of a `number`, so we get `NaN`.

### ToBoolean:

let's look at the `ToBoolean` abstract operation. And by the way, these four are what we're looking at, `toPrimitive`, `toString`, `toNumber`, and `toBoolean`. There are other abstract operations, but these are the major ones.

> Anytime we have any value that is not a `Boolean`, and it's used in a place that needs a `Boolean`, this operation occurs. Exactly the same as the other ones.

> The `ToBoolean` is less algorithmic and more lookup. So there's essentially a look up table.

There's not really anything to do, other than to say, is the value, what we call `falsy`, or not, that's really the only question here.

> If the value is one of these things (on look up table), return `false`. And otherwise just return `true`.

So it defines a very specific and short limited list of what we call `falsy` values.

> The values that will return `false` when coerced to a `Boolean`. These are the `falsy` values:
>
> - The empty `string`
> - either of the 0 (0, -0)
> - the `null`,
> - the `NaN`
> - the `false`
> - the `undefined`

| Falsy                              | Truthy                             |
| ---------------------------------- | ---------------------------------- |
| `""`                               | "foo"                              |
| `0,-0`                             | 23                                 |
| `null`                             | { a: 1 }                           |
| `NaN`                              | [1, 3]                             |
| `false`                            | `true`                             |
| `undefined`                        | function() {..}                    |
|                                    | ... (this list is infinitely long) |
| **Abstract Operations: ToBoolean** |                                    |

> If the value is not on that list, it is always truthy.

What would happen if you try to `toBoolean` an empty `array`? So is the empty `array` on the `falsy` the list? No, so it returns `truthy`

> The `ToBoolean`, it does not invoke the `toPrimitive` algorithm. Or the `toNumber`, or the `toString`, or anything, it just does a look up.

> when we're doing `toBooleans`, there's no other coercion stuff happening. It's just a straight look up, is it there or is it not.
>
> We can't override it with a `valueOf` or `toString` or anything. It's just is it on the list or is it not.

Essentially, memorize the falsy the list, and then always ask is the value on that list if so falsy, otherwise, it must be truthy.

### Cases of Coercion

> #### Converting Values:
>
> Converting a value from one type to another is often called `“type casting”`, when done `explicitly`, and `“coercion”` when done `implicitly` (forced by the rules of how a value is used).
>
> > It may not be obvious, but JavaScript coercions always result in one of the scalar primitive  values, like string, number, or boolean. There is no coercion that results in a complex value like object or function.“boxing,” which wraps scalar primitive values in their object counterparts, but this is not really coercion in an accurate sense.
>
> Another way these terms are often distinguished is as follows: `“type casting”` (or `“type conversion”`) occurs in statically typed languages at compile-time, while `“type coercion”` is a runtime conversion for dynamically typed languages.
>
> However, in JavaScript, most people refer to all these types of `conversions` as `coercion`, so the way I prefer to distinguish is to say `“implicit coercion”` versus `“explicit coercion”`.
>
> The difference should be obvious: `“explicit coercion”` is when it is obvious from looking at the code that a type conversion is intentionally occurring, whereas `“implicit coercion”` is when the type conversion will occur as a less obvious side effect of some other intentional operation.
>
> For example, consider these two approaches to `coercion`:
>
> ```JavaScript
> var a = 42;
> var b = a + "";        // implicit coercion
> var c = String( a );   // explicit coercion
> ```
>

Let's look at some examples where we're already doing coercion whether we realize it or not:

```
// ES6 Template literals (Template strings)

var numStudents = 16;

console.log(
  `There are ${numStrudents} students.`
);
// "There are 16 students."

// Coercion: number to string
```

> Overloaded operator: Defining or redefining how an operator (+, -, \*, /, etc.) acts.

> In JavaScript the `+` operator is overloaded to serve the purposes of both `number` addition and `string` concatenation.
>
> The plus operator (`+`) is normally thought of, is doing numerical operation.
>
> But with plus operator (`+`) if either one of them is a `string`, the plus operator prefers `string` concatenation.
>
> Which means, if only one of them is a `string`, it's gonna call a `toString` abstract operation on it, and turn it in to a `string`.

> We could throw a value into an `array`, just the one value into an `array`, and then call `.join` on it. And that actually ends up stringify it.
>
> ```JavaScript
> console.log([16].join(""));
> // "16"
> ```
>
> Even though it does no `string` concatenation at all, `.join` first turns it into a `string`.

Because we're dealing with web applications, which means grabbing things as `strings`:

```JavaScript
function addAStudent(numStudents) {
  return numStudents + 1;
}

addAStudent(studentsInputElem.value);
// "161"   OOPS!

// Coercion: string to number
```

> The plus operator (`+`) with `string` value (`+"6"` for example), invoke `toNumber` abstract operation.
>
> And if we add plus operator (`+`) to empty `string` value (+""), it end up to `0`.

```JavaScript
function addAStudent(numStudents) {
  return numStudents + 1;
}

addAStudent( + studentsInputElem.value);
// "17"

// Coercion: string to number
```

If we use the minus operator (`-`) that one is only defined for `numbers`.

That it's not overloaded for `string`, it wouldn't make any sense to subtract one `string` from another.

So that minus operator (`-`), is gonna invoke that `toNumber` abstract operation.

```JavaScript
function kickStudentOut(numStudents) {
  return numStudents - 1;
}

kickStudentOut(studentsInputElem.value);
// "15"

// Coercion: string to number
```

But what about `boolean`?

```JavaScript
if (studentsInputElem.value) {
  numStudents = Number(studentsInputElem.value)
}

// Coercion: __ to boolean
```

If `studentsInputElem.value` as an empty `string` that's gonna be `falsy`, But what if that `string` has just a bunch of white space, now it's gonna be `truthy`.
It's not a valid `string` that you care about because it's got a bunch of white space in it but all of a sudden it's going to be `truthy`.

```JavaScript
while (newStudents.length) {
  enrollStudent(newStudents.pop());
}

// Coercion: __ to boolean
```

So if my length is zero then it becomes `false` and if my length is anything non zero then it becomes `true`. Because it's not one of the zeros. But what happens when it's `NaN` it becomes `false`.

> The `Double NOT operator` or `Double negation` (`!!`) make things become a `boolean`.

> If wanna be super explicit, we can use:
>
> - `String()`
> - `Number()`
> - `Boolean()`

### Boxing

> Because of `boxing` in JavaScript, we are able to access properties on `primitive` values.
> For example access a length on a primitive `string` or some method on a primitive `number`.
>
> The `boxing` is a form of `implicit` coercion.
> It's not called out in the same way in the **abstract operations**.

> This DOM elements value is always a `string`.

It is saying you have this thing that is not an `object` and you're trying to use it as if it is an `object`. So JavaScript is gonna be helpful and go ahead and make it into an `object` for us.
The only other option would be for the JavaScript to throw an exception that said you're trying to access a property on an `primitive` value.

But fortunetly JavaScript `implicitly` coerces these `primitives` into their `object` counterpart so that we can access properties and methods on them.

> Because of the `boxing` most of people think “everything in JavaScript is an `object`”.
>
> It turns out that things can behave as `objects`, but that doesn't make them an `object`

> ### All programming languages have `type conversions`, because it's absolutly necessary.

> Whether we call them `coercion` or we call them `conversion` every single language in existence that we've ever programmed in has to deal with `type conversions`.

### Corner Case of Coercion

> Because all languages have `type conversions`, that means all languages have `corner cases`, including JavaScript.

Here's an example of some of these corner cases:

```JavaScript
Number("");                     //   0                    OOPS!
Number("   \t\n");              //   0                    OOPS!
Number(null);                   //   0                    OOPS!
Number(undefined);              //   NaN
Number([]);                     //   0                    OOPS!
Number([1, 2, 3]);              //   NaN
Number([null]);                 //   0                    OOPS!
Number([undefined]);            //   0                    OOPS!
Number({})                      //   NaN

String(-0);                     //   "0"                  OOPS!
String(null);                   //   "null"
String(undefined);              //   "undefined"
String([null]);                 //   ""                   OOPS!
String([undefined]);            //   ""                   OOPS!

Boolean(new Boolean(false));    //   true                 OOPS!


Coercion: corner cases
```

The root of all (Coercion) Evil:

```JavaScript
studentsInput.value = "";

// ..

Number(studentsInput.value);            //   0

studentsInput.value = "   \t\n";

// ..

Number(studentsInput.value);            //   0

// Coercion: corner cases
```

Not only does the empty `string` become zero, but any `string` that's full of white space also becomes zero.

Because the `toNumber` operations first strips off all leading and trailing `whitespace` before doing it’s `coercion`. So all examples of `whitespace` strings of all forms, still all end up producing that same `zero`.

There are also corner cases that are not as obvious:

```JavaScript
Number(true);              //   1
Number(false);             //   0

1 < 2;                     //   true
2 < 3;                     //   true
1 < 2 < 3;                 //   true      (but...)

(1 < 2) < 3;
(true) < 3;
1 < 3;                    //    true      (hmm...)

// *************************************

3 > 2;                     //   true
2 > 1;                     //   true
3 > 2 > 1;                 //   false      OOPS!

(3 > 2) > 1;
(true) > 1;
1 > 1;                     //   false

// Coercion: corner cases
```

## JavaScript's dynamic typing is not a weakness, it's one of its strong qualities.🥳









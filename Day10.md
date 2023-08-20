
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

## Coercion 💁‍♀ 🔜
### Abstract Operations
### toString
### toNumber
### toBoolean️
### Cases of Coercion
### Boxing
### Corner Case of Coercion

## Philosophy of Coercion 💁‍♀
### Intentional Coercion
### Culture of Learning
### Code Communication Q&A
### Implicit Coercion
### Understanding Features
### Coercion Exercise









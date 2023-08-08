
# Day 4🧑‍💻

## Functions
   > A JavaScript function is a block of code designed to perform a particular task.
   
   >📃 functions do things 
   
### declaring (creating) a function:
```
function half(x) {
    return x / 2;
}
```
### calling (using) a function:
```
const one = half(2);
```
### Parameters & Arguments
```
function add(x, y){
	return x + y
}

add(2, 3)
```
> A **parameter** is one of the variables in a function. And when a method is called, the **arguments** are the data you pass into the method's parameters.

> `x` and `y` are the **parameters** while `2` and `3` are the **arguments** here

### Function Can😉 / Can Not 🙅 :
✅   Some functions don't even need any values 
```
function getRandomNumber() {
    return Math.random();
}

getRandomNumber();
```

✅  Parameters should be named like variables, and behave like variables within the function body
```
function howAboutThis(1weirdVariable!) {
    return true;
}
```
❌  Parameter can not  be constant
```
🙅 function howAboutThis(1weirdVariable!) {
    return true;
}
```
✅  if we don't call a function with the intended argument(s)
```
function add3(x, y, z) {
    console.log("My parameters are named x, y, z");
    console.log("I received the arguments", x, y, z);
    return x + y + z;//NAN
    //4+5+undefined
}
```

### Return values
>  A `return` statement specifies the function's output value.

```
function square(x) {
    return x * x; //3*3=9
    
 }
 
 const nine = square(3);//9
```
### Functions don't return anything 
> if a function's execution doesn't end at a return statement, or if the return keyword doesn't have an expression after it, then the return value is **undefined**

```
function sayHello(name) {
    console.log("Oh hi, " + name + "!");
}
const hm = sayHello("Marc");//undefined
```

### Arrow functions
>Arrow functions allow us to write shorter function syntax:
```
let myFunction = (a, b) => a * b;
```

>Since arrow functions are expressions, we can assign them to a variable

```
const add = (x, y) => x + y;
```
**is equivalent to ↕️↕️**

```
function add(x, y) {
    return x + y;
}
```

> It gets shorter! If the function has only one statement, and the statement returns a value, you can remove the brackets and the return keyword:

```
hello = () => "Hello World!";
```

> if you have only one parameter, you can skip the parentheses as well

```
hello = val => "Hello " + val;
```

## Scope 
> Scopes are nested within the program
The widest scope is the global scope
Each function gets its own new scope within the scope where it was declared

```
let planet = "Jupiter";

function scopeOut() {
    let planet = "Mars";
    console.log("Inner planet:", planet);
}

scopeOut();
console.log("Outer planet:", planet);
```

> Within each scope, you can access variables declared in a wider scope (e.g. global scope)
But not those declared in a narrower scope (e.g. function scope)

>Variables declared with let can be modified from within a narrower scope This can be useful, but also dangerous!

```
let feeling = "free";
function trap() {
    feeling = "boxedIn";
}
trap();
console.log(feeling);//boxedIn
```

## Events & Handlers
> The web browser fires events when certain things happen on the page

>We can detect events with JS using an event listener
The .addEventListener() method lets us listen for events on a DOM element

```
document.addEventListener("click", () => {
    console.log("clicked")
});
```
### .addEventListener() takes 2 parameters:

1. The name of the event to listen to (e.g. "click")
2. A handler function that JS calls when that event is fired on this element

>**JS passes an event object to the handler function with information about the eventIf we accept this as a parameter, we can use it to get details**

```
document.addEventListener("click", (event) => {
    console.log(event);
});

```
> **event.target is the element the event fired on(in this case, which element was clicked)**
```
document.addEventListener("click", (event) => {
    console.log(event.target);
});
```

### "click" isn't the only type of event we can handle

➡️"dblclick"
➡️"mouseover"
➡️"mouseout"
👍...and lots more!


## Quiz Project
**Code :**
```
 <script type="text/javascript">
    // TODO 4: Declare disable & enable functions to set or remove the "disabled" attribute from a given button element
    // disable(button) should set the button element's attribute "disabled" to the value ""
    const disable = (button) => button.setAttribute("disabled","")

    // enable(button) should remove the attribute "disabled" from the button element
    const enable = (button) => button.removeAttribute("disabled")

    // TODO 5: Declare an isCorrect function that compares a guess to the right answer
    // isCorrect(guess) should return true if the guess matches the fact's answer
    function iscorrect(answer) {
      return fact.answer.toString() === answer;
    }
  </script>
```

## Coding Exercises

**QUESTION #1**
>Using let or const, declare a global variable named myGlobal outside of any function. Initialize it with a value of 10.
Inside function fun1, assign 5 to oopsGlobal without using the var, let or const keywords.

```
// Declare the myGlobal variable below this line
let myGlobal = 10;

function fun1() {
  // Assign 5 to oopsGlobal here
    oopsGlobal = 5;
}

// Only change code above this line

function fun2() {
  let output = "";
  if (typeof myGlobal != "undefined") {
    output += "myGlobal: " + myGlobal;
  }
  if (typeof oopsGlobal != "undefined") {
    output += " oopsGlobal: " + oopsGlobal;
  }
  console.log(output);
}
```
    
**QUESTION #2**
> The editor has two console.logs to help you see what is happening. Check the console as you code to see how it changes. Declare a local variable myVar inside myLocalScope and run the tests.

```
function myLocalScope() {
  // Only change code below this line
  let myVar = "sajida"
  console.log('inside myLocalScope', myVar);
}
myLocalScope();

// Run and check the console
// myVar is not defined outside of myLocalScope
console.log('outside myLocalScope', myVar);
```
    
**QUESTION #3**
> Add a local variable to myOutfit function to override the value of outerWear with the string sweater.

```
// Setup
const outerWear = "T-Shirt";

function myOutfit() {
  // Only change code below this line
   const outerWear = "sweater"
  // Only change code above this line
  return outerWear;
}

myOutfit();
```
**QUESTION #4**
>  Write a function nextInLine which takes an array (arr) and a number (item) as arguments.
Add the number to the end of the array, then remove the first element of the array.
The nextInLine function should then return the element that was removed.

```
function nextInLine(arr, item) {
  // Only change code below this line
  arr.push(item);
  
  return arr.shift();
  // Only change code above this line
}

// Setup
let testArr = [1, 2, 3, 4, 5];

// Display code
console.log("Before: " + JSON.stringify(testArr));
console.log(nextInLine(testArr, 6));
console.log("After: " + JSON.stringify(testArr));
```

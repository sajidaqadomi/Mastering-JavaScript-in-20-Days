
# Day 7 🥳‍💻
# **[JavaScript the Hard Parts](https://frontendmasters.com/courses/javascript-hard-parts-v2/promises-example-then/)** 🔥🔥

## JavaScript principles
**Thread of execution**
: Goes through the code line-by-line and runs/ ’executes’ each line

**Functiions**
: Code we save (‘define’) functions & can use (call/invoke/execute/run) later with the function’s name & ( ).

**Execution context**
: Created to run the code of a function - has 2 parts (we’ve already seen them!)
- Thread of execution 
- Memory

**Call stack**
- JavaScript keeps track of what function is currently running (where’s the thread of execution)
- Run a function - add to call stack
- Finish running the function - JS removes it from call stack
- Whatever is top of the call stack 
  - that’s the function we’re currently running

## 2. Callbacks & Higher order functions
**Higher order functions**
: The outer function that takes in a function

**Callback Function**
: The function we insert

>Functions in javascript = first class objects
They can co-exist with and can be treated like any other javascript object

1. Assigned to variables and properties of other objects
2. Passed as arguments into functions
3. Returned as values from functions

```
function copyArrayAndManipulate(array, instructions) {
 const output = [];
 for (let i = 0; i < array.length; i++) {
 output.push(instructions(array[i]));
 }
 return output;
}
function multiplyBy2(input) { return input * 2; }
const result = copyArrayAndManipulate([1, 2, 3], multiplyBy2);
```

**Callbacks and Higher Order Functions simplify our code and keep it DRY** 🔂
- **Declarative readable code:** Map, filter, reduce - the most readable way to write code to work with data
- **Codesmith & pro interview prep:** One of the most popular topics to test in interview both for Codesmith and mid/senior level job interviews
- **Asynchronous JavaScript:** Callbacks are a core aspect of async JavaScript, and are under-the-hood of promises, async/await

## arrow functions
> a shorthand way to save functions

```
function multiplyBy2(input) { return input * 2; }
const multiplyBy2 = (input) => { return input*2 }
const multiplyBy2 = (input) => input*2
const multiplyBy2 = input => input*2
const output = multiplyBy2(3) //6
```

**We can even pass in multiplyBy2 directly without a name**
But it’s still just the code of a function being passed into copyArrayAndManipulate

```
function copyArrayAndManipulate(array, instructions) {
 const output = [];
 for (let i = 0; i < array.length; i++) {
 output.push(instructions(array[i]));
 }
 return output;
}
//const multiplyBy2 = input => input*2            👎
const result = copyArrayAndManipulate([1, 2, 3], input => input*2);
```

### Anonymous and arrow functions

**This is a named function, aka a function declaration**
```
function brag(count) {
     return("I can do " + count + " pushups");
}
```

**This is an anonymous function, aka a function expression**
```
var brag = function(count) {
     return("I can do " + count + " pushups");
} 

console.log(brag(3)) // I can do 3 pushups
console.log(brag(3)) // I can do 3 pushups
```

**This is an arrow function, a special type of function expression.**

```
var brag = (count) => ("I can do " + count + " pushups");

console.log(brag(3)) // I can do 3 pushups
```
> It's still a function expression because everything to the right of the = is a value that we assign to the variable brag.
Note that (1) there's no curly braces used to define the code block, and (2) there's also no return statement. That's because an arrow function has implicit return, meaning the value is returned automatically. You don't actually need any parentheses either, but I left them in because they make the code more readable.

**Why would you use an anonymous function instead of a named function?**
>Sometimes you don't need to name a function because you're just going to use it as a callback to another function. Since you're not using it again elsewhere, it doesn't need a name.

> `For example`, here we're using a named function called 'brag' (also known as a function declaration):

```
function brag(count) {
     return("I can do " + count + " pushups");
} 

console.log(brag(3)) // I can do 3 pushups
```

> ...but we could just as well make it anonymous, like so:

```
console.log(function(count) {
     return("I can do " + count + " pushups");
} (3)) // I can do 3 pushups
```

## Closure (scope and execution context)
>  Closure is the most esoteric of JavaScript concepts
>  Enables powerful pro-level functions like ‘once’ and ‘memoize’
>  Many JavaScript design patterns including the module pattern use closure
>  Build iterators, handle partial application and maintain state in an 
asynchronous world

**Functions get a new memory every run/invocation**
```
function multiplyBy2 (inputNumber){
const result = inputNumber*2;
return result;
}
const output = multiplyBy2(7);
const newOutput = multiplyBy2(10);

```

**Functions with memories**
- When our functions get called, we create a live store of data (local 
memory/variable environment/state) for that function’s execution context.
- When the function finishes executing, its local memory is deleted (except the returned value)
- But what if our functions could hold on to live data between executions? 
- This would let our function definitions have an associated cache/persistent memory
- But it all starts with us returning a function from another function

**Functions can be returned from other functions in JavaScript**
```
function createFunction() {
 function multiplyBy2 (num){
 return num*2;
 }
 return multiplyBy2;
}
const generatedFunc = createFunction();
const result = generatedFunc(3); // 6

```

**Calling a function in the same function call as it was defined**
```
function outer (){
 let counter = 0;
 function incrementCounter (){
 counter ++;
 }
 incrementCounter();
}
outer();
```

**Calling a function outside of the function call in which it was defined**
```
function outer (){
 let counter = 0;
 function incrementCounter (){ counter ++; }
 return incrementCounter;
}
const myNewFunction = outer();
myNewFunction();
myNewFunction();
```

> When a function is defined, it gets a bond to the surrounding Local Memory (“Variable Environment”) in which it has been defined

**The ‘backpack’**
- We return incrementCounter’s code (function definition) out of outer into 
global and give it a new name - myNewFunction
- We maintain the bond to outer’s live local memory - it gets ‘returned out’ 
attached on the back of incrementCounter’s function definition.
- So outer’s local memory is now stored attached to myNewFunction - even 
though outer’s execution context is long gone
- When we run myNewFunction in global, it will first look in its own local 
memory first (as we’d expect), but then in myNewFunction’s ‘backpack’

**What can we call this ‘backpack’?**
- Closed over ‘Variable Environment’ (C.O.V.E.)
- Persistent Lexical Scope Referenced Data (P.L.S.R.D.)
- ‘Backpack’
- ‘Closure’

The ‘backpack’ (or ‘closure’) of live data is attached incrementCounter (then to myNewFunction) through a hidden property known as [[scope]] which persists when the inner function is returned out

```
//Let’s run outer again
function outer (){
 let counter = 0;
 function incrementCounter (){
 counter ++;
 }
 return incrementCounter;
}

const myNewFunction = outer();
myNewFunction();//1
myNewFunction();//2
const anotherFunction = outer();
anotherFunction();//1
anotherFunction();//2
```

**Individual backpacks**
>If we run 'outer' again and store the returned 'incrementCounter' function 
definition in 'anotherFunction', this new incrementCounter function was created in a new execution context and therefore has a brand new independent backpack

**Closure gives our functions persistent memories and entirely new toolkit for writing professional code**

- Helper functions: Everyday professional helper functions like ‘once’ and ‘memoize’
-Iterators and generators: Which use lexical scoping and closure to achieve the most contemporary patterns for handling data in JavaScript
- Module pattern: Preserve state for the life of an application without polluting the global namespace
- Asynchronous JavaScript: Callbacks and Promises rely on closure to persist state in an asynchronous environment

📖 Another reference I recommend **[https://www.freecodecamp.org/news/lets-learn-javascript-closures-66feb44f6a44/](https://www.freecodecamp.org/news/lets-learn-javascript-closures-66feb44f6a44/)** 💁‍♀️ 
## Coding Exercises 🔜 💁‍♀️ 

🔜 
  

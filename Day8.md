
# Day 8 💻 🥳

# **[JavaScript the Hard Parts](https://frontendmasters.com/courses/javascript-hard-parts-v2/promises-example-then/)** 🔥🔥

## Promises, Async & the Event Loop

> JavaScript is: 
- Single threaded (one command runs at a time)
- Synchronously executed (each line is run in order the code appe

**Our core JavaScript engine has 3 main parts:**

- Thread of execution
- Memory/variable environment
- Call stack

**We need to add some new components:**

- Web Browser APIs/Node background APIs
- Promises
- Event loop, Callback/Task queue and micro task queue

**ES5 solution: Introducing ‘callback functions’, and Web Browser APIs**

> Since JavaScript is a single-threaded programming language with a synchronous execution model that processes one operation after another, it can only process one statement at a time. However, an action like requesting data from an API can take an indeterminate amount of time, depending on the size of data being requested, the speed of the network connection, and other factors. If API calls were performed in a synchronous manner, the browser would not be able to handle any user input, like scrolling or clicking a button, until that operation completes. This is known as blocking.

> In order to prevent blocking behavior, the browser environment has many Web APIs that JavaScript can access that are asynchronous, meaning they can run in parallel with other operations instead of sequentially. This is useful because it allows the user to continue using the browser normally while the asynchronous operations are being processed.

### The Event Loop:

> how JavaScript handles asynchronous code with the event loop. 
> There are two elements of the event loop: **the stack** and **the queue**.

**JavaScript code that does not use any asynchronous Web APIs will execute in a synchronous manner—one at a time, sequentially**

```
function first() {
  console.log(1)
}

function second() {
  console.log(2)
}

function third() {
  console.log(3)
}

// Execute the functions
first()
second()
third()

//output
//1
//2
//3
```
🏃‍♀️ 
💁‍♀️ Add `first()` to the stack, ▶️ run `first()` which logs 1 to the console, 📤 `remove` first() from the stack.

💁‍♀️ Add `second()` to the stack,▶️ run `second(`) which logs 2 to the console, 📤remove `second(`) from the stack.

💁‍♀️Add `third()` to the stack,▶️ run`third()` which logs 3 to the console,📤 remove `third()` from the stack.

**When an asynchronous Web API is used. A built-in API that you can test this with is setTimeout, which sets a timer and performs an action after a specified amount of time. setTimeout needs to be asynchronous, otherwise the entire browser would remain frozen during the waiting, which would result in a poor user experience.**

```
// Define three example functions, but one of them contains asynchronous code
function first() {
  console.log(1)
}

function second() {
  setTimeout(() => {
    console.log(2)
  }, 0)
}

function third() {
  console.log(3)
}

// Execute the functions
first()
second()
third()

//Output
//1
//3
//2
```

> Whether you set the timeout to zero seconds or five minutes will make no difference—the console.log called by asynchronous code will execute after the synchronous top-level functions.

> This happens because the JavaScript host environment, in this case the browser, uses a concept called the event loop to handle concurrency, or parallel events. Since JavaScript can only execute one statement at a time, it needs the event loop to be informed of when to execute which specific statement. 

> Using setTimeout, an asynchronous Web API, introduces the concept of the **queue**
> The event loop handles this with the concepts of **a stack and a queue**.

💁‍♀️ Add first() to the stack, run first() which logs 1 to the console, remove first() from the stack.

💁‍♀️ Add second() to the stack, run second().

✋  Please   wait   🔥

 Add setTimeout() to the stack, run the setTimeout() Web API which starts a timer and 
 💁‍♀️adds the `anonymous function` to the **queue**, remove setTimeout() from the stack.
Remove second() from the stack.


💁‍♀️ Add third() to the stack, run third() which logs 3 to the console, remove third() from the stack.

✋  Please   wait   🔥
🔎 The event loop **checks the queue** for any pending messages and finds the `anonymous function` from setTimeout(), adds the function to the stack which logs 2 to the console, then removes it from the stack.

### Stack

>The stack, or call stack, holds the state of what function is currently running.
you can imagine it as an array with “Last in, first out” **(LIFO)** properties, meaning you can only add or remove items from the end of the stack.

### Queue

**Note:** There is also another queue called the **job queue** or **microtask queue** that handles promises. Microtasks like promises are handled at a higher priority than macrotasks like setTimeout.

>The queue, also referred to as message queue or task queue, is a waiting area for functions. Whenever the call stack is empty, the event loop will check the queue for any waiting messages, starting from the oldest message. Once it finds one, it will add it to the stack, which will execute the function in the message.

### Callback Functions:

>they are just a function that has been passed as an argument to another function. The function that takes another function as an argument is called a higher-order function. According to this definition, any function can become a callback function if it is passed as an argument. 

```
// A function
function fn() {
  console.log('Just a function')
}

// A function that takes another function as an argument
function higherOrderFunction(callback) {
  // When you call a function that is passed as an argument, it is referred to as a callback
  callback()
}

// Passing a function
higherOrderFunction(fn)
```

**Callbacks are not asynchronous by nature, but can be used for asynchronous purposes.**

```
// Define three functions
function first() {
  console.log(1)
}

function second(callback) {
  setTimeout(() => {
    console.log(2)

    // Execute the callback function
    callback()
  }, 0)
}

function third() {
  console.log(3)
}
```

### Promises

> A promise represents the completion of an asynchronous function.
It is an object that might return a value in the future.
It accomplishes the same basic goal as a callback function, but with many additional features and a more readable syntax. 

**Creating a Promise**
> You can initialize a promise with the new Promise syntax, and you must initialize it with a function. The function that gets passed to a promise has resolve and reject parameters. The resolve and reject functions handle the success and failure of an operation, respectively.

Write the following line to declare a promise:

```
// Initialize a promise
const promise = new Promise((resolve, reject) => {})
```

```
const promise = new Promise((resolve, reject) => {
  resolve('We did it!')
})
```

**A promise can have three possible states:**
1. pending
2. fulfilled 
3. rejected

**Then for accessing a Promise**

> Promises have a method called then that will run after a promise reaches resolve in the code. then will return the promise’s value as a parameter.

This is how you would return and log the value of the example promise:

```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('Resolving an asynchronous request!'), 2000)
})

// Log the result
promise.then((response) => {
  console.log(response)
})
```

### Using the Fetch API with Promises
> One of the most useful and frequently used Web APIs that returns a promise is the Fetch API, which allows you to make an asynchronous resource request over a network. fetch is a two-part process, and therefore requires chaining then. 

> This example demonstrates hitting the GitHub API to fetch a user’s data, while also handling any potential error:

```
// Fetch a user from the GitHub API
fetch('https://api.github.com/users/octocat')
  .then((response) => {
    return response.json()
  })
  .then((data) => {
    console.log(data)
  })
  .catch((error) => {
    console.error(error)
  })
```

The fetch request is sent to the **https://api.github.com/users/octocat** URL, which asynchronously waits for a response. The first then passes the response to an anonymous function that formats the response as JSON data, then passes the JSON to a second then that logs the data to the console. The catch statement logs any error to the console.

### Async Functions with async/await

> An async function can handle a promise called within it using the await operator. await can be used within an async function and will wait until a promise settles before executing the designated code.

```
// Handle fetch with async/await
async function getUser() {
  const response = await fetch('https://api.github.com/users/octocat')
  const data = await response.json()

  console.log(data)
}

// Execute async function
getUser()
```

### We have rules for the execution of our asynchronously delayed code

- Hold promise-deferred functions in a microtask queue and callback function in a 
task queue (Callback queue) when the Web Browser Feature (API) finishes

- Add the function to the Call stack (i.e. run the function) when: 
Call stack is empty & all global code run (Have the Event Loop check this condition)

- Prioritize functions in the microtask queue over the Callback queue


## Coding Exercises  💁‍♀️ 

**QUESTION #1**

> Write a closure named createCounter that takes an initial value start and returns a 
function. The returned function, when invoked, should increment the counter by 1 and return the updated value.

```
function createCounter(initvalue){
    let counter = initvalue;
    function incrementCounter(params) {
        return counter+1;
    }
    return incrementCounter;
}

let incrementCounter =createCounter(4);
console.log(incrementCounter);
```

**QUESTION #2**

> Write a closure named calculateAverage that takes an array of numbers, nums, and returns a 
 function. The returned function, when invoked, should calculate and return the average of the numbers in the array.
 
 ```
function calculateAverage(numbers){

     const avarage = () =>  numbers.reduce((acc,item)=> item+acc,0)/numbers.length
     return avarage;   
    
}
```

**QUESTION #3:**

> Write a closure named powerOf that takes a base number base and returns a function. The returned function, when invoked with an exponent exp, should calculate and return the result of base raised to the power of exp.

```
function powerOf(baseNumber){
    const power = (exp) =>  Math.pow(baseNumber,exp)
    return power;   
}

```

**QUESTION #4:**

> Write a closure named compose that takes multiple functions as arguments and returns a new function. The returned function should apply the provided functions in reverse order, passing the result of each function as an argument to the next function.

```
function compose(...funcs){
    //here I assume init argument=0;
    function applyFunctions(){
        return funcs.reduceRight((applyedResult, f) => f(applyedResult), 0);
    }
 
}
```


# Day 6🧑‍💻

## API & fetch
> APIs provide URLs that point at data we care about

```
https://dog.ceo/api/breed/hound/list

  {
    "message": [
      "afghan",
      "basset",
      "blood",
      "english",
      "ibizan",
      "plott",
      "walker"
    ],
    "status": "success"
  }
 ```
 
> The fetch() method starts the process of fetching a resource from a server or **load data from APIs**

> The fetch() method returns a Promise that resolves to a Response object.

**Sending a Request**

> The fetch() requires only one parameter which is the URL of the resource that you want to fetch

>It takes time to fetch data from the network ➡️ Promises

**Promises can be in 3 possible states:**

1. **pending**: still waiting for the value, hang tight
2. **fulfilled** (aka "resolved"): finally got the value, all done
3. **rejected**: sorry couldn't get the value, all done

> The fetch() method returns a Promise so you can use the then() and catch() methods to handle it:

```
 fetch("https://dog.ceo/api/breed/hound/list")
    .then(response => {
        // handle the response
        response.text()
    })
    .catch(error => {
        // handle the error
        console.log(erroe)
    });
```
> await lets us tell JS to stop and wait for an asynchronous operation to finish

> In practice, you often use the **async/await** with the **fetch()** method like this:

```
async function fetchText() {
    let response = await fetch('/readme.txt');
    let data = await response.text();//Calling the .json() method on the response parses its body as a JSON object and it is gives us another Promise!💁‍♀️
    
    console.log(data);
}
```

## Destructuring :
> Destructuring assignment is a special syntax that allows us to “unpack” arrays or objects into a bunch of variables, as sometimes that’s more convenient.

### **Array destructuring**
> Here’s an example of how an array is destructured into variables:

```
// we have an array with the name and surname
let arr = ["John", "Smith"]

// destructuring assignment
// sets firstName = arr[0]
// and surname = arr[1]
let [firstName, surname] = arr;

alert(firstName); // John
alert(surname);  // Smith
```
**Skip Items**

> 💡 You can skip unwanted items in an array without assigning them to local variables. For example, 
```
const arrValue = ['one', 'two', 'three'];

// destructuring assignment in arrays
const [x, , z] = arrValue;

console.log(x); // one
console.log(z); // three
```
> In the above program, the second element is omitted by using the comma separator ,.

**spread syntax ...**

> 💡 You can assign the remaining elements of an array to a variable using the spread syntax .... For example,

```
const arrValue = ['one', 'two', 'three', 'four'];

// destructuring assignment in arrays
// assigning remaining elements to y
const [x, ...y] = arrValue;

console.log(x); // one
console.log(y); // ["two", "three", "four"]
```
### **Object destructuring**

> **Note:** The order of the name does not matter in object destructuring 🌐

> **Note:** When destructuring objects, you should use the **same name** for the variable as the corresponding object key.🌐

```
// assigning object attributes to variables
const person = {
    name: 'Sara',
    age: 25,
    gender: 'female'    
}

// destructuring assignment
let { name, age, gender } = person;
```
## async function
> This tells JS to expect to await async operations inside the function

```
async function fetchResponse(url) {
    const response = await fetch(url);
    return response;
}
```

## Modules:

> Modules let us split big codebases across multiple files

> Module is a file that contains code to perform a specific task. A module may contain variables, functions, classes etc. Let's see an example,
Suppose, a file named greet.js contains the following code:

```
// exporting a function
export function greetPerson(name) {
    return `Hello ${name}`;
}
```

> Now, to use the code of greet.js in another file, you can use the following code:

```
// importing greetPerson from greet.js file
import { greetPerson } from './greet.js';

// using greetPerson() defined in greet.js
let displayName = greetPerson('Jack');

console.log(displayName); // Hello Jack
```

### import && export

> export lets us expose variables from our module's scope to the outside world

// myModule.js

```
const veryUsefulFunction = () => "I came from a module";
export { veryUsefulFunction };
```

> import lets us use an exposed variable from another module

```
// otherModule.js
import { veryUsefulFunction } from './myModule.js'

veryUsefulFunction();
```

## Debugging

- console.log() (or .warn() or .error()) is one way to understand what's happening when your program runs

```
function whyIsntThisWorking(input) {
    console.log("Well at least we got this far");
    console.log(input);
    return thingThatDoesntWork(input);
}
```

- Use the browser's debugger to pause JS and inspect what's happening

> The debugger statement creates a breakpoint where JS will pause and let you look around

```
function whyIsntThisWorking(input) {
    debugger;
    return thingThatDoesntWork(input);
} 
```

## Error handling
> Usually errors will cause JS to stop running our code

> Sometimes that's appropriate and what we want JS to do

>we might want to try again, or try a different way

> Or if it was optional, just skip it and move on with our (program's) lives

```
thisThrowsAnError();
console.log("I'll never get here");
```


```
try {
    thisMightThrowAnError();
} catch (error) {
    console.error("As if! Error:", error); 
    console.log("Whatever, let's press on anyway");
}
console.log("still rollin' with the homies");
```

## Coding Exercises

**QUESTION #1**
> [Create a web page that fetches data from the Rick and Morty API, and displays a list of characters.](https://github.com/orjwan-alrajaby/gsg-QA-Nablus-training-2023/blob/main/learning-sprint-1/week1%20-%20javascript-from-first-steps-to-professional/day%206/task.md)

**Solution**
Live Link :
[https://sajidaqadomi.github.io/Day6-task/](https://sajidaqadomi.github.io/Day6-task/)

```
const ListContainer = document.getElementById("characterList");

async function fetchCharechters() {
  try {
    const Charecters = await fetch("https://rickandmortyapi.com/api/character/?status=alive");
    const response = await Charecters.json();

    renderUI(response.results);

  } catch (error) {
    ListContainer.innerHTML = `<li class="error-message"> Something Went Wrong ❌ </li>`;
  }
}

function renderUI(items) {
  let charecterItems = "";
  const itemsLength = items.length;

  itemsLength > 50
    ? items.slice(0, 51)
    : itemsLength > 0
    ? items.forEach((item) => {
        charecterItems += `<li class="charecter-item">
    <img src="${item.image}" alt=${item.name} />
     <div class="charecter-info">
       <div class="charecter-info-item">
       <span class="label">Name:
       </span><span>${item.name}</span>
       </div>
       <div class="charecter-info-item">
       <span class="label">Gender:</span>
       <span>${item.gender}</span>
       </div>
       <div class="charecter-info-item">
       <span class="label">Species: </span>
       <span>${item.species}</span>
       </div>
       <div class="charecter-info-item">
       <span class="label">Location: </span>
       <span><a href="${item.location.url}">${item.location.url}</a></span>
       </div>
     </div>
     </li>`;
      })
    : `<li class="empty-characters">There is no any  characters 🥹🥹🥹</li>`;

  ListContainer.innerHTML = charecterItems;
}

fetchCharechters();

```

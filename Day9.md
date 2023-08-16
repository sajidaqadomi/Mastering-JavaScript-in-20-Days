
# Day 9💻
# **[JavaScript the Hard Parts](https://frontendmasters.com/courses/javascript-hard-parts-v2/promises-example-then/)** 🔥🔥

## Classes & Prototypes 🔎🔎

### Class & OOP Introduction 📃

#### Object-Oriented Programming 

>is a programming style based on classes and objects. These group data (properties) and methods (actions) inside a box.

> OOP was developed to make code more flexible and easier to maintain.

> JavaScript is prototype-based procedural language, which means it supports both functional and object-oriented programming.

#### JavaScript Objects

>A javaScript object is an entity having state and behavior (properties and method). For example: car, pen, bike, chair, glass, keyboard, monitor etc.

#### JavaScript Classes
> Classes are one of the features introduced in the ES6 version of JavaScript.

> A class is a blueprint for the object. You can create an object from the class.

> You can think of the class as a sketch (prototype) of a house. It contains all the details about the floors, doors, windows, etc. Based on these descriptions, you build the house. House is the object.

> Since many houses can be made from the same description, we can create many objects from a class.

---
### Creating Objects in JavaScript

**There are 3 ways to create objects.**
1. By object literal
    ```
    let emp={id:102,name:"Shyam Kumar",salary:40000}  
    ```
2. By creating instance of Object directly (using new keyword)
    ```
    var emp=new Object();  
    emp.id=101;  
    emp.name="Ravi Malik";  
    emp.salary=50000;  
    ```
3. By using an object constructor (using new keyword)

    Here, you need to create function with arguments. Each argument value can be assigned in the current object by using this keyword.
    
    ```
    function emp(id,name,salary){  
    this.id=id;  
    this.name=name;  
    this.salary=salary;  
    }  
    let e=new emp(103,"Vimal Jaiswal",30000);  
    ```

The this keyword refers to the current object.

### Access Object Properties

**You can access the properties of an object in JavaScript in 3 ways:**

1. Dot property accessor: `object.property`
    ```
    const hero = {
      name: 'Batman'
    };
    
    // Dot property accessor
    console.log(hero.name); // => 'Batman'
    ```
2. Square brackets property accessor: `object['property'];

    ```
    const property = 'name';
    const hero = {
      name: 'Batman'
    };
    
    // Square brackets property accessor:
    console.log(hero['name']);   // => 'Batman'
    console.log(hero[property]); // => 'Batman'
    ```
3. Object destructuring: `const { property } = object`

    ```
    const hero = {
      name: 'Batman'
    };
    
    // Object destructuring:
    const { name } = hero;
    console.log(name); // => 'Batman'
    ```
    
### JavaScript Factory Functions

> A factory function is a function that returns a new object

**The following creates a person object named person1**

```
let person1 = {
  firstName: 'John',
  lastName: 'Doe',
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};

console.log(person1.getFullName());
```

The person1 object has two properties: firstName and lastName, and one method getFullName() that returns the full name.

Suppose that you need to create another similar object called person2, you can duplicate the code as follows:

```
let person2 = {
  firstName: 'Jane',
  lastName: 'Doe',
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};

console.log(person2.getFullName());
```

In this example, the person1 and person2 objects have the same properties and methods.

⚡The problem is that the more objects you want to create, the more duplicate code you have.

✋💁‍♀️ T**o avoid copying the same code all over again, you can define a function `factory function` that creates the person object:**

```
function createPerson(firstName, lastName) {
  const newPerson = {};
  newPerson.firstName: firstName;
  newPerson.lastName: lastName;
  newPerson.getFullName= function() {
      return firstName + ' ' + lastName;
    },
  return newPerson;
  
}

const person1 = createPerson("sajida","qadomi");

const person2 = createPerson("sojood","qadomi");

person1.getFullName();
person2.getFullName()
```

> By using the factory function, you create any number of the person objects without duplicating code.

When you create an object, the JavaScript engine allocates memory to it. If you create many person objects, the JavaScript engine needs **lots of memory spaces** to store these objects.

🪔  However, each person object has a copy of the same getFullName() method. **It’s not efficient memory management.** ⚠️

💁‍♀️ **Solution : Using the prototype chain**

> To avoid duplicating the same getFullName() function in every object, you can remove the getFullName() method from the person object:

> Link person1 and functionStore so the interpreter, on not finding .getFullName(), makes 
sure to check up in functionStore where it would find it

> Make the link with `Object.create()` technique

### Object prototype ,\__proto__,  and Object.create()
> All objects have a **\__proto__** property by default which defaults to linking to a big 
object - **Object.prototype** full of (somewhat) useful functions
We get access to it via userFunctionStore’s **\__proto__** property - the chain

> The Object.create() static method creates a new object, using an existing object as the prototype of the newly created object.

```
function createPerson(firstName, lastName) {
  const newPerson = Object.create(functionStore);// function store is now using as prototype and new person object using proto to linked to it
  newPerson.firstName = firstName;
  newPerson.lastName = lastName;
  return newPerson;
  
}

const functionStore ={
    getFullName:function() {
      return this.firstName + ' ' + this.lastName;
    }
}

const person1 = createPerson("sajida","qadomi");

const person2 = createPerson("sojood","qadomi");

person1.getFullName();
person2.getFullName()
```

### this Key
> In **regular functions** the this keyword represented the object that called the function, which could be the window, the document, a button or whatever.

> With arrow functions the this keyword always represents the object that defined the arrow function.

```
function userCreator(name, score) {
 const newUser = Object.create(userFunctionStore);
 newUser.name = name;
 newUser.score = score;
 return newUser;
};
const userFunctionStore = {
 increment: function() {
 function add1() { this.score++; }
 add1()// this inside add1 will be window 😔
 add1.apply(this); // this here will be  user obj🥳 
 }
};
const user1 = userCreator("Will", 3);
const user2 = userCreator("Tim", 5);
console.log(user1.increment());
console.log(user1.increment().

```

💁‍♀️ **Arrow functions override the normal this rules**🔥🔥

```
function userCreator(name, score) {
 const newUser = Object.create(userFunctionStore);
 newUser.name = name;
 newUser.score = score;
 return newUser;
};
const userFunctionStore = {
 increment: function() {
 const add1 = () => { this.score++; } // this = user object
 add1()
 }
};
const user1 = userCreator("Will", 3);
const user2 = userCreator("Tim", 5);
user1.increment();

```

#### new keyword

- A new empty object is created.
- The new object’s internal ‘Prototype’ property (__proto__) is set the same as the prototype of the constructing function.
- The ‘this’ variable is made to point to the newly created object. It binds the property which is declared with ‘this’ keyword to the new object.

```
function userCreator(name, score) {
 //const newUser = Object.create(functionStore);no need new will create {}
 newUser this.name = name;
 newUser this.score = score;
 //return newUser; // new will return this (If the constructor function returns nothing, ‘this’ is return;)
};
 userCreator.prototype // {};
 userCreator.prototype.increment = function(){
 this.score++;
}
const user1 = new userCreator("Will", 3);////Automates the hard work
userCreator.increment()

```

###  class

**The class ‘syntactic sugar**

> We’re writing our shared methods separately from our object ‘constructor’ itself 
(off in the userCreator.prototype object)
Other languages let us do this all in one place. ES2015 lets us do so too

```
class UserCreator {
 constructor (name, score){
 this.name = name;
 this.score = score;
 }
 increment (){ this.score++; }
 login (){ console.log("login"); }
}
const user1 = new UserCreator("Eva", 9);
user1.increment()
```
💁‍♀️ In the end, classes are pretty much just syntactic sugar over prototypes and constructors, so they can do the same things. 

## Coding Exercises  💁‍♀️ 

**QUESTION #1**

> You are given a function executeInSequenceWithCBs and some code. The task is to modify the executeInSequenceWithCBs function so that it runs and executes all the tasks inside the asyncTasks array.
The function should return an array of messages obtained from each task's execution.
You are only allowed to change the executeInSequenceWithCBs function or add new functions/code. You cannot modify the tasks' functions.

```
const task1 = (cb) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      const message = "Task 1 has executed successfully!";
      cb(message, resolve);
    }, 3000);
  });

const task2 = (cb) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      const message = "Task 2 has executed successfully!";
      cb(message, resolve);
    }, 0);
  });

const task3 = (cb) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      const message = "Task 3 has executed successfully!";
      cb(message, resolve);
    }, 1000);
  });

const task4 = (cb) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      const message = "Task 4 has executed successfully!";
      return cb(message, resolve);
    }, 2000);
  });

const task5 = (cb) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      const message = "Task 5 has executed successfully!";
      return cb(message, resolve);
    }, 4000);
  });

const asyncTasks = [task1, task2, task3, task4, task5];

const executeInSequenceWithCBs = async (tasks, callback) => {
  const result = await Promise.all(
    tasks.map(async (task) => {
      return await task(callback);
    })
  );
  console.log(result);
  return result;
};

executeInSequenceWithCBs(asyncTasks, (m, resolve) => resolve(m));
```

**QUESTION #2**

> Your task is to write code that fetches the data of each API in parallel using promises. In Parallel means that the api which resolves first, returns its value first, regardless of the execution order.
The output of the executeInParallelWithPromises function should be an array containing the results of each API's execution.
Each result should be an object with three keys: apiName, apiUrl, and apiData

```
const apis = [
  {
    apiName: "products",
    apiUrl: "https://dummyjson.com/products",
  },
  {
    apiName: "users",
    apiUrl: "https://dummyjson.com/users",
  },
  {
    apiName: "posts",
    apiUrl: "https://dummyjson.com/posts",
  },
  {
    apiName: "comments",
    apiUrl: "https://dummyjson.com/comments",
  },
];

const executeInParallelWithPromises = async (apis) => {
  let result = await Promise.all(
    apis.map((api) =>
      fetch(api.apiUrl)
        .then((response) => response.json())
        .then((apiData) => ({
          apiName: api.apiName,
          apiUrl: api.apiUrl,
          apiData,
        }))
    )
  );
  console.log(result, "result");
};

executeInParallelWithPromises(apis);
```

**QUESTION #3**

> You are given a function called executeInSequenceWithPromises, which takes an array of APIs (represented by objects).
Your task is to write code that fetches the data of each API sequentially (one after the other) using promises.
In Sequence means that the api which executes first, returns its value first.
The output of the executeInSequenceWithPromises function should be an array containing the results of each API's execution.
Each result should be an object with three keys: apiName, apiUrl, and apiData.

```
const apis = [
  {
    apiName: "products",
    apiUrl: "https://dummyjson.com/products",
  },
  {
    apiName: "users",
    apiUrl: "https://dummyjson.com/users",
  },
  {
    apiName: "posts",
    apiUrl: "https://dummyjson.com/posts",
  },
  {
    apiName: "comments",
    apiUrl: "https://dummyjson.com/comments",
  },
];

//modify and write your code here
const executeInSequenceWithPromises = async (api) => {
  let result = []
  for (let i = 0; i < api.length; i++) {
    let apiResult = await fetch(api[i].apiUrl);
    let apiData = await apiResult.json();
    result.push({ apiName: api[i].apiName, apiUrl: api[i].apiUrl, apiData })
    
  }
    
    console.log(result)
};

executeInSequenceWithPromises(apis)

```

## Coding Challenge - freeCodeCamp.org 💪 🧑‍💻
**[SajidaQdomi-freeCodeCamp-account ](https://www.freecodecamp.org/fcc0c6de411-9019-4ce5-a333-fa316812d6a9)**




# Day 3🧑‍💻

## Arrays
   > An `array` is a special variable, which can hold more than one value:
   - Arrays can hold any type of items, or mix and match!
       ```
       let mixedArray = ["pop", 6, "squish", false, document];
       ```
    - Array **indexes** start with 0.
    [0] is the first element. [1] is the second element.
        ```
         mixedArray[0]
         mixedArray[1]
        ```
    - The `length` property of an array returns the length of an array (the number of array elements).
        ```
        mixedArray.length;//5
        ```
### Some JavaScript Array Methods and Properties
        
> const arr1 = ["sara", "Lone"];
const arr2 = ["qadomi", "leane", "majed"];
        
|  Name  | Description | Examble
    | -------- | ------- |------- |
    |  concat()  | method concatenates (joins) two or more arrays. | ```const children = arr1.concat(arr2);```|
    |  includes() | Check if an array contains the specified element |```arr1.icludes("sara")//true```|
    | indexOf()	  | Search the array for an element and returns its position  |`arr1.indexOf(sara)//0`|
    | join()	 | Joins all elements of an array into a string  |`arr1.join(" & ")`|
    |  pop()	 | Removes the last element of an array, and returns that element |`arr1.pop()`|
    | push()	| Adds new elements to the end of an array, and returns the new length |`arr1.push()`|
    
### Mutating vs Non-Mutating Methods 
> **Mutating methods** are array methods that modify the original array, while **non-mutating methods** return a new array without modifying the original.

1.  Mutating Array Methods like: 
- push()  
- pop() 
- sort()

2. Non-Mutating Array Methods like
- concat() 
- join()
- indexOf() 
- lastIndexOf() 
- includes() 

### Important Notes About  Mutating data 

> We can access each character in a string the same way as indexes in an array:
```
let treat = "bone"
treat[0] //b
```
> Let’s change character ‘b’. We will re-assign it to uppercase ‘B’
```
treat[0] = “B” ❌
treat // "bone"
```
>>  In Javascript, strings are primitive values. Primitive values have special rules, one being that you cannot mutate or modify them. We can see that we can access and read the value “bone”, but you can not change it. Primitives are immutable. 

>> Arrays are technically considered an object data type, and objects are not primitive. They are mutable!

#### immutable variable with mutable value
> Variables themselves can also be (im)mutable

```
let letVariable = "original value";
letVariable = "new value"; ✅mutable
```
```
const constVariable = "original value";
constVariable = "new Value";❌mutable
```
## JavaScript objects-: 
> In JavaScript, an object is an unordered collection of key-value pairs. Each key-value pair is called a property.

> The key of a property can be a string. And the value of a property can be any value, e.g., a string, a number, an array, and even a function.

```
let person = {
    firstName: 'John',
    lastName: 'Doe'
};
```
### Accessing properties
1.  The dot notation (.) : `person.firstName`
2. Array-like notation ( []): `person['firstName']`

### Modifying the value of a property
`person.firstName = 'Jane';`

### Object Methods
> Properties can point to functions too
We call function-properties "methods" on objects

```
const dog = {
    name: "Ein",
    breed: "Corgi",
    speak: function () {
        console.log("woof woof");
    }
}
dog.speak();
```
### JavaScript Built-in Objects
> Objects that are pre-defined in the JavaScript language
- Array Methods
        ```
        arr.length; 
        arr.slice(); 
        arr.splice(); 
        arr.pop(); 
        arr.push(); 
        arr.filter(); 
        arr.indexOf(); 
        ```
- console
        ```
        console.log("hello coder!");
        ```
- Math
        ```
        let randomNumber = Math.random();
        ```
- strings
    > Strings are primitive values (not objects)
    but JS automatically wraps them in String objects
    
    ```
    const hello = "hello";
    console.log(hello.length);
   const yello = hello.toUpperCase();
    ```
### What is this?
> In JavaScript, the this keyword refers to an object.
Which object depends on how this is being invoked (used or called).

1. In an object method, this refers to the object.

    >> const person = {
      firstName: "John",
      lastName : "Doe",
      id       : 5566,
      fullName : function() {
        return this.firstName + " " + this.lastName;
      }
    };
    ✅this.firstName is the firstName property of this (the person object).

2. Alone, this refers to the global object.
3. In a function, this refers to the global object.
4. In a function, in strict mode, this is undefined.
5. In an event, this refers to the element that received the event.
6. Methods like call(), apply(), and bind() can refer this to any object.

## Quiz Project
**Code :**
```
 <script type="text/javascript">

    // TODO 1: Declare & assign variables pointing to the corresponding element(s)
    // statement should be the "statement" div
    const statment = document.getElementById("statment")
    // optionButtons should be all the elements within the "options" div
    const optionButtons = document.querySelectorAll("button");
    // explanation should be the "explanation" div
    const explanation = document.getElementById("explanation")


    // TODO 2: Declare & assign a variable called fact
    // Its value should be an object with a statement, true/false answer, and explanation 
    const facts = {
        statment: "Arrays are like object",
        answer: true,
        explanation: "Arrays are type  object",
    }

    
    // TODO 3: Set the text of the statement element to the fact's statement
    statment.textContent = facts.statment;
  </script>
```

## Coding Exercises

**QUESTION #1**
>We have defined a function, forecast, that takes an array as an argument. Modify the function using slice() to extract information from the argument array and return a new array that contains the string elements warm and sunny.

```
function forecast(arr) {
 // Only change code below this line
  return arr.slice(2,4);
  }
n// Only change code above this line
 console.log(forecast(['cold', 'rainy', 'warm', 'sunny', 'cool', 'thunderstorms']));
```
    
**QUESTION #2**
> We have defined a function spreadOut that returns the variable sentence. Modify the function using the spread operator so that it returns the array ['learning', 'to', 'code', 'is', 'fun'].

```
function spreadOut() {
let fragment = ['to', 'code'];
let sentence = ['learning', ...fragment, 'is', 'fun']; // Change this line
return sentence;
}
console.log(spreadOut());
```
    
**QUESTION #3**
>Profile Lookup
We have an array of objects representing different people in our contacts lists.
A lookUpProfile function that takes name and a property (prop) as arguments has been pre-written for you.
The function should check if name is an actual contact's firstName and the given property (prop) is a property of that contact.
If both are true, then return the "value" of that property.
If name does not correspond to any contacts then return the string No such contact.
If prop does not correspond to any valid properties of a contact found to match name then return the string No such property.

```
// Setup
const contacts = [
  {
    firstName: "Akira",
    lastName: "Laine",
    number: "0543236543",
    likes: ["Pizza", "Coding", "Brownie Points"],
  },
  {
    firstName: "Harry",
    lastName: "Potter",
    number: "0994372684",
    likes: ["Hogwarts", "Magic", "Hagrid"],
  },
  {
    firstName: "Sherlock",
    lastName: "Holmes",
    number: "0487345643",
    likes: ["Intriguing Cases", "Violin"],
  },
  {
    firstName: "Kristian",
    lastName: "Vos",
    number: "unknown",
    likes: ["JavaScript", "Gaming", "Foxes"],
  },
];

function lookUpProfile(name, prop) {
  // Only change code below this line
 let contactIndex = contacts.findIndex(contact => contact.  firstName === name);

 if(contactIndex > -1){
   return contacts[contactIndex][prop] || "No such property"
 }
 return "No such contact"
  // Only change code above this line
}

lookUpProfile("Akira", "likes");
```
**QUESTION #4**
> Create a function called reusableFunction which prints the string Hi World to the dev console.
Call the function.

```
function reusableFunction(){
 console.log("Hi World");
}

reusableFunction();

```
    
**QUESTION #5**
>Create a function addFive without any arguments. This function adds 5 to the sum variable, but its returned value is undefined.
 ```
 // Setup
let sum = 0;

function addThree() {
  sum = sum + 3;
}

// Only change code below this line
function addFive(){
  sum += 5;
}

// Only change code above this line

addThree();
addFive();
 ```
 **QUESTION #6**
 > Create a function timesFive that accepts one argument, multiplies it by 5, and returns the new value.
 ```
 function timesFive(num){
  return num*5;
}


let newValue = timesFive(3);
 ```

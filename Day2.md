
# Day 2 🧑‍💻

## Values & Data Types
   **Value**: Data we want to work with.
    To check the data type for value use: `` typeof `` operator.
    
    ```javascript
    let myStr = "This is the first sentence.";
    console.log(typeof(mystr));
    ```
    
#### data Types in JS: 
- ###### Primitive types 
    &nbsp;
    |  type  | Examble |
    | -------- | ------- |
    |  Integer  | ``let x = 5`` |
    |  String  | ``let x = "sajida"`` |
    |  Boolean  | let x = true  |
    |  Null  | let x = null |
    |  Undefined  | let x ; |

- ###### Objects 
     &nbsp;
    |  type  | Examble |
    | -------- | ------- |
    |  Object  | ``let employee = {name: "sajida" , ID: 2222}`` |
    |  Array  | ``let employee = [sajida,25,qadomi]`` |

``
## Operators

1. ###### Arithmetic operators
- \+ add
- \- subtract
- \* multiply
- \/ divide
 
2. ###### Comparison operators
- \> greater than
- \< less than
- \>= greater than or equal to
- \<= less than or equal to

3.  ###### Equality operators
    &nbsp;
    |  strict  | loosey-goosey | meaning   |
    | -------- | ------- | ------- |
    |  ===  | == |equals |
    |  !==  | != | does not equal |

## variables
> **Variables** are containers for storing values.
> **Declare** a JavaScript variable with the var or the let keyword
```javascript
   var carName;
    // OR
    let carName;
```
> ***Assigns*** data into 
```javascript
   var carName = "ooohzbsxhj";
```

## Statements vs. Expressions
>> An **expression** "asks" JS for a value
 ```javascript
   myAssignedVariable
   6 + 4
  document.getElementById("board")
```
>> A **statement** "tells" JS to do something
 ```javascript
  let ten = 6 + 4;
myDeclaredVariable = "new value";
let board = document.getElementById("board");
 document.getElementById("board")
```
## Coding Exercises

1. QUESTION #1
    ```javascript
    let a = 0;
    let b = "0";
    let c = false;
    let d = "false";

   console.log(a == b);
   // true "==" checks only for equality in value
   console.log(b === c);
   // false: w "===" is a stricter equality test and returns false if either the value or the //type of the two variables are differnt
   console.log(!!d);
   //true :the first ! coerces the value //to a boolean and inverts it.  ```
    
2. QUESTION #2

   ```javascript
   
     console.log(4 + 5 * "7");
     //39 : Multiplication  and divisionhave higher precedence than addition and subtraction 
     //Type Coercion for "7" from string to number-> process of automatic or implicit conversion of values from /one data type to another

    ```
    
1. QUESTION #3

    ```javascript
       let result = 5 + 2 * 3 - 1;
       // result=10
       //2*3=6
       //5+6=11
       //11-1=10
    ```
1. QUESTION #4

    ```javascript
       let x = 10;
       let y = '10';
       console.log(x == y);//true :  checks only for equality in value
       console.log(x === y); // false: is a stricter equality test and returns false if either //the value or the type of the two variables are differnt 
    ```
    
1. QUESTION #5

    ```javascript
      let num = "15";
      let isPositive = true;
      let result = (num > 10 && isPositive) || num < 0;
      console.log(result);
      //tru
      //1-  num > 10 : 15 > 10 true
      //Type Coercion for "15" from string to number-> process of automatic or implicit conversion of values from /one data type to another
      // 2- true && isPositive :true where isPostive is true
      // 3- true || false (15 < 0) : true here there is type correction as before

```

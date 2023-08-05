
# Day 1 🧑‍💻

## JavaScript Introduction

### Definition:
``
JavaScript is a dynamic programming language that's used for web development, in web applications, for game development, and lots more. It allows you to implement dynamic features on web pages that cannot be done with only HTML and CSS.
``

### Where To:

- The browser's JS console 
- Local text file in editor, e.g. TextEdit, VS Code
- Online playground

## Document Object Model

``
When a web page is loaded, the browser creates a Document Object Model of the page.
The HTML DOM model is constructed as a tree of Objects
``

### With the object model, JavaScript can:

-  Chang all the HTML elements in the page
-  Change all the HTML attributes in the page
-  Change all the CSS styles in the page
-  Remove existing HTML elements and attributes
-  Add new HTML elements and attributes
-  React to all existing HTML events in the page
-  Create new HTML events in the page

### Coding Examples

|  Target  | Code |
| -------- | ------- |
|  Finding the (first) element with id="board"  |  `document.getElementById("board")` or `document.querySelector("#board")`    |
|Finding All the h1 elements |  ` document.getElementsByTagName("h1") ` or ` document.querySelectorAll("h1") `    |
| Finding all the elements with class="player"  |` document.getElementsByClassName("player") ` or ` document.querySelectorAll(".player") `    |
| Finding the number of elements with class="player" | ` document.getElementsByClassName("player").length `    |
| Finding the text inside the element with id="p1-name" | `  document.getElementById("p1-name").textContent `  |
|change the page title   |`document.title = "sajida page" `     |
| replace the text of the #p1-name element  | ` document.getElementById("p1-name").textContent = "Qadomi" `    |
| add to the end of the element's current text| ` document.getElementById("p1-name").append(" & friends") ` |

## Coding Exercises

1. [Compound Assignment With Augmented Multiplication](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/compound-assignment-with-augmented-multiplication)
    ```javascript
    let a = 5;
    let b = 12;
    let c = 4.6;
    
    a *= 5;
    b *= 3 ;
    c *= 10;
    ```
1. [Concatenating Strings with the Plus Equals Operator](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/concatenating-strings-with-the-plus-equals-operator)

    ```javascript
    let myStr = "This is the first sentence.";
    myStr += " This is the second sentence."
    ```

1. [Use Bracket Notation to Find the Nth-to-Last Character in a String](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/use-bracket-notation-to-find-the-nth-to-last-character-in-a-string)

    ```javascript
    const lastName = "Lovelace";
    const secondToLastLetterOfLastName = lastName[lastName.length - 2];
    ```



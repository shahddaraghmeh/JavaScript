# JavaScript First Steps — Course Notes



### Introduction
A short welcome to the course: what JavaScript is used for, what you'll build
(interactive web pages), and what background is assumed (basic HTML/CSS, no prior JS needed).

### Course Overview
The course roadmap: DOM basics → values & data types → operators → expressions →
arrays → objects → a small quiz project that ties everything together.

### What is JavaScript
- JavaScript (JS) is a **high-level, dynamically-typed** programming language.
- It's the language of the web browser — it adds **interactivity** to HTML/CSS pages.
- It also runs outside the browser (e.g. **Node.js**) for servers, scripts, tools.
- Standardized as **ECMAScript**; created in 1995 by Brendan Eich.

```js
console.log("Hello, JavaScript!");
```

### Where to Write JavaScript
Three common places to run JS:
1. **Browser DevTools Console** — quick experiments (right-click → Inspect → Console).
2. **Inline in HTML**, inside a `<script>` tag:
```html
<script>
  console.log("Hello from inline script");
</script>
```
3. **External file**, linked from HTML (recommended for real projects):
```html
<script src="app.js"></script>
```

---

## Section 1 — DOM (Document Object Model)

### Document Object Model
- The **DOM** is a tree-like representation of an HTML page that JavaScript can read and change.
- Every HTML tag becomes a **node/object** in this tree, so JS can select it and manipulate it.
```
document
 └── html
      ├── head
      └── body
           ├── h1
           └── p
```

### Finding Elements in a Web Page
```js
document.querySelector("h1");        // first matching element
document.querySelectorAll("p");      // all matching elements (a NodeList)
document.getElementById("title");    // element with id="title"
```

### `.length` & `.textContent`
```js
const paragraphs = document.querySelectorAll("p");
paragraphs.length;             // how many <p> elements were found

const title = document.querySelector("h1");
title.textContent;             // reads the text inside the element
```

### Finding Elements Exercise
> Select every `<li>` on the page and log how many there are.
```js
const items = document.querySelectorAll("li");
console.log(items.length);
```

### Changing a Web Page
```js
const title = document.querySelector("h1");
title.textContent = "New Title";       // change the text
title.style.color = "blue";            // change a CSS style
title.classList.add("highlight");      // add a CSS class
```

### Changing a Web Page Exercise
> Find the button with id `submit-btn` and change its text to "Submitted!" when clicked.
```js
const button = document.querySelector("#submit-btn");
button.addEventListener("click", function () {
  button.textContent = "Submitted!";
});
```

---

## Section 2 — Values & Data Types

### Values & Data Types
JavaScript has a few basic ("primitive") data types:
| Type | Example |
|---|---|
| String | `"hello"` |
| Number | `42`, `3.14` |
| Boolean | `true`, `false` |
| Undefined | `undefined` |
| Null | `null` |

```js
typeof "hello";     // "string"
typeof 42;           // "number"
typeof true;         // "boolean"
typeof undefined;    // "undefined"
typeof null;         // "object" (a famous JS quirk!)
```

### Values & Data Types Exercise
> Use `typeof` to check the type of 5 different values you create.
```js
typeof 100;
typeof "text";
typeof false;
typeof [1, 2, 3];   // "object"
typeof {};          // "object"
```

### Strings
- Text wrapped in quotes: `"double"`, `'single'`, or `` `backticks` `` (template literals).
- Strings have a `.length` and individual characters can be accessed by index.
```js
const greeting = "Hello";
greeting.length;      // 5
greeting[0];           // "H"
```

### indexOf
```js
const phrase = "JavaScript is fun";
phrase.indexOf("is");        // 11
phrase.includes("fun");      // true
phrase.startsWith("Java");   // true
phrase.toLowerCase();        // "javascript is fun"
```

### Working with Strings Exercise
> Given `const name = "Shahd";`, print its length and check if it includes the letter "a".
```js
const name = "Shahd";
console.log(name.length);          // 5
console.log(name.includes("a"));   // true
```

---

## Section 3 — Operators

### Operators
```js
5 + 3;    // 8   addition
5 - 3;    // 2   subtraction
5 * 3;    // 15  multiplication
5 / 3;    // 1.666...  division
5 % 3;    // 2   remainder (modulo)
2 ** 3;   // 8   exponent
```

### Operators Exercise
> Calculate the area of a rectangle with width 4 and height 7.
```js
const width = 4;
const height = 7;
const area = width * height;   // 28
```

### Comparison & Equality Operators
```js
5 > 3;     // true
5 < 3;     // false
5 >= 5;    // true

5 == "5";   // true  (loose equality — converts types)
5 === "5";  // false (strict equality — checks type too)
5 !== "5";  // true
```
> Best practice: prefer `===` and `!==` over `==` and `!=` to avoid unexpected type conversion.

---

## Section 4 — Expressions

### Expressions
An **expression** is any piece of code that produces a value.
```js
3 + 4;          // expression → produces 7
"a" + "b";      // expression → produces "ab"
```

### Declaring & Assigning Variables
```js
let age;          // declaration (no value yet)
age = 20;          // assignment
let name = "Ali";  // declaration + assignment in one line
```

### `const` & Accessing Variables
```js
const pi = 3.14159;   // must be assigned immediately, cannot be reassigned
console.log(pi);
```

### Variables Exercise
> Declare a variable for your favorite color and log it to the console.
```js
let favoriteColor = "teal";
console.log(favoriteColor);
```

### What are Variables?
Variables are named containers (references) that point to values in memory,
so you can store data once and reuse/reference it by name throughout your code.

### Evaluating Code
JavaScript evaluates expressions **inside-out**: the innermost/most nested
expressions are computed first, then combined into the outer result.
```js
const result = (2 + 3) * (4 - 1);   // (5) * (3) → 15
```

### Statements vs Expressions
- **Expression**: produces a value (`3 + 4`, `x > 5`).
- **Statement**: performs an action, doesn't necessarily produce a value
  (`if (...) {...}`, `for (...) {...}`, a variable declaration).
```js
// statement:
if (age > 18) {
  console.log("adult");
}
// expression inside it:
age > 18
```

---

## Section 5 — Arrays

### Arrays
An array is an ordered list of values, indexed starting at 0.
```js
const fruits = ["apple", "banana", "cherry"];
fruits[0];         // "apple"
fruits.length;      // 3
```

### Useful Array Methods
```js
const nums = [1, 2, 3];
nums.push(4);        // add to end → [1,2,3,4]
nums.pop();           // remove from end → [1,2,3]
nums.unshift(0);      // add to start → [0,1,2,3]
nums.shift();          // remove from start → [1,2,3]
nums.includes(2);      // true
nums.join("-");         // "1-2-3"
nums.slice(0, 2);       // [1,2] (does NOT change original)
```

### Mutability (from lecture)
`const` prevents **reassigning** the whole array, but individual elements can
still be modified — `const` fixes the **reference**, not the contents.

![const array note 1](images/02-const-array-note1.png)
![const array note 2](images/03-const-array-note2.png)

```js
const operands = [4, 6];
operands;              // Array [4, 6]

const sum = operands[0] + operands[1];
sum;                    // 10

operands[0] = 5;        // allowed even with const

const newSum = operands[0] + operands[1];
newSum;                 // 11
```
![array sum console demo](images/01-array-sum-console.png)

### Mutable & Immutable Data Exercise
> Predict the output before running it, then check:
```js
const colors = ["red", "green"];
colors.push("blue");
console.log(colors);          // ["red", "green", "blue"]  ← allowed
// colors = ["yellow"];       // ❌ TypeError: Assignment to constant variable
```

### Immutable Variables & Values (from lecture)
Immutable data:
- prevents unexpected changes
- reduces the likelihood of bugs
- makes code more predictable

![immutability benefits](images/05-immutable-benefits.png)

### Variables & Arrays — Shared Reference (from lecture)
When you do `let array2 = array1;`, both variables point to the **same** array
in memory — changing one changes the other.
```js
let array1 = [1, 2, 3];
let array2 = array1;

array2;              // Array(3) [1, 2, 3]

array1[1];            // 2
array1[1] = 4;

array1;               // Array(3) [1, 4, 3]
array2;               // Array(3) [1, 4, 3]  ← also changed!
```
![array reference console demo](images/06-array-reference-console.png)
![variables vs values diagram](images/07-variables-values-diagram.png)

---

## Section 6 — Objects

### Objects & Property Access (from lecture)
Objects group related values together using **properties** — similar to how
variables point at values, objects let properties point at related values.

![objects intro](images/08-objects-intro.png)

```js
const js = {
  name: "JavaScript",
  abbreviation: "JS",
  isAwesome: true,
  officialSpec: "ECMAScript",
  birthYear: 1995,
  creator: "Brendan Eich"
};

js.name;        // "JavaScript"
```
![object property access console](images/09-object-property-access.png)

### Visualizing Object Access (from lecture)
```js
indecisive;              // Object { lunch: "sandwich" }
indecisive.lunch;         // "sandwich"

indecisive.lunch = "tacos";   // change an existing property
indecisive.snack = "chips";   // add a new property
```
![object reassign and add property](images/10-object-reassign-add-property.png)

Arrays are actually objects too:
```js
typeof { snack: "chips" };   // "object"
typeof ["chips"];            // "object"
```
![typeof array vs object](images/11-typeof-array-object.png)

### Objects Exercise (from lecture)
> Create an object representing yourself.
```js
const anjana = {
  name: "Anjana",
  home: "San Francisco",
  languages: ["English", "German", "French"],
  pet: null,
  vehicle: "Vespa",
  hobbies: ["travel", "climbing", "gaming", "lindy hop"]
};
```
![exercise create object](images/12-exercise-create-object.png)

### Object Methods (from lecture)
A function stored as a property is called a **method**.
```js
const dog = {
  name: "Ein",
  breed: "Corgi",
  speak: function () {
    console.log("woof woof");
  }
};
dog.speak();   // "woof woof"
```
![methods example](images/14-methods.png)

`this` inside a method refers back to that same object's properties:
```js
anjana.speak = function () {
  console.log("Hi my name is", this.name);
};
anjana.speak();   // "Hi my name is Anjana"
```
![this keyword example](images/15-this-keyword.png)

### Object Methods Exercise
> Add a `greet` method to the `dog` object that logs "Hi, I'm <name>!".
```js
dog.greet = function () {
  console.log("Hi, I'm " + this.name + "!");
};
dog.greet();   // "Hi, I'm Ein!"
```

### Built-In Objects (from lecture + extra)
`Object.freeze()` locks an object completely — no new properties, no edits,
no deletions. This is the highest integrity level JavaScript provides.

![Object.freeze](images/13-object-freeze.png)

Other useful built-in objects:
```js
Math.max(3, 7, 2);     // 7
Math.round(4.6);        // 5
new Date();               // current date/time object
JSON.stringify({a: 1});  // '{"a":1}'
```

Console methods:
```js
console.log("hi");       // normal message
console.warn("uh oh");   // warning (yellow highlight)
```
![console.log vs console.warn](images/19-console-log-warn.png)

Strings are primitives, but JS wraps them in a temporary wrapper object
behind the scenes so methods like `.length` and `.indexOf()` work, while the
original string itself stays immutable.
![string wrapper object](images/20-string-wrapper-object.png)

### Nested Objects (from lecture)
```js
const menu = {
  lunch: {
    appetizer: "salad",
    main: "spaghetti",
    dessert: "tiramisu"
  },
  dinner: {
    appetizer: "samosa",
    main: "saag paneer",
    dessert: "gulab jamun"
  }
};

const tiramisu = menu.lunch.dessert;
```
![nested objects example](images/16-nested-objects.png)

**Exercise — spiceGirls:**
![exercise spiceGirls](images/17-exercise-spicegirls.png)
```js
spiceGirls.motto;             // "Girl Power"
spiceGirls.members[1];         // { name: "Geri", nickname: "Ginger" }
spiceGirls.albums[1];           // "Spiceworld"
spiceGirls.members[4].name;      // "Victoria"
```
![spiceGirls solution console](images/18-spicegirls-solution.png)

### Tic Tac Toe Demo
A short live-coding demo showing how objects + arrays + the DOM come together:
a 3x3 board is stored as an array, clicking a square updates that array
(the data), and the DOM is then updated to reflect the new board state.
```js
const board = ["", "", "", "", "", "", "", "", ""];
board[4] = "X";       // player marks the center square
// then: re-render the board in the DOM based on the `board` array
```

---

## Section 7 — Quiz Project

### JavaScript Pop Quiz & Project Setup
A short review quiz on everything covered so far (data types, operators,
arrays, objects), followed by setting up a small starter project (HTML file +
linked `script.js`) to practice reading input and updating the page.

### DOM Exercise
> Select the element with id `result` and set its text based on a variable.
```js
const result = document.querySelector("#result");
const score = 8;
result.textContent = "Your score: " + score;
```

### Declaring & Assigning a Variable
```js
let userAnswer = "B";     // declare & assign the user's selected choice
```

### Setting Statement Element
> Update a `<p>` element to show a pass/fail message based on the score.
```js
const message = document.querySelector("#message");
if (score >= 5) {
  message.textContent = "You passed!";
} else {
  message.textContent = "Try again!";
}
```

---

## Quick Summary Table

| Section | Key idea |
|---|---|
| Getting Started | JS adds interactivity to web pages; can run in console, `<script>`, or external file |
| DOM | JS reads/changes the page through a tree of elements (`document.querySelector`, `.textContent`) |
| Values & Data Types | string, number, boolean, undefined, null — check with `typeof` |
| Operators | arithmetic (`+ - * / %`) and comparison (`== === < >`) |
| Expressions | expressions produce values; statements perform actions; variables reference values |
| Arrays | ordered lists; `const` fixes the reference, not the contents; copies share the same reference |
| Objects | group related values as properties; methods are function-properties; `this` refers to the object; nested objects chain with `.` |
| Quiz Project | putting variables, DOM selection, and conditionals together in one small project |

# [Linkedin] JavaScript Essential Training

## 2 Up and Running with JS

#### Modern JS loading 02_03

`async/defer` should be the standard way of loading JS. JS loading should be placed in the `<head>` section, and places it in the bottom is anti-pattern.

##### Default Behavior

Content blocking: broswer rendering -> stops rendering and start downloading JS files when encountering JS -> executing JS -> resumes rendering

##### `async`

When encounter JS, downloads the JS in parallel while HTML renders. When JS file is fully downloaded, stop rendering and executes JS

##### `defer`

Browser downlaods JS in parallel with HTML rendering, after completing rendering the HTML, the browser starts executing the JS.

#### JS Module 02_04

Separating the JS code into modules to reduce code in a single document.

In `scripts.js`

```
import backpack from "./backpack.js";
```

In `backpack.js`

```
export default backpack;
```

In `index.html`, we have to reference both JS files and assign type attribute as `module`

```
<script type="module" src="backpack.js"></script>
<script type="module" src="script.js"></script>
```

Assign the type as `module` will automatically defer the loading of JS.

##### Console difference

02_03 the browser can reference ` backpack` directly while in 02_04 the `backpack` is in the scope of `script.js` so the browser can't reference it directly.

## 3 Objects

JS is prototype based object oriented language.

methods: Property-changing features inside objects

property: key-value pairs.

`this` keyword refers to the current object.

#### Object containers 03_03

We use `const` for objects, so we can't remove or replace the object, only to modify some of its properties.

```
const backpack = {
  name: "Everyday Backpack",
  volume: 30,
  color: "grey",
  pocketNum: 15,
  strapLength: {
    left: 26,
    right: 26,
  },
  lidOpen: false,
  toggleLid: function (lidStatus) {
    this.lidOpen = lidStatus;
  },
  newStrapLength: function (lengthLeft, lengthRight) {
    this.strapLength.left = lengthLeft;
    this.strapLength.right = lengthRight;
  },
};

```

- `const` constant type, so we can't change the object itself
- `backpack` name of the object container
- property: key-value pair
- `funcName: function (input) {} ` methods to modify the changeable properties in the object

#### Object Property

Colom separated key-value pairs

camelcase

#### Accessing Objects

`console.log(backpack)` will output the object automatically.

#### Accessing Object Property

- Dot notation (preferred way)

  - `console.log(backpack.color);`

- brackets

  - `console.log(backpack["color"])`

  - Bracket allows us to o more things

  - access property that breaks property name conventions, like `-` `.` Etc.

  - ```
    var query = "color";
    console.log(backpack[query]);
    ```

#### Classes: Object blueprints 03_10

perfect for modulation

use `constructor` method, we can also create other methods

```
class Backpack {
  constructor(
    // Defines parameters:
    name,
    volume,
    color,
    pocketNum,
    strapLengthL,
    strapLengthR,
    lidOpen
  ) {
    // Define properties:
    this.name = name;
    this.volume = volume;
    this.color = color;
    this.pocketNum = pocketNum;
    this.strapLength = {
      left: strapLengthL,
      right: strapLengthR,
    };
    this.lidOpen = lidOpen;
  }
  // Add methods like normal functions:
  toggleLid(lidStatus) {
    this.lidOpen = lidStatus;
  }
  newStrapLength(lengthLeft, lengthRight) {
    this.strapLength.left = lengthLeft;
    this.strapLength.right = lengthRight;
  }
}
```

How to generate an object based on the class

```
const everydayPack = new Backpack(
  "Everyday Backpack",
  30,
  "grey",
  15,
  26,
  26,
  false
);
```

You can only use a class after it's declared. As JS read file from top to bottom.

#### Object Constructors

Less advanced way of object template. Here methods is the same as how properties got defined.

```
function Backpack(
  name,
  volume,
  color,
  pocketNum,
  strapLengthL,
  strapLengthR,
  lidOpen
) {
  this.name = name;
  this.volume = volume;
  this.color = color;
  this.pocketNum = pocketNum;
  this.strapLength = {
    left: strapLengthL,
    right: strapLengthR,
  };
  this.lidOpen = lidOpen;
  this.toggleLid = function (lidStatus) {
    this.lidOpen = lidStatus;
  };
  this.newStrapLength = function (lengthLeft, lengthRight) {
    this.strapLength.left = lengthLeft;
    this.strapLength.right = lengthRight;
  };
}
```

## 4 Sidebar: String output

#### Mix text and variables with template literals

**Template Literals** use back-ticks (``) rather than the quotes ("") to define a string:

JS inject content into HTML files.

`${obj.property}` interpolation

```
/**
 * Use template literals to output HTML
 * @link https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
 *
 */
import Backpack from "./Backpack.js";

const everydayPack = new Backpack(
  "Everyday Backpack",
  30,
  "grey",
  15,
  26,
  26,
  false,
  "December 5, 2018 15:00:00 PST"
);

const content = `
  <main>
      <article>
        <h1>${everydayPack.name}</h1>
        <ul>
          <li>Volume: ${everydayPack.volume}</li>
          <li>Color: ${everydayPack.color}</li>
          <li>Age: ${everydayPack.backpackAge()}</li>
          <li>Number of pockets: ${everydayPack.pocketNum}</li>
          <li>Left strap length: ${everydayPack.strapLength.left}</li>
          <li>Right strap length: ${everydayPack.strapLength.right}</li>
          <li>Lid status: ${everydayPack.lidOpen}</li>
        </ul>
      </article>
    </main>
`;

document.body.innerHTML = content;

console.log("The everydayPack object:", everydayPack);
console.log("The pocketNum value:", everydayPack.pocketNum);
console.log("Days since aquired:", everydayPack.backpackAge());

```

#### Traditional string output

Break string into pieces and use + concatnations

```
const everydayPack = new Backpack(
  "Everyday Pack",
  30,
  "grey",
  15,
  26,
  26,
  false,
  "December 5, 2018 15:00:00 PST"
);

const content = "<h1>" + everydayPack.name + "</h1>";

document.body.innerHTML = content;
```

## 5 DOM

#### DOM: The Document Object Model

Describes a hierachical tree structure for the html document, how they relate to each other and nested.

#### **Access** elements with `querySelector` methods

queryselector targets CSS queries.

- `querySelector`
- `querySelectorAll`

```
document.querySelector(".maincontent");
```

`querySelector` return the first element that matches 

`querySelectorAll` return a node list that all of the elements match

```
document.querySelectorAll("main li").forEach(item => item.style.backgroundColor = "blue");
```

#### Access elements using older methods

- `getElementsByClassName()`
  - return all of the elements match
- `getElementById()`

#### Modifying element classes

To change the appearance or behavior of an element without having to inject the CSS into HTML itself.

Eg: hiding a panel, highlighting a button

- (Not good) `Element.className` is a property of the element in the DOM.
  - cluncky when an element has multiple classes
- `Element.classList` gives us a DOM token collection of all the classes appended to an element.
  - `remove`
  - `add`
  - Replace

## 6 Variables and Data Types

When we call a locally-scoped variable outside of its scope, 

```
script.js:20 Uncaught ReferenceError: titleColor is not defined
    at script.js:20:24
```

JS stops rendering at this point because there's an error.



When reassigning value to a `const`, we will receive error

```
Uncaught TypeError: Assignment to constant variable.
    at script.js:11:7
```

JS is a weakly typed language

`undefined`

- declared but didn't assign valur to it
- you can assign `undefined` to a variable

`typeof sth` will return the data type of that variable

- `==`   loose comparison
- `===` absolute equalance 

## 7 Arrays

`arr.join(", ")` converts an array into a string.

`arr.forEach()` grabs each item in the array and do sth to it

`arr.find()` grabs each item and checks if it satisfy the condition

## 8 Functions and Methods

#### Functions and Methods

##### function declaration:

hoisted to the global scope

```
function doSomeMath(a, b) {
  let c = a + b;
  return c;
}
```

##### function expression:

can't be redeclared, so don't need to worry about being overwritten

```
const doMoreMath = function (a = 3, b = 2) {
  let c = a * b;
  return c;
};
```

##### Immediately Invoked Function Expression (IIFE)

Wrap a function inside parenthesis, place another set of parenthses outside. This function immediately runs when the browser encounters it.

```
(function () {
  let a = 4;
  let b = 6;
  let c = doSomeMath(a, b);
  console.log(`The sum of a and b is: ${c}`);
})();
```

#### The arrow function

shorter way of writing functions

- remove `function` keyword
- remove `{}` 
- remove `()`

```
const arrowFunc = () => {
  let elem = document.querySelector("color");
  console.log(elem);
}
```

Why arrow functions?

- function declarations will be hoisted to the global scope, but arrow functions can only be called after they're declared
- arrow functions can't be the methods inside the objects

##### `this` keyword

an arrow function doesn't have its own `this` 

#### Callbacks

pass function as parameters to another function.

##### Looping through content

for loop:

```
for (let i = 0; i < stuff.length; i++) {
  let listItem = document.createElement("li");
  listItem.innerHTML = stuff[i];
  stuffList.append(listItem);
}
```

`for of` loop:

```
for (const item of stuff) {
  let listItem = document.createElement("li");
  listItem.innerHTML = item;
  stuffList.append(listItem);
}

```

`forEach` method:

```
stuff.forEach((item) => {
  let listItem = document.createElement("li");
  listItem.innerHTML = item;
  stuffList.append(listItem);
});
```

`for in` loop the objects

```
for (const singleObject in nestedObjects) {
  let listItem = document.createElement("li");
  listItem.innerHTML = `Name: ${nestedObjects[singleObject].name}`;
  stuffList.append(listItem);
}
```

##### `map()` method

If you want to create a new array out of the original array, and iterated and do sth to the element inside the array, use `map()` method.

## 9 Events

##### Event handling

key to JS interactivity.

Use `.addEventListener`, it can be added to any element inside the window and inside the DOM.

```
button.addEventListener("click", () => {
  button.classList.toggle("active");
  console.log("Button was clicked!");
}, false);
```

- `"click"` is the event that we need to respond when capture it.
- There's a callback function inside the event listening function.
- The callback function can either be inline anonymous function or external function, there's no parentheses 












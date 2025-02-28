---
title: JavaScript
parent: Web Fundamental
nav_order: 83
layout: default
---

## JavaScript

JavaScript (often shortened to JS) is a high-level, dynamic, interpreted programming language. It's one of the core technologies of the World Wide Web, alongside HTML and CSS. While HTML provides the structure and content of a webpage and CSS handles the styling, JavaScript adds _interactivity_ and dynamic behavior. JavaScript can also be used outside of web browsers (e.g., in server-side environments using Node.js).

---

## Core Concepts

- **Variables:** Used to store data. JavaScript has three keywords for declaring variables:

  - `var` (older, function-scoped - generally avoid for new code)
  - `let` (block-scoped - recommended for most variables)
  - `const` (block-scoped, for variables that should not be reassigned)

  ```javascript
  let myVariable = "Hello";
  const PI = 3.14159;
  // PI = 3.14;  // This would cause an error (cannot reassign a const)
  ```

- **Data Types:** JavaScript has several fundamental data types:

  - **String:** Text (e.g., `"Hello, world!"`, `'Single quotes also work'`).
  - **Number:** Numeric values (e.g., `10`, `3.14`, `-5`).
  - **Boolean:** `true` or `false`.
  - **Null:** Represents the intentional absence of a value (`null`).
  - **Undefined:** Represents a variable that has been declared but not assigned a value (`undefined`).
  - **Object:** A collection of key-value pairs (e.g., `{ name: "John", age: 30 }`).
  - **Array:** An ordered list of values (e.g., `[1, 2, 3, "four", true]`).

- **Operators:** Symbols that perform operations on values (operands).

  - **Arithmetic:** `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponentiation)
  - **Assignment:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`
  - **Comparison:** `==` (loose equality), `===` (strict equality), `!=` (loose inequality), `!==` (strict inequality), `>`, `<`, `>=`, `<=`
  - **Logical:** `&&` (AND), `||` (OR), `!` (NOT)

- **Control Flow:** Statements that control the order in which code is executed.

  - **`if`/`else if`/`else`:** Conditional execution.

    ```javascript
    let age = 20;
    if (age >= 18) {
      console.log("You are an adult.");
    } else if (age >= 13) {
      console.log("You are a teenager.");
    } else {
      console.log("You are a child.");
    }
    ```

  - **`for` loop:** Repeats a block of code a specified number of times.

    ```javascript
    for (let i = 0; i < 5; i++) {
      console.log(i); // Prints 0, 1, 2, 3, 4
    }
    ```

  - **`while` loop:** Repeats a block of code as long as a condition is true.

    ```javascript
    let count = 0;
    while (count < 5) {
      console.log(count);
      count++;
    }
    ```

  - **`do...while` loop:** Similar to while loop, but the code block always runs at least one.
  - **`for...in` loop:** Iterates over the properties of an object.
  - **`for...of` loop:** Iterates over the values of an iterable object (e.g., an array, string).
  - **`switch` statement**: multi-way branch statement.

- **Functions:** Reusable blocks of code that perform a specific task.

  ```javascript
  function greet(name) {
    console.log("Hello, " + name + "!");
  }

  greet("Alice"); // Calls the function, prints "Hello, Alice!"
  ```

- **Objects:** Collections of key-value pairs. Objects can represent real-world entities or abstract concepts.

  ```javascript
  let person = {
    firstName: "John",
    lastName: "Doe",
    age: 30,
    greet: function () {
      console.log("Hello, my name is " + this.firstName);
    },
  };

  console.log(person.firstName); // Access a property: Prints "John"
  person.greet(); // Call a method: Prints "Hello, my name is John"
  ```

- **Arrays:** Ordered lists of values.

  ```javascript
  let colors = ["red", "green", "blue"];
  console.log(colors[0]); // Access an element: Prints "red"
  colors.push("yellow"); // Add an element to the end
  ```

- **DOM Manipulation:** JavaScript can interact with the HTML Document Object Model (DOM) to dynamically change the content and structure of a webpage. This is how JavaScript makes web pages interactive.

  ```javascript
  // Get an element by its ID
  let heading = document.getElementById("myHeading");

  // Change the text content of the element
  heading.textContent = "New Heading Text";

  // Add a new paragraph element
  let newParagraph = document.createElement("p");
  newParagraph.textContent = "This is a new paragraph.";
  document.body.appendChild(newParagraph);

  // Change CSS style
  heading.style.color = "red";
  ```

- **Events:** JavaScript can respond to user actions and other events (e.g., clicks, mouse movements, key presses, page loads).

  ```html
  <button onclick="handleClick()">Click Me</button>

  <script>
    function handleClick() {
      alert("Button clicked!");
    }
  </script>
  ```

  - Common Events: `click`, `mouseover`, `mouseout`, `keydown`, `keyup`, `load`, `submit`, `change`.
  - Event listeners can be attached to the HTML elements.

- **Asynchronous JavaScript (Promises, async/await):** JavaScript can perform tasks asynchronously (without blocking the main thread), which is important for handling network requests, timers, and other operations that might take time.

  ```javascript
  // Using Promises
  fetch(
    "[https://api.example.com/data](https://www.google.com/search?q=https://api.example.com/data)"
  )
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));

  // Using async/await (a cleaner syntax for working with Promises)
  async function fetchData() {
    try {
      let response = await fetch(
        "[https://api.example.com/data](https://www.google.com/search?q=https://api.example.com/data)"
      );
      let data = await response.json();
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  }

  fetchData();
  ```

- **Comments**:

  ```javascript
  // This is a single-line comment

  /*
  This is a
  multi-line comment
  */
  ```

---

## Adding JavaScript to HTML

- **Inline (generally avoid):** Directly within an HTML element's attributes.

  ```html
  <button onclick="alert('Hello!')">Click Me</button>
  ```

- **Internal (Embedded):** Within `<script>` tags, usually in the `<head>` or `<body>` of the HTML document.

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>My Page</title>
      <script>
        function sayHello() {
          alert("Hello from internal script!");
        }
      </script>
    </head>
    <body>
      <button onclick="sayHello()">Click Me</button>
    </body>
  </html>
  ```

- **External (Recommended):** In a separate `.js` file, linked to the HTML document using the `<script>` tag's `src` attribute. This promotes code organization and reusability.

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>My Page</title>
      <script src="script.js"></script>
    </head>
    <body>
      <button onclick="sayHello()">Click Me</button>
    </body>
  </html>
  ```

  `script.js`:

  ```javascript
  function sayHello() {
    alert("Hello from external script!");
  }
  ```

_Note:_ Place `<script>` tags at the end of the `<body>` element to improve page load performance (the HTML will be parsed before the JavaScript is loaded and executed). Use `defer` or `async` attributes.

---

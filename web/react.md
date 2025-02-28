---
title: React Basics
parent: Web Fundamental
nav_order: 84
layout: default
---

## React Basics

React is a JavaScript library for building user interfaces (UIs). It's component-based, meaning you build UIs by composing reusable, independent components. React efficiently updates and renders only the components that change, making it fast and performant. It's widely used for building single-page applications (SPAs) and interactive web interfaces.

---

### Core Concepts

- **Components:** The building blocks of React applications. A component is a JavaScript function or class that returns a React element (describing what should appear on the screen).

  - **Functional Components (Recommended):** Use JavaScript functions. Modern React heavily uses functional components with _hooks_ (see below).
  - **Class Components (Older Style):** Use ES6 classes. Still supported, but less common in new development.

- **JSX (JavaScript XML):** A syntax extension to JavaScript that looks like HTML. JSX makes it easier to write and understand React components' UI structure. JSX is _not_ HTML, but it's very close. JSX gets compiled into regular JavaScript function calls.

- **Props (Properties):** How components receive data from their parent components. Props are read-only within the component that receives them. They are passed to components as attributes, similar to HTML attributes.

- **State:** Internal data that a component manages. When a component's state changes, React re-renders the component (and its children) to reflect the change. State is managed using _hooks_ in functional components (primarily `useState`).

- **Hooks:** Functions that let you "hook into" React state and lifecycle features from _functional_ components. Prior to hooks, state and lifecycle methods were only available in class components.

  - `useState`: Adds state to a functional component.
  - `useEffect`: Performs side effects (e.g., data fetching, subscriptions, DOM manipulation) in functional components. Replaces lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` from class components.
  - `useContext`: Consumes context (shared data) in functional components.
  - ...and many more.

- **Virtual DOM:** A lightweight in-memory representation of the actual DOM. React uses the virtual DOM to optimize updates. When a component's state changes, React updates the virtual DOM, compares it to the previous version, and then efficiently updates _only_ the changed parts of the real DOM.

- **One-Way Data Binding:** Data flows in one direction: from parent components to child components (via props). This makes data flow predictable and easier to debug.

---

### Creating a React App (using Create React App)

The easiest way to start a new React project is to use `create-react-app`, a tool that sets up a basic React project with a development server, build scripts, and sensible defaults.

1.  **Install Node.js and npm:** React development requires Node.js and npm (Node Package Manager). Download and install them from [https://nodejs.org/](https://nodejs.org/).

2.  **Create the App:**

    ```bash
    npx create-react-app my-react-app  # Creates a new project in a directory named 'my-react-app'
    cd my-react-app                  # Navigate into the project directory
    npm start                        # Start the development server
    ```

    _Explanation:_

    - `npx`: A tool for running npm packages without globally installing them.
    - `create-react-app`: The command to create a new React app.
    - `my-react-app`: The name of your project (and the directory that will be created).
    - `npm start`: Starts a local development server (usually on `http://localhost:3000`). Changes you make to your code will automatically reload in the browser.

3.  **Project Structure (Simplified):**

    ```
    my-react-app/
    ├── node_modules/      # Dependencies (managed by npm, don't edit directly)
    ├── public/            # Static assets (HTML file, favicon, etc.)
    │   └── index.html     # The main HTML file
    ├── src/               # Your source code
    │   ├── App.js        # The main application component
    │   ├── index.js      # The entry point for your application
    │   ├── components/    # (You'll likely create this directory)
    │   └── ...
    ├── package.json       # Project metadata and dependencies
    └── README.md          # Project description
    ```

---

### Example: A Simple Functional Component

```javascript
// src/App.js (or src/components/MyComponent.js)
import React, { useState } from "react"; // Import React and the useState hook

function MyComponent(props) {
  // Functional component, receives props as an argument
  const [count, setCount] = useState(0); // Use the useState hook to manage state

  return (
    <div>
      <h1>Hello, {props.name}!</h1> {/* Use props */}
      <p>Count: {count}</p> {/* Display the state */}
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default MyComponent;
```

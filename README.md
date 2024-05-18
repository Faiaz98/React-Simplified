# React-Simplified

React is a JavaScript library for building user interfaces. It makes interactive UIs painless by efficiently updating and rendering the right components.


## Table of Contents

- Introduction to React
- Setting up a React Environment
- React Components
- JSX
- Props
- State
- Lifecycle Methods (Class Components)
- Hooks (Function Components)
- Event Handling
- Conditional Rendering
- Lists and Keys
- Forms
- Lifting State Up
- Composition vs Inheritance
- React Router
- Context API
- Error Boundaries
- Higher-Order Components (HOCs)
- Code Splitting and Lazy Loading
- Testing in React



## 1. Introduction to React

What is React?

React is a JavaScript library for building user interfaces. It makes creating interactive UIs painless by efficiently updating and rendering the right components when your data changes.

### Why Use React?

- Declarative: React makes it easy to create interactive UIs.
- Component-Based: Build encapsulated components that manage their own state.
- Learn Once, Write Anywhere: You can develop new features in React without rewriting existing code.


## 2. Setting Up a React Environment

**Using Create React App**

Create React App is an officially supported way to create single-page React applications. It offers a modern build setup with no configuration.

  1. Install Node.js and npm
  2. Run the following command in your terminal:
     ```bash
     npx create-react-app my-app
     cd my-app
     npm start
     ```

## Example:

Here's what each command does:

- `npx create-react-app my-app`: Creates a new React project named "my-app".
- `cd my-app`: Changes the directory to your new project.
- `npm start`: Starts the development server.


## 3. React Components

**What are Components?**

Components are the building blocks of a React application. They let you split the UI into independent, reusable pieces.

**Types of Components:**

- Function Components: JavaScript functions that return JSX.
- Class Components: ES6 classes that extend `React.Component`.

**Example: Function Component**

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

**Example: Class Component**

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```


## 4. JSX

**What is JSX?**

JSX stands for JavaScript XML. It allows you to write HTML in React. JSX makes it easier to write and add HTML in React.

**Example:**

```jsx
const element = <h1>Hello, world!</h1>;
```


## 5. Props

**What are Props?**

Props are arguments passed into React components. They are used to pass data from one component to another.

**Example:**

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name} </h1>;
}

//Usage
<Welcome name="Sara" />
```
## 6. State

**What is State?**

State is a built-in object that stores property values that belong to a component. State changes can be asynchronous and can trigger re-renders.

**Example: Class Component with State**

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date(),
    });
  }

  render() {
    return (
      <div>
        <h1>It is {this.state.date.toLocaleTimeString()}.</h1>
      </div>
    );
  }
}

```

## 7. Lifecycle Methods(Class Components)

**What are Lifecycle Methods?**

Lifecycle methods are special methods each component can have that allow us to run code at particular times in the process.

**Example: Common Lifecycle Methods**

- `componentDidMount()`: Executed after the first render.
- `componentDidUpdate(prevProps, prevState)`: Executed after every update.
- `componentWillUnmount()`: Executed just before the component is removed from the DOM.

## 8. Hooks(Function Components)

**What are Hooks?**

Hooks are functions that let you use state and other React features in function components.

**Common Hooks**

- `useState`: Allows you to add state to function components.
- `useEffect`: Allows you to perform side effects in function components.

**Example: useState Hook**

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

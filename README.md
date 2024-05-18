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


## 9. Event Handling

**Handling Events**

Handling events with React elements is very similar to handling events on DOM elements. There are some syntax differences:

- React events are named using camelCase.
- You pass a function as the event handler, not a string.

**Example:**

```jsx
function Toggle() {
  const [isOn, setIsOn] = useState(true);

  const handleClick = () => {
    setIsOn(!isOn);
  };

  return (
    <button onClick={handleClick}>
      {isOn ? 'ON' : 'OFF'}
    </button>
  );
}
```

## 10. Conditional Rendering

**What is Conditional Rendering?**

Conditional rendering in React works the same way conditions work in JavaScript. Use JavaScript operators like `if` or `condition ? true : false` to create elements representting the current state.

**Example:**

```jsx
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  }
  return <h1>Please sign up.</h1>;
}
```

## 11. Lists and Keys

**Rendering Lists**

You can build collections of elements and include them in JSX using curly braces `{}`.

**Example:**

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);

function NumberList() {
  return (
    <ul>{listItems}</ul>
  );
}

```

## 12. Forms

**Handling Forms**

Forms in React are similar to regular HTML forms but with some additional functionality.

**Example: Controlled Component**

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: '' };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ value: event.target.value });
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <button type="submit">Submit</button>
      </form>
    );
  }
}

```

## 13. Lifting State Up

**What is Lifting State Up?**

Lifting state up means moving the state to a common ancestor of the components that need it. This helps keep data consistent and allows components to share state.

**Example:**

```jsx
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>The water would boil.</p>;
  }
  return <p>The water would not boil.</p>;
}

class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.state = { temperature: '' };

    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.setState({ temperature: e.target.value });
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input
          value={temperature}
          onChange={this.handleChange} />
        <BoilingVerdict
          celsius={parseFloat(temperature)} />
      </fieldset>
    );
  }
}
```


## 14. Composition vs Inheritance

**Composition**

Composition is a way to combine multiple components into one.

**Example:**

```jsx
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

## 15. React Router

**What is React Router?**

React Router is a library that helps you handle routing in a React application, enabling navigation between views or pages.

**Basic Setup:**

1. Install React Router:

   ```bash
    npm install react-router-dom
   ```

2. Basic Example:

```jsx
    import { BrowserRouter as Router, Route, Link, Switch } from 'react-router-dom';

function App() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
          </ul>
        </nav>

        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

export default App;

```

## 16. Context API

**What is Context API?**

The Context API is a way to pass data through the component tree without having to pass props down manually at every level.

**Example:**

1. Create a Context:

```jsx
const ThemeContext = React.createContext('light');
```

2. Provide Context:

```jsx
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

3. Consume Context:

```jsx
function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = React.useContext(ThemeContext);
  return <button theme={theme}>Button</button>;
}
```

## 17. Error Boundaries

**What are Error Boundaries?**

Error boundaries are React Components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

**Example:**

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.log(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}

function MyComponent() {
  return (
    <ErrorBoundary>
      <MyWidget />
    </ErrorBoundary>
  );
}
```

## 18. Higher-Order Components (HOCs)

**What are Higher-Order Components?**

A higher-order component (HOC) is a function that takes a component and returns a new component. HOCs are used to reuse component logic.

```jsx
function withLogger(WrappedComponent) {
  return class extends React.Component {
    componentDidMount() {
      console.log('Component mounted');
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
}

const EnhancedComponent = withLogger(MyComponent);
```

## 19. Code Splitting and Lazy Loading

**What is Code Splitting?**

Code splitting allows you to split your code into smaller bundles which can be loaded on demand. This can improve the performance of your application.

**Example:**

```jsx
import React, { Suspense, lazy } from 'react';

const OtherComponent = lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

## 20. Testing in React

**Why Test React Applications?**

Testing ensures that your components render correctly and behave as expected.

**Tools for Testing:**

- Jest: A testing framework.
- React Testing Library: A library for testing React components.

**Example: Basic Test with React Testing Library**

1. Install React Testing Library:

```bash
npm install @testing-library/react
```

2. Write a test:

```jsx
import { render, screen } from '@testing-library/react';
import MyComponent from './MyComponent';

test('renders a message', () => {
  render(<MyComponent />);
  const linkElement = screen.getByText(/hello, world/i);
  expect(linkElement).toBeInTheDocument();
});
```

# REACT ES6 CLASSES
ES6 classes are a fundamental part of creating components in React. A class is a type of function, but instead of using the keyword function to initiate it, we use the keyword class, and the properties are assigned inside a ``constructor()`` method.

## Class Component
A class component is a type of React component defined using the ES6 class syntax. Unlike functional components, class components have access to state and lifecycle methods, which makes them powerful for handling complex logic.

### Basic Structure of a Class Component

```js
import React, { Component } from 'react';

class MyComponent extends Component {
  // State is defined in the constructor
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  // Method to handle button click
  handleIncrement = () => {
    this.setState({ count: this.state.count + 1 });
  };

  // Render method is required to display content
  render() {
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.handleIncrement}>Increment</button>
      </div>
    );
  }
}

export default MyComponent;

```

## Key Concepts of ES6 Classes in React
### 1.  State management
State in React is an object that stores dynamic data for a component. It allows components to respond to user input, server responses, or other events by updating the state, which then triggers a re-render of the component to reflect the new state.
#### How to Use State in a Class Component

* State is typically initialized in the constructor method.
* You update the state using the ``setState()`` method, which ensures that the component re-renders when state changes.
Example:
```js
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    // Initializing state
    this.state = {
      count: 0
    };
  }

  // Method to update state
  incrementCount = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.incrementCount}>Increment</button>
      </div>
    );
  }
}

export default Counter;

```
Explanation:
* The state object is initialized in the constructor.
``setState()`` is used to update the count value.  
* Every time the button is clicked, the component re-renders with the updated count.
* React automatically merges the new state with the existing state.

### 2. Props (Properties)
Props are short for "properties" and are a way to pass data from a parent component to a child component. Unlike state, props are read-only; they cannot be modified by the receiving component.

#### Using Props in a Class Component
Example:
```jsx
import React, { Component } from 'react';

// Child component
class Greeting extends Component {
  render() {
    return <h2>Hello, {this.props.name}!</h2>;
  }
}

// Parent component
class App extends Component {
  render() {
    return <Greeting name="Millyannah" />;
  }
}

export default App;
```

Explanation:
* The Greeting component receives name as a prop from the parent component App.
* The Greeting component uses this.props.name to display the value.
* Props allow components to be reusable and configurable.

### 3. Lifecycle Methods
Lifecycle methods in React class components allow you to run code at specific stages in the component's lifecycle. This can be useful for tasks like data fetching, setting up subscriptions, or cleaning up resources.
#### Example of Using Lifecycle Methods:
```jsx
import React, { Component } from 'react';

class Timer extends Component {
  constructor(props) {
    super(props);
    this.state = { seconds: 0 };
  }

  componentDidMount() {
    // Start a timer when the component mounts
    this.interval = setInterval(() => {
      this.setState({ seconds: this.state.seconds + 1 });
    }, 1000);
  }

  componentDidUpdate() {
    console.log('Component updated:', this.state.seconds);
  }

  componentWillUnmount() {
    // Clean up the interval timer
    clearInterval(this.interval);
  }

  render() {
    return <h1>Seconds elapsed: {this.state.seconds}</h1>;
  }
}

export default Timer;
```
Explanation:
* ``componentDidMount()`` starts a timer after the component is rendered.
* ``componentDidUpdate()`` logs every time the component updates due to the state change.
* ``componentWillUnmount()`` clears the interval to prevent memory leaks when the component is removed.

### 4. Event Handling
Event handling in class components is similar to handling events in regular HTML, but with some important differences in how this is managed.

#### Handling Events in a Class Component
* You can define event handler methods directly in the class.
* Use arrow functions or bind methods to the class instance to handle the correct context of this.

Example:
```jsx
import React, { Component } from 'react';

class ClickButton extends Component {
  constructor(props) {
    super(props);
    this.state = { message: 'Click the button!' };
  }

  // Arrow function to handle 'this' context
  handleClick = () => {
    this.setState({ message: 'Button clicked!' });
  };

  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <p>{this.state.message}</p>
      </div>
    );
  }
}

export default ClickButton;
```
Explanation:
* Using an arrow function for ``handleClick ensures that this correctly refers to the class instance.
* When the button is clicked, the state is updated, causing the component to re-render.
### 5. Conditional Rendering
Conditional rendering in React means displaying certain content based on specific conditions.

Example:
```jsx
import React, { Component } from 'react';

class UserStatus extends Component {
  constructor(props) {
    super(props);
    this.state = { isLoggedIn: false };
  }

  toggleLogin = () => {
    this.setState({ isLoggedIn: !this.state.isLoggedIn });
  };

  render() {
    return (
      <div>
        {this.state.isLoggedIn ? <h1>Welcome, User!</h1> : <h1>Please Log In</h1>}
        <button onClick={this.toggleLogin}>
          {this.state.isLoggedIn ? 'Logout' : 'Login'}
        </button>
      </div>
    );
  }
}

export default UserStatus;
```
Explanation:
* The component conditionally renders a welcome message or a login prompt based on ``isLoggedIn``.
* The button toggles the login status when clicked.
#### Summary
* State is used to manage dynamic data within a component.
* Props are used to pass data between components.
* Lifecycle methods let you run code at specific stages of a component's existence.
* Event handling allows for interactivity, such as handling user inputs.
* Conditional rendering determines which UI elements to display based on conditions.

While ES6 class components have largely been replaced by functional components with Hooks, understanding these concepts remains important, especially for maintaining older codebases.
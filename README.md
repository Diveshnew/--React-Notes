# React-Learning

## :skull:Anatomy
> What are all the files in a React project?

### `React Build Tools`
There are many ways to build a react app. The most common options include:

1. [Create React App](https://create-react-app.dev/)
2. [Vite](https://vitejs.dev/)
3. [Next.js](https://nextjs.org/)
4. [Gatsby](https://www.gatsbyjs.com/)

### `React Files`
Get familiar with the files in your React project.

- `package.json` - The main file that defines the dependencies and other settings for your project.
- `node_modules` - Source code for depencies. Do not touch.
- `public` - The directory where your static files are stored.
- `src/index.js` - Main entrypoint to bootstrap the app.
- `src/App.js` - The root component of the app.
- `src/App.spec.js` - Unit tests for the app.
- `src/*.css` - Styles for the app.

### `Challenge`
Generate a new project with `npx create-react-app my-app`.

#

## :card_file_box:Components
> How does a component-based architecture for building UIs actually work?

### `React Dev Tools`
React Components are reusable pieces of UI that developers compose together as a tree to represent a complete frontend application. Before writing any code, install the [React Dev Tools](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) extension and go to a website like Facebook that uses react and inspect its code.

### `Define Components with JSX`
Now in your code, define a component by declaring a JavaScript function. It can use the function keyword, or be a function expression if you prefer. It’s return value is the UI represented in a JavaScript friendly version of HTML called JSX. It typically starts with parentheses, followed by exactly one parent element, or an empty element called a fragment, followed by some HTML. But it’s no ordinary HTML - it can also run JavaScript allowing you to include dynamic values from your code using braces. Once a component is defined it can be declared or used in other parts of the UI similar to other HTML elements.

```App.jsx
function MyComponent() {
  return <p>🔥 Hello!</p>;
}

<MyComponent />
```

### `Share Data with Props`
You can pass data into a component with props. Every functional component has a props argument that can accept external data. A prop can be a primitive value like a string or number, and object, or even another React component. Components can pass props from a parent to child, but not vice versa. This means that any state or data that changes is owned by one component, and can only be used by its children. This creates a one-way or unidirectional dataflow that keeps your code modular and predictable.

```App.jsx
function MyComponent(props) {
  return <p>🔥 {props.name}</p>;
}

<MyComponent name="Jeff" />


// Or use desctruturing to pass props

function MyComponent({ name }) {
  return <p>🔥 {name}</p>;
}

// Use braces to pass an expression

<MyComponent name={`JeffD` + 23} />
```

### `Virtual DOM and React Fiber`
What makes React so powerful, is that when this data changes the library knows how to efficiently rerend any each component using an internal mechanism called the [Virtual DOM](https://legacy.reactjs.org/docs/faq-internals.html) and more recently React Fiber. You don’t need to know much about VDOM or Fiber to use React, but it is important to be aware that it’s the magic that reconciles your react code with the real DOM in the browser at runtime. It you want to go further down this rabbit hole, check out the official documentation.

### `Challenge`
Define a set of 2 components - Card and Icon. the card takes the icon as a prop, then renders custom HTML below it with `props.children`.
[![PRACTICE LIVE](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/https://stackblitz.com/edit/react-b7htyi?file=src%2FApp.js)
```App.js
import React from 'react';
import './style.css';

function Card(props) {
  return (
    <section>
      <h2>{props.icon} Title</h2>
      {props.children}
    </section>
  );
}

function MyIcon() {
  return <i>🔥</i>;
}

export default function App() {
  return (
    <div>
      <Card icon={<MyIcon />}>
        <p>The body of the card</p>
      </Card>
    </div>
  );
}

```

#

## :arrows_clockwise:Conditional Rendering
> How to render a component based on a boolean condition

Conditional rendering is a very common pattern where you render a component based on a boolean condition. There are several ways to implement conditional rendering in React.


### `Option 1: If Else`
```App.js
function Conditional({ count }) {

  if (count > 5) {
    return <h1>Count is greater than 5</h1>;
  } else {
    return <h1>Count is less than 5</h1>;
  }
}
```


### `Option 2: Ternary`
```App.js
{count % 2 === 0 ? <h1>Count is even</h1> : <h1>Count is odd</h1> }
```


### `Option 3: Logical And`
```App.js
{count && 2 === 0 ? <h1>Count is even</h1> }
```


### `Challenge`
Define a LoadingButton component. The button takes loading state, onClick, and label as props then renders the label or loader depending on the loading state.
```App.js
import React, { useState } from 'react';
import './style.css';

const LoadingButton = (props) => {
  return (
    <button onClick={props.onClick} type="button">
      {props.loading ? <div className="loader" /> : props.label}
    </button>
  );
};

// Alternative
// const LoadingButton = (props) => {
//   const { onClick, loading, label } = props;
//   return (
//     <button onClick={onClick} type="button">
//       {loading ? <div className="loader" /> : label}
//     </button>
//   );
// };

// Alternative
// const LoadingButton = ({ onClick, loading, label }) => {
//   return (
//     <button onClick={onClick} type="button">
//       {loading ? <div className="loader" /> : label}
//     </button>
//   );
// };

function App() {
  const [isLoading, setIsLoading] = useState(false);

  return (
    <>
      <LoadingButton
        label="Press me"
        loading={isLoading}
        onClick={() => setIsLoading(!isLoading)}
      />
    </>
  );
}

export default App;

```

#

## :arrows_counterclockwise:Loops
> How to render a collection of items in JSX

### `Array Map`
The most common way to loop over a collection of data in React is to use the Array map method. It takes a callback function that gets called on each element to transform the data into UI elements.

```App.js
const data = [
  { id: 1, name: 'Fido 🐕' },
  { id: 2, name: 'Snowball 🐈' },
  { id: 3, name: 'Murph 🐈‍⬛' },
  { id: 4, name: 'Zelda 🐈' },
];

function ListOfAnimals() {
  return (
    <ul>
      {data && // Only render if there's data - see 'Conditional Rendering'
        data.map(({ id, name }) => {
          return <li key={id}>{name}</li>;
        })}
    </ul>
  );
}
```

### `Challenge`

Define an array of animals called data. Use a .map() to return a list of all the animals in the data array.

```App.js
import React from 'react';
import './style.css';

const data = [
  { id: 1, name: 'Fido 🐕' },
  { id: 2, name: 'Snowball 🐈' },
  { id: 3, name: 'Murph 🐈‍⬛' },
  { id: 4, name: 'Zelda 🐈' },
];

function App() {
  return (
    <>
      <ul>
        {data &&
          data.map(({ id, name }) => {
            return <li key={id}>{name}</li>;
          })}
      </ul>
    </>
  );
}

export default App;

```

#

## :parasol_on_ground:Events
> How to handle events in JSX

### `Events in Vanilla JS`
```App.js
const button = document.querySelector('button');

button.addEventListener('click', (event) => {
    console.log(event);
})
```


### `Events in React`
```App.js
function Events() {

  return <button onClick={(event => console.log(event))}>Click</button>
}
```

### `Challenge`

Implement a text input that updates the input value and logs the event target.
```App.js
import React, { useState } from 'react';
import './style.css';

function App() {
  const [value, setValue] = useState('');

  const eventHandler = (e) => {
    setValue(e.target.value);
    console.log(e.target);
  };

  return (
    <>
      <input
        value={value}
        placeholder="Enter some text"
        onChange={eventHandler}
      />
    </>
  );
}

export default App;

```

#

## :carousel_horse:State
> Working with the useState hook

### `Basic Usage`
```App.js
function Stateful() {

  const [count, setCount] = useState(0);
  const [prevCount, setPrevCount] = useState(0);

  const handleClick = () => {
    setCount((prev) => {
      setPrevCount(prev);
      setCount(count + 1);
    });
  };

  return (
    <>
      <h3>Current count: {count}</h3>
      <h3>Previous count: {prevCount}</h3>
      <button onClick={handleClick}>Increment</button>
    </>
  );
}
```

### `Updating Objects with useState`
```App.js
function Stateful() {
  const [state, setState] = useState({ count: 0, user: 'Bob' });

  const handleClick = () => {
    setState({
      ...state,
      count: state.count + 1,
    });
  };

  return (
    <>
      <h3>Count: {state.count}</h3>
      <h3>User: {state.user}</h3>
      <button onClick={handleClick}>Increment</button>
    </>
  );
}
```

### `Challenge`

Implement a `handleClick()` function to handle state using `useState()`.

```App.js
import React, { useState } from 'react';
import './style.css';

function App() {
  const [count, setCount] = useState(0);
  const [prevCount, setPrevCount] = useState(0);

  // const [state, setState] = useState({ count: 0, user: 'Bob' });

  const handleClick = () => {
    setCount((prev) => {
      setPrevCount(prev);
    });
    setCount(count + 1);
  };

  // const handleClick = () => {
  //   setState({
  //     ...state,
  //     count: state.count + 1,
  //   });
  // };

  return (
    <>
      <h3>Current count: {count}</h3>
      <h3>Previous count: {prevCount}</h3>
      {/* <h3>Count: {state.count}</h3>
      <h3>User: {state.user}</h3> */}
      <button onClick={handleClick}>Increment</button>
    </>
  );
}

export default App;

```

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/___YOUR_PATH___)

#

## :seedling:Lifecycle and Effects
> Working with the useEffect hook

### `Lifecycle with Class Components`
```App.js
class Lifecycle extends React.Component {
  
  componentDidMount() {
    // Initialize
  }

  componentDidUpdate() {
    // Updated
  }

  componentWillUnmount() {
    // Removed
  }
}
```

### `Lifecycle with useEffect`
```App.js
function Lifecycle() {

  const [count] = useState(0);

  useEffect(() => {
    
    console.log('count updated!')

    return () => console.log('destroyed!')

  }, [count]);

}
```

### `Challenge`

Implement a `CountdownTimer` component that implements `useState()` and `useEffect()` in conjunction with `setInterval` to handle the timer. Make sure you use the `useEffect()` hook to call `clearTimeout()` when the component is destroyed.
```App.js
import React, { useState, useEffect } from 'react';
import './style.css';

const Countdown = ({ hr, min, sec }) => {
  const [over, setOver] = useState(false);
  const [paused, setPaused] = useState(true);
  const [[h, m, s], setTime] = useState([hr, min, sec]);

  const tick = () => {
    if (paused || over) {
      return;
    }
    if (h === 0 && m === 0 && s === 0) {
      setOver(true);
    } else if (m === 0 && s === 0) {
      setTime([h - 1, 59, 59]);
    } else if (s === 0) {
      setTime([h, m - 1, 59]);
    } else {
      setTime([h, m, s - 1]);
    }
  };

  const handleReset = () => {
    setTime([hr, min, sec]);
    setPaused(true);
    setOver(false);
  };

  const handlePause = () => setPaused(!paused);

  const fmt = (val) => val.toString().padStart(2, '0');

  useEffect(() => {
    let ticker = setInterval(() => tick(), 1000);
    return () => {
      clearInterval(ticker);
    };
  });

  return (
    <>
      <h3 className="countdown">{`${fmt(h)}:${fmt(m)}:${fmt(s)}`}</h3>
      <button onClick={handlePause}>{paused ? 'Start' : 'Pause'}</button>
      <button onClick={handleReset}>Reset</button>
    </>
  );
};

function App() {
  return (
    <div>
      <Countdown hr={1} min={45} sec={0} />
    </div>
  );
}

export default App;

```

#

## :evergreen_tree:Context
> Working with the React Context API

### `Example of Prop Drilling`
```App.js
function PropDrilling() {

  const [count] = useState(0);

  return <Child count={count} />
}

function Child({ count }) {
  return <GrandChild count={count} />
}

function GrandChild({ count }) {
  return <div>{count}</div>
}
```

### `Sharing Data with Context`
```App.js
function PropDrilling() {

  const [count] = useState(0);

  return (
    <CountContext.Provider value={count}>
      <Child />
    </CountContext.Provider>
  )
}

function Child() {
  return <GrandChild />
}

function GrandChild() {

  const count = useContext(CountContext);

  return <div>{count}</div>
}
```

### `Challenge`
Create `CountContext` and `CountProvider` that uses `{ count, setCount }` as its values. This will allow the count and setCount function to be passed to any of its `{children}` in the tree. Create 2 components `Count` and `CountButton` that can each call `useContext(CountContext)` to update the count and display the current count value.
```App.js
import React, { useContext, createContext, useState } from 'react';
import './style.css';

const CountContext = createContext();

function CountProvider({ children }) {
  const [count, setCount] = useState(0);

  return (
    <CountContext.Provider value={{ count, setCount }}>
      {children}
    </CountContext.Provider>
  );
}

function Count() {
  const { count } = useContext(CountContext);
  return <h3>{`Current count: ${count}`}</h3>;
}

function CountButton() {
  const { setCount } = useContext(CountContext);
  return (
    <button onClick={() => setCount((count) => setCount(count + 1))}>
      Increment
    </button>
  );
}

function App() {
  return (
    <CountProvider>
      <Count />
      <CountButton />
    </CountProvider>
  );
}

export default App;
```

#

## :bangbang: Error Boundries
> How do Error Boundaries work in React?

```App.js
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.log('something went horribly wrong', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Fallback UI</h1>;
    }

    return this.props.children;
  }
}

// Example Usage

function Main() {
  return (
    <Dashboard>
      <ErrorBoundary>
        <Orders />
      </ErrorBoundary>
    </Dashboard>
  );
}
```

### `Challenge`
Create an `ErrorBoundary` class component that provides a fallback UI in the event an error occurs.
```App.js
import React from 'react';
import './style.css';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    // Change to true to enable error
    this.state = { hasError: true };
  }
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  componentDidCatch(err, errInfo) {
    console.log('something went horribly wrong', err, errInfo);
  }

  render() {
    if (this.state.hasError) {
      return (
        <div className="error-boundary">
          <h3>Fallback UI</h3>
        </div>
      );
    }
    return this.props.children;
  }
}

function App() {
  return (
    <div>
      <h3>Outside the error boundary</h3>
      <ErrorBoundary>
        <h3>Inside the error boundary</h3>
      </ErrorBoundary>
    </div>
  );
}

export default App;
```

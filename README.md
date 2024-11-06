\*\*React Hooks Overview\*\*

\*\*1. Introduction to Hooks\*\*

\- \*\*Definition\*\*: Hooks are functions that enable functional
components to manage state and lifecycle methods, similar to class
components .

\- \*\*Purpose\*\*: They simplify the way developers can use state and
other React features without needing to convert components to classes .

\*\*2. useState Hook\*\*

\- \*\*Purpose\*\*: The \`useState\` hook allows you to add state to
functional components .

\- \*\*State Definition\*\*: State refers to the values or variables
that determine the component\'s behavior and rendering .

\- \*\*Example\*\*:
import React, { useState } from 'react';

function Counter() {
  const [counter, setCounter] = useState(0);

  const increaseCounter = () => setCounter(counter + 1);

  return (
    <div>
      <p>Counter: {counter}</p>
      <button onClick={increaseCounter}>Increment</button>
    </div>
  );
}

export default Counter;

\- Create a counter component using \`useState\`:

\`\`\`javascript

const \[counter, setCounter\] = useState(0);

\`\`\`

\- Increment the counter:

\`\`\`javascript

const increaseCounter = () =\> setCounter(counter + 1);

\`\`\`

\- This updates the displayed counter value when the button is clicked .

\*\*3. Handling Objects with useState\*\*
import React, { useState } from 'react';

function UserDetails() {
  const [details, setDetails] = useState({ counter: 0, name: '' });

  const increaseCounter = () =>
    setDetails((prev) => ({ ...prev, counter: prev.counter + 1 }));

  return (
    <div>
      <p>Counter: {details.counter}</p>
      <button onClick={increaseCounter}>Increment</button>
    </div>
  );
}

export default UserDetails;

\- \*\*Object State\*\*: You can manage state as an object:

\`\`\`javascript

const \[details, setDetails\] = useState({ counter: 0, name: \'\' });

\`\`\`

\- \*\*Updating State\*\*: Use the spread operator to maintain previous
state values:

\`\`\`javascript

setDetails(prev =\> ({ \...prev, counter: prev.counter + 1 }));

\`\`\`

\- This ensures that other properties remain intact when updating .

\*\*4. useEffect Hook\*\*

\- \*\*Purpose\*\*: The \`useEffect\` hook is used to handle side
effects in functional components, such as data fetching or DOM
manipulation .

\- \*\*Usage\*\*: It accepts two arguments: a callback function for the
side effect and an optional dependency array .
import React, { useState, useEffect } from 'react';

function DataFetcher() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []); // Empty dependency array means this runs once on mount

  return (
    <div>
      <h2>Fetched Data:</h2>
      <ul>
        {data.map((item) => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}

export default DataFetcher;

\- \*\*Variations\*\*:

\- \*\*Without Dependencies\*\*: Runs on every render.

\- \*\*With Empty Array\*\*: Runs only on the first render, useful for
fetching data .

\- \*\*With Variables\*\*: Runs when specified variables change .

\- \*\*Cleanup Function\*\*: Use a return function within \`useEffect\`
to clean up side effects when the component unmounts .

\*\*5. useContext Hook\*\*

\- \*\*Purpose\*\*: \`useContext\` is used for managing global data in a
React application, avoiding the need to pass props through multiple
layers of components .
import React, { createContext, useContext } from 'react';

const ThemeContext = createContext();

function ThemedComponent() {
  const theme = useContext(ThemeContext);
  return <div style={{ backgroundColor: theme.background }}>Hello World</div>;
}

function App() {
  const theme = { background: 'lightblue' };

  return (
    <ThemeContext.Provider value={theme}>
      <ThemedComponent />
    </ThemeContext.Provider>
  );
}

export default App;

\- \*\*Steps to Use\*\*:

1\. \*\*Create Context\*\*: Use \`createContext\` to create a context .

2\. \*\*Provide Context\*\*: Use the context provider to wrap components
that need access to the context .

3\. \*\*Consume Context\*\*: Use \`useContext\` to access the context
value in any component .

\*\*6. useRef Hook\*\*

\- \*\*Purpose\*\*: \`useRef\` allows access to DOM elements and creates
mutable variables that do not cause re-renders .
import React, { useRef } from 'react';

function InputFocus() {
  const inputRef = useRef(null);

  const focusInput = () => inputRef.current.focus();

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Type something..." />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}

export default InputFocus;

\- \*\*Example\*\*:

\- Create a mutable variable:

\`\`\`javascript

const count = useRef(0);

\`\`\`

\- Access a DOM element:

\`\`\`javascript

const inputRef = useRef(null);

\<input ref={inputRef} /\>

\`\`\`

\- This allows direct manipulation of the DOM without triggering a
re-render .

\*\*7. Summary of Key Concepts\*\*

\- \*\*Hooks\*\*: Functions that enable state and lifecycle management
in functional components.

\- \*\*useState\*\*: Manages state variables.

\- \*\*useEffect\*\*: Handles side effects and cleanup.

\- \*\*useContext\*\*: Manages global state without prop drilling.

\- \*\*useRef\*\*: Accesses DOM elements and creates mutable variables.

This structured overview provides a clear understanding of the key
concepts and functionalities of React Hooks, using relevant excerpts for
reference.

\*\*React Hooks Overview\*\*

\*\*1. useRef Hook\*\*

\- \*\*Purpose\*\*: Allows the creation of mutable variables that do not
cause re-renders. Useful for accessing DOM elements without using
\`document.getElementById\` or class names.

\- \*\*Syntax\*\*:

\`\`\`javascript

const inputElement = useRef(initialValue);

\`\`\`

\- \*\*Accessing Properties\*\*: Use \`inputElement.current\` to access
or update the DOM element\'s properties .

\*\*2. useReducer Hook\*\*

\- \*\*Purpose\*\*: Manages state in React applications, functioning as
a state management tool. Ideal for complex state logic.
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}

export default Counter;

\- \*\*Syntax\*\*:

\`\`\`javascript

const \[state, dispatch\] = useReducer(reducer, initialState);

\`\`\`

\- \*\*Reducer Function\*\*: Takes two parameters: \`state\` (current
state) and \`action\` (action to perform). Returns the updated state
based on the action type .

\- \*\*Example\*\*: A counter application using \`useReducer\` to manage
increment and decrement actions .

\*\*3. useLayoutEffect Hook\*\*

\- \*\*Purpose\*\*: Similar to \`useEffect\`, but runs synchronously
before the DOM is painted. Useful for measuring elements or performing
layout calculations.
import React, { useLayoutEffect, useRef, useState } from 'react';

function LayoutComponent() {
  const boxRef = useRef(null);
  const [boxSize, setBoxSize] = useState({ width: 0, height: 0 });

  useLayoutEffect(() => {
    setBoxSize({
      width: boxRef.current.offsetWidth,
      height: boxRef.current.offsetHeight,
    });
  }, []);

  return (
    <div>
      <div ref={boxRef} style={{ width: '200px', height: '100px', background: 'lightgray' }} />
      <p>Width: {boxSize.width}, Height: {boxSize.height}</p>
    </div>
  );
}

export default LayoutComponent;

\- \*\*Difference from useEffect\*\*: \`useLayoutEffect\` runs before
the DOM is updated, while \`useEffect\` runs after .

\- \*\*Use Case\*\*: Measuring dimensions of an element and applying
styles accordingly .

\*\*4. useMemo Hook\*\*

\- \*\*Purpose\*\*: Optimizes performance by memoizing expensive
calculations, preventing them from running on every render.
import React, { useMemo, useState } from 'react';

function ExpensiveCalculationComponent({ num }) {
  const calculateFactorial = (n) => {
    console.log("Calculating factorial...");
    return n <= 1 ? 1 : n * calculateFactorial(n - 1);
  };

  const factorial = useMemo(() => calculateFactorial(num), [num]);

  return <p>Factorial of {num} is {factorial}</p>;
}

export default ExpensiveCalculationComponent;

\- \*\*Syntax\*\*:

\`\`\`javascript

const memoizedValue = useMemo(() =\> computeExpensiveValue(a, b), \[a,
b\]);

\`\`\`

\- \*\*Example\*\*: Memoizing a calculation based on an input number to
avoid unnecessary recalculations .

\*\*5. useCallback Hook\*\*

\- \*\*Purpose\*\*: Returns a memoized callback function, preventing
function recreation on re-renders.
import React, { useState, useCallback } from 'react';

function List({ getItems }) {
  return (
    <ul>
      {getItems().map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

function App() {
  const [count, setCount] = useState(0);

  const getItems = useCallback(() => {
    return [count, count + 1, count + 2];
  }, [count]);

  return (
    <div>
      <List getItems={getItems} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default App;

\- \*\*Syntax\*\*:

\`\`\`javascript

const memoizedCallback = useCallback(() =\> { doSomething(a, b); }, \[a,
b\]);

\`\`\`

\- \*\*Example\*\*: Using \`useCallback\` to optimize a function that
generates a table based on an input number, preventing unnecessary
recalculations when other state changes occur .

\*\*6. Custom Hooks\*\*

\- \*\*Definition\*\*: Reusable functions that encapsulate logic using
one or multiple built-in React hooks. They allow for cleaner and more
maintainable code.

\- \*\*Example\*\*: Creating a custom hook for fetching data from an
API, which can be reused across multiple components .
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}

// Usage
import React from 'react';
import useFetch from './useFetch';

function App() {
  const { data, loading } = useFetch('https://api.example.com/data');

  return (
    <div>
      {loading ? <p>Loading...</p> : <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
}

export default App;

\*\*Key Takeaways\*\*

\- React hooks enhance functional components by managing state and side
effects efficiently.

\- Understanding when and how to use each hook is crucial for building
performant React applications.

# Custom hooks

How do you see the interaction between the user interface and the logic? The view must draw elements for the user and record and display data based on the user's interactions. The logic, on the other hand, is responsible for requesting, generating, and processing data, as well as storing it for future use. In React, we can put States and use Effects to detect their changes, and we can handle a store-action app with these two Hooks. We can, however, make our own Hooks. Custom Hook is a single function that is prefixed with the word "use," such as "**useUser**" or "**useRole**." Hooks allow for the encapsulation and abstraction of complex operations into functional and linear code.

To create a hook, we must first understand that a custom hook is an extension for other hooks that is designed to expose a CUSTOM PROGRAMMING INTERFACE.&#x20;

## Functions and Results <a href="#b7fd" id="b7fd"></a>

A function is analogous to a black box that performs some action on input and produces some output. Identical to a crushing machine. The machine crushes something into a finished product (maybe a bin block). Using functions allows you to solve problems without having to know all of the details. Consider retrieving data from a server and having to recall the entire procedure each time. We can return any result we want when we write a custom function. The "programming interface" or "programming layout" is what this is called. The goal is to return the states and actions needed to start a conversation between the black-box (the internal function) and the external code. As if it were a window.

> The function is the black-box that exposes a programming interface to brings data throughout complex logic to simplify logic.

## Custom Hook <a href="#8fa7" id="8fa7"></a>

### Why custom hooks? <a href="#why-custom-hooks" id="why-custom-hooks"></a>

Because hooks can be treated in a variety of ways like functions, what we know about functions still applies.

* They're reusable
* We can break our larger hooks into smaller hooks
* We can compose our smaller hooks together, like lego bricks
* They're testable

Sure, you could always re-use the same sequence of hooks in each component (useState, useEffect, update state...), but why repeat yourself when you could extract the logic out into a well-tested custom hook?

A Custom Hook is in fact this. A window-programming-interface to expose states and actions and simplify the code. Let’s see an example.

We define a hook called "**useCounter**" in the following code. It reveals the "count" value thus far (state of current counting). And receive actions such as "reset with some value," "increment by one," "decrement by one," "add some value," and "subtract some value." This programming interface is accessible to any component and always performs the same function.

> **useCounter** — Create a counter and increment or decrement it by actions.

Any component that “use” this custom hook, it will able to get the current counting value and change the value throughout the defined actions.

```jsx
import { useReducer, useState } from "react";
import "./styles.css";

function useCounter() {
  const [count, setCount] = useState(0);

  return {
    count,
    increment() {
      setCount(count + 1);
    },
    decrement() {
      setCount(count - 1);
    },
    reset(value = 0) {
      setCount(value);
    },
    add(value = 0) {
      setCount(count + value);
    },
    subsctract(value = 0) {
      setCount(count - value);
    }
  };
}

export default function App() {
  const { count, increment, decrement, reset } = useCounter();

  return (
    <div className="w-screen h-screen flex flex-col justify-center items-center">
      <div className="p-10">
        <h1>{count}</h1>
      </div>
      <div className="p-2">
        <button
          className="rounded bg-purple-500 hover:bg-purple-700 focus:outline-none text-white px-2 py-1"
          onClick={() => increment()}
        >
          Increment
        </button>
      </div>
      <div className="p-2">
        <button
          className="rounded bg-purple-500 hover:bg-purple-700 focus:outline-none text-white px-2 py-1"
          onClick={() => decrement()}
        >
          Decrement
        </button>
      </div>
      <div className="p-2">
        <button
          className="rounded bg-red-500 hover:bg-red-700 focus:outline-none text-white px-2 py-1"
          onClick={() => reset()}
        >
          Reset
        </button>
      </div>
    </div>
  );
}
```

{% embed url="https://codesandbox.io/embed/usecounter-tvumj7?fontsize=14&hidenavigation=1&theme=dark" %}

# ❕ Custom hooks

How do you imagine the communication between the _view_ and the _logic_? The _view_ need to draw elements for user, It is responsible to catch user’s interaction and display data. On the other hand, the logic is responsible to request, generate and process the _data_, and save it for future access. In _React_, we can put _States_ and detect its changes by _Effects_, throughout this two _Hooks_, we can handle a _store-action_ _app_. But, we can also create our own Hooks. _Custom Hook_ is in fact a single function, prefixed by the word _“use”_, for example “_useTable_” or “_usePayment_”. This _hooks_ allows to encapsulate and abstract complex operations, into a functional and linear code.

To make a _hook_, we need to understand that a _custom hook_ is an extension for other _hooks_, and it is intended to expose a _CUSTOM PROGRAMMING INTERFACE_. In this article, we will learn about this concept.

## Functions and Results <a href="#b7fd" id="b7fd"></a>

_Function_ is like a black-box that do something with input and throw some output. Similar to a _**crushing machine**_. The machine takes something and crushes it into a result (maybe a bin block). Using functions allows solve tasks without the complex understanding about details. Imagine fetch data from server and have to remember whole process every time.

When we make a custom function, we are free to return any result. This result is called “the programming interface” or maybe “the programming layout”. The idea is return the states and actions necessary to create a dialog between the black-box (the function inside) and the external code. Like a window.

> The function is the black-box that exposes a programming interface to brings data throughout complex logic to simplify logic.

## Custom Hook <a href="#8fa7" id="8fa7"></a>

A Custom Hook is in fact this. A window-programming-interface to expose states and actions and simplify the code. Let’s see an example.

In the next code, we define a hook, called “_useCounter_”. It exposes the “_count_” value so far (state of current counting). And receive some actions like “_reset with some value_”, “_increment by one_”, “_decrement by one_”, “_add some value_” and “_substract some value_”. This _programming interface_ is exposed to any component and always do the same thing.

> useCounter — Create a counter and increment or decrement it by actions.

Any component that “use” this custom hook, it will able to get the current counting value and change the value throughout the defined actions.

> This kind of _**programming-interface**_ allows to handle data in a secure-way.

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

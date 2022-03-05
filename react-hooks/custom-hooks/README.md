# ❕ Custom hooks

How do you envision the interaction between the Ui and the logic? The view must draw elements for the user, as well as record and display data from the user's interactions. The logic, on the other hand, is in charge of requesting, generating, and processing data, as well as saving it for future use. In React, we can put States and detect their changes with Effects, and we can handle a store-action app with these two Hooks. However, we can also make our own Hooks. Custom Hook is actually a single function, prefixed with the word "use," such as "useTable" or "usePayment." This hooks enable the encapsulation and abstraction of complex operations into functional and linear code.

To create a hook, we must first understand that a custom hook is an extension for other hooks that is designed to expose a CUSTOM PROGRAMMING INTERFACE.&#x20;

## Functions and Results <a href="#b7fd" id="b7fd"></a>

A function is similar to a black box that does something with input and produces some output. The same as a crushing machine. The machine takes something and crushes it into a finished product (maybe a bin block). Using functions allows you to solve tasks without having to have a deep understanding of the details. Consider retrieving data from a server and having to remember the entire process each time. When we write a custom function, we can return any result we want. This is known as the "programming interface" or "programming layout." The goal is to return the states and actions required to initiate a conversation between the black-box (the function inside) and the external code. As in a window.



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

# ⚠ Custom hook pattern

Let's take a closer look at "reversal of control" here. Now the main logic is a user custom Hook forwarded to These hooks are user-accessible and allow easier control of the component by exposing several internal logic ( States , Handlers ) .

## Libraries that use this pattern

{% embed url="https://react-table.tanstack.com/docs/examples/basic" %}

{% embed url="https://react-hook-form.com/api" %}

## Advantages

More Control: Users can change the behavior of the main component by inserting their own logic between hooks and JSX components.

```jsx
import React from "react";
import { Counter } from "./Counter";
import { useCounter } from "./useCounter";

const Component =()=> {
  const { count, handleIncrement, handleDecrement } = useCounter(0);
  const MAX_COUNT = 10;

  const handleClickIncrement = () => {
    //Put your custom logic
    if (count < MAX_COUNT) {
      handleIncrement();
    }
  };

  return (
    <>
      <Counter value={count}>
        <Counter.Decrement
          icon={"minus"}
          onClick={handleDecrement}
        />
        <Counter.Label>Counter</Counter.Label>
        <Counter.Count />
        <Counter.Increment
          icon={"plus"}
          onClick={handleClickIncrement}
        />
      </Counter>
      <div>
        <button onClick={handleClickIncrement} >
          Custom increment btn 1
        </button>
      </div>
    </>
  );
}

export { Component };
```

&#x20;

![](https://blog.kakaocdn.net/dn/bIx0uy/btrh9RSWNVh/y3eFHfdUAKbbqZB7cO5Ul1/img.jpg)

## &#x20;Disadvantages

Implementation complexity: the logic is decoupled from the rendering and it is up to you to connect the two. To properly implement a component, you need a deep understanding of how the component works.

{% embed url="https://codesandbox.io/embed/react-patterns-uenl15?fontsize=14&hidenavigation=1&module=%2Fsrc%2Fpatterns%2Fcustom-hooks%2FUsage.js&theme=dark" %}

## References and articles :

{% embed url="https://blog.bitsrc.io/new-react-design-pattern-return-component-from-hooks-79215c3eac00" %}

{% embed url="https://blog.logrocket.com/advanced-react-hooks-creating-custom-reusable-hooks" %}

{% embed url="https://blog.logrocket.com/react-render-props-vs-custom-hooks" %}

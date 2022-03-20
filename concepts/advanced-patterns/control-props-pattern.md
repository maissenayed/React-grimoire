# ⚠ Control Props Pattern

Normally, you would control the state of a component from within its internal state. But there are a few instances where you want to be able to override the internal state of a component and control the state from the parent component such as updating content when something happens outside the component. This is easily achieved with the controlled props pattern. For example, you have a dropdown that keeps track of its own `open` state internally. But we want the parent component to be able to update the state of the component based on some other logic.

This pattern transforms a component into a Controlled Component . External state serves as a "single source of truth" that allows users to insert custom logic to change the default behavior of a component.

## Libraries that use this pattern

{% embed url="https://mui.com/components/rating#rating" %}

## Advantages

Giving more control: Because the main state is exposed outside the component, the user has direct control over that component.

```jsx
import React, { useState } from "react";
import { Counter } from "./Counter";

const Component = () => {
  const [count, setCount] = useState(0);

  const handleChangeCounter = (newCount) => {
    setCount(newCount);
  };
  return (
    <Counter value={count} onChange={handleChangeCounter}>
      <Counter.Decrement icon={"minus"} />
      <Counter.Label>Counter</Counter.Label>
      <Counter.Count max={10} />
      <Counter.Increment icon={"plus"} />
    </Counter>
  );
}

export { Component };
```

![](https://blog.kakaocdn.net/dn/dvk8p6/btrh9RZNfGO/kAO6ZnaPjLLpYN3tW7pgnk/img.jpg)

## Disadvantages

Implementation complexity: Component behavior was previously possible by implementing it in one place ( JSX ) , but now requires implementation in 3 different places ( JSX / useState / handleChange ) .

{% embed url="https://codesandbox.io/embed/react-patterns-uenl15?fontsize=14&hidenavigation=1&module=%2Fsrc%2Fpatterns%2Fcontrol-props%2FUsage.js&theme=dark" %}

## References and articles :

{% embed url="https://dev.to/robogeek95/react-controlled-props-pattern-3ej1" %}

{% embed url="https://kentcdodds.com/blog/control-props-vs-state-reducers" %}

{% embed url="https://itnext.io/controlled-and-uncontrolled-component-design-pattern-in-react-21e8d40e46e" %}

{% embed url="https://antongunnarsson.com/render-props" %}

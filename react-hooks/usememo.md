# ❕ useMemo

{% embed url="https://dmitripavlutin.com/react-usememo-hook" %}

As Apps grow in size and complexity, creating efficient React code becomes more important than ever. Re-rendering large components is costly, and providing a significant amount of work for the browser through a single-page application (SPA) increases processing time and can potentially drive away users.

A concern that most people have while working with React.js is performance. React is amazing and if used wisely you should not have re-render problems when states change.

First, let's understand the concept of memoization and why we need it.

## Memoization <a href="#f80e" id="f80e"></a>

{% embed url="https://en.wikipedia.org/wiki/Memoization" %}

> In computing, memorization or memorization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

Memorization is the idea to keep the value returned of a function or the function itself saved and don’t re-run it if the values sent to it don’t change.

{% hint style="info" %}
## Understanding JavaScript equality check <a href="#2855" id="2855"></a>

Functions in JavaScript are first-class citizens, meaning that a function is a regular object. The function object can be returned by other functions, be compared, etc exactly like an object.

But if we have one function and run it twice setting it to two different variables and compare it (like below), this will return `false` and we have the same logic applied to objects

```jsx
const sum =()=> {
  return (a, b) => a + b;
}

const sum1 = sum();
const sum2 = sum();
sum1(1, 2); // => 3
sum2(1, 2); // => 3

console.log(sum1 === sum2); // => false
console.log(sum1 === sum1); // => true
```
{% endhint %}

## **useMemo** <a href="#bfb8" id="bfb8"></a>

![](../.gitbook/assets/fddffd.png)

The hook `useMemo` receives two parameters: a function that will **compute** and return a value and an array of dependencies (like `useEffect`).&#x20;

During initial rendering, `useMemo(compute, dependencies)` invokes the `compute`  function memorizes the calculation result, and returns it to the component.

If during next renderings the dependencies don't change, then `useMemo()` _doesn't invoke_ `compute` but returns the memorized value.

But if dependencies change during re-rendering, then `useMemo()` _invokes_ `compute` function  memorizes the new value, and returns it.

If your computation callback uses props or state values, then be sure to indicate these values as dependencies:

![](../.gitbook/assets/dfdf.png)

This hook is normally used when we have some calculation based on a prop (like the example below) or when we want to memorize a component with the props sent.

```jsx
import * as React from "react";

const Element = ({ random }: { random: number }) => {
  const memoized = useMemo(() => (random * 100) / 33, [random]);
  return <>{memoized}</>;
};

export const App =()=> {
  const randomNumber = 100390;

  return <AnotherComponent random={random} />;
}
```

### Factorial example



{% embed url="https://codesandbox.io/embed/factorial-with-memoization-forked-xu9dwk?fontsize=14&hidenavigation=1&theme=dark" %}

{% embed url="https://alexsidorenko.com/blog/react-render-usememo" %}

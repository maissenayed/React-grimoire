# useEffect

`React.useEffect` is a built-in hook that allows you to run some custom code after React renders (and re-renders) your component to the DOM. It accepts a callback function which React will call after the DOM has been rendered but before all of that let's dive deep into what is an effect

## What are effects

"Side Effect" is not a react-specific term. It is a general concept about behaviours of functions. A function is said to have side effect if it trys to modify anything outside its body. For example, if it modifies a global variable, then it is a side effect. If it makes a network call, it is a side effect as well.

{% embed url="https://en.m.wikipedia.org/wiki/Side_effect_(computer_science)" %}

Side effects are basically anything that affects something outside of the scope of the current function that’s being executed. In our dashboard, this includes:

## React side Effect

Sometimes, however, we need our components to reach outside this data-flow process and directly interact with other APIs. An action that impinges on the outside world in some way is called a _side effect_. Common side effects include the following:

* handling subscriptions with event listeners
* dealing with manual DOM changes.
* Logging messages to the console or other service
* Setting or getting values in local storage
* Fetching data or subscribing and unsubscribing to services



{% embed url="https://overreacted.io/a-complete-guide-to-useeffect" %}

{% embed url="https://blog.logrocket.com/guide-to-react-useeffect-hook" %}

## UseEffect

&#x20;[`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect)  is a hook to let you  invoke side effects from within functional components,

The basic signature of `useEffect` is as follows:

![](../.gitbook/assets/effect.png)

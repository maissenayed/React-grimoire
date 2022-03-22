# useEffect

`React.useEffect` is an in-built **hook** that lets you run custom code after React renders (and re-renders) your component to the **DOM**. It accepts a callback function that React will call after the **DOM** has been rendered, but first, let's define an effect.

## What are effects

The term "Side Effect" does not refer to a specific reaction. It is a broad concept referring to the behaviors of functions. If a function attempts to modify anything outside of its body, it is said to have a side effect. It is a side effect, for example, if it modifies a global variable. It is also a side effect if it makes a network call.

{% embed url="https://en.m.wikipedia.org/wiki/Side_effect_(computer_science)" %}

Side effects are defined as anything that has an effect on something that is not within the scope of the current function being executed.

## React side Effect

However, there are times when we need our components to interact with APIs that are not part of the data-flow process. A side effect is an action that has an impact on the outside world in some way. The following are common side effects:

* handling subscriptions with event listeners
* dealing with manual **DOM** changes.
* Logging messages to the console or other service
* Setting or getting values in local storage
* Fetching data or subscribing and unsubscribing to services

&#x20;[`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect)  is a hook to let you  invoke side effects from within functional components,

The basic signature of `useEffect` is as follows:

![](<../.gitbook/assets/effect (1).png>)

Let's analyse this example

```jsx
import * as React from "react";

const BasicEffect = () => {
  const [counter, setCounter] = React.useState(0);
  const handleClick = () => setCounter((prev) => prev + 1);

  React.useEffect(() => {
    handleClick();
  });

  return (
    <div>
      <span> {`Counter is ${counter}`} </span>
    </div>
  );
};
```

{% embed url="https://codesandbox.io/embed/useeffecetconitnous-rerender-w850cp?fontsize=14&hidenavigation=1&theme=dark" %}

As we can see, **useEffect** will force the component to redraw because it is always invoked after each redraw, so when the counter is updated, **useEffect** will invoke **handleClick**, and we will be in an infinite loop.

### Empty dependency array

It is also possible to add an empty dependency array. In this case, effects are only executed once; it is similar to the [`componentDidMount()`](https://reactjs.org/docs/react-component.html#componentdidmount) lifecycle method. (similar by not exactly the same)

```jsx
import * as React from "react";

const BasicEffect = () => {
  const [counter, setCounter] = React.useState(0);
  const handleClick = () => setCounter((prev) => prev + 1);

  React.useEffect(() => {
    handleClick();
  },[]);

  return (
    <div>
      <span> {`Counter is ${counter}`} </span>
    </div>
  );
};
```

{% hint style="warning" %}
**`useEffect` is passed an empty array, `[]`. Hence, the effect function will be called only on mount**
{% endhint %}

### Triggering Effect

Let's take this example

```jsx
import * as React from "react";

const BasicEffect = () => {
  const [counter, setCounter] = React.useState(0);
  const handleClick = () => setCounter((prev) => prev + 1);

  React.useEffect(() => {
    handleClick();
  },[count]);

  return (
    <div>
      <span> {`Counter is ${counter}`} </span>
    </div>
  );
};
```

We still have an infinite loop , but why is that&#x20;

![](../.gitbook/assets/dependency.png)

The dependency array basically tells the hook to "only trigger when the dependency array changes". In the above example, it means "run the callback every time the `counter` variable changes".

If you have multiple elements in a dependency array, the hook will trigger if _any_ element of the dependency array changes.

### Skipping effects

```jsx
const ArrayDepMount = () => {
  const [randomNumber, setRandomNumber] = useState(0)
  const [effectLogs, setEffectLogs] = useState([])

  useEffect(
    () => {
      setEffectLogs(prevEffectLogs => [...prevEffectLogs, 'effect fn has been invoked'])
    },
    [randomNumber]
  )

  return (
    <div>
      <h1>{randomNumber}</h1>
      <button
        onClick={() => {
          setRandomNumber(Math.random())
        }}
      >
        Generate random number!
      </button>
      <div>
        {effectLogs.map((effect, index) => (
          <div key={index}>{'🍔'.repeat(index) + effect}</div>
        ))}
      </div>
    </div>
  )
}
```

We can see that the effect is dependent on the randomNumber state and will only be triggered if the randomNumber value has changed.

{% hint style="warning" %}
**If your effect is dependent on a state or prop value in scope, make sure to pass it as an array dependency to avoid accessing stale values within the callback. If the values referenced change over time and are used in the callback, include them in the array dependency.**
{% endhint %}

The React team recommends you use the [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It warns when dependencies are specified incorrectly and suggests a fix.

{% hint style="info" %}
### The importance of the dependency array

_**If no dependency array is provided, every scheduled useEffect is executed. This means that after each render cycle, each effect defined in the corresponding component is executed in the order specified in the source code.**_

_**As a result, the order of your effect definitions is important. In our case, whenever one of the state variables changes, our single useEffect statement is executed. In the source code, sitioning is used.**_

_**As array entries, you provide. React only executes the useEffect statement in these cases if at least one of the provided dependencies has changed since the previous run. In other words, the dependency array makes the execution conditional on certain conditions.**_

_**Most of the time, this is what we want; we usually want to execute side effects when certain conditions are met, such as when data changes, a prop changes, or the user first sees our component.**_
{% endhint %}

### Multiple effects

Multiple `useEffect` calls can happen within a functional component, as shown below:

```jsx
const MultipleEffects = () => {
  // ⏬ 
  useEffect(() => {
    const clicked = () => console.log('window clicked')
    window.addEventListener('click', clicked)

    return () => {
      window.removeEventListener('click', clicked)
    }
  }, [])

  // ⏬  another useEffect hook 
  useEffect(() => {
    console.log("another useEffect call");
  })

  return <div>
    Check your console logs
  </div>
}
```

Note that `useEffect` calls can be skipped, not invoked on every render. This is done by passing a second array argument to the effect function.

## Cleaning up an effect <a href="#cleaningupaneffect" id="cleaningupaneffect"></a>

The application of React By cleaning up effects, the effect cleanup function protects applications from undesirable behaviors such as memory leaks. We can improve the performance of our application by doing so.

### What is the `useEffect` cleanup function?

The **useEffect** cleanup function, as the name implies, allows us to clean up our code before our component unmounts. When our code runs and reruns for each render, **useEffect** uses the cleanup function to clean up after itself.

The **useEffect** Hook is designed in such a way that we can return a function from within it, and it is within this return function that the cleanup occurs. The cleanup function prevents memory leaks and eliminates some unwanted and unnecessary behaviors.

Note that you don’t update the state inside the return function either:

![](../.gitbook/assets/cleanuo.png)

### Why is the `useEffect` cleanup function useful?

As previously stated, the **useEffect** cleanup function assists developers in cleaning up effects that prevent unwanted behaviors and improve application performance.

It is important to note, however, that the useEffect cleanup function runs not only when our component wants to unmount, but also right before the execution of the next scheduled effect.

&#x20;In fact, the next scheduled effect is usually based on the dependency array after our effect has completed.

As a result, whenever our effect is dependent on our prop or whenever we set up something that persists, we have a reason to invoke the cleanup function.

Consider the following scenario: suppose we receive a **fetch** of a specific user via a **user's id** and, before the fetch is completed, we change our mind and attempt to obtain another user.

While the previous fetch request is still in progress, the **prop**, or in this case, the **id**, updates. To avoid exposing our application to a memory leak, we must abort the fetch using the cleanup function.

### When should we use the `useEffect` cleanup?

Let’s say we have a React component that fetches and renders data. If our component unmounts before our promise resolves, `useEffect` will try to update the state (on an unmounted component) and send an error that looks like this:

![Warning Error](../.gitbook/assets/Warning-error.png)

To fix this error, we use the cleanup function to resolve it.

_`"React performs the cleanup when the component unmounts"`_ according to the official documentation. However, effects are applied to each render, not just the first. This is why React also cleans up effects from previous renders before running them again."

The cleanup is commonly used to cancel all subscriptions made and cancel fetch requests.

{% embed url="https://alexsidorenko.com/blog/useeffect-cleanups" %}

## Fetch Data from an API

### Create the asynchronous function

Then, let's create an [asynchronous function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function) to fetch our data. An asynchronous function is a function that needs to wait after the [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Promise) is resolved before continuing. In our case, the function will need to wait after the data is fetched (our promise) before continuing.

```jsx
const fetchData = async (url) => {
    try {
        const response = await fetch(url);
        const json = await response.json();
        console.log(json);
		} catch (error) {
        console.log("error", error);
		}
};
```

Put the **fetchData** function above in the **useEffect** hook and call it, like so:

```jsx
useEffect(() => {
    // advice free ap
    const url = "https://api.adviceslip.com/advice";

    const fetchData = async () => {
      try {
        const response = await fetch(url);
        const json = await response.json();
        console.log(json);
      } catch (error) {
        console.log("error", error);
      }
    };

    fetchData();
}, []);
```

The function we just created is wrapped in a [try...catch statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) so that the function catches the errors and prints them in the console. This helps debug and prevents the app to crash unexpectedly.

Inside of the try, we are using the built-in [fetch API from JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/Fetch\_API) to get the advice from the Advice Slip JSON API. We put the [await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) keyword just in front of it to tell the function to wait for the fetch task to be done before running the next line of code.

Once we get a response, we are parsing it using the [.json() function](https://developer.mozilla.org/en-US/docs/Web/API/Body/json), meaning that we are transforming the response into JSON data that we can easily read. Then, we are printing the JSON data in the console.

Then, instead of printing the advice in the console, we'll save it in the advice state.

```jsx
const [advice, setAdvice] = useState("")
setAdvice(json.slip.advice)
```

{% embed url="https://codesandbox.io/embed/fetch-data-from-an-api-forked-b0euj8?fontsize=14&hidenavigation=1&theme=dark" %}

## References and articles :

{% embed url="https://alexsidorenko.com/blog/useeffect" %}

{% embed url="https://overreacted.io/a-complete-guide-to-useeffect" %}

{% embed url="https://blog.logrocket.com/guide-to-react-useeffect-hook" %}

{% embed url="https://academind.com/tutorials/useeffect-abort-http-requests" %}

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-call-web-apis-with-the-useeffect-hook-in-react" %}

{% embed url="https://devtrium.com/posts/async-functions-useeffect" %}

{% embed url="https://epicreact.dev/myths-about-useeffect" %}

{% embed url="https://kentcdodds.com/blog/react-hooks-pitfalls" %}

{% embed url="https://www.youtube.com/watch?t=4s&v=lStfMBiWROQ" %}

{% embed url="https://www.youtube.com/watch?v=F-0SZ_TicXA" %}

{% embed url="https://www.youtube.com/watch?t=628s&v=dH6i3GurZW8" %}

{% embed url="https://www.youtube.com/watch?index=6&list=PLNqp92_EXZBKa1U7JbgUwBnDk3XzYDvXe&v=OCg4DJyVGk0" %}

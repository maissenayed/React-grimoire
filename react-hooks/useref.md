---
description: useRef is like class instance variable for function components.
---

# useRef

## What are refs

Sometimes when using React you’ll need an escape hatch to write imperative-style code to interact directly with DOM elements. Using React’s createRef method allows you to do just that!

React provides a way to get references to DOM nodes by using `React.createRef()`. It’s really just an equivalent of this all-too-familiar snippet of JavaScript:

```javascript
document.getElementById('element');
```

This is exactly what `React.createRef()` does, although it requires a bit of a different setup.

```jsx
import React, { Component } from 'react';

class Foobar extends Component {
  constructor(props) {
    super(props);
    this.myInput = React.createRef();    // initialize "this.myInput"  
  }

  render() {
    return (
      <input ref={this.myInput}/>        {/* pass "this.myInput" as prop */}
    );
  }
}
```

When working with class-based components in the past, we used `createRef()` to create a ref. However, now that React recommends functional components, and general practice is to follow the Hooks way of doing things, we don’t need to use `createRef()`. Instead, we use `useRef(null)` to create refs in functional components.

## What is useRef used for?

The `useRef` Hook in React can be used to directly access DOM nodes, as well as persist a mutable value across rerenders of a component.

The basic signature for the `useRef` Hook looks like this:

```
const refObject = useRef(initialValue)
```

`useRef` returns a mutable object whose value is set as: `{current: initialValue}`.

{% hint style="info" %}
* returns a 'ref' object.
* Call signature: `const` refObject `= useRef(initialValueToBePersisted)`
* Value is persisted in the refObject`.current` property.
* values are accessed from the `.current` property of the returned object.
* The`.current` property could be initialised to an initial value e.g. `useRef(initialValue)`
* The object is persisted for the entire lifetime of the component.
{% endhint %}

### Directly access DOM nodes

When combined with the `ref` attribute, we could use `useRef` to obtain the underlying DOM nodes to perform DOM operations imperatively. In fact, this is really an escape hatch. We should only do this sparsely for things that React doesn't provide a declarative API for, such as focus management.&#x20;

One of the many concepts that React popularized among developers is the concept of declarative views. Before declarative views, most of us were modifying the DOM by calling functions that explicitly changed it.

As mentioned at the introduction of this article, we are now declaring views based on a state, and — though we are still calling functions to alter this state — we are not in control of when the DOM will change or even if it should change.

Because of this inversion of control, we’d lose this imperative nature if it weren’t for refs.

The difference between using `useRef` and manually setting an object value directly within your component, e.g., `const myObject = {current: initialValue}`, is that the `ref` object remains the same all through the lifetime of the component, i.e., across re-renders.

```
const App = () => {
   const refObject = useRef("value")
   //refObject will always be {current: "value"} every time App is re-rendered. 
}
```

To update the value stored in the `ref` object, you go ahead and mutate the `current` property as follows:

```
const App = () => {
   const refObject = useRef("value")

   //update ref 
   refObject.current = "new value" 

  //refObject will always be {current: "new value"} 
}
```

The returned object from invoking `useRef` will persist for the full lifetime of the component regardless of re-renders.

A common use case for `useRef` is to manage child DOM nodes:

```
function TextInputWithFocusButton() {
  //1. create a ref object with initialValue of null
  const inputEl = useRef(null);

  const onButtonClick = () => {
    // 4. `current` points to the mounted text input element
    // 5. Invoke the imperative focus method from the current property
    inputEl.current.focus();
  };

  return (
    <>
      {/* 2. as soon as input is rendered, the element will be saved in the ref object, i.e., {current: *dom node*}  */}
      <input ref={inputEl} type="text" />
      {/* 3. clicking the button invokes the onButtonClick handler above */}
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

The example above works because if you pass a `ref` object to React, e.g., `<div ref={myRef} />`, React will set its `current` property to the corresponding DOM node whenever that node changes, i.e., `myRef = {current: *dom node*}`.

`useRef` returns a plain JavaScript object, so it can be used for holding more than just DOM nodes — it can hold whatever value you want. This makes it the perfect choice for simulating instance-like variables in functional components:

```
const App = ({prop1}) => {
    // save props1 in ref object on render
        const initialProp1 = useRef(prop1)

    useEffect(() => {
       // see values logged here
       console.log({
         initialProp1: initialProp1.current,
         prop1
       })
    }, [prop1])
}
```

In the example above, we log `initialProp1` and `prop1` via `useEffect`. This will be logged on mount and every time `prop1` changes.

Since `initialProp1` is `prop1` saved on initial render, it never changes. It’ll always be the initial value of `props1`. Here’s what we mean.

If the first value of `props1` passed to `App` were `2`, i.e., `<App prop1={2} />`, the following will be logged on mount:

```
{
  initialProp1: 2,
  prop1: 2,
}
```

If `prop1` passed to `App` were changed from `2` to `5` — say, owing to a state update — the following will be logged:

```
{
  initialProp1: 2, // note how this remains the same
  prop1: 5,
}
```

`initialProp1` remains the same through the lifetime of the component because it is saved in the `ref` object. The only way to update this value is by mutating the current property of the `ref` object: `initialProp1.current =`` `_`*new value*`_.

With this, you can go ahead and create [instance-like variables](https://reactjs.org/docs/hooks-faq.html#is-there-something-like-instance-variables) that don’t change within your functional component.

Remember, the only difference between `useRef` and creating a `{current: ...}` object yourself is that `useRef` will give you the same `ref` object on every render.

There’s one more thing to note. `useRef` doesn’t notify you when its content changes, i.e., mutating the `current` property doesn’t cause a re-render. For cases such as performing a state update after React sets the current property to a DOM node, make use of a callback ref as follows:

```
function UpdateStateOnSetRef() {
  // set up local state to be updated when ref object is updated
  const [height, setHeight] = useState(0);

  // create an optimised callback via useCallback
  const measuredRef = useCallback(node => {
    // callback passed to "ref" will receive the DOM node as an argument
    if (node !== null) {
      // check that node isn't empty before calling state
      setHeight(node.getBoundingClientRect().height);
    }
  }, []);

  return (
    <>
      {/* pass callback to the DOM ref */}
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  );
}
```

\
\


### `useRef` vs. `createRef`

``

{% embed url="https://blog.logrocket.com/complete-guide-react-refs" %}

{% embed url="https://blog.logrocket.com/react-reference-guide-hooks-api" %}

{% embed url="https://dmitripavlutin.com/react-useref-guide" %}

{% embed url="https://learnreact.design/posts/react-useref-by-example#what-is-useref-used-for" %}

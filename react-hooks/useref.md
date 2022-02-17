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



### `useRef` vs. `createRef`

``

{% embed url="https://blog.logrocket.com/complete-guide-react-refs" %}

{% embed url="https://blog.logrocket.com/react-reference-guide-hooks-api" %}

{% embed url="https://dmitripavlutin.com/react-useref-guide" %}

{% embed url="https://learnreact.design/posts/react-useref-by-example#what-is-useref-used-for" %}

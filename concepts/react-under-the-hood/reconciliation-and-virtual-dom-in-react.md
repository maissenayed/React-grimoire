# 🏁 Reconciliation & Virtual DOM in React

When the props or state of a component change, React determines whether an actual DOM update is required by comparing the newly returned element to the previously rendered one.

&#x20;React will update the DOM if they are not equal. This is known as "reconciliation." It's critical to understand how React's reconciler works in order to build performant apps and avoid perplexing bugs.

## Overview

To try to illustrate how the reconciler works at a high-level, we’ll look at an example.

Let’s say we had the following list of items rendered with React:

```jsx
return (
    <ul className="list">
      <li>A</li>
      <li>B</li>
      <li>C</li>
    </ul>
  );
```

And we wanted to transition to the following new state:

```jsx
return (
    <ul className="list">
      <li>A</li>
      <li>B</li>
      <li className="selected">C</li>
    </ul>
  );
```

One solution would be to re-render our component from scratch each time and replace the DOM. However, by recreating the same DOM elements every time, components would lose their state and performance would suffer. This could also have an impact on overall user experience; for example, if we were constantly re-rendering an input as a user typed into it, the user would lose focus while typing each time our input re-rendered.

Instead, React uses a different approach called **reconciliation**.

When you use React, you can think of the render() function as creating a tree of React elements at a single point in time. This tree has been saved to memory. That render() function will return a different tree of React elements on the next re-render (typically triggered by a state or props update).&#x20;

React will determine which child components to mount, update, and unmount during this update stage. React must then figure out how to update the UI in an efficient manner to match the most recent tree. To accomplish this, React compares the new and old trees and translates the differences to a set of DOM operations (in the case of a React Native application, it would translate to a set of

## Reconciliation versus rendering

The DOM is just one of the rendering environments React can render to, with native iOS and Android views via React Native being the other major targets. (This is why the term "virtual DOM" is a bit misleading.) Because React is designed in such a way that reconciliation and rendering are separate phases, it can support so many targets.&#x20;

The reconcile determines which parts of a tree have changed, and the **renderer** uses that information to update the rendered app. Because of this separation, React **DOM** and React Native can use their own **renderers** while sharing the same **reconciler** provided by React's core.

## **The Diffing Process**

The diffing algorithm in React is based on two assumptions:

1. Two elements of different types are assumed to generate substantially different trees. React will not attempt to diff them, but rather replace the old tree completely.
2. The developer can hint at which child elements may be stable across different renders with a `key` prop. Keys should be stable, predictable, and unique.&#x20;

With these assumptions in mind, React compares its internal DOM tree model (aka virtual DOM) to the actual DOM, starting with the two root elements.&#x20;

When comparing two trees, React compares the two root elements first.

## References and articles :&#x20;

{% embed url="https://www.youtube.com/watch?t=905s&v=EZV2rwnGgZA" %}

{% embed url="https://reactjs.org/docs/reconciliation.html" %}

{% embed url="https://reactjs.org/docs/codebase-overview.html#stack-reconciler" %}

{% embed url="https://reactjs.org/docs/implementation-notes.html#updating" %}

{% embed url="https://reactjs.org/docs/design-principles.html" %}

{% embed url="https://github.com/acdlite/react-fiber-architecture" %}

{% embed url="https://www.fatalerrors.org/a/virtual-dom-and-diff-algorithm-in-react.html" %}

{% embed url="https://medium.com/@gethylgeorge/how-virtual-dom-and-diffing-works-in-react-6fc805f9f84e" %}

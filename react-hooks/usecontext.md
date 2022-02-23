---
description: Context is React’s way of handling shared data between multiple components.
---

# ⚠ useContext

### Introduction to prop drilling

There has always been a need to share data with different components when working with React. This can be achieved in the most basic way using prop drilling. Prop drilling allows for unidirectional data sharing between components. The data passed or shared in the form of props.

Let’s consider the diagram below:

![](../.gitbook/assets/props-drilling.png)

&#x20;

For the data in the A component to be accessed in the C component, it has to be passed down as prop to the B component, and then finally the C component. This is known as threading.

From the above explanation, you can understand the basics of what prop drilling is and why we need it.

### React Context <a href="#gettingstartedwithreactcontext" id="gettingstartedwithreactcontext"></a>

According to the React docs, Context provides a way to pass data through the component tree from parent to child components, without having to pass props down manually at each level.

Each component in Context is context-aware. Essentially, instead of passing props down through every single component on the tree, the components in need of a prop can simply ask for it, without needing intermediary helper components that only help relay the prop.

### API <a href="#api" id="api"></a>

#### `React.createContext` <a href="#reactcreatecontext" id="reactcreatecontext"></a>

The `createContext` method is used to create a Context object to which components can subscribe. These components are able to get the context value from the closest matching Provider above them in the tree.

```
const NewContext = React.createContext({ color: 'black' });
```

Components are usually wrapped in a Provider in order to get their context value. However, when there’s no matching Provider above a component in the tree, the component will get its context from the default argument `{ color: 'black' }` in the `createContext` method. This is especially useful when testing components in isolation.

#### `Context.Provider` <a href="#contextprovider" id="contextprovider"></a>

The `React.createContext` method will return a Provider component when it is called. Providers are React components from Context objects that allow other components to access those context values and subscribe to their changes.

```
const { Provider } = NewContext;
```

The Provider component accepts a `value` prop, which can then be accessed by its consuming child components. A Provider can have multiple child components or consumers.

```
<Provider value={{color: 'blue'}}>
  {children}
</Provider>
```

Components will use the default context value from the `createContext` method when they have no matching parent Provider. However, once a Provider is available, even if its `value` prop is `undefined`, its child components or consumers will use its value.

Whenever a Provider’s `value` prop changes, its subscribed consumers will re-render.

**Consuming the context**

Consuming the context can be performed in 2 ways.

The first way, the one I recommend, is to use the `useContext(Context)` React hook:

```
import { useContext } from 'react';function MyComponent() {  const value = useContext(Context);  return <span>{value}</span>;}
```

The hook returns the value of the context: `value = useContext(Context)`. The hook also makes sure to re-render the component when the context value changes.

The second way is by using a render function supplied as a child to `Context.Consumer` special component available on the context instance:

```
function MyComponent() {  return (    <Context.Consumer>      {value => <span>{value}</span>}    </Context.Consumer>  );}
```

Again, in case if the context value changes, `<Context.Consumer>` will re-render its render function.

![React Context](https://dmitripavlutin.com/90649ae4bdf379c482ad24e0dd220bc4/react-context-3.svg)

You can have as many consumers as you want for a single context. If the context value changes (by changing the `value` prop of the provider `<Context.Provider value={value} />`), then all consumers are immediately notified and re-rendered.

If the consumer isn't wrapped inside the provider, but still tries to access the context value (using `useContext(Context)` or `<Context.Consumer>`), then the value of the context would be the default value argument supplied to `createContext(defaultValue)` factory function that had created the context.

### Global shared state with React Context

Another use case for React Context is using it as a global state mechanism, like we have in between `TopNav` and `Profile`. Updating the `username` in `Profile` immediately updates the shared state in `UserProvider`, providing a mechanism for global state management.

As with prop drilling, there can be some performance drain when using Context. Whenever it renders, its child components also render. One way to minimize rendering is to keep Context as close to where it’s being used as possible, like we’ve done with `UserProvider`. Although we could position it higher up in the component tree, it would be less effective.

### What the React Context API is used for <a href="#whatthereactcontextapiisusedfor" id="whatthereactcontextapiisusedfor"></a>

With React Context, we can pass data deeply. While some developers may want to use Context as a global state management solution, doing so is tricky. While React Context is native and simple, it isn’t a dedicated state management tool like Redux, and it doesn’t come with sensible defaults.

If you decide to use React Context at all, you should be aware of its potential for performance drain. You can very easily get carried away and add too many components where they aren’t needed. To prevent re-rendering, be sure to place contexts correctly only in the components that require them.

The main idea of using the context is to allow your components to access some global data and re-render when that global data is changed. Context solves the props drilling problem: when you have to pass down props from parents to children.

You can hold inside the context:

* global state
* theme
* application configuration
* authenticated user name
* user settings
* preferred language
* a collection of services

On the other side, you should think carefully before deciding to use context in your application.

First, integrating the context adds complexity. Creating the context, wrapping everything in the provider, using the `useContext()` in every consumer — this increases complexity.

Secondly, adding context makes it more difficult to unit test the components. During unit testing, you would have to wrap the consumer components into a context provider. Including the components that are indirectly affected by the context — the ancestors of context consumers!

### Redux vs. the React Context API <a href="#reduxvsthereactcontextapi" id="reduxvsthereactcontextapi"></a>

Does React Context replace Redux? The short answer is no, it doesn’t. As we’ve seen, Context and Redux are two different tools, and comparison often arises from misconceptions about what each tool is designed for.

Although Context can be orchestrated to act as a state management tool, it wasn’t designed for that purpose, so you’d have to do put in extra effort to make it work. There are already a lot of state management tools that work well and will ease your troubles.

In my experience with Redux, it can be relatively complex to achieve something that is easier to solve today with Context. Keep in mind, prop drilling and global state management is where Redux and Context’s paths cross. Redux has more functionality in this are.

Ultimately, Redux and Context should be considered complementary tools that work together instead of alternatives. My recommendation is to use Redux for complex global state management and Context for prop drilling.

{% embed url="https://reactjs.org/docs/context.html" %}

{% embed url="https://medium.com/vectoscalar/react-context-api-a-complete-guide-bc0898b71dc9" %}

{% embed url="https://blog.logrocket.com/pitfalls-of-overusing-react-context" %}

{% embed url="https://kentcdodds.com/blog/how-to-use-react-context-effectively" %}

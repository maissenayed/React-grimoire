---
description: the old way prior to react 16.8.0
---

# 🏁 Class Component State

## What is State?

A state in React is a simple JavaScript object that allows you to keep track of a component's data. The state of a component can change. The functionality of the application determines a change in the state of a component. User input, new server-side messages, network responses, or anything else can cause changes.

The state of a component is expected to be private to the component and controlled by the same component. To change the state of a component, you must do so within the component — the initialization and updating of the component's state.

The state of a component is expected to be private to the component and controlled by the same component. To change the state of a component, you must do so within the component — the initialization and updating of the component's state.

In React, there are primarily two ways to create a component:

* class-based component (the old way)
* functional component (the new way )

You should be familiar with both class-based and functional components, as well as hooks.

Instead of learning functional components directly with React hooks, you should first understand class-based components so that you can quickly master the fundamentals.

{% embed url="https://reactjs.org/docs/faq-state.html#gatsby-focus-wrapper" %}

## The old Class Components

Before React 16.8.\* States were only available to components that are called **class components**. The only reason why people used  class components over their counterpart, functional components, is that class components could have state.&#x20;

How do I define class components?

You can make a component by extending the **React** Component class with an **ES6** class keyword, as shown below:

You just wrap a function component in a class! There are just three rules:

1. The class must extend from `React.Component`
2. You must define a `render()` method that returns a React element
3. Props are accessed through `this.props` instead of through function arguments.

```javascript
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = { username: 'Mayssa' }
  }
  render() {
    const { username } = this.state
    return(
      <div>
        { username }
      </div>
    )
  }
}
```

### The Constructor

[According to the official documentation](https://reactjs.org/docs/react-component.html#constructor), State should be initialized in the **constructor**. Setting `this.state` to an object, as shown above, is how state is initialized. Remember that state is a simple JavaScript object. The App component's initial state has been set to a state object containing the key username and its value. Mayssa makes use of

`this.state = { username: 'Mayssa' }`.

Initializing a component state can get as complex as what you can see here:

```javascript
constructor(props) {
  super(props)
  this.state = { 
    total: 0,
    status: false, 
    isDisabled: false, 
    todoList: [],
    name: 'Mayssa'
    ...
  }
}
```

### Accessing State

An initialized state can be accessed in the `render()` method, as I did above.

```javascript
render() {
  const { username } = this.state
  return(
    <div>
      { username }
    </div>
  )
}
```

An alternative to the above snippet is:

```javascript
render() {
  return(
    <div>
      { this.state.username }
    </div>
  )
}
```

The difference is that I extracted the username from state in the first example, but it can also be written as `const status = this.state.username`. Thanks to [ES6 destructuring](https://css-tricks.com/new-favorite-es6-toy-destructured-objects-parameters/), I do not have to go that route. Do not get confused when you see things like this. It is important to know that I am not reassigning state when I did that. The initial setup of state was done in the constructor, and should not be done again&#x20;

{% hint style="danger" %}
**Directly updating/mutating state in React is a terrible practice that will cause problems in your application. In addition, if you make a direct state change, your component will not be re-rendered.**
{% endhint %}

A state can be accessed using `this.state."property name"`. Do not forget that aside from the point where you initialized your state, the next time you are to make use of `this.state` is when you want to access the state.

### Updating State

To make the state change, React gives us a `setState` function that allows us to update the value of the state.

The `setState` function has the following syntax:

```
setState(updater, [callback])
```

* `updater` can either be a function or an object
* `callback` is an optional function that gets executed once the state is successfully updated

> Calling `setState` automatically re-renders the entire component and all its child components. We don't need to manually re-render as seen previously using the [**reverseAndRender**](arrays-and-key-props.md#arrays-and-key-props) function

The only permissible way to update a component’s state is by using `setState()`. Let’s see how this works practically.

First, I'll write the method that is called to update the component's username. This method is expected to receive an argument and to use that argument to update the state.

```javascript
handleInputChange(username) {
  this.setState({username})
}
```

You can see that I am again passing an object to `setState().` After that, I'll need to pass this function to the event handler, which is called whenever the value of an input box changes. The event handler will provide the context of the triggered event, allowing the value entered in the input box to be obtained using `event.target.value.` This is the argument passed to the method `handleInputChange()`. As a result, the render method should look something like this.

```javascript
render() {
  const { username } = this.state
  return (
    <div>
      <div>
        <input 
          type="text"
          value={this.state.username}
          onChange={event => this.handleInputChange(event.target.value)}
        />
      </div>
      <p>Your username is, {username}</p>
    </div>
  )
}
```

When `setState()` is called, a request to React is sent to update the **DOM** with the newly updated state. Having this mindset allows you to recognize that state updates may be delayed.

Your component should look like this;

```javascript
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = { username: 'Mayssa' }
  }
  handleInputChange(username) {
    this.setState({username})
  }
  render() {
    const { username } = this.state
    return (
      <div>
        <div>
          <input 
            type="text"
            value={this.state.username}
            onChange={event => this.handleInputChange(event.target.value)}
          />
        </div>
        <p>Your username is, {username}</p>
      </div>
    )
  }
}
```

### Passing State as Props

A state can be passed as a prop from a parent component to a child component. To demonstrate this, let's create a new component for making a To Do List. This component will have an input field where users can enter daily tasks, which will be passed as props to the child component.

Try to create the parent component on your own, using the lessons you have learned thus far.

Let’s start with creating the initial state of the component.

```javascript
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = { todoList: [] }
  }
  render() {
    return()
  }
}
```

The component’s state has its `todoList` set to an empty array. In the `render()` method, I want to return a form for submitting tasks.

```javascript
render() {
  const { todoList } = this.state
  return (
    <div>
      <h2>Enter your to-do</h2>
      <form onSubmit={this.handleSubmit}>
        <label>Todo Item</label>
        <input
          type="text"
          name="todoitem"
        />
        <button type="submit">Submit</button>
      </form>
    </div >
  )
}
```

The method `handleSubmit` is called every time a new item is entered and the submit button is clicked. This method will be used to update the component's state. I want to update it by concatenating the new value into the `todoList` array. This will set the `todoList` value inside the `setState()` method. This is how it should look:

```javascript
handleSubmit = (event) => {
  event.preventDefault()
  const value = (event.target.elements.todoitem.value)
  this.setState(({todoList}) => ({
    todoList: todoList.concat(value)
  }))
}
```

Each time the submit button is pressed, the event context is obtained. We use `event.preventDefault()` to prevent the default action of submission from reloading the page. When `todoList.concat()` is called, the value entered in the input field is assigned to a variable called value, which is then passed an argument. React updates the **todoList's** state by appending the new value to the initial empty array. This new array becomes the **todoList's** current state. The cycle is restarted when another item is added.

`Initial state` :point\_right:`[]`

`After button click the form event handler will set the state to the value indicated by the input let's say read more books`

`updated state d` :point\_right:`["read more books"]`

The goal here is to pass the individual item to a child component as props. For this tutorial, we’ll call it the `TodoItem` component. Add the code snippet below inside the parent div which you have in `render()` method.

```javascript
<div>
  <h2>Your todo lists include:</h2>
  { todoList.map(i => <TodoItem item={i} /> )}
</div>
```

You're using `map` to iterate through the `todoList` array, which means that each item is passed as props to the `TodoItem` component. To use this, you must have a `TodoItem` component that accepts props and renders them on the **DOM**. I'll demonstrate how to do this with functional and class components.

Written as a functional component:

```javascript
const TodoItem = (props) => {
  return (
    <div>
      {props.item}
    </div>
  )
}
```

For the class component, it would be:

```javascript
class TodoItem extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    const {item} = this.props
    return (
      <div>
        {item}
      </div>
    )
  }
}
```

{% embed url="https://daveceddia.com/visual-guide-to-state-in-react" %}

## _props_ vs _state_

> It's relatively simple to understand how they work, especially when seen in context, but it's more difficult to grasp them conceptually. It's perplexing at first because they both have abstract terms and values that appear to be the same, but they also play very different roles.

A Component's primary responsibility is to convert raw data into rich HTML. Keeping this in mind, the props and state together form the raw data from which the HTML output is generated.



Before separating _props_ and _state_, let's also identify where they overlap.

* Both _props_ and _state_ are **plain JS objects**
* Both _props_ and _state_ changes trigger a **render update**
* Both _props_ and _state_ are **deterministic.** If your Component generates different outputs for the same combination of _props_ and _state_ then you're doing something wrong.

#### Does this go inside _props_ or _state_?

{% hint style="info" %}
**If a Component needs to change one of its attributes at some point in time, that attribute should be part of the Component's state; otherwise, it should be a prop for that Component.**
{% endhint %}

{% hint style="success" %}
_**To recapitulate :**_

_**props**_** (short for **_**properties**_**) are a Component's configuration, its **_**options**_** if you may. They are received from above and immutable as far as the Component receiving them is concerned.**

**A Component cannot change its **_**props,**_** but it is responsible for putting together the **_**props**_** of its child Components.**

**The **_**state**_** starts with a default value when a Component mounts and then suffers from mutations in time (mostly generated from user events). It's a serializable\* representation of one point in time—a snapshot.**

**A Component manages its own **_**state**_** internally, but—besides setting an initial state—has no business fiddling with the **_**state**_** of its children. You could say the state is private.**

**We didn't say **_**props**_** are also serializable because it's pretty common to pass down callback functions through **_**props.**_
{% endhint %}



|                                              | _props_ | _state_ |
| -------------------------------------------- | ------- | ------- |
| Can get initial value from parent Component? | Yes     | Yes     |
| Can be changed by parent Component?          | Yes     | No      |
| Can set default values inside Component?\*   | Yes     | Yes     |
| Can change inside Component?                 | No      | Yes     |
| Can set initial value for child Components?  | Yes     | Yes     |
| Can change in child Components?              | Yes     | No      |

{% hint style="warning" %}
**Note that both **_**props**_** and **_**state**_** initial values received from parents override default values defined inside a Component.**
{% endhint %}

#### **Component types**

* **Pure Component** — Only _props_, no _state._ There's not much going on besides the `render()` function and all their logic revolves around the _props_ they receive. This makes them very easy to follow (and test for that matter).&#x20;
* **Stateful Component** — Both _props_ and _state._ We also call these _state managers_. They are in charge of client-server communication (XHR, web sockets, etc.), processing data and responding to user events. These sort of logistics should be encapsulated in a moderate number of _Stateful Components_, while all visualization and formatting logic should move downstream into as many _Stateless Components_ as possible.

## References and articles :&#x20;

{% embed url="https://kentcdodds.com/blog/props-vs-state" %}

{% embed url="https://reactjs.org/docs/thinking-in-react.html#step-4-identify-where-your-state-should-live" %}

{% embed url="https://www.youtube.com/watch?index=5&list=PLNqp92_EXZBKa1U7JbgUwBnDk3XzYDvXe&v=-urz6Sh7RE8" %}

{% embed url="https://www.youtube.com/watch?index=9&list=PLNqp92_EXZBKa1U7JbgUwBnDk3XzYDvXe&v=LyS1bB96FDg" %}

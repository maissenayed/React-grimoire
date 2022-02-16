---
description: the old way prior to react 16.8.0
---

# Class Component State

## What is State?

State, in React, is a **plain JavaScript object** that allows you keep track of a component’s data. The state of a component can change. A change to the state of a component depends on the functionality of the application. Changes can be based on user response, new messages from server-side, network response, or anything.

Component state is expected to be private to the component and controlled by the same component. To make changes to a component’s state, you have to make them inside the component — the initialization and updating of the component’s state.

In React, all the code we write is defined inside a component.

There are mainly two ways of creating a component in React:

* class-based component
* functional component

You should know how to work with class-based components as well as functional components, including hooks.

Instead of directly learning functional components with React hooks, you should first understand class-based components so it's easy to clear the basics.

{% embed url="https://reactjs.org/docs/faq-state.html#gatsby-focus-wrapper" %}

## The old Class Components

Before React 16.8.\* States were only available to components that are called **class components**. The only reason why people used  class components over their counterpart, functional components, is that class components could have state.&#x20;

How do I define class components?

You can create a component by using an ES6 class keyword and by extending the `Component` class provided by React like this:

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

[According to the official documentation](https://reactjs.org/docs/react-component.html#constructor), the constructor is the right place to initialize state. Initializing state is done by setting `this.state` to an object, like you can see above. Remember: **state is a plain JavaScript object**. The initial state of the App component has been set to a state object which contains the key username, and its value `johndoe` using `this.state = { username: 'johndoe' }`.

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
**Never ever directly update/mutate state in React, as it's a bad practice and it will cause issues in your application. Also, your component will not be re-rendered on state change if you make a direct state change.**
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

First, I will start with creating the method that gets called to update the component’s username. This method should receive an argument, and it is expected to use that argument to update the state.

```javascript
handleInputChange(username) {
  this.setState({username})
}
```

Once again, you can see that I am passing in an object to `setState()`. With that done, I will need to pass this function to the event handler that gets called when the value of an input box is changed. The event handler will give the context of the event that was triggered which makes it possible to obtain the value entered in the input box using `event.target.value`. This is the argument passed to `handleInputChange()` method. So, the render method should look like this.

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

Each time `setState()` is called, a request is sent to React to update the DOM using the newly updated state. Having this mindset makes you understand that state update can be delayed.

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

A state can be passed as props from a parent to the child component. To see this in action, let’s create a new component for creating a To Do List. This component will have an input field to enter daily tasks and the tasks will be passed as props to the child component.

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

Each time a new item is entered and the submit button is clicked, the method `handleSubmit` gets called. This method will be used to update the state of the component. The way I want to update it is by using `concat` to add the new value in the `todoList` array. Doing so will set the value for `todoList` inside the `setState()` method. Here’s how that should look:

```javascript
handleSubmit = (event) => {
  event.preventDefault()
  const value = (event.target.elements.todoitem.value)
  this.setState(({todoList}) => ({
    todoList: todoList.concat(value)
  }))
}
```

The event context is obtained each time the submit button is clicked. We use `event.preventDefault()` to stop the default action of submission which would reload the page. The value entered in the input field is assigned a variable called `value`, which is then passed an argument when `todoList.concat()` is called. React updates the state of `todoList` by adding the new value to the initial empty array. This new array becomes the current state of `todoList`. When another item is added, the cycle repeats.

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

You’re using `map` to loop through the `todoList` array, which means the individual item is then passed to the `TodoItem` component as props. To make use of this, you need to have a `TodoItem` component that receives props and renders it on the DOM. I will show you how to do this using functional and class components.

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

> It's fairly easy to understand how they work—especially when seen in context—but it's also a bit difficult to grasp them conceptually. It's confusing at first because they both have abstract terms and their values look the same, but they also have very different _roles._

The main responsibility of a Component is to translate raw data into rich HTML. With that in mind, the _props_ and the _state_ together constitute the _raw data_ that the HTML output derives from.

You could say _props_ + _state_ is the input data for the `render()` function of a Component, so we need to zoom in and see what each data type represents and where does it come from.

### Common ground

Before separating _props_ and _state_, let's also identify where they overlap.

* Both _props_ and _state_ are **plain JS objects**
* Both _props_ and _state_ changes trigger a **render update**
* Both _props_ and _state_ are **deterministic.** If your Component generates different outputs for the same combination of _props_ and _state_ then you're doing something wrong.

#### Does this go inside _props_ or _state_?

{% hint style="info" %}
If a Component needs to alter one of its attributes at some point in time, that attribute should be part of its _state_, otherwise it should just be a _prop_ for that Component.
{% endhint %}

_**To recapitulate :**_

_**props**_** (short for **_**properties**_**) are a Component's configuration, its **_**options**_** if you may. They are received from above and immutable as far as the Component receiving them is concerned.**

**A Component cannot change its **_**props,**_** but it is responsible for putting together the **_**props**_** of its child Components.**

**The **_**state**_** starts with a default value when a Component mounts and then suffers from mutations in time (mostly generated from user events). It's a serializable\* representation of one point in time—a snapshot.**

**A Component manages its own **_**state**_** internally, but—besides setting an initial state—has no business fiddling with the **_**state**_** of its children. You could say the state is private.**

**We didn't say **_**props**_** are also serializable because it's pretty common to pass down callback functions through **_**props.**_

### **Changing **_**props**_** and **_**state**_

|                                              | _props_ | _state_ |
| -------------------------------------------- | ------- | ------- |
| Can get initial value from parent Component? | Yes     | Yes     |
| Can be changed by parent Component?          | Yes     | No      |
| Can set default values inside Component?\*   | Yes     | Yes     |
| Can change inside Component?                 | No      | Yes     |
| Can set initial value for child Components?  | Yes     | Yes     |
| Can change in child Components?              | Yes     | No      |

{% hint style="warning" %}
Note that both _props_ and _state_ initial values received from parents override default values defined inside a Component.
{% endhint %}

### Should this Component have _state_?

_State_ is optional. Since _state_ increases complexity and reduces predictability, a Component without _state_ is preferable. Even though you clearly can't do without state in an interactive app, you should avoid having too many _Stateful Components._

#### **Component types**

* **Stateless Component** — Only _props_, no _state._ There's not much going on besides the `render()` function and all their logic revolves around the _props_ they receive. This makes them very easy to follow (and test for that matter).&#x20;
* **Stateful Component** — Both _props_ and _state._ We also call these _state managers_. They are in charge of client-server communication (XHR, web sockets, etc.), processing data and responding to user events. These sort of logistics should be encapsulated in a moderate number of _Stateful Components_, while all visualization and formatting logic should move downstream into as many _Stateless Components_ as possible.

{% embed url="https://kentcdodds.com/blog/props-vs-state" %}

{% embed url="https://reactjs.org/docs/thinking-in-react.html#step-4-identify-where-your-state-should-live" %}

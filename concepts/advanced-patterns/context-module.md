# Context Module

You can use the Context Module Functions Pattern to encapsulate a complex set of state changes in a utility function that can be tree-shaken and loaded lazily.

Let's take a look at an example of a simple context and a reducer combo:

```jsx
const CounterContext = React.createContext()

function CounterProvider({step = 1, initialCount = 0, ...props}) {
  const [state, dispatch] = React.useReducer(
    (state, action) => {
      const change = action.step ?? step
      switch (action.type) {
        case 'increment': {
          return {...state, count: state.count + change}
        }
        case 'decrement': {
          return {...state, count: state.count - change}
        }
        default: {
          throw new Error(`Unhandled action type: ${action.type}`)
        }
      }
    },
    {count: initialCount},
  )

  const value = [state, dispatch]
  return <CounterContext.Provider value={value} {...props} />
}

function useCounter() {
  const context = React.useContext(CounterContext)
  if (context === undefined) {
    throw new Error(`useCounter must be used within a CounterProvider`)
  }
  return context
}

export {CounterProvider, useCounter}
```

```jsx
import {useCounter} from 'context/counter'

function Counter() {
  const [state, dispatch] = useCounter()
  const increment = () => dispatch({type: 'increment'})
  const decrement = () => dispatch({type: 'decrement'})
  return (
    <div>
      <div>Current Count: {state.count}</div>
      <button onClick={decrement}>-</button>
      <button onClick={increment}>+</button>
    </div>
  )
}
```

```jsx
import {CounterProvider} from 'context/counter'

function App() {
  return (
    <CounterProvider>
      <Counter />
    </CounterProvider>
  )
}
```

I want to focus in on the user of our reducer (the `Counter` component). Notice that they have to create their own `increment` and `decrement` functions which call `dispatch`. I don't think that's a super great API. It becomes even more of an annoyance when you have a sequence of `dispatch` functions that need to be called (like you'll see in our exercise).x

The first inclination is to create "helper" functions and include them in the context. Let's do that. You'll notice that we have to put it in `React.useCallback` so we can list our "helper" functions in dependency lists):

```jsx
const increment = React.useCallback(
  () => dispatch({type: 'increment'}),
  [dispatch],
)
const decrement = React.useCallback(
  () => dispatch({type: 'decrement'}),
  [dispatch],
)
const value = {state, increment, decrement}
return <CounterContext.Provider value={value} {...props} />

// now users can consume it like this:

const {state, increment, decrement} = useCounter()
```

This isn't a _bad_ solution necessarily. But [DanAbramov](https://twitter.com/dan\_abramov/status/1125758606765383680) said:

> Helper methods are object junk that we need to recreate and compare for no purpose other than superficially nicer looking syntax.

Dan suggests (and what Facebook does) the use  of importable "helpers" that accept dispatch. Let's take a look at how that might work:

```jsx
const CounterContext = React.createContext()

function CounterProvider({step = 1, initialCount = 0, ...props}) {
  const [state, dispatch] = React.useReducer(
    (state, action) => {
      const change = action.step ?? step
      switch (action.type) {
        case 'increment': {
          return {...state, count: state.count + change}
        }
        case 'decrement': {
          return {...state, count: state.count - change}
        }
        default: {
          throw new Error(`Unhandled action type: ${action.type}`)
        }
      }
    },
    {count: initialCount},
  )

  const value = [state, dispatch]

  return <CounterContext.Provider value={value} {...props} />
}

function useCounter() {
  const context = React.useContext(CounterContext)
  if (context === undefined) {
    throw new Error(`useCounter must be used within a CounterProvider`)
  }
  return context
}

const increment = dispatch => dispatch({type: 'increment'})
const decrement = dispatch => dispatch({type: 'decrement'})

export {CounterProvider, useCounter, increment, decrement}
```

```jsx
import {useCounter, increment, decrement} from 'context/counter'

function Counter() {
  const [state, dispatch] = useCounter()
  return (
    <div>
      <div>Current Count: {state.count}</div>
      <button onClick={() => decrement(dispatch)}>-</button>
      <button onClick={() => increment(dispatch)}>+</button>
    </div>
  )
}
```

**This may look like overkill, and it is.** However, in some situations this pattern can not only help you reduce duplication, but it also [helps improve performance](https://twitter.com/dan\_abramov/status/1125774170154065920) and helps you avoid mistakes in dependency lists.

## References and articles :

{% embed url="https://vtechguys.medium.com/context-module-pattern-in-react-dd3e89d56f2d" %}

{% embed url="https://medium.com/shunze0925/advanced-react-patterns-note-a0fcad56e43b" %}

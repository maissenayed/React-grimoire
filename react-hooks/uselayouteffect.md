# ⚠ useLayoutEffect

{% embed url="https://blog.logrocket.com/useeffect-vs-uselayouteffect-examples" %}

### Timing of an effect <a href="#timingofaneffect" id="timingofaneffect"></a>

There’s a very big difference between when the `useEffect` callback is invoked and when class methods such as `componentDidMount` and `componentDidUpdate` are invoked.

The effect callback is invoked after the browser layout and painting are carried out. This makes it suitable for many common side effects, such as setting up subscriptions and event handlers since most of these shouldn’t block the browser from updating the screen.

![An illustration of the effect callback](../.gitbook/assets/effect-callback-illustration.png)

This is the case for `useEffect`, but this behavior is not always ideal.

What if you wanted a side effect to be visible to the user before the browser’s next paint? Sometimes, this is important to prevent visual inconsistencies in the UI,.

For such cases, React provides another Hook called `useLayoutEffect`. It has the same signature as `useEffect`; the only difference is in when it’s fired, i.e., when the callback function is invoked.

> **N.B.**, although `useEffect` is deferred until the browser has painted, **it is still guaranteed to be fired before any re-renders. This is important.**

![useEffect is fired before any new re-renders](<../.gitbook/assets/effect-callback-illustration (1).png>)

React will always flush a previous render’s effect before starting a new update.

### `useLayoutEffect` <a href="#uselayouteffect" id="uselayouteffect"></a>

[`useLayoutEffect`](https://reactjs.org/docs/hooks-reference.html#uselayouteffect) has the very same signature as `useEffect`. We’ll discuss the difference between `useLayoutEffect` and `useEffect` below.

```
useLayoutEffect(() => {
//do something
}, [arrayDependency])
```

#### Similar usage as `useEffect`

Here’s the same example for `useEffect` built with `useLayoutEffect`:

```
const ArrayDep = () => {
    const [randomNumber, setRandomNumber] = useState(0)
    const [effectLogs, setEffectLogs] = useState([])
  
    useLayoutEffect(
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

{% embed url="https://blog.logrocket.com/useeffect-vs-uselayouteffect-examples" %}

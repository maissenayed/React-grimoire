# useState

{% embed url="https://blog.logrocket.com/react-reference-guide-hooks-api" %}

{% embed url="https://enlear.academy/types-of-react-hooks-best-practices-45c275b55b1f" %}

{% embed url="https://blog.logrocket.com/react-hooks-cheat-sheet-unlock-solutions-to-common-problems-af4caf699e70" %}

{% embed url="https://react-hooks-cheatsheet.com" %}

{% embed url="https://daveceddia.com/usestate-hook-examples" %}

The signature for the `useState` Hook is as follows:

```jsx
                 const [state, setState] = useState(initialState);
//                        👆      👆 
// Think about it as a getter and a setter
```

Here, `state` and `setState` refer to the state value and updater function returned on invoking `useState` with some `initialState`.

It’s important to note that when your component first renders and invokes `useState`, the `initialState` is the returned state from `useState`.

{% hint style="warning" %}
**Always remember that the value of the state is always the initial state value on the first render**
{% endhint %}


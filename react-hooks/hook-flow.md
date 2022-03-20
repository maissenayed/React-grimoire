# 🆗 Hook flow

> But what exactly is the React Hook Flow?

{% hint style="info" %}
**You probably already know the Lifecycle Methods like componentDidMount or componentDidUpdate. These are used in Class Components. Since most of the time, it’s easier to write a functional component . For this, the React Core Team introduced hooks in Version 16.8. Hooks get called in a specific order, and that’s what we call the hook flow.**
{% endhint %}

![](<../.gitbook/assets/React Hook Flow Diagram.png>)

React Hooks flow includes:

1. Mount
2. Update (when state changes based on any event)
3. UnMount

### Definition <a href="#dd44" id="dd44"></a>

### Render <a href="#dd44" id="dd44"></a>

Once the lazy initializers are called react renders the JSX defined in the return Statement of the component to its Virtual DOM.

### React updates DOM <a href="#571c" id="571c"></a>

Once the Virtual DOM is updated React updates the real DOM.

### Cleanup LayoutEffects <a href="#b175" id="b175"></a>

If you have defined a **useLayoutEffect** which is a very rare case, react will call the function returned from the hook. You can read more about cleanup functions in the official React docs.

### Run LayoutEffects <a href="#a5b1" id="a5b1"></a>

This Phase executed the code inside a **useLayoutEffect** hook.

### Browser paints screen <a href="#5e11" id="5e11"></a>

In this Phase, the Browser paints the updated DOM screen.

### Cleanup Effects <a href="#21d6" id="21d6"></a>

In here the functions returned in the **useEffect** hook get executed.

### Run Effects <a href="#f01d" id="f01d"></a>

This Phase executed the code inside a **useEffect** hook.

## Phases

### Mount:

1. Run the lazy initializer (functions passed to useState or useReducer)
2. Continue the rest of the render function
3. React updates the DOM
4. It runs LayoutEffects
5. Browser paints the screen to reflect
6. Runs the effects

### Update: (When the user make any event it update the state)

1. Runs the render phase
2. React updates DOM
3. Cleanup LayoutEffects first
4. Run LayoutEffects
5. Browser paints the screen
6. Cleanup the effects first
7. Run the effects in the render

### Unmount: Component gets removed from the screen (navigate to other screen or from user event)

1. Cleanup LayoutEffects
2. Cleanup Effects

{% hint style="danger" %}
**Never confuse them with lifecycle methods in Class Components.**
{% endhint %}

A great example of hook flow i found is Kent c dodds example :

{% embed url="https://codesandbox.io/embed/hook-flow-dqk28u?fontsize=14&hidenavigation=1&theme=dark" %}

## References and articles :

{% embed url="https://reactjs.org/docs/hooks-reference.html" %}

{% embed url="https://github.com/donavon/hook-flow" %}

{% embed url="https://egghead.io/lessons/react-understand-the-react-hook-flow" %}

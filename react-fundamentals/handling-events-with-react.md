# 🏁 Handling Events With React

Handling events with **React** elements is very similar to handling events on **DOM** elements. There are some syntax differences:

* **React** events are named using **camelCase**, rather than **lowercase**.
* With **JSX** you pass a function as the event handler, rather than a string.

In the **JavaScript** community, these handler functions are sometimes called **callback functions**, or **callbacks** for short (but this is really just a fancy way of saying _function_.) For example, you could use a callback to verify if a button is clicked

```jsx
<button onClick={() => alert("I'm clicked")}>Click me</button>
```

## Event props

**React’s** event props are named after **DOM** events from raw **JavaScript**. For example, the `onClick` prop from the above example is named after the [`DOM click event`](https://developer.mozilla.org/en-US/docs/Web/Events/click). If you’ve used **jQuery** or raw **JavaScript** before, **React’s** events will feel familiar.

React has props for most DOM events. For example:

* `onClick` and `onMouseMove` can be used with any **HTML** element
* `onKeyDown` and `onFocus` can be used with focusable elements
* `onSubmit` can be used with `<form>` elements

## Event Objects

Whenever **React** calls an event **callback**, it passes a single argument that holds the **event object**.

```jsx
<select id="cars Select"
    onChange={(event) => {
        console.log(event);        
    }}>
    <option value="Audi">Audi</option>
    <option value="BMW">BMW</option>
    <option value="Mercedes">Mercedes</option>
    <option value="Volvo">Volvo</option>
</select>
```

Here, `event` is a synthetic event. **React** defines these synthetic events according to the [W3C spec](https://www.w3.org/TR/DOM-Level-3-Events/), so you don’t need to worry about cross-browser compatibility. **React** events do not work exactly the same as native events. See the [`SyntheticEvent`](https://reactjs.org/docs/events.html) reference guide to learn more.

## Keyboard <a href="#keyboard" id="keyboard"></a>

**Keyboard** events can be used with any focusable element. This includes **HTML** form elements, as well as any element with a `tabIndex` property.

• `onKeyDown` is called when a key is depressed\
• `onKeyPress` is called after the key is released, but before `onKeyUp` is triggered\
• `onKeyUp` is called last, after the key is pressed



To check the key that was pressed, use the `key` property. This holds a string that represents the key.

The `altKey`, `ctrlKey`, `metaKey` and `shiftKey` properties let you check if a modifier key was depressed at the time of the event. These are all booleans.

A numeric `keyCode` property is also available, but try to avoid this as it will make your code harder to read.

{% embed url="https://stackblitz.com/edit/vitejs-vite-rsusfx?devtoolsheight=33&embed=1&file=src%2Fcomponent%2FKeyboard.jsx&hideExplorer=1&view=preview" %}

## Focus <a href="#focus" id="focus"></a>

• `onBlur` is called when a control loses focus\
• `onFocus` is called when a control receives focus

When switching between elements, `onBlur` will always be called before `onFocus`.

It is probably best to avoid the event object for focus events, as browser support for the underlying events varies significantly. In particular, the `preventDefault()` method will not work reliably.

{% embed url="https://stackblitz.com/edit/vitejs-vite-rsusfx?devtoolsheight=33&embed=1&file=src%2Fcomponent%2FFocus.jsx&hideExplorer=1&view=preview" %}

## Mouse <a href="#mouse" id="mouse"></a>

• `onClick`: a mouse button was pressed and released. Called before `onMouseUp`.\
• `onContextMenu`: the right mouse button was pressed.\
• `onDoubleClick`\
• `onMouseDown`: a mouse button is depressed\
• `onMouseEnter`: the mouse moves over an element or its children\
• `onMouseLeave`: the mouse leaves an element\
• `onMouseMove`\
• `onMouseOut`: the mouse moves off of an element, or onto one of its children\
• `onMouseOver`: the mouse moves directly over an element\
• `onMouseUp`: a mouse button was released

**React’s** drag and drop events have access to the same event object properties as the **mouse** events. However, I’d recommend using [react-dnd](https://github.com/react-dnd/react-dnd) instead of using the raw events where possible. For reference, the drag/drop events are:

`onDrag` `onDragEnd` `onDragEnter` `onDragExit` `onDragLeave` `onDragOver` `onDragStart` `onDrop`



The `button` property holds a number that represents which **mouse** button was pressed. This will be `0` for the left button and `1` for the middle button. Theoretically, `2` represents the right button, but most browsers will not trigger any events other than `onContextMenu` when the right button is pressed.

The properties `altKey`, `ctrlKey`, `metaKey` and `shiftKey` allow you to check if a modifier key was pressed on your **keyboard** when the event was triggered, just like with **keyboard** events. These are all booleans.

The `preventDefault()` method can be used to cancel default click actions. For example, to prevent the browser from navigating when a link is clicked, you can call `event.preventDefault()` within an `<a>` element’s `onClick` handler.

There are also a number of positioning properties:

• `clientX` and `clientY` contain the coordinates measured from the top left of the visible part of the page (regardless of the scroll position.)\
• `pageX` and `pageY` contain the coordinates from the top of the page — which may be currently off-screen due to scrolling.\
• `screenX` and `screenY` give the position within the entire screen.

{% embed url="https://stackblitz.com/edit/vitejs-vite-rsusfx?devtoolsheight=33&embed=1&file=src%2Fcomponent%2FMouse.jsx&hideExplorer=1&view=preview" %}

## References and articles :&#x20;

{% embed url="https://reactjs.org/docs/handling-events.html#gatsby-focus-wrapper" %}

{% embed url="https://www.the-guild.dev/blog/react-dom-event-handling-system" %}

{% embed url="https://reactjs.org/docs/events.html" %}

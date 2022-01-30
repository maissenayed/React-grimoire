# Form

In React, there actually aren't a ton of things you have to learn to interact with forms beyond what you can do with regular DOM APIs and JavaScript. Which I think is pretty awesome.

You can attach a submit handler to a form element with the `onSubmit` prop. This will be called with the submit event which has a `target`. That `target` is a reference to the `<form>` DOM node which has a reference to the elements of the form which can be used to get the values out of the form!

• `onChange` is called when the user changes the value in a form control.\
• `onInput` is identical to `onChange`. Prefer `onChange` where possible.\
• `onSubmit` is a special prop for `<form>` elements that is called when a `<button type='submit'>` is pressed, or when the user hits the _return_ key within a field.

{% hint style="warning" %}
For **`onChange`**, the `event.target` object allows you to acces the control 's [DOM node](https://developer.mozilla.org/en/docs/Web/API/Node). You can then use `event.target.value` to get the new value that was entered into the control.

The **`event.preventDefault()`** method allows you to prevent default behavior. When used within **`onSubmit`**, this will prevent the browser from navigating to a new page. When used within **`onChange`**, it will prevent whatever character was entered from being added to the control.
{% endhint %}

### Form default behavior&#x20;

If we consider this component&#x20;

```jsx
import * as React from "react";

export const MyForm = ({ onSubmitUsername }) => {
  const handleSubmit = () => {};
  return (
    <form onSbumit={handleSubmit}>
      <div>
        <label>name:</label>
        <input type="text" />
      </div>
      <button type="submit">Submit</button>
    </form>
  );
};

```

It's a simple Form with a button that have the type submit .when clicked the form **`onSubmit()`** will get triggered. But we will have a full refresh of the page .

I prepped a small sandbox if you open the console and hit submit you will see that the page get refreshed&#x20;

{% embed url="https://codesandbox.io/s/form-kw7uq?from-embed=" %}

That's because the default the browser will make a GET request to the current URL with the values of the form. to fix that we should  use ** `event.preventDefault();`**&#x20;

As we know event is a [**`SyntheticEvent`**](https://reactjs.org/docs/events.html) **** that is just React even that behave exactly  as a regular event but if you want to get the native event just by  **event.nativeEvent()** and you will get our submit event triggred by the form .

{% hint style="warning" %}
**event.target\[index of the input].value** is the common why to get our event value but it will always be relative to the order of the form fields .&#x20;

To link the label of our input we use the **`for`** attribute generally in html with react lie className we use htmlFor instead , therefor  we can access our inputes by&#x20;

**event.target.elements.\[the name of the input].value**  and **** with that we will have more control on wish element value that we are interacting with
{% endhint %}

{% hint style="info" %}
Another way to get the value is via **`ref`** in React. a **`ref`** is an object that stays consistent between renders of react component.&#x20;

It has a **current** property on it which can be updated to any value at any time .In case of interacting with DOM nodes, you can pass a **`ref`** to a react element and react will set the current property to the OM node that's rendered.

For this cas we use a special funtion called **`React.useRef`** that return a reference add a s ref to the input and get it value by **`inputRef.current.value`**([https://reactjs.org/docs/hooks-reference.html#useref](https://reactjs.org/docs/hooks-reference.html#useref))

We will dive deeper into React.useRef() in it appropriate section .
{% endhint %}


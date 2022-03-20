# Form

There aren't many things you have to learn in **React** to interact with forms beyond what you can do with regular **DOM APIs** and **JavaScript**.

The `onSubmit` prop can be used to attach a submit handler to a form element. This will be called in conjunction with the submit event, which has a target. That target is a reference to the  **DOM** node which has a reference to the elements of the form which can be used to get the values out of the form!

• `onChange` is called when the user changes the value in a form control.\
• `onInput` is identical to `onChange`. Prefer `onChange` where possible.\
• `onSubmit` is a special prop for `<form>` elements that is called when a `<button type='submit'>` is pressed, or when the user hits the _**return**_ key within a field.

{% hint style="warning" %}
For **`onChange`**, the `event.target` object allows you to acces the control 's [DOM node](https://developer.mozilla.org/en/docs/Web/API/Node). You can then use `event.target.value` to get the new value that was entered into the control.

The **`event.preventDefault()`** method allows you to prevent default behavior. When used within **`onSubmit`**, this will prevent the browser from navigating to a new page. When used within **`onChange`**, it will prevent whatever character was entered from being added to the control.
{% endhint %}

### Form default behavior&#x20;

If we consider this component:

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

It's a simple form with a button that has the type submit .when clicked, the form **`onSubmit()`** will get triggered. But we will have a full refresh of the page.

I prepped a small sandbox. If you open the console and hit submit, you will see that the page gets refreshed.

{% embed url="https://codesandbox.io/s/form-kw7uq?from-embed=" %}

That's because the default browser will make a **GET** request to the current **URL** with the values of the form. To fix that, we should  use ** `event.preventDefault();`**&#x20;

As we know, event is a [**`SyntheticEvent`**](https://reactjs.org/docs/events.html) **** that is just a **React** event that behaves exactly as a regular event but if you want to get the native event just by **event.nativeEvent()** and you will get our submit event triggered by the form.

{% hint style="warning" %}
**`event.target[index of the input].value` is the common why to get our event value. But it will always be relative to the order of the form fields .**&#x20;

**To link the label of our input, we use the `for` attribute generally in HTML.However with React (like `className`) we use `htmlFor` instead.  Therefore, we can access our inputes by `event.target.elements.[the name of the input].value` and with that we will have more control on wish element value that we are interacting with.**
{% endhint %}

{% hint style="info" %}
**Another way to get the value is via `ref` in React. a `ref` is an object that stays consistent between renders of react components.**&#x20;

**It has a current property according to which can be updated to any value at any time .**

**In case of interacting with DOM nodes, you can pass a `ref` to a react element and react will set the current property to the DOM node that's rendered.**

**For this case we use a special function called `React.useRef`() `` that return a reference add a s ref to the input and get it value by**

**`inputRef.current.value`(**[**https://reactjs.org/docs/hooks-reference.html#useref**](https://reactjs.org/docs/hooks-reference.html#useref)**)**

****

**We will dive deeper into React.useRef() in it appropriate section .**
{% endhint %}

## References and articles :&#x20;

{% embed url="https://reactjs.org/docs/forms.html#gatsby-focus-wrapper" %}

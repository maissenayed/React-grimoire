# Form

In React, there actually aren't a ton of things you have to learn to interact with forms beyond what you can do with regular DOM APIs and JavaScript. Which I think is pretty awesome.

You can attach a submit handler to a form element with the `onSubmit` prop. This will be called with the submit event which has a `target`. That `target` is a reference to the `<form>` DOM node which has a reference to the elements of the form which can be used to get the values out of the form!

• `onChange` is called when the user changes the value in a form control.\
• `onInput` is identical to `onChange`. Prefer `onChange` where possible.\
• `onSubmit` is a special prop for `<form>` elements that is called when a `<button type='submit'>` is pressed, or when the user hits the _return_ key within a field.

{% hint style="warning" %}
For `onChange`, the `event.target` object allows you to acces the control 's [DOM node](https://developer.mozilla.org/en/docs/Web/API/Node). You can then use `event.target.value` to get the new value that was entered into the control.

The `event.preventDefault()` method allows you to prevent default behavior. When used within `onSubmit`, this will prevent the browser from navigating to a new page. When used within `onChange`, it will prevent whatever character was entered from being added to the control.
{% endhint %}


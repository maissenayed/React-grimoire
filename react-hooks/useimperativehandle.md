# 🏁 useImperativeHandle

According to the definition on [Reactjs’ official website](https://reactjs.org/docs/hooks-reference.html#useimperativehandle), useImperativeHandle customizes the instance value that is exposed to parent components when using ref.

As to let useImperativeHandle work, it must be wrapped inside the forwardRef. If you didn’t know about forwardRef, [you can visit our previous article on forwardRef](https://codezup.com/forwardref-in-functional-components-react-hooks/).

Now, the basic signature for the useImperativeHandle Hook is:

```jsx
useImperativeHandle(ref, createHandle, [deps])
```

useImperativeHandle React Hook accepts a ref object and a function whose return value replaces the ref object's stored value, and the entire function is updated when the deps array changes.

**With useImperativeHandle React Hook, we can do 2 things:**

* If you do not use the useImperativeHandle Hook and use simple ref, then it will not allow us to control the value that is returned.

So, for example, if you are referring to an element, the current object of ref will contain the entire element within it.

However, instead of returning the instance element, we can specify what the return value should be, such as the focus, blur, or functions we want to return from child component to parent component.

* In addition, instead of returning native functions like blur, focus, and so on, useImperativeHandle Hook allows us to return custom-defined functions via the createHandle function.

So, before discussing the example, we all know Reactjs code is to have a unidirectional flow of data and logic.

That means, we should pass functions and data down through props and a component should only depend on what is passed in as props.

So, for achieving, **bidirectional flow**, we can use Redux or React’s context API.

But, for just the simple access, we can’t just be embedded or use the Redux or Context library.

So, at that place, useImperativeHandle Hook also comes into play to make the flow bidirectional.

## Example of useImperativeHandle React Hook

**App.js**

```jsx
import React from "react";
import Phone from "./Phone";

const App = () => {
  return (
    <>
      <Phone />
    </>
  );
}

export default App;
```

**Phone.js**

```jsx
import React, { useRef }from "react";
import TextInput from './TextInput'
const Phone = () => {
  const phoneEl = useRef(null)

  const handlePhone = () => {
    
    //1. Access Custom Defined Functions
    
    phoneEl.current.verify()
    phoneEl.current.validate()


    //2. Restrict to functions which we pass directly in createHandle function object

    // If below line is uncommented, then it will return in error as it is not defined in useImperativeHandle Hook even it is native js function

    // phoneEl.current.focus()

  }

  return (
    <div>
      <TextInput ref={phoneEl} onChange={handlePhone}/>
    </div>
  )
}

export default Phone;
```

**TextInput.js**

```jsx
import React, { forwardRef, useImperativeHandle }from "react";
const TextInput = forwardRef((props, ref) => {
  const verify = () => {
    console.log("-----Verify() function called----")
    // You can actual verify and update your states here and also perform other stuff
  }

  const validate = () => {
    console.log("-----validate() function called----")
  }

  useImperativeHandle(ref, () => ({ verify, validate }), [ ])

  return (
    <input {...props} type="text" />
  )
})

export default TextInput
```

{% embed url="https://codesandbox.io/embed/useimperativehandler-2wccpz?autoresize=1&expanddevtools=1&fontsize=14&hidenavigation=1&module=%2Fsrc%2FTextInput.js&theme=dark" %}

In the preceding example, we created three Javascript files: **App.js, Phone.js**, and **TextInput.js.**

So, **App.js** is the main component that will render the child component.

**Phone.js** is the parent component of **TextInput** Component, which is a reusable component in this case.

As we created TextInput as a reusable component, we want some functionalities like validation, verification, updation common to all parent components where we use TextInput.

But the arguments may differ or the data may differ for every component. That means like for the age field, you have some custom array of validators that need to be validated like required validator, age limit validator, and others as well.

While similarly, another component like the Phone has some different validators like Must be of n Length, which starts with +91 validators and all.

So, if we need to manually validate every Component that uses TextInput, we must duplicate the code in all components. As a result, there will be nothing reusable.&#x20;

However, by declaring the child component methods and functions inside the createHandle function of useImperativeHandle Hook, we can easily access them.

As a result, even though we did not pass ref directly to the HTML input element, we can access the verify() and validate() functions.&#x20;

So, as I mentioned in the conditions above, instead of returning the entire element, we can return some of the functions, whether custom or javascript native functions, and limit the DOM's other accessibility.

So, if you remove the comment from the line where we are calling the focus() method, you will get the error. As we know, this is a javascript native function that should be accessed everywhere via the ref current property, but by using the useImperativeHandle Hook, we can restrict the DOM and also specify what should be exposed to the other end.

## Real Example

The [GSAP library](https://blog.logrocket.com/animations-react-hooks-greensock/) is a popular choice for animation examples. To use it, we need to send a DOM element to any of its methods.

Passing around props or using Context works well in most situations, but using those mechanisms cause re-renders, which could hurt performance if you're constantly changing a value, like something based on the mouse position.

To bypass React’s rendering phase, we can use the [useImperativeHandle hook](https://reactjs.org/docs/hooks-reference.html#useimperativehandle), and create an API for our component.

```tsx
const Circle = forwardRef((props, ref) => {
  const el = useRef();
    
  useImperativeHandle(ref, () => {           
    
    // return our API
    return {
      moveTo(x, y) {
        gsap.to(el.current, { x, y });
      }
    };
  }, []);
  
  return <div className="circle" ref={el}></div>;
});
```

Whatever value the imperative hook returns will be forwarded as a ref

```tsx
function App() {    
  const circleRef = useRef();
       
  useEffect(() => {    
    // doesn't trigger a render!
    circleRef.current.moveTo(300, 100);
  }, []);
    
  return (
    <div className="app">   
      <Circle ref={circleRef} />
    </div>
  );
}
```

{% embed url="https://codesandbox.io/embed/falling-sun-hibztj?fontsize=14&hidenavigation=1&theme=dark" %}

{% hint style="info" %}
**Finally, if you are using useImperativeHandle, then you should only use it in combination with the forwardRef**
{% endhint %}

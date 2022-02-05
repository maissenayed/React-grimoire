# Array and Lists

## Create a list

If there’s one unchanging thing about web applications, it’s that they have lists. And so as you might expect, most frameworks attempt to make your life easier with a special syntax for lists.

But with React, elements are just objects, `React.createElement()` is just a function, and lists are just old plain arrays&#x20;

Rendering a list with React involves three steps:

1. Create an array of element objects
2. Set that array as the `children` of a container element
3. Render the container element

Let take a look at this react component&#x20;

```jsx
import * as React from "react";

const animals = ["🦇" ,"🐕" ,"🐈" , "🐄"]
 

function App() {
  return (
    <div className="keys">
      <ul style={{ listStyle: "none", paddingLeft: 0 }}>
        {animals.map((item) => (
          <li>
            <div>{item}</div>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;

```

As you can see we are creating an array of animals ,Simple right but if we try to open our dev tools and check our console we will find a common react list error

{% hint style="danger" %}
**Warning: Each child in a list should have a unique "key" prop.**
{% endhint %}

## Arrays and `key` props <a href="#arrays-and-key-props" id="arrays-and-key-props"></a>

When React encounters an array of elements with identical `type` and `props`, despite _looking_ identical from the outside, it cannot know that they are _really_ identical. It could be that they each have different internal states.

This becomes a problem when the _order_ of the elements changes. Because all the elements look identical, React can’t reorder the corresponding DOM nodes.

To demonstrate, this example renders an array of checkbox elements. Try clicking a checkbox and then clicking the “Reverse” button. Notice how nothing happens.

{% embed url="https://codesandbox.io/embed/array-and-list-key-js8s7?fontsize=14&hidenavigation=1&module=%2Fsrc%2Fcomponents%2FList.js&theme=dark" %}

And when i tried to log what checkboxes is rendering  i have this particular tree

![](<../.gitbook/assets/Screenshot from 2022-02-01 22-13-23.png>)

We can observe that indeed we have 3 Element of type input that they all have a prop type="checkbox",but there is not really something that can distinguish them.

But while React can’t distinguish between identical elements in an array, you can always give it some help! And that is what the `key` prop is for. By providing a `key`, you’re giving React a way to keep track of otherwise identical elements.

To see this in action, if i try adding unique `key` props to each of the checkboxes above. (keys can be strings or numbers — the only thing that matters is that they’re unique). Once you’ve added these, when click a checkbox and then click "Reverse"; the checked boxes should now move as expected!

{% embed url="https://codesandbox.io/embed/array-and-list-key-js8s7?fontsize=14&hidenavigation=1&theme=dark" %}

{% hint style="danger" %}
**As you can see in our example, we've moved the content JSX and ReactDOM.render method call inside a reverseAndRender function. Then, once defined, we call the function, which will render the content on the UI on page load. It's worth noting that we've also inserted the reverseAndRender function call within the onClick function. So, whenever we click the button, the reverseAndRender function is called, and we see the updated reversed checkboxes on the UI.**

****

But still, it's not feasible to call the **reverseAndRender** function every time we want to update the UI. So React added the concept of **State**.
{% endhint %}

{% embed url="https://reactjs.org/docs/lists-and-keys.html#gatsby-focus-wrapper" %}

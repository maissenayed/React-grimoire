# Array and Lists

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

As you can see we are creating an array of animals&#x20;

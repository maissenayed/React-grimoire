# Components

You frequently want to share code, just like in regular JavaScript, which you do by using functions. If you want to distribute JSX, you can do so as well. These functions are referred to as "components" in React and have some unique properties that's defined or called props.

To be more specific, components are functions that tell React how to render one type of element. Each function takes a `props` object, and returns a new element that will be rendered in place of the original.

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    function message(props) {
    // take it as a habit to dustruct props
    const {name,ocupation} = props
    
      return (
        <div>
          {greeting}, {subject}
        </div>
      )
    }
    const props = { name:"Mayssa", ocupation:"best linguist researher" }
    const customCompnent = message(props)
    const element = <div>{customCompnent}</div>
   
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

So what type of `props` can a component receive?

Like HTML elements, they can certainly receive strings and numbers. But custom components can also receive objects, arrays, functions — or even other elements!

If we want to write JavaScript inside of JSX we need to wrap it with curly braces {} .we call that Interpolation

&#x20;Taking template literals as an example :

```javascript
const name = "Mayssa" 
const message =`Hello I'm ${name}`
```

Anything inside \`\` will be considered in string context but if we wrap it by ${} we can write JavaScript inside it and that's the JavaScript context . that's literally Interpolation in action .

Same thing inside JSX but we just ditch the $ and use curly braces and babel will understand that we are writing JavaScript there.

{% hint style="danger" %}
Bear in mind that you can't do statements inside of the curly braces as babel can't interpret them so the best why to do it is to wrap it inside a function&#x20;

**Expression:** Something which evaluates to a value. Example:  (1 + 5) / 2\
**Statement:** A line of code which does something. Example: _if Somthing do something_
{% endhint %}

{% hint style="info" %}
_OPTIONAL_ :mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board:

For an explanation of the important differences in composability (chainability) of expressions vs statements, my favorite reference is John Backus's Turing award paper, [_Can programming be liberated from the von Neumann style?_](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.130.4539\&rep=rep1\&type=pdf).

Imperative languages (C, Java, etc.) emphasize statements for program structure and have expressions as an afterthought. Expressions are prioritized in functional languages.&#x20;

Because pure functional languages have such powerful expressions, statements can be omitted entirely.
{% endhint %}

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    const condition =true
    const element = <div>
    {  
    // this is wrong  ⛔ ⛔ ⛔ ⛔ ⛔ ⛔ ⛔ 
    if(condition){console.log("this will throw an error")}
    }
    </div>
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

But you can use ternary operator _because like you thought it, it returns an **expression**_

{% embed url="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator" %}

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    const condition =true
    const element = (
      <div>
        {
        condition
          ? "I'll be rendered hoooray"
          : "I'll will not be rendered"
        }
      </div>
    );
    
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

Now let's return to our initial code&#x20;

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    function message(props) {
    // take it as a habit to dustruct props
    const {name,ocupation,children} = props
    
      return (
        <div>
          {name}, {ocupation} {children}
        </div>
      )
    }
    const props = { name:"Mayssa", ocupation:"best linguist researher", children:"Im here" }
    const customCompnent = message(props)
    const element = <div>{customCompnent}</div>
   
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

Remember React.createElement():

```jsx
React.createElement(
  type,
  {...props},
  [...children]
)
```

As we said the type argument for React.createElement() can accept various things one of them is a React Element .

In our case we want to create a React Element representing the message function.

```jsx
const messageElement = React.createElement(message,props);
```

That will work just fine as react instead of creating a DOM node , it create an element that is saved in memory and that it will call our message function when we render it on the page .

And if you recall we can convert React.createElement() to JSX. Then our code will look like this

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    function message(props) {
    // take it as a habit to dustruct props
    const {name,ocupation,children} = props
    
      return (
        <div>
          {name}, {ocupation} {children}
        </div>
      )
    }
    
    const props = { name:"Mayssa", ocupation:"best linguist researher" }
   
    const element = (
      <div>
        <message name="Mayssa" ocupation="best linguist researher">
          Hey I'm here
        </message>
      </div>
    );     
    
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

{% hint style="danger" %}
But babel compiler will not recognize message as a React Element, but instead will try to find it as a HTML Tags without a result so it will throw an error.
{% endhint %}

If you want learn more about HTML tags :&#x20;

{% embed url="https://maissen.gitbook.io/maissen-grimoire/html-grimoire/html-cheat-sheet" %}

So we need to tell babel to know that's a React Element and for That all our React component need to start it name by **Uppercase** letter.

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    function message(props) {
    // take it as a habit to dustruct props
    const {name,ocupation,children} = props
    
      return (
        <div>
          {name}, {ocupation} {children}
        </div>
      )
    }
    
   
    const element = (
      <div>
        <Message name="Mayssa" ocupation="best linguist researher">
          Hey I'm here
        </Message>
      </div>
    );   
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

We can even nest those element inside each others:

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script type="text/babel">
 
    function message(props) {
    // take it as a habit to dustruct props
    const {name,ocupation,children} = props
    
      return (
        <div>
          {name}, {ocupation} {children}
        </div>
      )
    }
    
    const props = { name:"Mayssa", ocupation:"best linguist researher" }
   
   const element = (
      <div>
        <Message name="Mayssa" ocupation="best linguist researher">
          Hey I'm here
        </Message>
        <Message name="Maissen" ocupation="Suikoden Guru">
          <Message name="Maissen child" ocupation="Suikoden hater">
            Hey I'm here
          </Message>
        </Message>
      </div>
    );
    
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

{% hint style="info" %}
From here one i'll will be using JSX in the next chapters as it's easier to write and more readable specially if we had a complex tree of components.

But always bear in mind that anything that we will do with JSX we can do it with React raw API's .&#x20;
{% endhint %}

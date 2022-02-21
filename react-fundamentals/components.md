# 🆗 Components

## Custom components

You frequently want to share code, just like in regular **JavaScript**, which you do by using functions. If you want to distribute **JSX**, you can do so as well. These functions are referred to as "components" in **React** and have some unique properties that's defined or called props.

To be more specific, components are functions that tell **React** how to render one type of element. Each function takes a `props` object, and returns a new element that will be rendered in place of the original.

```jsx
...
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
...
```

So what type of `props` can a component receive?

Like **HTML** elements, they can certainly receive strings and numbers. Custom components can also receive objects, arrays, functions — or even other elements!

If we want to write JavaScript inside of **JSX** we need to wrap it with curly braces {} .we call that Interpolation

Taking template literals as an example :

```javascript
const name = "Mayssa" 
const message =`Hello I'm ${name}`
```

Anything inside \`\` will be considered in string context but if we wrap it by ${} we can write JavaScript inside it and that's the JavaScript context . that's literally Interpolation in action .

Same thing inside **JSX** but we just ditch the $ and use curly braces and babel will understand that we are writing JavaScript there.

{% hint style="danger" %}
**Bear in mind that you can't do statements inside of the curly braces as babel can't interpret them so the best why to do it is to wrap it inside a function**&#x20;

**Expression: Something which evaluates to a value. Example:  (1 + 5) / 2**\
**Statement: A line of code which does something. Example: **_**if Somthing does something**_
{% endhint %}

{% hint style="info" %}
_**OPTIONAL** _ :mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board::mortar\_board:

**For an explanation of the important differences in composability (chainability) of expressions vs statements, my favorite reference is John Backus's Turing award paper,** [_**Can programming be liberated from the von Neumann style?**_](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.130.4539\&rep=rep1\&type=pdf)**.**

**Imperative languages (C, Java, etc.) emphasize statements for program structure and have expressions as an afterthought. Expressions are prioritized in functional languages.**&#x20;

**Because pure functional languages have such powerful expressions, statements can be omitted entirely.**
{% endhint %}

```jsx
...
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
...
```

But you can use ternary operator _because like you thought, it returns an **expression**_

{% embed url="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator" %}

```jsx
...
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
...
```

Now let's return to our initial code&#x20;

```jsx
...
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
...
```

Remember **React.createElement()**:

```jsx
React.createElement(
  type,
  {...props},
  [...children]
)
```

As we said, the type argument for React.createElement() can accept various things one of which is a **React Element** .

In our case, we want to create a **React Element** representing the message function.

```jsx
const messageElement = React.createElement(message,props);
```

That will work just fine as **react** instead of creating a **DOM** node. It creates an element that is saved in memory and that will call our message function when we render it on the page.

If you can recall we can convert **React.createElement()** to **JSX**. Then our code will look something like this:

```jsx
...
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
...
```

{% hint style="danger" %}
**Babel compiler will not recognize message as a React Element. Instead, it will try to find it as a HTML Tags without a result so it will throw an error.**
{% endhint %}

If you want learn more about **HTML** **tags** :&#x20;

{% embed url="https://maissen.gitbook.io/maissen-grimoire/html-grimoire/html-cheat-sheet" %}

So we need to let **babel** know that's a React Element, and for that, all our React component's name will need to start with **Uppercase** letter.

```jsx
...
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
...
```

We can even nest those element inside each others:

```jsx
...
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
...
```

{% hint style="info" %}
**From here on, i'll will be dealing with JSX in the next chapters as it's easier to write and is more readable especially if we have a complex tree of components.**

**But always bear in mind that anything that we will do with JSX we can do with React raw APIs.**&#x20;
{% endhint %}

## React Fragments

{% embed url="https://reactjs.org/docs/fragments.html" %}

When using **React**, it's a common pattern to return multiple elements by wrapping them with a container element like **div**. This works fine, but by doing so, we're adding an extra node to the **DOM**. As your app grows, these extra nodes contribute to slow performance. Below is an example without fragments:

```jsx
const Paper = () => {
  return (
    <div>
      <Header />
      <Main />
    </div>
  );
};

const Home = () => {
  return (
    <Layout>
      <Paper />
      <Sidebar />
    </Layout>
  );
};

```

As you see in the dashboard component, we wrap the child elements with a **div** and then call the **Paper** component in the **Home** component. Now, let's see what it looks like in the browser.

```jsx
<Layout>
    <div>
        <Header />
        <Main />
    </div>
    <Sidebar />
</Layout>
```

As you can see in the example, we have an unused div that doesn't contribute to anything in the layout. This is redundant.

### How to use Fragments?

To solve this problem, Fragments were introduced in **React**. Fragments are used to group a list of children without adding extra nodes to the **DOM**. Let's look at an example where we use Fragments:

```jsx
const Paper = () => {
  return (
    <React.Fragment>
      <Header />
      <Main />
    </React.Fragment>
  );
};

const Home = () => {
  return (
    <React.Fragment>
      <Paper />
      <Sidebar />
    </React.Fragment>
  );
};
```

Now, if we look at the browser we'll see that no additional elements have been added to the **DOM**.

```jsx
<Layout>
    <Header/>
    <Main/>
    <Sidebar/>
<Layout>
```

### Syntax

Fragments can be used using two types of syntax. The first one is using **React.Fragment** which we've used multiple times above. The other one is a new shorter syntax, using empty brackets, that does the same thing.

```jsx
// Using React.Fragment tags  that support Keys or attributes
return (
  <React.Fragment>
    <Paper />
    <Sidebar />
  </React.Fragment>
);

// Using empty brackets
return (
  <>
    <Paper />
    <Sidebar />
  </>
);
```

Both of these types of syntax work the same. Although, the newer syntax doesn't support keys or attributes.

---
description: The Elegant React way
---

# 🆗 JSX

Writing our code with React.createElement() and reactDOM.render(), it's a little bit verbose; not that readable.

The good thing the react team thought about that too and create a HTML-like syntactic suger on top of the raw React Api's called JSX

### JSX rewrites your JavaScript files <a href="#jsx-rewrites-your-javascript-files" id="jsx-rewrites-your-javascript-files"></a>

JSX is just a tool that converts files like this:

```jsx
const element =
  <div id="container">
    Hello, world!
  </div>
```

into files like this:

```jsx
const element =
  React.createElement(
    'div',
    {id:'container'},
    "Hello, world!"
  )
```

### Why use JSX? <a href="#why-use-jsx" id="why-use-jsx"></a>

To use JSX with reasonable performance, you'd need a build process, which would entail (at a minimum) understanding and installing node.js and create-react-app or babel. While this is usually acceptable, there are times when you'd rather avoid the overhead.

Learning all of this just to avoid typing createElement() a few times doesn't make much sense if you're just getting started. However, there will come a point when your apps will be large enough that tooling will be a worthwhile investment. And once you've arrived at this point, JSX is a fantastic tool to have:

* Large element definitions are simplified.
* &#x20;It provides visual cues and assists editors with syntax highlighting.&#x20;
* It assists React in producing more useful error and warning messages

{% hint style="info" %}
Because JSX is not actually JavaScript, you have to convert it using something called a code compiler. [Babel](https://babeljs.io) is one such tool.

Pro tip: If you'd like to see how JSX gets compiled to JavaScript, [check out the online babel REPL here](https://babeljs.io/repl#?builtIns=App\&code\_lz=MYewdgzgLgBArgSxgXhgHgCYIG4D40QAOAhmLgBICmANtSGgPRGm7rNkDqIATtRo-3wMseAFBA\&presets=react\&prettier=true).

If you can train your brain to look at JSX and see the compiled version of that code, you'll be MUCH more effective at reading and using it! I strongly recommend you give this some intentional practice.   &#x20;

Because JSX is not actually JavaScript, it must be converted using a code compiler. One such tool is Babel.

If you want to see how JSX is compiled to JavaScript, use the [online babel REPL.](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie\_mob%2011\&build=\&builtIns=App\&corejs=3.6\&spec=false\&loose=false\&code\_lz=MYewdgzgLgBArgSxgXhgHgCYIG4D40QAOAhmLgBICmANtSGgPRGm7rNkDqIATtRo-3wMseAFBA\&debug=false\&forceAllTransforms=false\&shippedProposals=false\&circleciRepo=\&evaluate=false\&fileSize=false\&timeTravel=false\&sourceType=module\&lineWrap=true\&presets=react\&prettier=true\&targets=\&version=7.16.12\&externalPlugins=\&assumptions=%7B%7D)&#x20;

You'll be MUCH more effective at reading and using JSX if you can train your brain to look at it and see the compiled version of the code! I strongly advise you to put this into practice on a regular basis.
{% endhint %}

So let's convert our code to JSX. First of all, like react and reactDOM, we will add babel script from unpkg

```jsx
 ...
   <body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
    <script type="module">
    
    const element = React.createElement('div', {
      className: 'container',
      children: 'Hello World',
    })

    ReactDOM.render(element, document.getElementById('root'));
    </script>
  </body>
...
```

Then let's try to change our React.createElement() to JSX

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script type="text/babel">
    // 🔥 "type="text/bable" to indicate that this code need to be compiled by babel
    
    // const element = React.createElement('div', { className = 'container' }); 
    
                                          👇
    
    const element = <div className="container"></div>
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
...
```

Easy right? How about children?

```jsx
...
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>
  <script type="text/babel">
  // 🔥  "type="text/bable" to indicate that this code need to be compiled by babel
  
    // const element = React.createElement('div', { className = 'container' }, [
    //  React.createElement('div', { className = 'container' }, "I'm the first child"),
    //  React.createElement('div', { className = 'container' }, "I'm the first child"),
    // ]); 
                                    👇 

    const element = (
      <div className="container">
        <div className="firstChild">I'm the first child</div>
        <div className="secondChild">I'm the second child</div>
      </div>
      );
    ReactDOM.render(element, document.getElementById('root'));
  </script>
</body>
...
```

{% hint style="danger" %}
**You may have noticed that I changed the type of our JavaScript from module to text/babel and that's to indicate to the browser not to evaluate the script . However, babel will control the compiling for that script** &#x20;
{% endhint %}

## References and articles :&#x20;

{% embed url="https://reactjs.org/docs/introducing-jsx.html" %}

{% embed url="https://reactjs.org/docs/jsx-in-depth.html" %}

{% embed url="https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html" %}

{% embed url="https://www.youtube.com/watch?index=2&list=PLNqp92_EXZBKa1U7JbgUwBnDk3XzYDvXe&v=HwNArS3f1Ss" %}

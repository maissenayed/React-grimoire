# The Basic javascript "Hello world"

Going back to basics allows us to review knowledge and, in some senses of the word, connect the dots on ambiguous aspects.

Before tackling React, maybe we should review how to make a basic web page using vanilla JavaScript.

Basically the most minimal thing that we can call a web page is just one Html File that say Hello world .

Like this one :

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
   <div id='root'>Hello World</div>
</body>
</html>
```

{% hint style="info" %}
The browser parses this HTML code and creates the DOM (Document Object Model). The browser then exposes the DOM to JavaScript, at that point your web page will become interactive where you can do the basic events that we will talk about in another Section.
{% endhint %}

Now if we want to add some JavaScript we can just use the script tag&#x20;

```html
<html>
  <body>
    <div id='root'>Hello World</div>
    <script type="module">
      // your JavaScript here
    </script>
  </body>
</html>
```

{% hint style="success" %}
**`import` and ES6 modules**

Did you notice the ES6 `import` statement in the above example?

In order to ensure that the `import` statements work, the `<script>` tag in your HTML file will need to have the attribute `type="module"`. Surprisingly, this actually works as-is in most modern browsers.
{% endhint %}

The first question i ever asked my self is how really JavaScript can inter-react with the DOM .

How i can really create , modify or delete DOM element using JavaScript and of course it lead to my two ever JavaScript command i  wrote :

```javascript
// Create an element in the DOM .
const root = document.createElement('div')

// the constant root is now a taking some space in our memory without doing anything ,
// To make it show up we need to append it the document body (DOM tree).
document.body.append(rootElement)
```

To read more about the browser Document interface :

{% embed url="https://developer.mozilla.org/en-US/docs/Web/API/Document" %}

{% hint style="info" %}
The DOM represents a document with a logical tree. Each branch of the tree ends in a node, and each node contains objects. DOM methods allow programmatic access to the tree. With them, you can change the document's structure, style, or content.
{% endhint %}

Manipulating an Element is easy we can add styling or getting and adding content. Lets try to play with some stuff

```tsx
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    /* just some indicative styling */
    <style>
      #root {
        background-color: aqua;
      }
    </style>
  </head>
  <body>
    <script type="module">
      const root = document.createElement('div');

      // Adding htmlElement attributes to our root element
      // https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute
      root.setAttribute('id', 'root');
    
      // https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent
      root.textContent = 'Hello world';
      
      // We always need to append the root element to the document
      document.body.append(root);
    </script>
  </body>
</html>
```

As you can see i added the id selector and the class selector to the root element added some styling and even added our hello world text, thus we can always use html tags to create the div element  with it's attributes but i just wanted to show how really JavaScript can leverage all of that programmatically &#x20;

{% hint style="warning" %}
People were creating HTML on the server and then layering JavaScript on top of it for interactivity. However, as the requirements for that interactivity grew more difficult, this approach resulted in applications that were difficult to maintain and had performance issues.&#x20;

As a result, instead of defining the DOM in hand-written HTML, modern JavaScript frameworks were developed to address some of the issues. Like our beloved React
{% endhint %}


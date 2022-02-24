# Concepts to always have in mind

## MODERN JAVASCRIPT CORE CONCEPTS YOU NEED TO KNOW TO USE REACT <a href="#section-1-modern-javascript-core-concepts-you-need-to-know-to-use-react" id="section-1-modern-javascript-core-concepts-you-need-to-know-to-use-react"></a>

### **Find out if you have to learn something before diving into learning React**

If you are willing to learn React, you first need to have a few things under your belt. There are some prerequisite technologies you have to be familiar with, in particular related to some of the more recent JavaScript features you’ll use over and over in React.

Sometimes people think one particular feature is provided by React, but instead it’s just modern JavaScript syntax.

There is no point in being an expert in those topics right away, but the more you dive into React, the more you’ll need to master those.

I will mention a list of things to get you up to speed quickly.

### Variables <a href="#variables" id="variables"></a>

A variable is a literal assigned to an identifier, so you can reference and use it later in the program.

Variables in JavaScript do not have any type attached. Once you assign a specific literal type to a variable, you can later reassign the variable to host any other type, without type errors or any issue.

This is why JavaScript is sometimes referred to as “untyped”.

A variable must be declared before you can use it. There are 3 ways to do this, using `var`, `let` or `const`, and those 3 ways differ in how you can interact with the variable later on.

**Using `var`**

Until ES2015, `var` was the only construct available for defining variables.

```jsx
var a = 0
```

If you forget to add `var` you will be assigning a value to an undeclared variable, and the results might vary.

In modern environments, with strict mode enabled, you will get an error. In older environments (or with strict mode disabled) this will simply initialize the variable and assign it to the global object.

If you don’t initialize the variable when you declare it, it will have the `undefined` value until you assign a value to it.

```jsx
var a //typeof a === 'undefined'
```

You can redeclare the variable many times, overriding it:

```jsx
var a = 1
var a = 2
```

You can also declare multiple variables at once in the same statement:

```js
var a = 1, b = 2jsx
```

The **scope** is the portion of code where the variable is visible.

A variable initialized with `var` outside of any function is assigned to the global object, has a global scope and is visible everywhere. A variable initialized with `var` inside a function is assigned to that function, it's local and is visible only inside it, just like a function parameter.

Any variable defined in a function with the same name as a global variable takes precedence over the global variable, shadowing it.

It’s important to understand that a block (identified by a pair of curly braces) does not define a new scope. A new scope is only created when a function is created, because `var` does not have block scope, but function scope.

Inside a function, any variable defined in it is visible throughout all the function code, even if the variable is declared at the end of the function it can still be referenced in the beginning, because JavaScript before executing the code actually _moves all variables on top_ (something that is called **hoisting**). To avoid confusion, always declare variables at the beginning of a function.

**Using `let`**

`let` is a new feature introduced in ES2015 and it's essentially a block scoped version of `var`. Its scope is limited to the block, statement or expression where it's defined, and all the contained inner blocks.

Modern JavaScript developers might choose to only use `let` and completely discard the use of `var`.

> _If `let` seems an obscure term, just read `let color = 'red'` as_ let the color be red _and it all makes much more sense_

Defining `let` outside of any function - contrary to `var` - does not create a global variable.

**Using `const`**

Variables declared with `var` or `let` can be changed later on in the program, and reassigned. Once a `const` is initialized, its value can never be changed again, and it can't be reassigned to a different value.

```jsx
const a = 'test'
```

We can’t assign a different literal to the `a` const. We can however mutate `a` if it's an object that provides methods that mutate its contents.

`const` does not provide immutability, just makes sure that the reference can't be changed.

`const` has block scope, same as `let`.

Modern JavaScript developers might choose to always use `const` for variables that don't need to be reassigned later in the program.

Why? Because we should always use the simplest construct available to avoid making errors down the road.

### Arrow functions <a href="#arrow-functions" id="arrow-functions"></a>

Arrow functions were introduced in ES6 / ECMAScript 2015, and since their introduction they changed forever how JavaScript code looks (and works).

In my opinion this change was so welcoming that you now rarely see the usage of the `function` keyword in modern codebases.

Visually, it’s a simple and welcome change, which allows you to write functions with a shorter syntax, from:

```jsx
const myFunction = function() {
  //...
}
```

to

```jsx
const myFunction = () => {
  //...
}
```

If the function body contains just a single statement, you can omit the brackets and write all on a single line:

```jsx
const myFunction = () => doSomething()
```

Parameters are passed in the parentheses:

```jsx
const myFunction = (param1, param2) => doSomething(param1, param2)
```

If you have one (and just one) parameter, you could omit the parentheses completely:

```jsx
const myFunction = param => doSomething(param)
```

Thanks to this short syntax, arrow functions **encourage the use of small functions**.

### Implicit return <a href="#implicit-return" id="implicit-return"></a>

Arrow functions allow you to have an implicit return: values are returned without having to use the `return` keyword.

It works when there is a one-line statement in the function body:

```jsx
const myFunction = () => 'test'

myFunction() //'test'
```

Another example, when returning an object, remember to wrap the curly brackets in parentheses to avoid it being considered the wrapping function body brackets:

```jsx
const myFunction = () => ({ value: 'test' })

myFunction() //{value: 'test'}
```

### How this works in arrow functions <a href="#how-this-works-in-arrow-functions" id="how-this-works-in-arrow-functions"></a>

`this` is a concept that can be complicated to grasp, as it varies a lot depending on the context and also varies depending on the mode of JavaScript (_strict mode_ or not).

It’s important to clarify this concept because arrow functions behave very differently compared to regular functions.

When defined as a method of an object, in a regular function `this` refers to the object, so you can do:

```jsx
const car = {
  model: 'Fiesta',
  manufacturer: 'Ford',
  fullName: function() {
    return `${this.manufacturer} ${this.model}`
  }
}
```

calling `car.fullName()` will return `"Ford Fiesta"`.

The `this` scope with arrow functions is **inherited** from the execution context. An arrow function does not bind `this` at all, so its value will be looked up in the call stack, so in this code `car.fullName()` will not work, and will return the string `"undefined undefined"`:

```jsx
const car = {
  model: 'Fiesta',
  manufacturer: 'Ford',
  fullName: () => {
    return `${this.manufacturer} ${this.model}`
  }
}
```

Due to this, arrow functions are not suited as object methods.

Arrow functions cannot be used as constructors either, when instantiating an object will raise a `TypeError`.

This is where regular functions should be used instead, **when dynamic context is not needed**.

This is also a problem when handling events. DOM Event listeners set `this` to be the target element, and if you rely on `this` in an event handler, a regular function is necessary:

```jsx
const link = document.querySelector('#link')
link.addEventListener('click', () => {
  // this === window
})

const link = document.querySelector('#link')
link.addEventListener('click', function() {
  // this === link
})
```

### Rest and spread <a href="#rest-and-spread" id="rest-and-spread"></a>

You can expand an array, an object or a string using the spread operator `...`.

Let’s start with an array example. Given

```jsx
const a = [1, 2, 3]
```

you can create a new array using

```jsx
const b = [...a, 4, 5, 6]
```

You can also create a copy of an array using

```jsx
const c = [...a]
```

This works for objects as well. Clone an object with:

```jsx
const newObj = { ...oldObj }
```

Using strings, the spread operator creates an array with each char in the string:

```jsx
const hey = 'hey'
const arrayized = [...hey] // ['h', 'e', 'y']
```

This operator has some pretty useful applications. The most important one is the ability to use an array as function argument in a very simple way:

```jsx
const f = (foo, bar) => {}
const a = [1, 2]
f(...a)
```

(in the past you could do this using `f.apply(null, a)` but that's not as nice and readable)

The **rest element** is useful when working with **array destructuring**:

```jsx
const numbers = [1, 2, 3, 4, 5]
[first, second, ...others] = numbers
```

and **spread elements**:

```jsx
const numbers = [1, 2, 3, 4, 5]
const sum = (a, b, c, d, e) => a + b + c + d + e
const sumOfNumbers = sum(...numbers)
```

ES2018 introduces rest properties, which are the same but for objects.

### **Rest properties**:

```jsx
const { first, second, ...others } = {
  first: 1,
  second: 2,
  third: 3,
  fourth: 4,
  fifth: 5
}

first // 1
second // 2
others // { third: 3, fourth: 4, fifth: 5 }
```

**Spread properties** allow to create a new object by combining the properties of the object passed after the spread operator:

```jsx
const items = { first, second, ...others }
items //{ first: 1, second: 2, third: 3, fourth: 4, fifth: 5 }
```

### Object and array destructuring <a href="#object-and-array-destructuring" id="object-and-array-destructuring"></a>

Given an object, using the destructuring syntax you can extract just some values and put them into named variables:

```jsx
const person = {
  firstName: 'Tom',
  lastName: 'Cruise',
  actor: true,
  age: 54 //made up
}

const { firstName: name, age } = person //name: Tom, age: 54
```

`name` and `age` contain the desired values.

The syntax also works on arrays:

```jsx
const a = [1, 2, 3, 4, 5]
const [first, second] = a
```

This statement creates 3 new variables by getting the items with index 0, 1, 4 from the array `a`:

```jsx
const [first, second, , , fifth] = a
```

### Template literals <a href="#template-literals" id="template-literals"></a>

Template Literals are a new ES2015 / ES6 feature that allows you to work with strings in a novel way compared to ES5 and below.

The syntax at a first glance is very simple, just use backticks instead of single or double quotes:

```jsx
const a_string = `something`
```

They are unique because they provide a lot of features that normal strings built with quotes do not, in particular:

* they offer a great syntax to define multiline strings
* they provide an easy way to interpolate variables and expressions in strings
* they allow you to create DSLs with template tags (DSL means domain specific language, and it’s for example used in React by Styled Components, to define CSS for a component)

Let’s dive into each of these in detail.

### **Multiline strings**

Pre-ES6, to create a string spanning over two lines you had to use the `\` character at the end of a line:

```jsx
const string =
  'first part \
second part'
```

This allows to create a string on 2 lines, but it’s rendered on just one line:

`first part second part`

To render the string on multiple lines as well, you explicitly need to add  at the end of each line, like this:

```
const string =
  'first line\n \
second line'
```

or

```
const string = 'first line\n' + 'second line'
```

Template literals make multiline strings much simpler.

Once a template literal is opened with the backtick, you just press enter to create a new line, with no special characters, and it’s rendered as-is:

```
const string = `Hey
this
string
is awesome!`
```

Keep in mind that space is meaningful, so doing this:

```
const string = `First
                Second`
```

is going to create a string like this:

```jsx
First
                Second
```

an easy way to fix this problem is by having an empty first line, and appending the trim() method right after the closing backtick, which will eliminate any space before the first character:

```jsx
const string = `
First
Second`.trim()
```

### **Interpolation**

Template literals provide an easy way to interpolate variables and expressions into strings.

You do so by using the `${...}` syntax:

```jsx
const myVariable = 'test'
const string = `something ${myVariable}` //something test
```

inside the `${}` you can add anything, even expressions:

```jsx
const string = `something ${1 + 2 + 3}`
const string2 = `something ${foo() ? 'x' : 'y'}`
```

### Classes <a href="#classes" id="classes"></a>

In 2015 the ECMAScript 6 (ES6) standard introduced classes.

JavaScript has a quite uncommon way to implement inheritance: prototypical inheritance. [Prototypal inheritance](https://flaviocopes.com/javascript-prototypal-inheritance/), while in my opinion great, is unlike most other popular programming language’s implementation of inheritance, which is class-based.

People coming from Java or Python or other languages had a hard time understanding the intricacies of prototypal inheritance, so the ECMAScript committee decided to sprinkle syntactic sugar on top of prototypical inheritance so that it resembles how class-based inheritance works in other popular implementations.

This is important: JavaScript under the hood is still the same, and you can access an object prototype in the usual way.

#### **A class definition**

This is how a class looks.

```jsx
class Person {
  constructor(name) {
    this.name = name
  }
  
  hello() {
    return 'Hello, I am ' + this.name + '.'
  }
}
```

A class has an identifier, which we can use to create new objects using `new ClassIdentifier()`.

When the object is initialized, the `constructor` method is called, with any parameters passed.

A class also has as many methods as it needs. In this case `hello` is a method and can be called on all objects derived from this class:

```
const flavio = new Person('Flavio')
flavio.hello()
```

#### **Class inheritance**

A class can extend another class, and objects initialized using that class inherit all the methods of both classes.

If the inherited class has a method with the same name as one of the classes higher in the hierarchy, the closest method takes precedence:

```jsx
class Programmer extends Person {
  hello() {
    return super.hello() + ' I am a programmer.'
  }
}

const flavio = new Programmer('Flavio')
flavio.hello()
```

(the above program prints “_Hello, I am Flavio. I am a programmer._”)

Classes do not have explicit class variable declarations, but you must initialize any variable in the constructor.

Inside a class, you can reference the parent class calling `super()`.

#### **Static methods**

Normally methods are defined on the instance, not on the class.

Static methods are executed on the class instead:

```jsx
class Person {
  static genericHello() {
    return 'Hello'
  }
}

Person.genericHello() //Hello
```

#### **Private methods**

JavaScript does not have a built-in way to define private or protected methods.

There are workarounds, but I won’t describe them here.

#### **Getters and setters**

You can add methods prefixed with `get` or `set` to create a getter and setter, which are two different pieces of code that are executed based on what you are doing: accessing the variable, or modifying its value.

```jsx
class Person {
  constructor(name) {
    this.name = name
  }
  
  set name(value) {
    this.name = value
  }
  
  get name() {
    return this.name
  }
}
```

If you only have a getter, the property cannot be set, and any attempt at doing so will be ignored:

```
class Person {
  constructor(name) {
    this.name = name
  }
  
  get name() {
    return this.name
  }
}
```

If you only have a setter, you can change the value but not access it from the outside:

```jsx
class Person {
  constructor(name) {
    this.name = name
  }
  
  set name(value) {
    this.name = value
  }
}
```

### Callbacks <a href="#callbacks" id="callbacks"></a>

Computers are asynchronous by design.

Asynchronous means that things can happen independently of the main program flow.

In the current consumer computers, every program runs for a specific time slot, and then it stops its execution to let another program continue its execution. This thing runs in a cycle so fast that’s impossible to notice, and we think our computers run many programs simultaneously, but this is an illusion (except on multiprocessor machines).

Programs internally use _interrupts_, a signal that’s emitted to the processor to gain the attention of the system.

I won’t go into the internals of this, but just keep in mind that it’s normal for programs to be asynchronous, and halt their execution until they need attention, and the computer can execute other things in the meantime. When a program is waiting for a response from the network, it cannot halt the processor until the request finishes.

Normally, programming languages are synchronous, and some provide a way to manage asynchronicity, in the language or through libraries. C, Java, C#, PHP, Go, Ruby, Swift, Python, they are all synchronous by default. Some of them handle async by using threads, spawning a new process.

JavaScript is **synchronous** by default and is single threaded. This means that code cannot create new threads and run in parallel.

Lines of code are executed in series, one after another, for example:

```jsx
const a = 1
const b = 2
const c = a * b
console.log(c)
doSomething()
```

But JavaScript was born inside the browser, its main job, in the beginning, was to respond to user actions, like `onClick`, `onMouseOver`, `onChange`, `onSubmit` and so on. How could it do this with a synchronous programming model?

The answer was in its environment. The **browser** provides a way to do it by providing a set of APIs that can handle this kind of functionality.

More recently, Node.js introduced a non-blocking I/O environment to extend this concept to file access, network calls and so on.

You can’t know when a user is going to click a button, so what you do is, you **define an event handler for the click event**. This event handler accepts a function, which will be called when the event is triggered:

```
document.getElementById('button').addEventListener('click', () => {
  //item clicked
})
```

This is the so-called **callback**.

A callback is a simple function that’s passed as a value to another function, and will only be executed when the event happens. We can do this because JavaScript has first-class functions, which can be assigned to variables and passed around to other functions (called **higher-order functions**)

It’s common to wrap all your client code in a `load` event listener on the `window`object, which runs the callback function only when the page is ready:

```
window.addEventListener('load', () => {
  //window loaded
  //do what you want
})
```

Callbacks are used everywhere, not just in DOM events.

One common example is by using timers:

```
setTimeout(() => {
  // runs after 2 seconds
}, 2000)
```

XHR requests also accept a callback, in this example by assigning a function to a property that will be called when a particular event occurs (in this case, the state of the request changes):

```
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4) {
    xhr.status === 200 ? console.log(xhr.responseText) : console.error('error')
  }
}
xhr.open('GET', 'https://yoursite.com')
xhr.send()
```

### **Handling errors in callbacks**

How do you handle errors with callbacks? One very common strategy is to use what Node.js adopted: the first parameter in any callback function is the error object: **error-first callbacks**

If there is no error, the object is `null`. If there is an error, it contains some description of the error and other information.

```
fs.readFile('/file.json', (err, data) => {
  if (err !== null) {
    //handle error
    console.log(err)
    return
  }
  
  //no errors, process data
  console.log(data)
})
```

### **The problem with callbacks**

Callbacks are great for simple cases!

However every callback adds a level of nesting, and when you have lots of callbacks, the code starts to be complicated very quickly:

```
window.addEventListener('load', () => {
  document.getElementById('button').addEventListener('click', () => {
    setTimeout(() => {
      items.forEach(item => {
        //your code here
      })
    }, 2000)
  })
})
```

This is just a simple 4-levels code, but I’ve seen much more levels of nesting and it’s not fun.

How do we solve this?

### ALTERNATIVES TO CALLBACKS <a href="#alternatives-to-callbacks" id="alternatives-to-callbacks"></a>

Starting with ES6, JavaScript introduced several features that help us with asynchronous code that do not involve using callbacks:

* Promises (ES6)
* Async/Await (ES8)

### Promises <a href="#promises" id="promises"></a>

Promises are one way to deal with asynchronous code, without writing too many callbacks in your code.

Although they’ve been around for years, they were standardized and introduced in ES2015, and now they have been superseded in ES2017 by async functions.

**Async functions** use the promises API as their building block, so understanding them is fundamental even if in newer code you’ll likely use async functions instead of promises.

**How promises work, in brief**

Once a promise has been called, it will start in **pending state**. This means that the caller function continues the execution, while it waits for the promise to do its own processing, and give the caller function some feedback.

At this point, the caller function waits for it to either return the promise in a **resolved state**, or in a **rejected state**, but as you know JavaScript is asynchronous, so _the function continues its execution while the promise does it work_.

**Which JS API use promises?**

In addition to your own code and library code, promises are used by standard modern Web APIs like [Fetch](https://flaviocopes.com/fetch-api/) or [Service Workers](https://flaviocopes.com/service-workers/).

It’s unlikely that in modern JavaScript you’ll find yourself _not_ using promises, so let’s start diving right into them.

**Creating a promise**

The Promise API exposes a Promise constructor, which you initialize using `new Promise()`:

```
let done = true

const isItDoneYet = new Promise((resolve, reject) => {
  if (done) {
    const workDone = 'Here is the thing I built'
    resolve(workDone)
  } else {
    const why = 'Still working on something else'
    reject(why)
  }
})
```

As you can see the promise checks the `done` global constant, and if that's true, we return a resolved promise, otherwise a rejected promise.

Using `resolve` and `reject` we can communicate back a value, in the above case we just return a string, but it could be an object as well.

**Consuming a promise**

In the last section, we introduced how a promise is created.

Now let’s see how the promise can be _consumed_ or used.

```
const isItDoneYet = new Promise()
//...

const checkIfItsDone = () => {
  isItDoneYet
    .then(ok => {
      console.log(ok)
    })
    .catch(err => {
      console.error(err)
    })
}
```

Running `checkIfItsDone()` will execute the `isItDoneYet()` promise and will wait for it to resolve, using the `then` callback, and if there is an error, it will handle it in the `catch` callback.

**Chaining promises**

A promise can be returned to another promise, creating a chain of promises.

A great example of chaining promises is given by the [Fetch API](https://flaviocopes.com/fetch-api/), a layer on top of the XMLHttpRequest API, which we can use to get a resource and queue a chain of promises to execute when the resource is fetched.

The Fetch API is a promise-based mechanism, and calling `fetch()` is equivalent to defining our own promise using `new Promise()`.

Example:

```
const status = response => {
  if (response.status >= 200 && response.status < 300) {
    return Promise.resolve(response)
  }
  return Promise.reject(new Error(response.statusText))
}

const json = response => response.json()

fetch('/todos.json')
  .then(status)
  .then(json)
  .then(data => {
    console.log('Request succeeded with JSON response', data)
  })
  .catch(error => {
    console.log('Request failed', error)
  })
```

In this example, we call `fetch()` to get a list of TODO items from the `todos.json` file found in the domain root, and we create a chain of promises.

Running `fetch()` returns a [response](https://fetch.spec.whatwg.org/#concept-response), which has many properties, and within those we reference:

* `status`, a numeric value representing the HTTP status code
* `statusText`, a status message, which is `OK` if the request succeeded

`response` also has a `json()` method, which returns a promise that will resolve with the content of the body processed and transformed into JSON.

So given those premises, this is what happens: the first promise in the chain is a function that we defined, called `status()`, that checks the response status and if it's not a success response (between 200 and 299), it rejects the promise.

This operation will cause the promise chain to skip all the chained promises listed and will skip directly to the `catch()` statement at the bottom, logging the `Request failed` text along with the error message.

If that succeeds instead, it calls the json() function we defined. Since the previous promise, when successful, returned the `response` object, we get it as an input to the second promise.

In this case, we return the data JSON processed, so the third promise receives the JSON directly:

```
.then((data) => {
  console.log('Request succeeded with JSON response', data)
})
```

and we simply log it to the console.

**Handling errors**

In the above example, in the previous section, we had a `catch` that was appended to the chain of promises.

When anything in the chain of promises fails and raises an error or rejects the promise, the control goes to the nearest `catch()` statement down the chain.

```
new Promise((resolve, reject) => {
  throw new Error('Error')
}).catch(err => {
  console.error(err)
})

// or

new Promise((resolve, reject) => {
  reject('Error')
}).catch(err => {
  console.error(err)
})
```

**Cascading errors**

If inside the `catch()` you raise an error, you can append a second `catch()` to handle it, and so on.

```
new Promise((resolve, reject) => {
  throw new Error('Error')
})
  .catch(err => {
    throw new Error('Error')
  })
  .catch(err => {
    console.error(err)
  })
```

**Orchestrating promises with `Promise.all()`**

If you need to synchronize different promises, `Promise.all()` helps you define a list of promises, and execute something when they are all resolved.

Example:

```
const f1 = fetch('/something.json')
const f2 = fetch('/something2.json')

Promise.all([f1, f2])
  .then(res => {
    console.log('Array of results', res)
  })
  .catch(err => {
    console.error(err)
  })
```

The ES2015 destructuring assignment syntax allows you to also do

```jsx
Promise.all([f1, f2]).then(([res1, res2]) => {
  console.log('Results', res1, res2)
})
```

You are not limited to using `fetch` of course, **any promise is good to go**.

**Orchestrating promises with `Promise.race()`**

`Promise.race()` runs as soon as one of the promises you pass to it resolves, and it runs the attached callback just once with the result of the first promise resolved.

Example:

```
const promiseOne = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one')
})
const promiseTwo = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two')
})

Promise.race([promiseOne, promiseTwo]).then(result => {
  console.log(result) // 'two'
})
```

### Async/Await <a href="#async-await" id="async-await"></a>

JavaScript evolved in a very short time from callbacks to promises (ES2015), and since ES2017 asynchronous JavaScript is even simpler with the async/await syntax.

Async functions are a combination of promises and generators, and basically, they are a higher level abstraction over promises. Let me repeat: **async/await is built on promises**.

**Why were async/await introduced?**

They reduce the boilerplate around promises, and the “don’t break the chain” limitation of chaining promises.

When Promises were introduced in ES2015, they were meant to solve a problem with asynchronous code, and they did, but over the 2 years that separated ES2015 and ES2017, it was clear that _promises could not be the final solution_.

Promises were introduced to solve the famous _callback hell_ problem, but they introduced complexity on their own, and syntax complexity.

They were good primitives around which a better syntax could be exposed to developers, so when the time was right we got **async functions**.

They make the code look like it’s synchronous, but it’s asynchronous and non-blocking behind the scenes.

**How it works**

An async function returns a promise, like in this example:

```jsx
const doSomethingAsync = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('I did something'), 3000)
  })
}
```

When you want to **call** this function you prepend `await`, and **the calling code will stop until the promise is resolved or rejected**. One caveat: the client function must be defined as `async`. Here's an example:

```
const doSomething = async () => {
  console.log(await doSomethingAsync())
}
```

**A quick example**

This is a simple example of async/await used to run a function asynchronously:

```
const doSomethingAsync = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('I did something'), 3000)
  })
}

const doSomething = async () => {
  console.log(await doSomethingAsync())
}

console.log('Before')
doSomething()
console.log('After')
```

The above code will print the following to the browser console:

```
Before
After
I did something //after 3s
```

**Promise all the things**

Prepending the `async` keyword to any function means that the function will return a promise.

Even if it’s not doing so explicitly, it will internally make it return a promise.

This is why this code is valid:

```
const aFunction = async () => {
  return 'test'
}

aFunction().then(alert) // This will alert 'test'
```

and it’s the same as:

```
const aFunction = async () => {
  return Promise.resolve('test')
}

aFunction().then(alert) // This will alert 'test'
```

**The code is much simpler to read**

As you can see in the example above, our code looks very simple. Compare it to code using plain promises, with chaining and callback functions.

And this is a very simple example, the major benefits will arise when the code is much more complex.

For example here’s how you would get a JSON resource, and parse it, using promises:

```
const getFirstUserData = () => {
  return fetch('/users.json') // get users list
    .then(response => response.json()) // parse JSON
    .then(users => users[0]) // pick first user
    .then(user => fetch(`/users/${user.name}`)) // get user data
    .then(userResponse => userResponse.json()) // parse JSON
}

getFirstUserData()
```

And here is the same functionality provided using await/async:

```
const getFirstUserData = async () => {
  const response = await fetch('/users.json') // get users list
  const users = await response.json() // parse JSON
  const user = users[0] // pick first user
  const userResponse = await fetch(`/users/${user.name}`) // get user data
  const userData = await userResponse.json() // parse JSON
  return userData
}

getFirstUserData()
```

**Multiple async functions in series**

Async functions can be chained very easily, and the syntax is much more readable than with plain promises:

```
const promiseToDoSomething = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('I did something'), 10000)
  })
}

const watchOverSomeoneDoingSomething = async () => {
  const something = await promiseToDoSomething()
  return something + ' and I watched'
}

const watchOverSomeoneWatchingSomeoneDoingSomething = async () => {
  const something = await watchOverSomeoneDoingSomething()
  return something + ' and I watched as well'
}

watchOverSomeoneWatchingSomeoneDoingSomething().then(res => {
  console.log(res)
})
```

Will print:

```
I did something and I watched and I watched as well
```

**Easier debugging**

Debugging promises is hard because the debugger will not step over asynchronous code.

Async/await makes this very easy because to the compiler it’s just like synchronous code.

### ES Modules <a href="#es-modules" id="es-modules"></a>

ES Modules is the ECMAScript standard for working with modules.

While Node.js has been using the CommonJS standard for years, the browser never had a module system, as every major decision such as a module system must be first standardized by ECMAScript and then implemented by the browser.

This standardization process completed with ES6 and browsers started implementing this standard trying to keep everything well aligned, working all in the same way, and now ES Modules are supported in Chrome, Safari, Edge and Firefox (since version 60).

Modules are very cool, because they let you encapsulate all sorts of functionality, and expose this functionality to other JavaScript files, as libraries.

**The ES Modules Syntax**

The syntax to import a module is:

```
import package from 'module-name'
```

while CommonJS uses

```
const package = require('module-name')
```

A module is a JavaScript file that **exports** one or more values (objects, functions or variables), using the `export` keyword. For example, this module exports a function that returns a string uppercase:

> _uppercase.js_

```
export default str => str.toUpperCase()
```

In this example, the module defines a single, **default export**, so it can be an anonymous function. Otherwise it would need a name to distinguish it from other exports.

Now, **any other JavaScript module** can import the functionality offered by uppercase.js by importing it.

An HTML page can add a module by using a `<scri`pt> tag with the sp`ecial type="m`odule" attribute:

```
<script type="module" src="index.js"><;/script>
```

> _Note: this module import behaves like a `defer` script load. See_ [_efficiently load JavaScript with defer and async_](https://flaviocopes.com/javascript-async-defer/)

It’s important to note that any script loaded with `type="module"` is loaded in [strict mode](https://flaviocopes.com/javascript-strict-mode/).

In this example, the `uppercase.js` module defines a **default export**, so when we import it, we can assign it a name we prefer:

```
import toUpperCase from './uppercase.js'
```

and we can use it:

```
toUpperCase('test') //'TEST'
```

You can also use an absolute path for the module import, to reference modules defined on another domain:

```
import toUpperCase from 'https://flavio-es-modules-example.glitch.me/uppercase.js'
```

This is also valid import syntax:

```
import { foo } from '/uppercase.js'import { foo } from '../uppercase.js'
```

This is not:

```
import { foo } from 'uppercase.js'
import { foo } from 'utils/uppercase.js'
```

It’s either absolute, or has a `./` or `/` before the name.

#### Other import/export options <a href="#other-import-export-options" id="other-import-export-options"></a>

We saw this example above:

```jsx
export default str => str.toUpperCase()
```

This creates one default export. In a file however you can export more than one thing, by using this syntax:

```
const a = 1
const b = 2
const c = 3

export { a, b, c }
```

Another module can import all those exports using

```jsx
import * from 'module'
```

You can import just a few of those exports, using the destructuring assignment:

```
import { a } from 'module'
import { a, b } from 'module'
```

You can rename any import, for convenience, using `as`:

```
import { a, b as two } from 'module'
```

You can import the default export, and any non-default export by name, like in this common React import:

```jsx
import React, { Component } from 'react'
```

You can see an ES Modules example here: [https://glitch.com/edit/#!/flavio-es-modules-example?path=index.html](https://glitch.com/edit/#!/flavio-es-modules-example?path=index.html)

### **CORS**

Modules are fetched using [CORS](https://flaviocopes.com/cors/). This means that if you reference scripts from other domains, they must have a valid CORS header that allows cross-site loading (like `Access-Control-Allow-Origin: *`)

**What about browsers that do not support modules?**

Use a combination of `type="module"` and `nomodule`:

```html
<script type="module" src="module.js"></script>
<script nomodule src="fallback.js"></script>
```

ES Modules are one of the biggest features introduced in modern browsers. They are part of ES6 but the road to implement them has been long.

We can now use them! But we must also remember that having more than a few modules is going to have a performance hit on our pages, as it’s one more step that the browser must perform at runtime.

Webpack is probably going to still be a huge player even if ES Modules land in the browser, but having such a feature directly built in the language is huge for a unification of how modules work client-side and on Node.js as well.

## The Virtual DOM <a href="#the-virtual-dom" id="the-virtual-dom"></a>

Many existing frameworks, before React came on the scene, were directly manipulating the DOM on every change.

It’s kept in the browser memory, and directly linked to what you see in a page. The DOM has an API that you can use to traverse it, access every single node, filter them, modify them.

The API is the familiar syntax you have likely seen many times, if you were not using the abstract API provided by jQuery and friends:

```
document.getElementById(id)
document.getElementsByTagName(name)
document.createElement(name)
parentNode.appendChild(node)
element.innerHTML
element.style.left
element.setAttribute()
element.getAttribute()
element.addEventListener()
window.content
window.onload
window.dump()
window.scrollTo()
```

React keeps a copy of the DOM representation, for what concerns the React rendering: the Virtual DOM

### **The Virtual DOM Explained**

Every time the DOM changes, the browser has to do two intensive operations: repaint (visual or content changes to an element that do not affect the layout and positioning relative to other elements) and reflow (recalculate the layout of a portion of the page — or the whole page layout).

React uses a Virtual DOM to help the browser use less resources when changes need to be done on a page.

When you call `setState()` on a Component, specifying a state different than the previous one, React marks that Component as **dirty**. This is key: React only updates when a Component changes the state explicitly.

What happens next is:

* React updates the Virtual DOM relative to the components marked as dirty (with some additional checks, like triggering `shouldComponentUpdate()`)
* Runs the diffing algorithm to reconcile the changes
* Updates the real DOM

### **Why is the Virtual DOM helpful: batching**

The key thing is that React batches much of the changes and performs a unique update to the real DOM, by changing all the elements that need to be changed at the same time, so the repaint and reflow the browser must perform to render the changes are executed just once.

### Unidirectional Data Flow <a href="#unidirectional-data-flow" id="unidirectional-data-flow"></a>

Working with React you might encounter the term Unidirectional Data Flow. What does it mean? Unidirectional Data Flow is not a concept unique to React, but as a JavaScript developer this might be the first time you hear it.

In general this concept means that data has one, and only one, way to be transferred to other parts of the application.

In React this means that:

* state is passed to the view and to child components
* actions are triggered by the view
* actions can update the state
* the state change is passed to the view and to child components

The view is a result of the application state. State can only change when actions happen. When actions happen, the state is updated.

Thanks to one-way bindings, data cannot flow in the opposite way (as would happen with two-way bindings, for example), and this has some key advantages:

* it’s less error prone, as you have more control over your data
* it’s easier to debug, as you know _what_ is coming from _where_
* it’s more efficient, as the library already knows what the boundaries are of each part of the system

A state is always owned by one Component. Any data that’s affected by this state can only affect Components below it: its children.

Changing state on a Component will never affect its parent, or its siblings, or any other Component in the application: just its children.

This is the reason that the state is often moved up in the Component tree, so that it can be shared between components that need to access it.

### Single Page Applications <a href="#single-page-applications" id="single-page-applications"></a>

React Applications are also called Single Page Applications. What does this mean?

In the past, when browsers were much less capable than today, and JavaScript performance was poor, every page was coming from a server. Every time you clicked something, a new request was made to the server and the browser subsequently loaded the new page.

Only very innovative products worked differently, and experimented with new approaches.

Today, popularized by modern frontend JavaScript frameworks like React, an app is usually built as a single page application: you only load the application code (HTML, [CSS](https://flaviocopes.com/css/), [JavaScript](https://flaviocopes.com/javascript/)) once, and when you interact with the application, what generally happens is that JavaScript intercepts the browser events and instead of making a new request to the server that then returns a new document, the client requests some JSON or performs an action on the server but the page that the user sees is never completely wiped away, and behaves more like a desktop application.

Single page applications are built in JavaScript (or at least compiled to JavaScript) and work in the browser.

The technology is always the same, but the philosophy and some key components of how the application works are different.

**Examples of Single Page Applications**

Some notable examples:

* Gmail
* Google Maps
* Facebook
* Twitter
* Google Drive

**Pros and cons of SPAs**

An SPA feels much faster to the user, because instead of waiting for the client-server communication to happen, and wait for the browser to re-render the page, you can now have instant feedback. This is the responsibility of the application maker, but you can have transitions and spinners and any kind of UX improvement that is certainly better than the traditional workflow.

In addition to making the experience faster to the user, the server will consume less resources because you can focus on providing an efficient API instead of building the layouts server-side.

This makes it ideal if you also build a mobile app on top of the API, as you can completely reuse your existing server-side code.

Single Page Applications are easy to transform into Progressive Web Apps, which in turn enables you to provide local caching and to support offline experiences for your services (or simply a better error message if your users need to be online).

SPAs are best used when there is no need for SEO (search engine optimization). For example for apps that work behind a login.

Search engines, while improving every day, still have trouble indexing sites built with an SPA approach rather than the traditional server-rendered pages. This is the case for blogs. If you are going to rely on search engines, don’t even bother with creating a single page application without having a server rendered part as well.

When coding an SPA, you are going to write a great deal of JavaScript. Since the app can be long-running, you are going to need to pay a lot more attention to possible memory leaks — if in the past your page had a lifespan that was counted in minutes, now an SPA might stay open for hours at a time and if there is any memory issue that’s going to increase the browser memory usage by a lot more and it’s going to cause an unpleasantly slow experience if you don’t take care of it.

SPAs are great when working in teams. Backend developers can just focus on the API, and frontend developers can focus on creating the best user experience, making use of the API built in the backend.

As a con, Single Page Apps rely heavily on JavaScript. This might make using an application running on low power devices a poor experience in terms of speed. Also, some of your visitors might just have JavaScript disabled, and you also need to consider accessibility for anything you build.

### **Overriding the navigation**

Since you get rid of the default browser navigation, URLs must be managed manually.

This part of an application is called the router. Some frameworks already take care of them for you (like Ember), others require libraries that will do this job (like [React Router](https://flaviocopes.com/react-router/)).

What’s the problem? In the beginning, this was an afterthought for developers building Single Page Applications. This caused the common “broken back button” issue: when navigating inside the application the URL didn’t change (since the browser default navigation was hijacked) and hitting the back button, a common operation that users do to go to the previous screen, might move to a website you visited a long time ago.

This problem can now be solved using the [History API](https://flaviocopes.com/history-api/) offered by browsers, but most of the time you’ll use a library that internally uses that API, like **React Router**.

### Declarative <a href="#declarative" id="declarative"></a>

What does it mean when you read that React is declarative? You’ll run across articles describing React as a **declarative approach to building UIs**.

React made its “declarative approach” quite popular and upfront so it permeated the frontend world along with React.

It’s really not a new concept, but React took building UIs a lot more declaratively than with HTML templates:

* you can build Web interfaces without even touching the DOM directly
* you can have an event system without having to interact with the actual DOM Events.

The opposite of declarative is **imperative**. A common example of an imperative approach is looking up elements in the DOM using jQuery or DOM events. You tell the browser exactly what to do, instead of telling it what you need.

The React declarative approach abstracts that for us. We just tell React we want a component to be rendered in a specific way, and we never have to interact with the DOM to reference it later.

### Immutability <a href="#immutability" id="immutability"></a>

One concept you will likely meet when programming in React is immutability (and its opposite, mutability).

It’s a controversial topic, but whatever you might think about the concept of immutability, React and most of its ecosystem kind of forces this, so you need to at least have a grasp of why it’s so important and the implications of it.

In programming, a variable is immutable when its value cannot change after it’s created.

You are already using immutable variables without knowing it when you manipulate a string. Strings are immutable by default, when you change them in reality you create a new string and assign it to the same variable name.

An immutable variable can never be changed. To update its value, you create a new variable.

The same applies to objects and arrays.

Instead of changing an array, to add a new item you create a new array by concatenating the old array, plus the new item.

An object is never updated, but copied before changing it.

This applies to React in many places.

For example, you should never mutate the `state` property of a component directly, but only through the `setState()` method.

In Redux, you never mutate the state directly, but only through reducers, which are functions.

The question is, why?

There are various reasons, the most important of which are:

* Mutations can be centralized, like in the case of Redux, which improves your debugging capabilities and reduces sources of errors.
* Code looks cleaner and simpler to understand. You never expect a function to change some value without you knowing, which gives you **predictability**. When a function does not mutate objects but just returns a new object, it’s called a pure function.
* The library can optimize the code because for example JavaScript is faster when swapping an old object reference for an entirely new object, rather than mutating an existing object. This gives you **performance**.

### Purity <a href="#purity" id="purity"></a>

In JavaScript, when a function does not mutate objects but just returns a new object, it’s called a pure function.

A function, or a method, in order to be called _pure_ should not cause side effects and should return the same output when called multiple times with the same input.

A pure function takes an input and returns an output without changing the input nor anything else.

Its output is only determined by the arguments. You could call this function 1M times, and given the same set of arguments, the output will always be the same.

React applies this concept to components. A React component is a pure component when its output is only dependant on its props.

All functional components are pure components:

```
const Button = props => {
  return <button>{props.message}</button>
}
```

Class components can be pure if their output only depends on the props:

```
class Button extends React.Component {
  render() {
    return <button>{this.props.message}</button>
  }
}
```


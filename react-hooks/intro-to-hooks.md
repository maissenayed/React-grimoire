# Intro to hooks

React Hooks fancy name for functions that allows you to hook into React state and lifecycle features in functional components. This was introduced with React 16.8 update and has become a must-needed part of any React application since then.

## What are React Hooks? <a href="#b5a7" id="b5a7"></a>

> _With the new addition of hooks( along with React 16.8), functional components could maintain states and lifecycle features without using classes. Simply hooks are features that allow you to “hook into” React state and lifecycle features from function components._

__

## Why We Need React Hooks? <a href="#c1d9" id="c1d9"></a>

Previously, If you write a function component and notice that you need to apply some state to it all you have to do is, change that functional component into a class.

> _But with the new update, you can just use a Hook inside the function component, making the refactoring procedure easy._

also, there are many advantages of using React hooks like:

* More flexibility in reusing an existing piece of code.
* There is no need to refactor the functional component into a class component when it grows complex.
* You don’t have to worry about this at all.
* No more bindings for methods
* It is simpler to distinguish logic and UI using hooks.

## React Hook Types <a href="#d8b1" id="d8b1"></a>

It is possible to divide the built-in hooks into two sections, which are given below. React offers a few built-in hooks, such as

### **Basic Hooks** <a href="#4a94" id="4a94"></a>

{% content-ref url="usestate.md" %}
[usestate.md](usestate.md)
{% endcontent-ref %}

{% content-ref url="useeffect.md" %}
[useeffect.md](useeffect.md)
{% endcontent-ref %}

{% content-ref url="usecontext.md" %}
[usecontext.md](usecontext.md)
{% endcontent-ref %}

### **Additional Hooks** <a href="#3843" id="3843"></a>

{% content-ref url="usereducer.md" %}
[usereducer.md](usereducer.md)
{% endcontent-ref %}

{% content-ref url="usememo.md" %}
[usememo.md](usememo.md)
{% endcontent-ref %}

{% content-ref url="usecallback.md" %}
[usecallback.md](usecallback.md)
{% endcontent-ref %}

{% content-ref url="useimperativehandle.md" %}
[useimperativehandle.md](useimperativehandle.md)
{% endcontent-ref %}

{% content-ref url="usedebugvalue.md" %}
[usedebugvalue.md](usedebugvalue.md)
{% endcontent-ref %}

{% content-ref url="useref.md" %}
[useref.md](useref.md)
{% endcontent-ref %}

{% content-ref url="uselayouteffect.md" %}
[uselayouteffect.md](uselayouteffect.md)
{% endcontent-ref %}

### Rules of Hooks <a href="#rules-of-hooks" id="rules-of-hooks"></a>

It ain’t Fight Club, but we do have some rules to follow:

1. Only call hooks at the top level of your function. Don’t put them in loops, conditionals, or nested functions. In order for React to keep track of your hooks, the same ones need to be called in the same order every single time.
2. Only call hooks from React function components, or from [custom hooks. ](custom-hooks.md)Don’t call them from outside a component (what would that even do?). Keeping all the calls inside components and custom hooks makes your code easier to follow too, because all the related logic is grouped together.
3. The names of hooks must start with “use”. Like `useState` or `useEffect` (well, not those two, those are taken).

The React team created some ESLint rules to catch problematic usage of hooks (install from [here](https://reactjs.org/docs/hooks-rules.html#eslint-plugin)), and the linter needs a way to identify “a hook.” Hence the naming prefix. Nothing magical going on there. The linter will be able to warn you if you violate rule 1 or 2, but only if you follow rule 3 ;)

{% embed url="https://reactjs.org/docs/hooks-rules.html" %}

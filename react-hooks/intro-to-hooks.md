# 🏁 Intro to hooks

React Hooks is a fancy name for functions that let you hook into React state and lifecycle features in functional components. This was introduced with the React 16.8 update and has since become an essential component of any React application.

## What are React Hooks? <a href="#b5a7" id="b5a7"></a>

> Hooks, which were introduced with React 16.8, allowed functional components to maintain states and lifecycle features without the use of classes. Simply put, hooks are features that allow function components to "hook into" React state and lifecycle features.

__

## Why We Need React Hooks? <a href="#c1d9" id="c1d9"></a>

Previously, if you wrote a function component and realized you needed to apply some state to it, all you had to do was convert it to a class.

> However, with the new update, you can simply use a Hook within the function component, making the refactoring process much easier.

also, there are many advantages of using React hooks like:

* Increased flexibility in reusing existing code.
* &#x20;When the functional component becomes complex, there is no need to refactor it into a class component.&#x20;
* You don't need to be concerned about this at all.
* &#x20;There will be no more method bindings.&#x20;
* Using hooks makes it easier to distinguish between logic and UI.

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

{% content-ref url="custom-hooks/usedebugvalue.md" %}
[usedebugvalue.md](custom-hooks/usedebugvalue.md)
{% endcontent-ref %}

{% content-ref url="useref.md" %}
[useref.md](useref.md)
{% endcontent-ref %}

{% content-ref url="uselayouteffect.md" %}
[uselayouteffect.md](uselayouteffect.md)
{% endcontent-ref %}

### Rules of Hooks <a href="#rules-of-hooks" id="rules-of-hooks"></a>

It ain’t Fight Club, but we do have some rules to follow:

1. Hooks should only be called at the top level of your function. They should not be used in loops, conditionals, or nested functions.
2. Hooks should only be called from React function components or custom hooks. Don't call them from outside of a component (what good would that do?). Keeping all calls within components and custom hooks also makes your code easier to follow because all related logic is grouped together.
3. Hook names must begin with "use." similar to `useState` or `useEffect` (well, not those two, those are taken).

![](<../.gitbook/assets/Hook rule.png>)

{% hint style="info" %}
**The React team created some ESLint rules to catch problematic usage of hooks (install from** [**here**](https://reactjs.org/docs/hooks-rules.html#eslint-plugin)**), and the linter needs a way to identify “a hook.” Hence the naming prefix. Nothing magical going on there. The linter will be able to warn you if you violate rule 1 or 2, but only if you follow rule**&#x20;
{% endhint %}

{% embed url="https://reactjs.org/docs/hooks-rules.html" %}

{% embed url="https://www.youtube.com/watch?v=b0IZo2Aho9Y" %}

## References and articles :

{% embed url="https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e" %}

{% embed url="https://blog.logrocket.com/react-hooks-frustrations" %}

{% embed url="https://www.youtube.com/watch?v=TNhaISOUy6Q" %}

{% embed url="https://www.youtube.com/watch?v=dpw9EHDh2bM" %}

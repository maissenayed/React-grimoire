# 🏁 React hooks guidelines

> Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

{% hint style="info" %}
**Before react 16.8, it was already possible to reuse some stateful logic across your app with higher-order components and render props but Custom Hooks let you do it without adding more components to your tree.**
{% endhint %}

Hooks are a way to reuse _stateful logic_, not state itself. In fact, each _call_ to a Hook has a completely isolated state — so you can even use the same custom Hook twice in one component.

Custom Hooks are more of a convention than a feature. If a function’s name starts with ”`use`” and it calls other Hooks, we say it is a custom Hook. The `useSomething` naming convention is how the linter plugin is able to find bugs in the code using Hooks.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven’t considered.

## When should I create a new custom hook?

When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!

Hooks core motivations :

* It’s hard to reuse stateful logic between components
* Complex components become hard to understand
* Classes confuse both people and machines

With this in mind, you can create new custom hooks when :

* There is similar stateful logic across components
* You want to write specific stateful logic without rendering anything.
* You want to extract logic from your component body to make it easier to read/understand/maintain, or you want to separate render and logic concerns.

Hooks can be shared easily between pages, components, and hooks! So, when creating a new custom hook, consider whether there is any shareable logic that can be isolated in the `hooks/` folder.

Otherwise, you have the choice between letting your custom hook's code in the same file as your page or creating a new file aside your component's file.

Please remember **that every file need to be tested**.

You can found some example on

{% embed url="https://reactjs.org/docs/hooks-custom.html" %}

## Document your custom hooks! <a href="#document-your-custom-hooks" id="document-your-custom-hooks"></a>

As with most things in a large organization, the more custom hooks your team creates, the easier it is to lose track of them.

It's a good idea to keep track of every hook you make. If not for the sake of your team, then for the sake of yourself in the future. Make sure people are aware of your hook's existence, what it does, and what your intentions were, whether it's a **README** in each hook's folder or a doc in a wiki.

A note like "This was a massive hack where we only covered case X due to this buggy API we use" is far more valuable than nothing.

Adding [JSDOC](https://jsdoc.app/about-getting-started.html) comments above your hooks is also useful&#x20;

{% embed url="https://devhints.io/jsdoc" %}

```jsx
/**  * This is a JSDOC comment. 
     * VS Code's tooltip will show extra information because of me. 
     */
const useMyCustomHook = (props) => { };
```

Don't make the mistake of assuming that your code is self-documenting or simple to understand. Because it's still fresh in your mind, you're probably thinking your code is simple.

## Testing custom hooks <a href="#testing-custom-hooks" id="testing-custom-hooks"></a>

Thanks to React Testing Library's [react-hooks-testing-library](https://github.com/testing-library/react-hooks-testing-library), it's never been easier to test hooks in isolation.

Here's an example from their docs. Given a hook extracted as `useCounter`:

```jsx
import { useState, useCallback } from 'react';

function useCounter() {  
  const [count, setCount] = useState(0);
  const increment = useCallback(() => setCount((x) => x + 1), []);
  
  return { count, increment };
  }
  
export default useCounter;
```

Your tests would look like this:

```jsx

import { renderHook, act } from '@testing-library/react-hooks';
import useCounter from './useCounter';

test('should increment counter', () => {  
  const { result } = renderHook(() => useCounter());
  
  act(() => {    result.current.increment();  });
  expect(result.current.count).toBe(1);
  
  });
```

## References and articles :

{% embed url="https://reactjs.org/docs/hooks-rules.html" %}

{% embed url="https://www.smashingmagazine.com/2020/04/react-hooks-best-practices" %}

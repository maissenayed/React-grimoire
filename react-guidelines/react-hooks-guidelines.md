# React hooks guidelines

> Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

If you're not familiar with the concept of react hooks, please read this before going any further.

{% embed url="https://reactjs.org/docs/hooks-intro.html" %}

&#x20;Before react 16.8, it was already possible to reuse some stateful logic across your app with higher-order components and render props but Custom Hooks let you do it without adding more components to your tree.

Hooks are a way to reuse _stateful logic_, not state itself. In fact, each _call_ to a Hook has a completely isolated state — so you can even use the same custom Hook twice in one component.

Custom Hooks are more of a convention than a feature. If a function’s name starts with ”`use`” and it calls other Hooks, we say it is a custom Hook. The `useSomething` naming convention is how the linter plugin is able to find bugs in the code using Hooks.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven’t considered.

#### When should I create a new custom hook?

When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!

Hooks core motivations :

* It’s hard to reuse stateful logic between components
* Complex components become hard to understand
* Classes confuse both people and machines

With this in mind, you can create new custom hooks when :

1. there is similar stateful logic across components
2. you want to write specific stateful logic but you don't want to render anything
3. you want to extract logic from your component body because it could make it easier to read/understand/maintain or if you want to separate concerns between render and logic.

Hooks can be easily shared between pages, components, and hooks too! So when you're designing a new custom hook, take some time to identify if there's some shareable logic that can be isolated in the `hooks/` folder.

Otherwise, you have the choice between letting your custom hook's code in the same file as your page or creating a new file aside your component's file.

Please remember **that every file need to be tested**.

You can found some example on

{% embed url="https://reactjs.org/docs/hooks-custom.html" %}

{% embed url="https://reactjs.org/docs/hooks-rules.html" %}

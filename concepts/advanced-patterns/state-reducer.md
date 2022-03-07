# ⚠ State Reducer

The state reducer pattern gives even more control to the consumer than the render props patterns. Whereas the render props pattern allows consumers to be in control over the UI based on state, the state reducer pattern allows the consumer to add logic to state changes themselves, while also rendering any content they would like.

You may wonder why use render props at all if state reducer can do everything render props can do and more but I would argue that you don’t always want to use state reducer and render props just because you can. If you don’t need to make your component super reusable then don’t do it. These patterns are great but making your components reusable comes at a cost. They will make your components more complex than they need to be, its often better to make your components simple first, and then refactor into these patterns as needed.



In this example, we used the State reducer pattern and the Custom hook pattern together, but you can also use it with the Compound components pattern to pass the reducer directly to the main component Counter .

## Advantages

Granting more control: Even in the most complex cases, using state reducers is the best way to hand over control to the user. All internal component operations are now externally accessible and can be overridden.

&#x20;

![](https://blog.kakaocdn.net/dn/cdhpp5/btrh93G47Eu/Mk2tSYN6Jaw1gBgcwHuL11/img.png)

&#x20;

## Disadvantages

· Implementation complexity: This pattern is certainly the most difficult implementation for both component developers and users.

· Lack of visibility: The behavior of reducers can change, requiring a deep understanding of the component's internal logic.

## Libraries using this pattern&#x20;

{% embed url="https://github.com/downshift-js/downshift#statereducer" %}

## &#x20;References and articles :

{% embed url="https://kentcdodds.com/blog/the-state-reducer-pattern-with-react-hooks" %}

{% embed url="https://kentcdodds.com/blog/the-state-reducer-pattern" %}

{% embed url="https://engineering.dollarshaveclub.com/reacts-state-reducer-pattern-f66e82a82697" %}

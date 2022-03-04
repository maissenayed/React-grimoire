# ⚠ State Reducer

### State reducer pattern

This is the most advanced pattern in terms of reversal of control. This gives the user an advanced way to change the behavior inside the component.\
The code is similar to the Custom Hook pattern, but defines a reducer that the user passes to the hook . This reducer overloads the internal behavior of the component.

&#x20;

#### ㅣ Example

**· Github:**[**https://github.com/alex83130/advanced-react-patterns/tree/main/src/patterns/state-reducer**](https://github.com/alex83130/advanced-react-patterns/tree/main/src/patterns/state-reducer)

In this example, we used the State reducer pattern and the Custom hook pattern together, but you can also use it with the Compound components pattern to pass the reducer directly to the main component Counter .

&#x20;

#### ㅣ Advantages

**· Granting more control: Even in the most complex cases, using state reducers is the best way to hand over control to the user. All internal component operations are now externally accessible and can be overridden.**

&#x20;

![it outsourcing wish](https://blog.kakaocdn.net/dn/cdhpp5/btrh93G47Eu/Mk2tSYN6Jaw1gBgcwHuL11/img.png)

&#x20;

#### ㅣ Disadvantages

**· Implementation complexity: This pattern is certainly the most difficult implementation for both component developers and users.**

**· Lack of visibility: The behavior of reducers can change, requiring a deep understanding of the component's internal logic.**

&#x20;

#### ㅣ Evaluation items

**· Reversal of Control: 4/4**

**· Implementation Complexity: 4/4**

&#x20;

#### ㅣ Libraries that use this pattern

&#x20;  ·  [Downshift](https://github.com/downshift-js/downshift#statereducer)

&#x20;

{% embed url="https://kentcdodds.com/blog/the-state-reducer-pattern-with-react-hooks" %}

{% embed url="https://kentcdodds.com/blog/the-state-reducer-pattern" %}

{% embed url="https://engineering.dollarshaveclub.com/reacts-state-reducer-pattern-f66e82a82697" %}

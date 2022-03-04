# ⚠ Props Getters Pattern

### Props Getters Pattern

While this pattern gives you a lot of control, it's harder to integrate your components. Users have to deal with the many props of native hooks themselves and rewrite the logic themselves. The Props Getters pattern hides this complexity by providing a list of props getters instead of exposing the default props. A getter is a function that returns a bunch of props, and gives it a meaningful name so that users can easily connect to the correct JSX element.

&#x20;

#### ㅣ Example

&#x20;

**· Github:**[**https://github.com/alex83130/advanced-react-patterns/tree/main/src/patterns/props-getters**](https://github.com/alex83130/advanced-react-patterns/tree/main/src/patterns/props-getters)

#### ㅣ Advantages

**· Easy to use: Provides an easy way to integrate components and hides complexity. Users just need to connect the correct getter to the correct JSX element.**

&#x20;

![it outsourcing wish](https://blog.kakaocdn.net/dn/bsVSTY/btrijq7Vi0k/K9bWazPtinptyPf3FBKxbk/img.png)

&#x20;

**· Flexibility: Users can override the props contained in the getter if needed for a specific use case.**

![it outsourcing wish](https://blog.kakaocdn.net/dn/drl3Wn/btricDBqcaf/0EmCMRsaRFRmKGgnrI2G5k/img.png)

&#x20;

#### ㅣ Disadvantages

**· Lack of visibility: The abstraction provided by getters makes it easier to implement components, but can feel like a "magic box" with no visible insides. To redefine a component correctly, the user needs to know what the list of props exposed by the getter is and how changing one of them will affect the internal logic.**

&#x20;

#### ㅣ Evaluation items

**· Reversal of Control: 3/4**

**· Implementation Complexity: 3/4**

&#x20;

#### ㅣ Libraries that use this pattern

&#x20; · [React table](https://react-table.tanstack.com/docs/examples/basic)

&#x20; · [Downshift](https://github.com/downshift-js/downshift#usage)

{% embed url="https://kentcdodds.com/blog/how-to-give-rendering-control-to-users-with-prop-getters" %}

{% embed url="https://www.middle-engine.com/blog/posts/2021/12/20/performance-issues-with-the-prop-getters-pattern-in-react" %}

# ⚠ Custom hook pattern

### &#x20;Custom Hook Pattern

Let's take a closer look at "reversal of control" here. Now the main logic is a user custom Hookis forwarded to These hooks are user-accessible and allow easier control of the component by exposing several internal logic ( States , Hnadlers ) .

&#x20;

#### ㅣ Example

Github: [https://github.com/alex83130/advanced-react-patterns/tree/main/src/patterns/custom-hooks](https://github.com/alex83130/advanced-react-patterns/tree/main/src/patterns/custom-hooks)

#### ㅣ Advantages

· More Control: Users can change the behavior of the main component by inserting their own logic between hooks and JSX components.

&#x20;

![wishette](https://blog.kakaocdn.net/dn/bIx0uy/btrh9RSWNVh/y3eFHfdUAKbbqZB7cO5Ul1/img.jpg)

#### ㅣ Disadvantages

· Implementation complexity: the logic is decoupled from the rendering and it is up to you to connect the two. To properly implement a component, you need a deep understanding of how the component works.

&#x20;

![wishette](https://blog.kakaocdn.net/dn/Opk2U/btrh5ZdmQfg/kXcePR9sx9HgPFpkSBMf0K/img.jpg)

#### ㅣ Evaluation items

&#x20; · Reversal of control: 2/4

&#x20; · Implementation complexity: 2/4

&#x20;

#### ㅣ Libraries that use this pattern

&#x20; · [React table](https://react-table.tanstack.com/docs/examples/basic)

&#x20; · [React hook form](https://react-hook-form.com/api)

{% embed url="https://blog.bitsrc.io/new-react-design-pattern-return-component-from-hooks-79215c3eac00" %}

{% embed url="https://blog.logrocket.com/advanced-react-hooks-creating-custom-reusable-hooks" %}

{% embed url="https://blog.logrocket.com/react-render-props-vs-custom-hooks" %}

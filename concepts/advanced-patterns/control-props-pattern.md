# ⚠ Control Props Pattern

### Control Props Pattern

This pattern transforms a component into a Controlled Component . External state serves as a "single source of truth" that allows users to insert custom logic to change the default behavior of a component.

#### Advantages

**· Giving more control: Because the main state is exposed outside the component, the user has direct control over that component.**

&#x20;

![wishette](https://blog.kakaocdn.net/dn/dvk8p6/btrh9RZNfGO/kAO6ZnaPjLLpYN3tW7pgnk/img.jpg)

#### ㅣ Disadvantages

**· Implementation complexity: Component behavior was previously possible by implementing it in one place ( JSX ) , but now requires implementation in 3 different places ( JSX / useState / handleChange ) .**

&#x20;

![wishette](https://blog.kakaocdn.net/dn/lhbCB/btrh6I9WZWJ/vOkKD52QozvoMdwNeCD7t1/img.jpg)

####

&#x20;

#### ㅣ Libraries that use this pattern

&#x20;  · [Material UI](https://material-ui.com/components/rating/#rating)

&#x20;

\


{% embed url="https://dev.to/robogeek95/react-controlled-props-pattern-3ej1" %}

{% embed url="https://kentcdodds.com/blog/control-props-vs-state-reducers" %}

{% embed url="https://itnext.io/controlled-and-uncontrolled-component-design-pattern-in-react-21e8d40e46e" %}

{% embed url="https://antongunnarsson.com/render-props" %}

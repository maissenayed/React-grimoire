# ProtoTypes

Every React app will be composed of an hierarchical tree of components that have different props, certainly then we will need to define and structure our props , to avoid bugs and errors .

Just as a function may have required arguments, a React component may require a prop to be defined in order to render properly. If you fail to pass a required prop into a component that requires it, your app may behave unexpectedly.

Lets take the example below

```jsx
import  * as React from "react";
import ReactDOM from "react-dom";

const Alert =(props) => {
const {title,importantMessage,riskNumber,total=Math.max(1, score)} =props
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <span>{ Math.round(score / total * 100) }%</span>
    </div>
  );
}
const rootElement = document.getElementById("root");
ReactDOM.render(
    <Alert title="danger zone" importantMessage="This is very dangerous" riskNumber={70}/>
  rootElement
);

```

This alert component requires four props for proper rendering: `title`,`importantMessage` ,`riskNumber`, and `total`. Default values are set for `total` prop in case they are not provided.

Based on what we see we can conclude that `title` and `importantMessage` props are expected to be a `string`. In the same vein, `riskNumber` and `total` are required to be `numeric` values because they are used for computing `percent`. Also, `total` is expected to never be `0` since it is being used as a divisor.

But what if we define the props with wrong types like this

```jsx
import  * as React from "react";
import ReactDOM from "react-dom";

const Alert =(props) => {
const {title,importantMessage,riskNumber,total=Math.max(1, score)} =props
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <span>{ Math.round(score / total * 100) }%</span>
    </div>
  );
}
const rootElement = document.getElementById("root");
ReactDOM.render(
<>   
 <Alert title="Error zone" importantMessage="This is very dangerous" riskNumber={func=>func} total={0}/>
 <Alert title="Error zone" importantMessage="This is very dangerous" riskNumber={70} total="0"/>
</>,
  rootElement
);
```

The app will render with invalid props, try to imagine this problem in a big complex app , that's why we needed to find a solution to define props type and keep the sanity of the developers

## Protypes

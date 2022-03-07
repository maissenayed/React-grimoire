# 🏁 PropTypes

Every React app will be composed of an hierarchical tree of components that have different props, certainly then we will need to define and structure our props , to avoid bugs and errors .

Just as a function may have required arguments, a React component may require a prop to be defined in order to render properly. If you fail to pass a required prop into a component that requires it, your app may behave unexpectedly.

Lets take the example below

```jsx
import  * as React from "react";
import ReactDOM from "react-dom";

const Alert =(props) => {
const {title,importantMessage,riskNumber,total=Math.max(1, riskNumber)} =props
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <span>{ Math.round(riskNumber / total * 100) }%</span>
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
const {title,importantMessage,riskNumber,total=Math.max(1, riskNumber)} =props
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <span>{ Math.round(riskNumber / total * 100) }%</span>
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

## Proptypes

PropTypes is React’s internal mechanism for adding type checking to components.

React components use a special property named `propTypes` to set up type checking.

```jsx
/**
 * FORFUNCTIONAL COMPONENTS
 */
function ReactComponent(props) {
  // ...implement render logic here
}

ReactComponent.propTypes = {
  // ...prop type definitions here
}


/**
 * CLASS COMPONENTS: METHOD 1
 */
class ReactComponent extends React.Component {
  // ...component class body here
}

ReactComponent.propTypes = {
  // ...prop type definitions here
}


/**
 * CLASS COMPONENTS: METHOD 2
 * Using the `static` class properties syntax
 */
class ReactComponent extends React.Component {
  // ...component class body here
  
  static propTypes = {
    // ...prop type definitions here
  }
}
```

When props are passed to a React component, they are checked against the type definitions configured in the `propTypes` property. When an invalid value is passed for a prop, a warning is displayed on the JavaScript console.

So how can i create a prototype validation for  Alert component props .let's take a look at the code below :

```jsx
const Alert = (props) => {
  const {
    title,
    importantMessage,
    riskNumber,
    total = Math.max(1, riskNumber)
  } = props;
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <span>{Math.round((riskNumber / total) * 100)}%</span>
    </div>
  );
};

Alert.propTypes = {
  title(props, propName, componentName) {
    const type = typeof props[propName];
    if (type !== "string") {
      return new Error(
        `Prop ${propName} on the component ${componentName} must be of type string`
      );
    }
  }
};

```

**`Alert.propTypes`** it's an object that react reference when it render a component with props and pass each one of them to a validation function that we provide

Her we have validated the title prop to be always of type string

```jsx
Alert.propTypes = {
  title(props, propName, componentName) {
    const type = typeof props[propName];
    if (type !== "string") {
      return new Error(
        `Prop ${propName} on the component ${componentName} must be of type string`
      );
    }
  }
};
```

![](<../.gitbook/assets/Screenshot from 2022-02-08 21-32-09.png>)

And here you go a custom error for in our console to alert us of prop validation problems

we can even push it forward by creating an object that define generic validation like defining a generic error for every prop that need to be string or number:

```jsx
const prototypes = {
  string(props, propName, componentName) {
    const type = typeof props[propName];
    if (type !== "string") {
      return new Error(
        `Prop ${propName} on the component ${componentName} must be of type string`
      );
    }
  },
  number(props, propName, componentName) {
    const type = typeof props[propName];
    console.log(type);
    if (type !== "number") {
      return new Error(
        `Prop ${propName} on the component ${componentName} must be of type number`
      );
    }
  }
};
const Alert = (props) => {
  const {
    title,
    importantMessage,
    riskNumber,
    total = Math.max(1, riskNumber)
  } = props;
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <>{Math.round((riskNumber / total) * 100)}%</>
    </div>
  );
};
Alert.propTypes = {
  title: prototypes.string,
  importantMessage: prototypes.string,
  riskNumber: prototypes.number,
  total: prototypes.number
};
```

{% hint style="danger" %}
**Proptypes doesn't chip with production build  for performance issues , as it's a tool for developer to maintain and structure the code , it's not necessarily to have it on production either way**&#x20;
{% endhint %}

## &#x20;Prop-types package

{% embed url="https://www.npmjs.com/package/prop-types" %}

It will always be nicer if we had pre built validators for our props , as it will be a little bit tedious to define prop types over and over again, and here come prop-type package

{% hint style="info" %}
**Prior to React 15.5.0, a utility named `PropTypes` was available as part of the React package, which provided a lot of validators for configuring type definitions for component props. It could be accessed with `React.PropTypes`.**
{% endhint %}

However, in later versions of React, this utility has been moved to a separate package named [`prop-types`](https://www.npmjs.com/package/prop-types), so you need to add it as a dependency for your project in order to get access to the `PropTypes` utility.

{% code title="" %}
```jsx
npm install prop-types --save
yarn add prop-types 
```
{% endcode %}

It can be imported into your project files as follows:

```jsx
import PropTypes from 'prop-types';
```

To learn more about how you can use `prop-types`, how it differs from using `React.PropTypes`, and all the available validators, see the [official `prop-types` documentation](https://github.com/facebook/prop-types/blob/master/README.md).

```jsx
import PropTypes from 'prop-types';
const Alert = (props) => {
  const {
    title,
    importantMessage,
    riskNumber,
    total = Math.max(1, riskNumber)
  } = props;
  return (
    <div className="alert">
      <h1>{title}</h1>
      <h2>{importantMessage}</h2>
      <>{Math.round((riskNumber / total) * 100)}%</>
    </div>
  );
};

Alert.propTypes = {
  title: propTypes.string,
  importantMessage: propTypes.string,
  riskNumber: propTypes.number,
  total: propTypes.number
};
```

### React PropTypes validators <a href="#reactproptypesvalidators" id="reactproptypesvalidators"></a>

The PropTypes utility exports a wide range of validators for configuring type definitions. Below we’ll list the available validators for basic, renderable, instance, multiple, collection, and required prop types.

#### Basic types

Below are the validators for the basic data types.

* `PropTypes.any`: The prop can be of any data type
* `PropTypes.bool`: The prop should be a Boolean
* `PropTypes.number`: The prop should be a number
* `PropTypes.string`: The prop should be a string
* `PropTypes.func`: The prop should be a function
* `PropTypes.array`: The prop should be an array
* `PropTypes.object`: The prop should be an object
* `PropTypes.symbol`: The prop should be a symbol

```
Component.propTypes = {
  anyProp: PropTypes.any,
  booleanProp: PropTypes.bool,
  numberProp: PropTypes.number,
  stringProp: PropTypes.string,
  functionProp: PropTypes.func
}
```

#### Renderable types

`PropTypes` also exports the following validators for ensuring that the value passed to a prop can be rendered by React.

* `PropTypes.node`: The prop should be anything that can be rendered by React — a number, string, element, or array (or fragment) containing these types
* `PropTypes.element`: The prop should be a React element

```
Component.propTypes = {
  nodeProp: PropTypes.node,
  elementProp: PropTypes.element
}
```

One common usage of the `PropTypes.element` validator is in ensuring that a component has a single child. If the component has no children or multiple children, a warning is displayed on the JavaScript console.

```
Component.propTypes = {
  children: PropTypes.element.isRequired
}
```

#### Instance types

In cases where you require a prop to be an instance of a particular JavaScript class, you can use the `PropTypes.instanceOf` validator. This leverages the underlying JavaScript `instanceof` operator.

```
Component.propTypes = {
  personProp: PropTypes.instanceOf(Person)
}
```

#### Multiple types

`PropTypes` also exports validators that can allow a limited set of values or multiple sets of data types for a prop. Here they are:

* `PropTypes.oneOf`: The prop is limited to a specified set of values, treating it like an enum
* `PropTypes.oneOfType`: The prop should be one of a specified set of types, behaving like a union of types

```
Component.propTypes = {

  enumProp: PropTypes.oneOf([true, false, 0, 'Unknown']),
  
  unionProp: PropTypes.oneOfType([
    PropType.bool,
    PropType.number,
    PropType.string,
    PropType.instanceOf(Person)
  ])
  
}
```

#### Collection types

Besides the`PropTypes.array` and `PropTypes.object` validators, `PropTypes` also provides validators for more fine-tuned validation of arrays and objects.

**`PropTypes.arrayOf`**

`PropTypes.arrayOf` ensures that the prop is an array in which all items match the specified type.

```
Component.propTypes = {

  peopleArrayProp: PropTypes.arrayOf(
    PropTypes.instanceOf(Person)
  ),
  
  multipleArrayProp: PropTypes.arrayOf(
    PropTypes.oneOfType([
      PropType.number,
      PropType.string
    ])
  )
  
}
```

**`PropTypes.objectOf`**

`PropTypes.objectOf` ensures that the prop is an object in which all property values match the specified type.

```
Component.propTypes = {

  booleanObjectProp: PropTypes.objectOf(
    PropTypes.bool
  ),
  
  multipleObjectProp: PropTypes.objectOf(
    PropTypes.oneOfType([
      PropType.func,
      PropType.number,
      PropType.string,
      PropType.instanceOf(Person)
    ])
  )
  
}
```

**`PropTypes.shape`**

You can use `PropTypes.shape` when a more detailed validation of an object prop is required. It ensures that the prop is an object that contains a set of specified keys with values of the specified types.

```
Component.propTypes = {
  profileProp: PropTypes.shape({
    id: PropTypes.number,
    fullname: PropTypes.string,
    gender: PropTypes.oneOf(['M', 'F']),
    birthdate: PropTypes.instanceOf(Date),
    isAuthor: PropTypes.bool
  })
}
```

**`PropTypes.exact`**

For strict (or exact) object matching, you can use `PropTypes.exact` as follows:

```
Component.propTypes = {
  subjectScoreProp: PropTypes.exact({
    subject: PropTypes.oneOf(['Maths', 'Arts', 'Science']),
    score: PropTypes.number
  })
}
```

#### Required types

The `PropTypes` validators we’ve explored so far all allow the prop to be optional. However, you can chain `isRequired` to any prop validator to ensure that a warning is shown whenever the prop is not provided.

```
Component.propTypes = {

  requiredAnyProp: PropTypes.any.isRequired,
  requiredFunctionProp: PropTypes.func.isRequired,
  requiredSingleElementProp: PropTypes.element.isRequired,
  requiredPersonProp: PropTypes.instanceOf(Person).isRequired,
  requiredEnumProp: PropTypes.oneOf(['Read', 'Write']).isRequired,
  
  requiredShapeObjectProp: PropTypes.shape({
    title: PropTypes.string.isRequired,
    date: PropTypes.instanceOf(Date).isRequired,
    isRecent: PropTypes.bool
  }).isRequired
  
}
```

### Custom validators for type-checking React props <a href="#customvalidatorsfortypecheckingreactprops" id="customvalidatorsfortypecheckingreactprops"></a>

Usually, you need to define some custom validation logic for component props — e.g., ensuring that a prop is passed a valid email address. `prop-types` allows you to define custom validation functions that can be used for type checking props.

#### Basic custom validators

The custom validation function takes three arguments:

1. `props`, an object containing all the props passed to the component
2. `propName`, the name of the prop to be validated
3. `componentName`, the name of the component

If the validation fails, it should return an `Error` object. The error should not be thrown. Also, `console.warn` should not be used inside the custom validation function.

```
const isEmail = function(props, propName, componentName) {
  const regex = /^((([^<>()[]\.,;:s@"]+(.[^<>()[]\.,;:s@"]+)*)|(".+"))@(([[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}])|(([a-zA-Z-0-9]+.)+[a-zA-Z]{2,})))?$/;
  
  if (!regex.test(props[propName])) {
    return new Error(`Invalid prop `${propName}` passed to `${componentName}`. Expected a valid email address.`);
  }
}

Component.propTypes = {
  email: isEmail,
  fullname: PropTypes.string,
  date: PropTypes.instanceOf(Date)
}
```



Custom validation functions can also be used with `PropTypes.oneOfType`. Here is a simple example using the `isEmail` custom validation function in the previous code snippet:

```
Component.propTypes = {
  email: PropTypes.oneOfType([
    isEmail,
    PropTypes.shape({
      address: isEmail
    })
  ])
}
```

`Component` will be valid in both of these scenarios:

```
<Component email="glad@me.com" />
<Component email={{ address: 'glad@me.com' }} />
```

#### Custom validators and collections

Custom validation functions can also be used with `PropTypes.arrayOf` and `PropTypes.objectOf`. When used this way, the custom validation function are called for each key in the array or object.

However, the custom validation function takes five arguments instead of three:

1. `propValue`, the array or object itself
2. `key`, the key of the current item in the iteration
3. `componentName`, the name of the component
4. `location`, the location of the validated data (usually `“prop”`)
5. `propFullName`, the fully resolved name of the current item being validated. For an array, this will be `array[index]`; for an object, it will be `object.key`

Below is a modified version of the `isEmail` custom validation function for use with collection types.

```
const isEmail = function(propValue, key, componentName, location, propFullName) {
  const regex = /^((([^<>()[]\.,;:s@"]+(.[^<>()[]\.,;:s@"]+)*)|(".+"))@(([[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}])|(([a-zA-Z-0-9]+.)+[a-zA-Z]{2,})))?$/;
  
  if (!regex.test(propValue[key])) {
    return new Error(`Invalid prop `${propFullName}` passed to `${componentName}`. Expected a valid email address.`);
  }
}

Component.propTypes = {
  emails: PropTypes.arrayOf(isEmail)
}
```

#### All-purpose custom validators

Taking all we’ve learned about custom validation functions into account, let’s go ahead and create all-purpose custom validators that can be used as standalone validators and also with collection types.

A slight modification to the `isEmail` custom validation function will make it an all-purpose validator, as shown below.

```
const isEmail = function(propValue, key, componentName, location, propFullName) {
  // Get the resolved prop name based on the validator usage
  const prop = (location && propFullName) ? propFullName : key;
  
  const regex = /^((([^<>()[]\.,;:s@"]+(.[^<>()[]\.,;:s@"]+)*)|(".+"))@(([[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}])|(([a-zA-Z-0-9]+.)+[a-zA-Z]{2,})))?$/;
  
  if (!regex.test(propValue[key])) {
    return new Error(`Invalid prop `${prop}` passed to `${componentName}`. Expected a valid email address.`);
  }
}

Component.propTypes = {
  email: PropTypes.oneOfType([
    isEmail,
    PropTypes.shape({
      address: isEmail
    })
  ]),
  emails: PropTypes.arrayOf(isEmail)
}
```

{% embed url="https://reactjs.org/docs/typechecking-with-proptypes.html" %}

{% hint style="info" %}
**I intensively use Typescript for all what concerns Types and types checking , and with that and i don't ever use proptypes in my projects , but it's always good to have such an amazing features on your grasp**  &#x20;
{% endhint %}

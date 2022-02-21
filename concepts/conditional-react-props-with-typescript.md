---
description: a prop which should only be set when another prop has a specific value.
---

# 🆗 Conditional React props with TypeScript

Relationships between React component props can make you feel the pinch. This article will be your road-map to conditional props pattern employed using Typescript. I will propose different situations and demonstrate the answers to these questions:&#x20;

How can we create a dependent relationship between several props using TypeScript?

What can we do to have it generate TypeScript errors when a relationship is broken?

## Conflicting properties

Working on a design system, I had to create an avatar component. To pass props to the avatar component, different conditions were present:

* If i pass the `icon` prop i can't pass the `src` prop
* If i pass the `src` prop i can't pass the `icon` prop

Here an example for the simple avatar component without the conditions

```tsx
type AvatarProps = {
  icon?: JSX.Element;
  src?: string;
  children:React.ReactNode;
};

export const Avatar = (props: AvatarProps): JSX.Element => {
  const { icon, src } = props;
  return (
    <div>
      {icon && icon}
      {JSON.stringify(src)}
      {children}
    </div>
  );
};
```

&#x20;If we import the component while passing both props, the component will not raise any errors.

Therefore, we have to provide an indication for the developer to tell them that passing the two in the same time is forbidden by just throwing a typescript error.

To achieve that , we can create [union type ](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)using two types that reflect the two scenarios our component supports:

```tsx
interface CommonProps {
  children?: React.ReactNode

  // ...other props that always exist
}

type ConditionalProps =
  | {
      icon?: JSX.Element;
      src?: never;
    }
  | {
      icon?: never;
      src?: string;
    };
    
type Props = CommonProps & ConditionalProps  

export const Avatar = (props: Props): JSX.Element => {
  const { icon, src } = props;
  return (
    <div>
      {icon && icon}
      {JSON.stringify(src)}
      {children}
    </div>
  );
};
```

For those of you who are already familiar with TypeScript, that should be sufficient information

However, in just a few lines of code, there is a lot going on. Let's break it down into chunks if you're wondering about what it all means and how it all works.

```typescript
interface CommonProps {
  children: React.ReactNode

  // ...other props that always exist
}
```

`CommonProps` is your typical props definition in TypeScript. It’s for all of the “Common” props that figure in all scenarios and that aren’t dependent on other props. In addition to `children,` there might be `shadow`, `size`, `shape`, etc.

```typescript
type ConditionalProps =
// If i pass the icon prop i can't pass the src prop
  | {
      icon?: JSX.Element;
      src?: never;
    }
// If i pass the src prop i can't pass the icon prop
  | {
      src?: string;
      icon?: never;
    };
```

_`ConditionalProps`_ is where the magic happens. It’s what’s called a ”[discriminated union](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions).”  It’s  union of object definitions.&#x20;

Let’s break it down further and we’ll come back to see how the discriminated union works for us.

```tsx
{
 icon?: JSX.Element;
 src?: never;
} 
```

The first part of the discriminated union is when the `icon` prop is defined, In this case, we want the `src` prop to be invalid. It shouldn’t be able to be set.&#x20;

```tsx
{   
 icon?: never;
 src?: string;
};
```

The second part is when the `icon` prop is unspecified (`undefined`). Then we can pass the src props with no problems

```typescript
type ConditionalProps =
  | {
      icon?: JSX.Element;
      src?: never;
    }
  | {
      icon?: never;
      src?: string;
    };
```

So now back to the entire [discriminated union](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions). It’s saying that the configuration for the `icon` and `src` props can either be the first case or the second case.&#x20;

{% hint style="info" %}
It's worth noting that we've used the keyword [never ](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-never-type) in this example. The best explanation of this keyword can be found in the TypeScript documentation:

> “TypeScript will use a never type to represent a state which shouldn’t exist.”

To reiterate, we defined two types for two scenarios and combined them using the union operator.
{% endhint %}

```typescript
type Props = CommonProps & ConditionalProps  
```

`Props` becomes the [intersection](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html#intersection-types) of `CommonProps` and `ConditionalProps`.&#x20;

`Props` is the combination of the two types. So it’ll have all the properties from `CommonProps` as well as this dependent relationship we created with `ConditionalProps`.

Now finally, in the `Avatar` component, both the `icon` and `src` props will be of there type respectively `JSX.Element | undefined` and  `string | undefined` So their types come out straightforward as if you hadn’t created the dependent relationship.

Now if we try to provide both props, we will see a TypeScript error:

![](<../.gitbook/assets/Screenshot from 2021-11-15 21-37-00.png>)

## Conditional prop variation

I needed to create a component with different variants, for each variant we have a set of props .

We want those props to be provided only when a matching variant is selected.

in our case we have 3 variants `"text" | "number" | "element"`

* If the we chose to set the `variant` to `text` , we need to have a `message` prop of type `string`, and we can't set `componentName` prop
* If the we chose to set the `variant` to `number` , we need to have a `message` props of type `number`, and we can't set `componentName` prop
* If we do pass the `variant` as `element` , here we can use finally `componentName` also the  `message` prop will become of type `JSX.Element`

Lets take a look at this example&#x20;

```tsx
interface CommonProps {
  children?: React.ReactNode;
  // ...other props that always exist
}
type ConditionalProps =
  | {
      componentName?: string;
      message?: JSX.Element;
      variant?: "element";
    }
  | {
      componentName?: never;
      message?: string;
      variant?: "text";
    }
  | {
      componentName?: never;
      message?: number;
      variant?: "number";
    };

type Props = CommonProps & ConditionalProps;

export const VariantComponent = (props: Props): JSX.Element => {
  const { message, componentName, variant = "element", children } = props;
  return (
    <div>
      {message && message}
      {variant === "element" && componentName}
      {children}
    </div>
  );
};

```

```tsx
/* 
 * If the we chose to set the variant to text,
 * we need to have a message props of type string,
 * We can't set componentName prop
 */

{
 componentName?: never;
 message?: string;
 variant?: "text";
}
```

```tsx
/*
 * If the we chose to set the variant to number,
 * we need to have a message props of type number,
 * and we can't set componentName prop
 */
{
 componentName?: never;
 message?: number;
 variant?: "number";
}
```

```tsx
/*
 * If we do pass the variant as element, 
 * here we can use finally componentName
 * also the message prop will become of type JSX.Element
 */
{
 componentName: string;
 message?: JSX.Element;
 variant?: "element";
}
```

Once we set the `variant` prop , TypeScript narrows down component’s type to their respective desired properties and tells you what you need to provide

## Conditional props for collection with generic type <a href="#conditional-props-for-collection-items" id="conditional-props-for-collection-items"></a>

For our next use case, let’s try defining conditional props for a Select component. Our component needs to be flexible enough to accept an array of strings or objects for its `options` property.

If the component receives an array of objects, we want the developer to specify which fields of those objects we should use as a label and value.\


### Conditional types for collection property

```tsx
type SelectProps<T> =
  | {
      options: Array<string>;
      labelProp?: never;
      valueProp?: never;
    }
  | {
      options: Array<T>;
      labelProp: keyof T;
      valueProp: keyof T;
    };

export const Select = <T extends unknown>(props: SelectProps<T>) => {
  return <div>{JSON.stringify(props)}</div>;
};

```

To match the object that the user provide to the select. we can use [generics ](https://www.typescriptlang.org/docs/handbook/2/generics.html)in TypeScript.

```tsx
{
 options: Array<T>;
 labelProp: keyof T;
 valueProp: keyof T;
}
```

In our second type, we change the `options` prop from `Array<Object>` to `Array<T>` for our generic object. The client has to provide an array of items of the generic object type.

We're using the  [keyof ](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html)keyword to tell TypeScript that we're expecting `labelProp` and `valueProp` to be generic object fields.

Now when you try to provide `valueProp` or `labelProp`, you’ll see a nice autocomplete suggestion based on the fields of the options items.

However, there is a minor change that we must make in order to avoid certain issues. We want to make sure that the generic object we've been given is a custom object rather than a primitive, such as a string:

```tsx
type SelectProps<T> = T extends string
  ? {
      options: Array<string>;
      labelProp?: never;
      valueProp?: never;
    }
  : {
      options: Array<T>;
      labelProp: keyof T;
      valueProp: keyof T;
    };

export const Select = <T extends unknown>(props: SelectProps<T>) => {
  return <div>{JSON.stringify(props)}</div>;
};
```

Here we changed the union type by ternary operator to check if our generic type is a string, and based on that, we set our component’s type to the appropriate option.\


### &#x20;                Here’s a link to the [code sandbox ](https://codesandbox.io/s/conditional-react-props-with-typescript-7fje4?file=/src/components/VariantComponent.tsx)for this tutorial.

# ⚠ React Components Composition Guidelines

> One of the many great parts of React is how it makes you think about apps as you build them.

This document is made to explain how you should extract and define your components at a structural level when you're starting a new development or a refactor.

We highly recommend you to go to :

{% embed url="https://reactjs.org/docs/components-and-props.html" %}

{% embed url="https://reactjs.org/docs/composition-vs-inheritance.html" %}

Component composition is the fundamental concept in React that’s essential to learn to become a solid React developer. Newer React devs tend to use inheritance and Context to solve problems that could often be solved more elegantly using composition.

Let’s review the basic principles behind composition in React and brush up on our fundamentals.

### Overview of Component composition <a href="#overview-of-component-composition" id="overview-of-component-composition"></a>

Simply put, component composition means building more complex components on top of simpler ones. There are two ways to go about it:

* Specialized components
* Container components

Let’s cover these two approaches in more detail.

## Specialized component <a href="#specialized-component" id="specialized-component"></a>

Specialized components are more opinionated versions of generic components. In other words, specialized components are usually non-reusable versions of the generic components that we tailored for a specific use case.

We create specialized components by rendering generic ones and configuring the props to match our specific use case.

Let’s see an example where we create our newsletter sign-up form using a generic form component.\
We will start with the generic form:

![](../.gitbook/assets/text.png)

`Form` is a generic component used to build different forms throughout your app. It’s versatile and lets you configure the inputs for your form, the header, and the submit button.

Now, we will create the specialized `NewsletterForm` component on top of our `Form`:

![](../.gitbook/assets/fsdfdfff.png)

identifying patterns that you use a lot throughout your app and turning them into generic reusable components is an important skill to develop.

Once you have a solid set of generic components, it’s much easier and faster to create specialized ones on top of them. That’s why it’s always a good idea to include a UI component library in your new project.

## Container component <a href="#container-component" id="container-component"></a>

The container component provides certain functionality without knowing its children ahead of time. This kind of component usually has a `children` prop that lets you pass any arbitrary content. Good examples of container components are sidebars or dialogs.

The container component is a flexible and versatile pattern. An example I often use in my applications is the gate component that checks the user’s authentication status before rendering its children.&#x20;

Now, let’s see this pattern in action and create a simple version of the gating component:

![](../.gitbook/assets/gate.png)

### Container with multiple child props <a href="#container-with-multiple-child-props" id="container-with-multiple-child-props"></a>

In some cases, you might need container components with multiple places to inject your custom content.

One example could be a hypothetical `Dashboard` component that accepts header and content components.

![](../.gitbook/assets/dash.png)

When you need to build a container with multiple “holes,” you can break away from the pattern of using the `children` prop and add custom props for your injected content.

### Why composition is important <a href="#why-composition-is-important" id="why-composition-is-important"></a>

By now, you should see that component composition is extremely useful when working with React. Still, let’s list the main advantages of using component composition:

* When building your components on top of the generic ones, you have fewer components that feel like a black box. That, in turn, will improve the transparency in your code and will make it more readable.
* Using intelligent component composition, you can often avoid prop drilling without Context or Redux. More often than not, when you think you need Context to pass props, you need to rethink your component composition.
* Over time, you will build a component toolbox that will increase the velocity of your development. Creating new components will become much faster.

## Tips and tricks

Always Start by highlighting and identify the composition of the top-level App component and the composition of global layers like pages, global layers ( such as Headers, Sidebars, Layouts, Footer ), etc…

#### Shared components definition roadmap (no code involved)

1. Given your base material ( mockups/wireframes or existing ) begin page by page, examine all the elements, look at the current data the page is requesting, list every data involved. To correctly implement user actions, separate concerns, and simplify the development process, you also need to list all the current user actions on the page. Then extract the "final components" identified ( root react component without wrappers/providers ).

Reusable components are often agnostic. They don’t know what they render, neither hold any specific logic, they just render.

If you’re having a hard time figuring out what elements you should create components, you can start to imagine what are states you need to create and how they’ll flow with data through your UI ([https://reactjs.org/docs/thinking-in-react.html](https://reactjs.org/docs/thinking-in-react.html) ). if you need, consider using a scoped [react context](https://reactjs.org/docs/context.html) too.



* Alongside the previous point, for each underlying component extracted, if some wrappers are business logic components, associate the logic attached by simply writing what this logic is supposed to accomplish. This includes smart components with logic.
* If you see that some non-business logic used in multiple places, think about creating **custom hooks** ( please read the [**react hooks guidelines**](broken-reference) ) at page-level or shared for the app. If you think that some of the business logic of your page could be or should be isolated in a custom hook, please discuss this subject with your colleague to define if it's a good idea or not               ( maybe you should consider moving this logic in an API / library / micro-front / ... instead )&#x20;
* &#x20;Process and standardize the props. Inspect the similar components by summarizing the common props, list them and try to create a uniform experience across every component. ( ex: if you have two components that take a string and displays it as a title one props is name `title` and the other `headerText` consider using only one of them across both components )

```tsx
// from
<Dialog title="some text" />
<Card headerText="some text" />

// to 
<Dialog title="some text" />
<Card title="some text" />

```

#### References and articles :

{% embed url="https://overreacted.io/writing-resilient-components" %}

{% embed url="https://dlinau.wordpress.com/2016/02/22/how-to-name-props-for-react-components" %}

{% embed url="https://airbnb.io/javascript/react" %}

{% embed url="https://react.statuscode.com" %}

{% embed url="https://formidable.com/blog/2021/react-composition" %}

{% embed url="https://codeburst.io/a-complete-guide-to-props-children-in-react-c315fab74e7c" %}

{% embed url="https://javascript.plainenglish.io/a-complete-guide-of-the-composition-process-of-a-react-native-app-dd9f89542c46" %}

{% embed url="https://www.codeinwp.com/blog/react-best-practices" %}

{% embed url="https://github.com/mediamonks" %}

{% embed url="https://dmitripavlutin.com/7-architectural-attributes-of-a-reliable-react-component" %}

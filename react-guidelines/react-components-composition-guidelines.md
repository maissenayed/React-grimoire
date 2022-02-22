# React Components Composition Guidelines

> One of the many great parts of React is how it makes you think about apps as you build them.

This document is made to explain how you should extract and define your components at a structural level when you're starting a new development or a refactor.

We highly recommend you to go to :

{% embed url="https://reactjs.org/docs/components-and-props.html" %}

and check out the [#references](https://www.notion.so/React-Components-Composition-Guidelines-19b9f598f8ab46f89cbc2f7203988e1f) section before going any further.

Start by highlighting and identify the composition of the top-level App component and the composition of global layers like pages, global layers ( such as Headers, Sidebars, Layouts, Footer ), etc…

If you want, you can create a list to sort your new components by types or folders they'll go in as you read through this document.&#x20;

#### Shared components definition roadmap (no code involved)

1. Given your base material ( mockups/wireframes or existing ) begin page by page, examine all the elements, look at the current data the page is requesting, list every data involved. To correctly implement user actions, separate concerns, and simplify the development process, you also need to list all the current user actions on the page. Then extract the "final components" identified ( root react component without wrappers/providers ).

Reusable components are often agnostic. They don’t know what they render, neither hold any specific logic, they just render.

If at the root of the wrappers of one component, there is an underlying TextComponent, the TextComponent is the component to extract.

If you’re having a hard time figuring out what elements you should create components, you can start to imagine what are states you need to create and how they’ll flow with data through your UI ([https://reactjs.org/docs/thinking-in-react.html](https://reactjs.org/docs/thinking-in-react.html) ). if you need, consider using a scoped [react context](https://reactjs.org/docs/context.html) too.

If you feel like you need to create components for some composition in your most complex pages, you're free to define them **in the same file** as long as it serves **only for composition** and the logic cannot be shared between other components. Otherwise, it should be added to the `components/` or `hoc/` folders.&#x20;

( "what's composition?" : [https://reactjs.org/docs/composition-vs-inheritance.html](https://reactjs.org/docs/composition-vs-inheritance.html) )

* Alongside the previous point, for each underlying component extracted, if some wrappers are business logic components, associate the logic attached by simply writing what this logic is supposed to accomplish. This includes smart components with logic.
* If you see that some non-business logic used in multiple places, think about creating **custom hooks** ( please read the [**react hooks guidelines**](broken-reference) ) at page-level or shared for the app. If you think that some of the business logic of your page could be or should be isolated in a custom hook, please discuss this subject with your colleague to define if it's a good idea or not               ( maybe you should consider moving this logic in an API / library / micro-front / ... instead )&#x20;
* &#x20;Group them by type and role and try to figure out where you should create new folder/files ( please refer to [Folders Structure](https://www.notion.so/Folders-Structure-bf195400819c440890717755d0169404) )&#x20;
* &#x20;Process and standardize the props. Inspect the similar components by summarizing the common props, list them and try to create a uniform experience across every component. ( ex: if you have two components that take a string and displays it as a title one props is name `title` and the other `headerText` consider using only one of them across both components )



```tsx
// from
<Dialog title="some text" />
<Card headerText="some text" />

// to 
<Dialog title="some text" />
<Card title="some text" />



```

Take a look at the existing shared components API to be sure to match the project props naming conventions.

If you need to add some new props, please discuss them with other colleagues and respect some props naming conventions :

* always use camelCase
* for booleans :
* use prefix is, can, has
* try to do positive props ( `isFoo` instead of `isFoo={false}` ) to allow implicit use ( [jsx-boolean-value](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md) )
* respect eslint and typescript rules

#### What you should do next :

Once all the possibly sharable components of the page are standardized :

1. define the specific APIs of the unique components of the page
2. Separate data calls ( queries / mutations / ... ) from components as much as possible. All the operations of the page will be defined in corresponding files or hooks. ( it will also help you if you want to mock the data during development )
3. create components with tests
4. implement them in your page with logic and style
5. handle loading/error states
6. finish and adjust styles

The state management needs to be reduced to simple components, context, and hooks. This will allow us to test our files very easily and independently.

#### Testing :

Every development needs to be tested before merging to the main branch.

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

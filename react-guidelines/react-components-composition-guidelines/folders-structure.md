# Folders Structure

Useful links :

In our desire to simplify yet give flexibility to our development environment, a simple and efficient folder structure is difficult to agree with when going deep in the details and each one's perception of "efficient".

Nonetheless, usually we do agree on simple things, as they're most likely able to keep everyone on the same page.

Finally, simple does not mean painful. No matter the form, the substance should be somewhat logical and easily understandable to any developer.

NextJS adds it's own .next folder and other files along, but they're out of the scope of this guide. We focus on the structure of what developers create in the folder.

Following these principles, here is what our NextJS apps look like :

```jsx
app/
|-components/
| |--Component/
|    |--index.ts
|    |--Component.tsx
|    |--Component.spec.tsx
|-hooks/
| |--useCustomSharedHook/
|    |--useCustomSharedHook.ts
|    |--useCustomSharedHook.spec.ts
| |--...
|-pages/
| |--index.tsx
| |--some-page/
|    |--index.ts
|    |--SomePage.tsx
|    |--SomePage.spec.tsx
|    |--[id]/
|       |--index.ts
|       |--SomeNestedPage.spec.tsx
|       |--SomeNestedPage.tsx
|-providers/
| |--SomeProvider/
|    |--index.ts
|    |--SomeProvider.tsx
|    |--SomeProvider.spec.tsx
|-public/
| |--images/
|    |--some-image.jpg
| |--...
|-utils/
| |--someUtil
|    |--index.ts
|    |--someUtil.ts
|    |--someUtil.spec.ts
|-types/
| |--foo.d.ts
| |--bar.ts
|-global.css
```

Let's dig in.

**components**

All the components that are **not** providers or **page** components, used across the app go here. The root folder has an index where all components are exported. Each main component has its own folder, and is exported via the `index.ts` file inside. The component's actual code is written in the `Component.tsx` file. This file export **one and only one** React component. **All other components in the same folder, have to be descendants of the main component and have their own unit test file.**

Note : **It is very important to choose carefully the composition of a component.** When composing a component, we tend to over-split and create a terrible React tree. It's far more efficient to simply write JSX around a reusable component than creating new components over and over, just for the sake of being React. This assumption is false. The React way among other things, is to split UI components into logical and reusable pieces.

**sub-components, related only to their main component live close to it.** We do not recreate a component folder dedicated for them.

If you find yourself creating multiple sub-components with no business logic, that are simply wrappers around even smaller sub-components, because you want "minimal jsx with html elements", or for more "clarity", you're probably doing something wrong and these component should be refactored and composed into a smarter component.

**hooks**

This folder contains all custom hooks shared across the entire app. Any hook sharable across multiple front end apps should be placed in the `aos-client-lib` library instead.

**Every custom hooks in this folder are tested**. A hook used only by a specific component is placed **inside this component and is not to be tested.** It's an **implementation detail** and is covered by the component's unit test. All hooks must follow the [React hooks rules](https://reactjs.org/docs/hooks-rules.html)

A custom hook used only by another specific one, **has to be written** inside the main hook and is **not to be tested**.

**pages**

Any component considered a page live here in its own folder, with the associated test file and an index file exporting it. Page components follow the same rules as the regular components when it comes to sub-components and colocation. The `index.tsx` file is the `/` route of the app. Any component rendered in this file will be considered to be the landing page. The name of the folder is mapped by NextJS to create the url file. This way the url is web standard compliant.

**You cannot import any page in any other component or page.**

The `_app.tsx` is explained [here](https://nextjs.org/docs/advanced-features/custom-app).

**providers**

Every provider component is located here in its own folder. A provider is a React component that returns a Provider component produced by a `React.createContext` , or a React component that returns an augmented Provider or a Every custom Provider must export its own dispatch function, or any update function along with the Provider component. More on this pattern [here](https://kentcdodds.com/blog/how-to-use-react-context-effectively) and [here](https://kentcdodds.com/blog/application-state-management-with-react)

If you need to export a hook outside the Provider module, put it at the same level with a meaningful name. An extracted hook must be unit tested.

**public**

All static assets go in this folder. Create a specific folder for a group of assets, e.g `images/` contains all image type assets.

**styles**

Except for exceptional circumstances, we should only see one or very few css files here. One is mandatory and is the `global.css` file, used by the `_app.tsx` file when there is one (which should be always the case. More on this file [here](https://nextjs.org/docs/advanced-features/custom-app)

If for some critical reason, the styling of a component require custom file css, create a `Component.module.css` next to the component and import it only in this module. More [here](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css)

This css file must have in its name, the name of the component(case-sensitive)

**utils**

Every utility function is declared in its own file here. We use camel case for utils naming. Each utils has its own test file located at the same level. Utils follow the same rules as hooks for when it comes to testing. If a util is only useful in one specific module, it should be implemented inside that module.

**types**

This folder contains app relatives typescript interfaces and types declarations that cannot be exported into packages or anywhere else. It should not be used every time you create a new type, but only when you feel it's necessary. ( instead, you create a `types.ts` file where you need it ). Example :

* a file `segment.d.ts` that declares the global variable `analytics` because you can access it everywhere.

And that's it !

A word on services. In the previous architecture, some services and interfaces (which are simply sub-systems of a service) were directly integrated inside the app folder. This doesn't make much sense in a distributed and component architecture. A service possess business rules, business code and perform operation related to its business. For instance, a package which only goal is to import a spreadsheet from user desktop to the browser, has nothing to do with the app itself. The service can be used by any other front app, and if it is tied to that specific container, then it's nothing more than a utility, since it's sole goal is to help the view layer behave as expected.

Another benefit of separating concerns, is that a dedicated squad can be responsible of working specifically on curated libraries commonly consumed by containers apps, without even knowing anything of the consumers. This splits responsibility among squads of developers and result in a non-blocking release process, and incremental adoption.

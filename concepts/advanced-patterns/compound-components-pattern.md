# ⚠ Compound Components Pattern

## Compound Components Pattern <a href="#6eaa" id="6eaa"></a>

This pattern allows creating expressive and declarative components, without unnecessary [pr](https://kentcdodds.com/blog/prop-drilling)

[ op drilling](https://kentcdodds.com/blog/prop-drilling). You should consider using this pattern if you want to make your **** component more customizable, with a better separation of concern and an understandable API.

## What is the Compound Component pattern? <a href="#what-is-the-compound-component-pattern" id="what-is-the-compound-component-pattern"></a>

As mentioned before, the Compound components pattern allows writing a declarative and flexible API for complex components. You build the component using multiple loosely coupled child components. Each of them performs a different task, yet they all share the same implicit state. When put together, these child components make up our compound component.

You have, no doubt, encountered compound components before when working with a UI library. Take a look at this snippet:

```jsx
export default function App() {
  return (
    <div className="App">
      <Menu>
        <Item id="1">
          <AccordionHeader>Header 1</AccordionHeader>
          <AccordionPanel>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua.
          </AccordionPanel>
        </AccordionItem>
        <AccordionItem id="2">
          <AccordionHeader>Header 2</AccordionHeader>
          <AccordionPanel>
            Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris
            nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in
            reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
            pariatur.
          </AccordionPanel>
        </AccordionItem>
        <AccordionItem id="3">
          <AccordionHeader>Header 3</AccordionHeader>
          <AccordionPanel>
            Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
            officia deserunt mollit anim id est laborum.
          </AccordionPanel>
        </AccordionItem>
      </Accordion>
    </div>
  );
}
```

Does the structure look familiar? That’s what the API typically looks like for compound components.

Here’s the structure of the Accordion component at a high level:

![](https://isamatov.com/images/compound-components-react/accordion-diagram.png)

As a side note, a lot of UI libraries like ant D use `.` for their compound component API like so:

```jsx
<Dropdown text="File">
    <Dropdown.Menu>
      <Dropdown.Item text="New" />
      <Dropdown.Item text="Open..."  />
      <Dropdown.Item text="Save as..."  />
    </Dropdown.Menu>
</Dropdown>
```

This approach is strictly optional and you can write your component however you prefer. It doesn’t affect the end result in any significant way.

### Why use the Compound Component pattern? <a href="#why-use-the-compound-component-pattern" id="why-use-the-compound-component-pattern"></a>

let's imagine that we were going to implement a custom select. A naive implementation would look something like this:

```
<CustomSelect
  options={[
    {value: '1', display: 'Option 1'},
    {value: '2', display: 'Option 2'},
  ]}
/>
```

This works fine, but it's less extensible/flexible than a compound components API. For example. What if I want to supply additional attributes on the `<option>` that's rendered, or I want the `display` to change based on whether it's selected? We can easily add API surface area to support these use cases, but that's just more for us to code and more for users to learn. That's where compound components come in really handy!\


To reiterate, the main advantage of building complex components this way is how easy it is to use them. Thanks to the implicit state, the inner workings of the compound component are hidden from the clients. At the same time, the clients get the flexibility to rearrange and customize the child components in any way they please.

Notice how we declaratively listed the content of the Accordion yet didn’t have to meddle with its inner state.

`Menu` will handle all of the inner state logic, including shrinking and expanding items on click. All we had to do is list the items in the order we want.

So let’s go over the advantages of using the Compound Component pattern one last time:

1. The API for your component is declarative.
2. Your child components are loosely coupled. That makes it easy to reorder, add and remove the child component without affecting its siblings.
3. Much easier to style and change the design of the component.

Now that you’re hopefully convinced to give this thing a shot, let’s start with the tutorial. We will build the `Menu` we’ve been talking about this whole time.

Example

```jsx
import styled from "@emotion/styled";
import {
  Children,
  cloneElement,
  Context,
  createContext,
  ReactNode,
  useContext,
  useMemo,
  useState
} from "react";

const AccordionContext: Context<{
  openItem: string;
  setOpenItem: any;
}> = createContext({
  openItem: "",
  setOpenItem: null
});
const AccordionContainer = styled.div`
  border: 1px solid #d3d3d3;
  border-radius: 8px;
  padding: 8px;
`;

function Accordion({ children }: { children: ReactNode }) {
  const [openItem, setOpenItem] = useState("");

  const value = useMemo(() => ({ openItem, setOpenItem }), [openItem]);

  return (
    <AccordionContainer>
      <AccordionContext.Provider value={value}>
        {children}
      </AccordionContext.Provider>
    </AccordionContainer>
  );
}
```

e create `MenuContext` and use `MenuContext.Provider` to pass `openItem` and `setOpenItem` props. Also note how we wrapped `value` with [useMemo](https://reactjs.org/docs/hooks-reference.html#usememo) to prevent redundant re-renders.

#### MenuItem <a href="#accordionitem-1" id="accordionitem-1"></a>

Here’s the code for `MenuItem`:

```jsx
export const AccordionItem = ({
  children,
  id
}: {
  children: ReactNode;
  id: string;
}) => {
  return (
    <div>
      {Children.map(children, (child: any) => cloneElement(child, { id }))}
    </div>
  );
};
```

Notice how we no longer need to pass the props received from the Accordion. But we’re still using `cloneElement` here to pass the `id` prop.

#### MenuPanel & MenuHeader <a href="#accordionpanel--accordionheader" id="accordionpanel--accordionheader"></a>

These child elements now pull the shared state directly from the context using the `useContext` hook. Here’s the implementation of both of them:

```jsx
onst useAccordionContext = () => useContext(AccordionContext);

const AccordionHeaderContainer = styled.div`
  padding: 8px 16px;
  background: #f5f5f5;
  border-top: 1px solid #d3d3d3;
  cursor: pointer;
`;

const AccordionPanelContainer = styled.div<{ height: string; padding: string }>`
  padding: ${({ padding }: { padding: string }) => padding};
  height: ${({ height }: { height: string }) => height};
  overflow: hidden;
  border-bottom: 1px solid #d3d3d3;
`;

export const AccordionHeader = ({
  id,
  children
}: {
  id?: string;
  children: ReactNode;
}) => {
  const { setOpenItem } = useAccordionContext();
  return (
    <AccordionHeaderContainer onClick={() => setOpenItem(id)}>
      {children}
    </AccordionHeaderContainer>
  );
};

export const AccordionPanel = ({
  children,
  id
}: {
  children: ReactNode;
  id?: string;
}) => {
  const { openItem } = useAccordionContext();
  return (
    <AccordionPanelContainer
      padding={openItem === id ? "16px" : "0px"}
      height={openItem === id ? "fit-content" : "2px"}
    >
      {children}
    </AccordionPanelContainer>
  );
};
```

Overall, this implementation has less code and better performance. That’s because `cloneElement` causes a slight performance penalty.

However, the main advantage is that we have a much more flexible API for our Accordion, and the example code that broke earlier now works just fine.

## Counter example

#### l Advantages

**· Reduced API complexity: Instead of putting all props in one huge parent component and descending into sub UI components, each prop is tied to the most appropriate SubComponent.**

![](https://blog.kakaocdn.net/dn/yf23A/btriac3DGbW/K3mrlDDkP4fx0dlAToJhA1/img.jpg)

**· Flexible markup structure: The component's UI has great flexibility and can create multiple cases from one component. For example, the user can change the order of SubComponents or decide which of them should be displayed.**

![](https://blog.kakaocdn.net/dn/8ZzdS/btrh4NYxSeo/tVje3ivYkfDqGi2oCDkcdk/img.jpg)

**· Separation of concerns: Most of the logic is contained in the main Counter component, and React.Context is used to share the states and handlers of all child components . This allows for a clear separation of responsibilities.**

![](https://blog.kakaocdn.net/dn/dGLSX7/btriac3DKnt/gjeFYUUFMUCEcZZUp2KlT1/img.jpg)

#### ㅣ Disadvantages

**· Too much flexibility in the UI: More flexibility means it's more likely to cause unexpected behavior. For example, there may be unneeded child components, the child components may be out of order, and the necessary child components may not exist.**\
**Depending on how you want your users to use your component, you may want to limit your flexibility to some extent.**

&#x20;

![](https://blog.kakaocdn.net/dn/r59h6/btribAQterl/b96c4sa5jUwYsjusvqEz51/img.jpg)

**· JSX too heavy: Applying this pattern JSXThe number of lines increases, especially if you are using a linter like EsLint or a code formatter like Prettier . It's not a big deal at the single-component level, but the difference becomes more apparent as you scale up.**\


&#x20;

![](https://blog.kakaocdn.net/dn/b5O5mN/btriaVAxR9y/TR7AH27P5cr511615WWgkk/img.jpg)

#### ㅣ Evaluation items

**· Reversal of Control: 1/4**

**· Implementation Complexity: 1/4**

&#x20;

#### ㅣ Libraries that use this pattern

·  React Bootstrap

· Reach UI

&#x20;

{% embed url="https://antongunnarsson.com/compound-components-in-react" %}

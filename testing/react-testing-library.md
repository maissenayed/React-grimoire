---
cover: ../.gitbook/assets/testinglibrary-image.jpeg
coverY: 49.48680351906158
---

# React Testing Library

Do you feel compelled to manually test your React frontend after each deploy, because it’s not tested as well as your backend? Or perhaps you already have frontend tests, but you feel that they only serve as a hindrance, slowing down your development speed? Perhaps it’s time to give frontend testing another go, with the React Testing Library!

The React Testing Library (_RTL_) lets you test your React components in their natural habitat, that is, in the DOM. The goal is to test your components in a way that most closely resembles how the user will interact with them. That means fully rendered components in a browser-like environment, and assertions that test the contents of the document. As the library’s author, Kent C. Dodds, puts it:

> The more your tests resemble the way your software is used, the more confidence they can give you.

### Great, show me a minimal example

Let’s start off simple. Here’s a Jest test that uses RTL to assert that a `CustomButton` component is rendered with the correct label as defined by its label prop.

```jsx
import { render, screen } from "@testing-library/react";

const CustomButton = ({ label }) => {
  return <button>{label}</button>;
}

test("can render CustomButton", () => {
  const buttonLabel = "Submit";
  render(<CustomButton label={buttonLabel} />);
  expect(screen.getByText(buttonLabel)).toBeInTheDocument();
});
```

Fairly straight forward, huh? Let’s break it down a bit anyway. RTL provides a `render` function that lets us, well, render our component. Specifically, it renders it into the document body that the tests operate on. The second import, `screen`, then lets us query the contents of the document, here by searching for any element with the given text. Lastly, we _expect_ such an element _to be in the document_. The latter is an argument matcher from `@testing-library/jest-dom` which gives us declarative assertions. The test is dead simple and only tests what the user cares about: how the component appears on the screen.

### Avoid testing implementation details

RTL tries to encourage writing tests that do not depend on how the components work internally. One example we’ve seen already is the way we query the document for an element  — by its text content. The tests should approach the component like the end user would; they should only care that the button be present and that it have the correct label. The alternative of querying an element by its CSS selector (a widespread approach) is thus discouraged.

One reason you may have felt that frontend tests hinder you in the past could be due to what Dodds refers to as the _test user_. The essence is that your components normally have two users: the end user and the developer. For each user, you have to maintain the interface through which they access the component. The end user cares about the UX interface on his screen, while the developer cares about the component’s API. However, if your tests depend on the _implementation details_ of your component, you’ve added another (informal) interface that you need to maintain —  you’ve introduced the test user. Now you might find that any future changes or internal refactoring break the tests unnecessarily, and you’re slowed down. Oof.

So let’s avoid that! RTL does a good job at providing an API that uses your components in the same way that they’re used in your production code, and interacts with it like the end user would.

### Querying by role

Let’s return to our example for a second. Searching for the button by its text content is nice and simple. But what happens if you’re testing a more complex component (or a whole page) and there are multiple matches? After all, `getByText` matches _any_ text node. We can do a bit better by using the `getByRole` query:

```jsx
expect(
  screen.getByRole("button", {
    name: buttonLabel,
  })
).toBeInTheDocument();
```

This is no doubt a more specific query, and it also has an additional advantage: it forces us to think about accessibility. The “role” refers to the accessible role of the element (e.g. `button`, `input`, `link`, `search`, etc.), and the “name” is its semantic name, which a screen reader would use to narrate the element. Now, if your tests can find the button with the provided text, a screen reader would too! Tests that behave the same way as your end users are the tests that keep giving. Dodds recommends using the “by role” queries _most of the time_.

### User interaction and asynchronicity

Let’s say that when our button is clicked, it triggers the loading of some data, which is then rendered somehow. We can test this scenario using the user-event utility and asynchronous queries. We’ll find the button, click it and then assert that the content eventually shows up. Let’s assume that the component `MyComponent` includes a button with the label "Load Data" and that the loaded content has the header "Your Data_"_.

```jsx
import userEvent from "@testing-library/user-event";
// ...

test("can load data on click", async () => {
  render(<MyComponent />);

  const button = screen.getByRole("button", {
    name: /load data/i,
  });

  expect(button).toBeInTheDocument();

  userEvent.click(button);

  const content = await screen.findByRole("heading", { name: /your data/i });

  expect(content).toBeInTheDocument();
});
```

For a bit of extra robustness, I replaced the strings here with case-insensitive regex expressions (no need for the tests to break if the capitalisation changes). We first assert that the button is present, so that we get a better indication of what’s wrong if the test fails. Then, `userEvent` handles the button click action in a _realistic_ way, meaning it generates all the appropriate events. Lastly, we use the `findByRole` query in place of `getByRole`. The former is asynchronous, and waits a maximum of 4500 ms for the content to appear before the test fails. Usually, it proceeds almost immediately, especially if the fetch call is mocked out. This is extremely useful and ensures our tests never wait longer than they have to.

### What about global state stores, like Redux?

You can still test your components with RTL, even when they utilize a state store, context or router. Although _pure_ components are easier to test (just as for pure functions), you can override the `render` method to render the components within a wrapper where you set up all your providers. For state stores, you can then either let all your tests use the initial state, or override parts of the state on a test-by-test basis. The docs offer some excellent examples for this.

When you’re writing tests that operate heavily on local or global state, you may be tempted to assert that parts of the state have correct values after performing an action. In this case, the more idiomatic approach is to verify the state through how the component is rendered, in line with avoiding testing implementation details. This ensures you’ll be able to freely move parts of the state from global to component level and vice versa in the future. If necessary, you can always supplement the RTL tests with additional Jest unit tests to verify the correctness of your reducers.

### Final thoughts

The React Testing Library makes it possible to write quick, concise, powerful and maintainable frontend tests. It’s pretty easy to get started, so why don’t you give it a shot? The next step can be to [check out the docs](https://testing-library.com/docs/react-testing-library/intro/). There’s also quite a few nice articles about the library on [Dodd’s blog](https://kentcdodds.com/blog/).

{% embed url="https://www.toptal.com/react/react-testing-library-tutorial" %}


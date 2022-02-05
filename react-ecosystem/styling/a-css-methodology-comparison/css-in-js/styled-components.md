# Styled-components

On to the last styling methodology: CSS-in-JS, with a focus on React.js library [styled-components](https://styled-components.com). CSS-in-JS has similar ideas to Tailwind regarding `separation of concerns`, namely, that there is no separation between markup and styling, however styled-components provides a way to write regular CSS within your Javascript code, which is especially handy for things like theming.

![An example of a React Button component written with styled-components.](https://ttt.studio/wp-content/uploads/2020/11/image-1.png?x42814)

### **CSS-in-JS: Pros**

**Naming + Context Switching**

Same as with utility classes above, styled-components also alleviates these two problems with CSS. Your CSS code lives right in the same file as your markup and you do not have to worry about switching back and forth.

**Scoped Styles**

Again, like Tailwind, styles are scoped to a specific component. This results in way easier maintenance since styles can be found side by side with the markup they refer to. The worry of affecting anything else within the app is eliminated.&#x20;

This also enforces best code practices when it comes to making small, reusable components instead of huge, long components that contain what could be multiple components. By forcing you to think about each element you want to style as a component, it also enforces extracting away reusable React components where possible.

**JS Functionality within CSS**

Since your CSS code lives within your JS code, you can use any JS functionality you might need to determine styling. For me, this is one of the biggest draws of CSS-in-JS. Traditionally this would need to be done with classes, so if you had 5 different button types, you would need the corresponding classes for each type. With styled-components, you can handle it all in JS which makes your workflow much smoother.&#x20;

![Line of code highlighting Javascript functionality within CSS](https://ttt.studio/wp-content/uploads/2021/10/theming-1024x626.png?x42814)

This is especially useful for **theming** + styles based on user input

### **CSS-in-JS: Cons**

**Performance**

In the past it’s been said that performance has historically been an issue with styled-components. From what I’ve seen, however, it seems that in their new v5 release they claim to have made vast improvements to both performance and bundle size, boasting an impressive 26% smaller bundle size, 26% faster updating of dynamic styles and 45% faster server-side rendering. You can find more information regarding the v5 updates in this [Medium article.](https://medium.com/styled-components/announcing-styled-components-v5-beast-mode-389747abd987#:\~:text=Fast%2C%20faster%2C%20styled-components%20%F0%9F%8F%8E%F0%9F%92%A8\&text=1%20and%20another%2025%25%20boost,bundle%20size%20\(16.2kB%20vs.\))

### Thoughts

Styled-component are a good solution for apps that don’t often have lots of components re-rendering at the same time, or small apps not heavy in UI display. It is very dependent on the quality of React Lifecycle management in the app. The fact that styled components re-creates higher order components, themselves dependent on the lifecycle management surrounding, and the fact the devs usually choose the option of creating a new styled-component instead of using available component in the UI library, causes the react tree to grow at very fast paced, quickly getting out of control, and eventually resulting to a Bad UI/UX.In an experienced team of devs, working on a correctly designed architecture, with a light UI that rarely changes, styled-components are relevant and perfectly viable .

* We will have to heavily encourage devs to use the build-in components of the library instead of constantly re-creating new ones. Most of the time, we don’t need to create new components, especially when we have a custom component library.

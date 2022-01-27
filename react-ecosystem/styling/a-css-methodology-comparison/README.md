# A CSS methodology comparison

## **Motivations and Interrogations**

Using [Ant design](https://ant.design) or [material ui ](https://mui.com)is nit for fast MVP to production based apps,If you work with a modest team on a single app, you’re better off with a directory of UI components.

But the question arise when having the need of sharing UI components across many projects. and I you find yourself pasting the same UI components, here comes the need for a design system

{% hint style="info" %}
if you want to know more about the difference between ui libs and design system please read ([What's a design system anyway ?​?](../../../design-system/whats-a-design-system-anyway.md))
{% endhint %}

{% hint style="warning" %}
I highly recommend to read  [Thoughtful CSS Architecture](https://sparkbox.com/foundry/thoughtful\_css\_architecture) before going any further .
{% endhint %}

Working with design systems we need to carefully pick or chose the tools that will base our project on and can be integrated smoothly with the react Ecosystem and also react organism philosophy&#x20;

The market is overloaded of solutions, most not suitable or answering a specific need, or too generic.

This is a small effort to clear the difference between the tools  and have an objective view on the design systems tools adoption choice .

### **Precursor: Common CSS Problems**

If you are already familiar with the many challenges of writing clean CSS, feel free to jump forward to my thoughts on the individual frameworks. To offer a bit of context to my thoughts, I’d like to go through why you should even care about using these new frameworks instead of just plain ol’ CSS.

**Inheritance**

Although the C of CSS stands for Cascading, it doesn’t mean we should abuse this power. More often than not, using nested selectors leads to unintended complexity with too many layers of specificity. The more layers of specificity there is, the harder it gets to change the styles of that element without resorting to !important. Relying on inheritance is also problematic as it ties our styles to the structure of the HTML. If the HTML changes, we need to make sure our CSS is adjusted accordingly. If we had used a unique class to target that element, then changing the HTML around would not affect the CSS. Of course, there are times when using some inheritance in our selectors is unavoidable (for example, when overriding a third party library’s styles), but generally we should try to keep specificity as low as we can.

**Reusing classes**

Isn’t the point of using classes so you can reuse them? Yes, but reusing classes often results in **unintended side effects**. It’s easy to forget where you have reused your classes, and changing the style to fit one use-case can inadvertently break a different use-case elsewhere in your app. A great way to have reusability in a React app, would be to instead have components that can be reused instead of classes. This way, that one class is always tied to the same component, making it easy to see what changing the class will affect. Again, this isn’t to say you should never reuse classes. Having simple utility classes that are unlikely to change are great ways to keep consistent font/padding/margin/etc. (But more on utility classes in the Tailwind section 😉 )

**Code Organization**

If CSS is not broken up into files/sections, it becomes hard to find and edit the CSS you are looking for. In traditional websites, there is generally only one `styles.css` , making organization difficult to upkeep. Long stylesheets that no one understands often result in what we call “append only stylesheets”. If developers can’t easily find what they need to update, they will just append new CSS to the bottom of the sheet, instead of maintaining what they already have.

The crux of CSS problems really boils down to one thing: CSS can get unwieldy very quickly if not properly managed. We would like to avoid too-long sheets, deep nested selectors, and unnecessary !important’s. Each of the following CSS methodologies approach solving these problems in their own way.

# 🏁 What's a design system anyway ?​?



![](../.gitbook/assets/271933992\_346146360462142\_736163572486681419\_n.png)

The scale and speed at which UI screens must be created has increased as UI design has improved over time. Not only are there millions of apps and billions of websites (with more being launched every year), but each app and website may have hundreds or thousands of pages (or screens). With such rapid growth comes a pressing need for businesses to streamline their design processes. As a result, many design teams rely on sophisticated design systems to manage large-scale projects.

## **What is a Design System?** <a href="#0a04" id="0a04"></a>

Definitions of what a design system is:

> “The complete set of design standards, documentation, and principles along with the toolkit (UI patterns and code components) to achieve those standards”

_— Uxpin.com_

> “Simply put, a design system is a collection of reusable components to tie whole products together”

_— Freecodecamp.org_

> “Everything that makes up your product” — “From typography, layouts and grids, colors, icons, components and coding conventions, to voice and tone, style-guide and documentation, a design system is bringing all of these together in a way that allows your entire team to learn, build and grow”

_— css-tricks.com_

{% hint style="info" %}
_**`We can conclude by defining the design system`**_**`by a complete set of standards intended to manage design at scale` **_****_** `using reusable components and patterns.`**
{% endhint %}

## **Contents of a Design System** <a href="#309a" id="309a"></a>

Despite the fact that not all design systems are the same (most are customised to a certain brand or product), they all contain similar content. The design system consists of the brand's shared values and purpose, design principles, brand identity and language, style-guides, components and patterns, coding conventions, best practices, and rules that guide it, all with the goal of facilitating teamwork.

**Before diving deep in the content of the design system we should first understand the** [**Atomic design concept** ](https://bradfrost.com/blog/post/atomic-web-design/)****

### What is Atomic Design? <a href="#3896" id="3896"></a>

Atomic Design is a methodology developed by [Brad Frost](https://bradfrost.com/blog/post/atomic-web-design/). The modular structure of this methodology breaks down building blocks of design such as buttons, search bars and navigation into a hierarchy of components based on chemistry principles:

* Atoms are the most fundamental UI elements, such as icons and buttons, that can't be broken down any further.
* &#x20;Molecules are a collection of atoms that come together to form a more complicated component, such as a search bar. In this example, the search bar component will have the input field, search button, and icon.&#x20;
* Organisms, like a top navigation bar, are even more complicated components that can incorporate both molecules and atoms. The navigational atoms "home" and "login," as well as the molecular component of the search bar and the brand insignia, may be included in the bar.

![](<../.gitbook/assets/re-render queue (3) (1).gif>)

### What Is A Style Guide?

**Style guides** include specific implementation guidelines, visual references, and design principles for developing interfaces and other design deliverers. Most style guides are focused on branding or editorial style.

{% hint style="info" %}
* **Acceptable logo usage, color palette, font trademarks, and print media are frequently specified in branding style guides.**
* **Writing style, grammar, punctuation, Voice and Tone, and other content-editing criteria are all specified in editorial style guidelines. Many websites and magazines have style guides, which content teams are expected to adhere to.**
{% endhint %}

However, style guides also provide content guidance, such as visual and interaction design standards.

These guidelines are occasionally incorporated into the component library to provide context-specific guidance.

The simplest list of style guide content can be like this

* Purpose — Individual parts of the company's goals, ethics, perspective,&#x20;
* Product Branding Guidelines – A company's internal product and service branding guidelines.&#x20;
* Visual Elements — Where components' visual styling is specified.
* Fonts — Fonts and information on how to use them.&#x20;
* Product Editorial Guidelines — Grammar, punctuation, and other content-editing rules
* Language – The ability to communicate clearly in one or more languages..

{% embed url="https://www.facebook.com/brand" %}
Meta Brand guideline
{% endembed %}

{% embed url="https://medium.design/logos-and-brand-guidelines-f1a01a733592" %}
Medium Brand guideline
{% endembed %}

{% embed url="https://ant.design/docs/spec/introduce" %}
Ant D style Guide
{% endembed %}

{% embed url="https://design.gs.com/foundation" %}
Goldman Sachs foundation style guide
{% endembed %}

### What Is A **Component** Library?

Many people associate design systems with component libraries (also referred to as design libraries): these large libraries contain predefined, reusable user interface elements and serve as a one-stop shop for designers and developers to learn about and build various UI components. It takes a significant amount of time and effort to build these libraries.

In general, they include some graphical examples of components.

A component library must include&#x20;

* **Component name:** a specific and unique UI component name, to avoid miscommunication between designers and developers
* **Description:** a clear explanation for what this element is and how it is typically used, occasionally accompanied by do’s and don’ts for context and clarification
* **Attributes:** variables or adjustments that can be made to customize or adapt the component for specific needs (i.e., color, size, shape, copy)
* **State:** recommended defaults and the subsequent changes in appearance
* **Code snippets:** the actual code excerpt for the element (some design systems go as far as sharing multiple examples and offering a “sandbox” environment to try out different component customizations)
* **Front-end & backend frameworks** to implement the library (if applicable), to avoid painful and unnecessary debugging



{% embed url="https://design.gs.com/components" %}
Goldman Sachs foundation component library
{% endembed %}

{% embed url="https://ant.design/components/overview" %}

### What Is A Pattern Library?

The terms 'component library' and 'pattern library' are sometimes used interchangeably, although there is a difference between the two types of libraries. Individual UI elements are specified in **component libraries,** whereas **pattern libraries** contain sets of UI-element groups or layouts. When compared to component libraries, pattern libraries are typically perceived to be less robust, yet they can be as detailed or as high-level as desired. Content structures, layouts, and/or templates are usually included. The patterns, like the components, are meant to be reused and adapted.

{% embed url="https://design.gs.com/patterns" %}
Goldman Sachs foundation patterns library
{% endembed %}

{% embed url="https://tailwinduikit.com" %}
Tailwind CSS templates free and patterns
{% endembed %}

&#x20;

## How to Approach Design-System Adoption

With my numerous affiliation with startups, at the start we certainly will be a small team

The most non costly way is to adopt an existing design system.

> To say the truth and it's extremely subjective I use Ant design design system, in all my small projects, MVP or just to create something for fun, as i loved it and i will always use it.

We need to always remember the objective of our choice, resources and Time limit.

Projects grow and mature, and you start having the urge to optimize your branding, hiring designers, thus adapting the design system to your designers need. creating a specific package of reusable custom components tweeked from the adopted design system

Finally you start to expand, and have multiple project that use the same components, patterns  custom brand philosophies and design principals and you find yourself in need to create your own design system&#x20;

So there are generally three approaches to using a design system:

* **adopting** an existing design system
* **adapting** an existing design system
* **creating your own** proprietary or custom design system

Each has advantages and disadvantages, but in general, the more customized your design-system solution, the more time and money it will take to implement. As a result, using an existing design system is the least expensive and takes the least amount of time to implement. (It will still take longer than if you just keep designing as usual because you will have to replace or update some UI elements and agree on a standard.)

If the organization has specific needs that cannot be met by open-source design systems, the investment in a custom design system will be worthwhile. As customizations and adjustments to the design system increase, the cost savings you may have gained by using the existing design system will diminish, and you may be better off creating your own design system anyway in the long run. Before embarking on design system endeavors and weighing the tradeoffs, make sure you understand what your organization requires.

![](<../.gitbook/assets/re-render queue (2) (4).gif>)

Finally, establishing a full-fledged design system for a proof of concept or an initial prototype that is expected to alter is likely to be time and money consuming. After all, the benefit is design replicability, which is in the future. Though it may be tempting to establish these right away, note that a design system isn't intended to be a portfolio of work, but rather a functional toolkit or resource that allows designers and developers to work more efficiently. Nevertheless, if you are unsure about the usefulness of a design system, think about the duration you will use to evaluate your design work. When a company anticipate years of future, iterative design work, design systems are ideal.

### Why Use a Design System?

When properly implemented, design systems can provide a design team with numerous benefits:

* **Projects in design (and development) can be easily developed and replicated at a scale.** The major value of design systems is their ability to quickly duplicate concepts using pre-made UI components and elements. Teams can reuse the same components over and over, reducing the need to reinvent the wheel and the risk of unintentional inconsistency.
* **It frees up design resources to focus on bigger, more complex problems.** Since the most basic UI elements have already been created and are reusable, design resources can concentrate on tackling more difficult problems rather than fine-tuning the aesthetic look (like information prioritization, workflow optimization, and journey management). While this benefit may seem modest when only a few screens are created, when dozens of teams and thousands of screens are involved, it becomes considerable.
* **It creates a unified language within and between cross-functional teams.**\
  A single language eliminates wasted design or development time caused by miscommunications, especially when design responsibilities shift or teams grow geographically dispersed.&#x20;
* **Visual consistency is achieved across products, channels, and departments.** The absence of an organization-wide design system can result in uneven visual appearance and experiences that appear fragmented or unrelated to the brand, especially when teams work in silos, where each product or channel functions independently of the others. Design systems connect disparate experiences by providing a common source of components, patterns, and styles that make them visually harmonious and appear to be part of the same ecosystem. Any big visual rebranding or redesigns can also be managed at scale using the design system.
* **It can serve as an educational tool and reference for junior-level designers and content contributors**. \
  Individual contributors who are new to UI design or content development can be onboarded with explicit use instructions and style guides, which also act as a reminder to the rest of the contributors.

### Why Not Use a Design System?

There are some potential hurdles and limitations which may prevent a design team from using a design system:

1. **Creating and maintaining a design system is a time-consuming task that necessitates the presence of a dedicated team.** Unfortunately, design systems are not a one-size-fits-all answer. They are continually improving at their best, as teams gather feedback from those who utilize them.
2. **Teaching others how to use the design system takes time.** Even if it was derived from an existing system, any design system need instructions for use; otherwise, it risks being applied inconsistently or improperly across screens or across teams.
3. **There's a widespread assumption that projects are one-off, static creations that don't require reusable components.** This notion, whether accurate or not, may indicate a lack of a coherent strategy across projects and a wasted opportunity to improve efficiency.

## _Conclusion_

* The graphics Styles and their applications are the center of this style guide. Colors, fonts, graphics, illustrations, and so on are examples of graphic style. The pattern library, on the other hand, will provide functional components as well as how they are used. The visual styling of components is defined by the style guide.
* The visual and interactive aspects of components are defined by the components library. how a component should behave when clicked or hovered over, or how a form should behave when an incorrect input is entered.
* The behavior of components is also explained in the pattern library. But in a comprehensible fashion, because a pattern is only a collection of 1 to n components.
* Everything in the pattern library, brand value, shared ways of working, mindset, and common belief is contained in the design system. It includes everything you'll need to get started on your design and development project. It can include a code snippet or a link to the code snippet for developers.
* Design systems are made up of a variety of components, patterns, styles, and rules that can help you operationalize and optimize your design efforts. People, on the other hand, are in charge of planning, managing, and implementing them. The breadth and replicability of your projects, as well as the money and time available, are the most critical factors to consider while creating a design system. If established and managed wrong, design systems can become unmanageable collections of components and code; yet, when handled properly, they can educate team members, speed work, and empower designers to tackle difficult UX problems.

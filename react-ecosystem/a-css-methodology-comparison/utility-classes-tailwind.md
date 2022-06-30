# 🏁 Utility Classes: Tailwind

Utility-first CSS is a methodology that came about in an effort to solve all the cons mentioned above with writing traditional CSS. Utility-first CSS involves using many small helper classes to make up a component’s styles, instead of writing class names based on semantic meaning. One thing to keep in mind is that utility-first CSS doesn’t need any library, it is simply a methodology that can be applied to CSS, similar to how BEM works.

I will be focusing on the library [Tailwind CSS](https://tailwindcss.com/), since it is probably the most popular approach developers are flocking to for implementing utility-first css.

Tailwind css is a utility-first, flex-based framework using PostCss to build any design using a composition directly in the markup&#x20;

It is made for small teams projects, but shines with Design System-ready teams

### Example

Here, you can find a button design implemented with classic CSS:

![](../../.gitbook/assets/css)



Here, is that same Button implemented with Tailwind classes:

![](../../.gitbook/assets/tail)

In the above line of code, a simple button is defined using the following classes:

* `bg-blue-500` class sets the background color of the button to blue. The number 500 specifies the shade.
* `hover:bg-blue-700` class makes the button a slightly different shade of blue upon hovering.
* `text-white` makes the text ‘Button’ white.
* `font-bold` is used to bold the text.
* `py-2` sets the height.
* `px-4` sets the width.
* `rounded-full` rounds the shape of the button.

Right off the bat, you’re probably thinking “Ew, talk about hard to read markup.” Even the developers of Tailwind will admit, in terms of first impressions, it’s not great, and that you have to try it to believe it! When I first looked into Tailwind, I was skeptical. I value readable code, and this seems like the opposite so why are so many developers swearing by Tailwind’s approach to utility-first?

### **Utility-First: Pros**

**Context Switching**

As mentioned in Sass’s cons, context switching between files can hamper a developer’s focus and result in lost time. Tailwind solves this hassle and allows you to write your styles right there inline with markup. What some may consider a small headache, may be a huge time saver for others.

**Naming**

Again, as I have brought up in the Sass cons list, naming is a frustrating thing to navigate. With Tailwind, you are no longer coming up with your own classes for each element, you are instead making up an element’s styling using their provided utility classes. For example, if you just need a flexbox quickly, it’s very easy to throw a `flex justify-center` onto a div and you’re all set.&#x20;

**Your CSS Stops Growing**

Tailwind CSS provides you with a set of utility classes to use and besides those, you very rarely will need to write your own custom CSS, resulting in smaller CSS output.

If you are worried about including all the extra unused utility classes Tailwind provides, you can use a tool like PurgeCSS that will remove all unused CSS.

**Making Changes Feels Safer**

Because the styling is done in the markup instead of an external stylesheet, when you need to change styles, it’s easy to see exactly what you are updating. There are no unintended side effects elsewhere in the app.&#x20;

**You Can Still Create Components**

You might be thinking, “okay utility sounds nice but what about when I want a button to have the same style throughout the app?”. Good news, it’s called “utility-first” not “utility-only.” You can still create regular classes while using Tailwind! If you need a button component, you can easily extract your Tailwind code to reusable classes

![](../../.gitbook/assets/aply)

As you start to write utility-first css, you may come to the realization that most “components” don’t end up being reused anyway. It might seem necessary to have a class for your “Notification Bar” component, but will that class actually get reused somewhere? Probably not! You may use your `<NotificationBar />` component multiple places, but if your code is already extracted to its own component, what need will those _classes_ have elsewhere?

**Cache Invalidation**

Browsers cache static assets, which is good for performance, but if you just need to make some CSS style tweaks to your website, you then need to purge the file from cache. With Tailwind however, since the styling is within the markup now, you don’t have to worry about invalidating your css assets.

### **Utility-First: Cons**

**Hard to Read Markup**

Readability definitely suffers when using utility classes. Especially if you need different class names for different breakpoints or hover events, you can very quickly end up with very long class names.&#x20;

**Learning Curve**

There is an initial learning curve that comes with moving to utility classes. When I started experimenting with Tailwind, I found it frustrating knowing exactly what style properties I wanted to apply, but didn’t know the Tailwind equivalent, and had to keep tabbing to a[ Tailwind Cheat Sheet](https://nerdcave.com/tailwind-cheat-sheet) (this was a life-saver). Once you are more familiar with the classes, I can see this speeding up drastically, and actually increasing dev speed. In the beginning, however, there will definitely be a bit of a hump to get over.

**No more ‘cascading’**

I put this in the ‘cons’ section because when I first started learning about Tailwind, I thought it was one. However, the loss of the ‘cascade’ is actually a **GOOD** thing.

Specificity has got to be the number one source of CSS bugs. If you have ever had to override third party styles then you probably know the pain of jumping over 5 levels of specificity before you:

a) Find the level you need and successfully apply your style

b) Give up and slap an !important on the end. (Assuming there weren’t already `!important`‘s within the existing CSS 😱)

Using class names and avoiding child selectors is something one can do while working with regular CSS of course, but it is up to the **developer** to enforce that rule. With Tailwind, it is already enforced by the **framework.**

Overall, utility-first CSS using Tailwind seems like a solid pick. I think the biggest draws of Tailwind are the speed at which it allows developers to style elements, as well as limiting the chance for misuse. That isn’t to say Tailwind can’t be misused. Everything can be, but there are _less_ ways to misuse it than regular CSS.

### **Cache Benefits**

* Using a traditional CSS framework or custom CSS, you’ll most likely need to make changes to your CSS file when making changes to your design. However, when using Tailwind, since you’re using the same classes over and over in your markup instead of changing your CSS file, you may not even have to bust your CSS cache to make small changes to your design. This means your users won’t have to redownload your CSS file as often.

### Thoughts&#x20;

I think Tailwind has a lot of practical advantage on the other css methodology like:&#x20;

* No need of creating atomic classes, with unique class names with constrained set of properties. With react, Tailwind automatically creates css classnames tied to the actual components names. Making it extremely easy to track components styling while designing
* The css files don’t grow infinitely until they become legacy resource no one understands. Any time a components needs style update, only it’s classname is updated and or interchanged. No need to maintain many css files. Of course, it is possible to use custom css files, usually in the form of CSS modules. But TailwindCSS provides us a simple way of creating a dedicated DSM by modifying and creating directly the utilities classnames we need to design our system.
* Changes in styles are extremely easy to track and control. Since we rarely write custom css files, it’s very hard to get out of the framework and break something unintentionally. It is also very easy to use reusable
* Unlike inline css, it is impossible to collapse css properties. The values of any constraint is pre-defined and you cannot get out of the custom DSM. This is a great advantage for consistent UIs a given app, and multiple apps using the same DSM
* Inline styles are limited and cannot use some common css properties like Hover, focus, and other state variants, which are built-in Tailwind system
* Everything is build in CSS under the hood, with 0 JavaScript involved
* Provides error detection during development, linting, autocomplete and CSS purge (equivalent of tree-shaking for Javascript)
* Responsiveness is a breeze. Adding a responsive version of a UI only needs a utility directive like
* Only the needed CSS for a given page is loaded
* Mobile-first with breakpoints easily applicable and customizable
* Even the custom css can be written using only Tailwind utilities with directives, such as @apply (but with React this is almost useless)
* Maintainability is drastically easier than with large CSS files spread across large codebases
* It allows building scalable CSS architecture. With a single source of truth which is the DSM, it makes it very hard to mess up with the styles
* Plugins to convert Figma design to tailwind usable components
* Improved development experience
* Community components with pure html and utility-classes only, easily customizable, and use as cheatsheet
* A lot of industry state of the art design principles and rules built-in
* Impressive documentation
* Large community
* Multi projects configuration made simple with configuration presets
* Uniformisation between frontend engineering team
* Extensibility + development of the state of the art

## Bundle Info

{% embed url="https://bundlephobia.com/package/tailwindcss@3.0.23" %}

## References and articles :

{% embed url="https://chrome.google.com/webstore/detail/css-to-tailwind/jlmlldiahhaejpjnonbddoniicdemakl" %}

{% embed url="https://css-irl.info/a-year-of-utility-classes" %}

{% embed url="https://locastic.com/blog/i-was-wrong-about-utility-first-css-and-here-is-why" %}

{% embed url="https://davidtheclark.com/on-utility-classes" %}

{% embed url="https://css-irl.info/a-year-of-utility-classes" %}

{% embed url="https://adamwathan.me/css-utility-classes-and-separation-of-concerns" %}

{% embed url="https://blog.logrocket.com/css-utility-classes-library-extendable-styles" %}

{% embed url="https://johnpolacek.github.io/the-case-for-atomic-css" %}

{% embed url="https://css-tricks.com/if-were-gonna-criticize-utility-class-frameworks-lets-be-fair-about-it" %}

{% embed url="https://css-tricks.com/building-a-scalable-css-architecture-with-bem-and-utility-classes" %}

{% embed url="https://github.com/aniftyco/awesome-tailwindcss" %}

{% embed url="https://www.creative-tim.com/learning-lab/tailwind-starter-kit/presentation" %}

{% embed url="https://heroicons.com" %}

{% embed url="https://usewindy.com" %}

{% embed url="https://blocks.wickedtemplates.com" %}

{% embed url="https://www.creative-tim.com/search?buton=&q=tailwind&utf8=%E2%9C%93" %}

{% embed url="https://tailwindui.com/components" %}

{% embed url="https://tailblocks.cc" %}

{% embed url="https://builtwithtailwind.com" %}

{% embed url="https://github.com/tailwindlabs/headlessui/blob/develop/packages/%40headlessui-react/README.md" %}

{% embed url="https://github.com/heybourn/headwind" %}

{% embed url="https://tailwind-converter.netlify.app" %}

{% embed url="https://transform.tools/css-to-tailwind" %}

{% embed url="https://blog.logrocket.com/10-tailwind-css-tips-to-boost-your-productivity" %}

{% embed url="https://github.com/aniftyco/awesome-tailwindcss" %}

{% embed url="https://www.figma.com/community/file/768809027799962739" %}

{% embed url="https://tailwindcss.com/docs/adding-base-styleshttps://tailwindcss.com/docs/preflight" %}

{% embed url="https://tailwindcss.com/docs/hover-focus-and-other-states" %}

{% embed url="https://tailwindcss.com/docs/preflighthttps://unpkg.com/tailwindcss@2.0.2/dist/base.css" %}

{% embed url="https://tailwindcss.com/docs/optimizing-for-production" %}

{% embed url="https://www.youtube.com/watch?v=mr15Xzb1Ook" %}

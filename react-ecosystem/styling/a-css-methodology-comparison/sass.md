# 🆗 Post CSS processor :Sass

CSS is at the heart of it all, the bread and butter, if you will. This is what every web developer should learn first, and in many cases, plain ol' CSS will suffice. Setting the foundation for your learning is critical, and it should be done before learning any new "fancier" ideas.

Sass is a scripting language for preprocessors that is compiled into CSS. Sass is an improved way of writing CSS that provides developers with powerful tools such as variables, mixins, and nesting; in short, it makes CSS writing easier and more efficient.

Officially described as “[CSS with superpowers](https://sass-lang.com),” SCSS (or Sass) offers a way to write styles for websites with more enhanced CSS syntax. In general, browsers do not know how to process SCSS features, such as functions, mixins, and nesting. We’ll need to convert them to regular CSS files to run them in the browser.

### **Sass: Pros**

**Sass Features**

Variables, mathematical operations, mixins, loops, functions, imports, and other interesting functionalities that make writing CSS much more powerful are all available in Sass. Simply put, Sass is like writing CSS, but with more features!

**Variables:**&#x20;

![](https://ttt.studio/wp-content/uploads/2021/10/Variables-2-1024x223.png?x42814)

Line of code comparing sass to CSS for variables

**Nesting:**

![](https://ttt.studio/wp-content/uploads/2021/10/Nesting-1024x400.png?x42814)

Line of code comparing sass to CSS for nesting

**Mixins:**

![](https://ttt.studio/wp-content/uploads/2021/10/Mixins-1024x210.png?x42814)

Line of code comparing sass to CSS for mixins

**Modules**

Although not unique to Sass, using bundlers such as webpack allows you to split your Sass (or CSS, in the case of CSS modules) into files. This is useful because it helps organize code and makes CSS maintenance easier.

**Freedom**

A big benefit of Sass (compared to the other two frameworks in this post) is the freedom to write your own CSS how you want. At TTT we generally stick to the BEM (Block Element Modifier methodology, however writing your own Sass lets you write your CSS however you think is best.&#x20;

### **Sass: Cons**

**Freedom!**

As we just read, the freedom that Sass gives you allows you to write code in whichever way you want, which can be great, but is also dangerous if misused. As the saying goes “_With great power comes great responsibility.”_&#x20;

Many developers, such as juniors or backend devs, don’t have a complete understanding of CSS, which can lead to unnecessarily complex CSS that future developers are too afraid to touch in fear of breaking things. Because Sass offers such freedoms, these developers aren’t “reined in” by the framework. This misuse can be avoided by having solid CSS guidelines and code review, however, it is on the **developer (or team of developers)** to enforce those guidelines.&#x20;

**Context Switching**

Picture this: You are working away on your component, creating `div`‘s, `p`‘s, and `headers`. You know these will need some styling, so you assign some class names that you think make sense! Now that you’re done your markup, you switch over to your CSS file to start styling and….you’ve forgotten what the class names were and have to tab back to your markup. If this hasn’t happened to you, well then your memory is better than mine.&#x20;

The fact remains that there is a disconnect between your styles and your markup. Many of you may be thinking, but that’s a good thing, “separation of concerns” right? And yes, as developers we live by this principle, and at first glance, yes we should keep the markup (the content) and the styling separate right? However in practice, styling and markup are not separate concerns at all! How many times have you had to add a `div` purely for styling purposes? Markup and styles are so intertwined now, we as frontend developers are constantly tabbing between our HTML and CSS, causing a maybe minor inconvenience, but an inconvenience nonetheless.

**Naming**

> _There are only two hard things in Computer Science: cache invalidation and naming things._
>
> _— Phil Karlton_

You may have heard this joke before, but it’s true! Naming things is hard! BEM is a methodology that aims to help us come up with meaningful class names, and it does help. However, you do still have to spend time thinking about meaningful blocks, with appropriate elements and modifiers.

It also gets tedious naming every single class for every single element you need to style, since we don’t want to mix inline styles and stylesheets. It results in a lot of classes being created simply for adding a width: 100% or some margin or padding.

Sometimes we just want to add one or two little styles. Especially when it comes to layout, we don’t exactly need a reusable class that is in use only in the first specific part of your page telling the buttons how they should sit next to each other. It is a pain having to make one and come up with a name for it, which leads us nicely into our next methodology….\


## Thoughts

CSS preprocessors in combination with BEM definitely improve the development experience a lot, but that doesn’t mean it’s perfect. When your codebase grows, you might start to wonder in which files you should put certain styles and how it should be scoped. You also wonder if old styles are still being used. And you also have to think about performance: you don’t want to load in every single line of CSS on the first page when most of it is used on other pages.

## Usefull-Links:

{% embed url="https://sass-lang.com/guide" %}

{% embed url="https://blog.logrocket.com/the-definitive-guide-to-scss" %}

{% embed url="https://cheesecakelabs.com/blog/css-architecture-first-steps#:~:text=What%20is%20a%20CSS%20Architecture,to%20scale%20and%20more%20reusable." %}

{% embed url="https://www.cqlcorp.com/insights/widely-used-css-architectures-and-how-they-function" %}

{% embed url="https://blog.allegro.tech/2021/07/css-architecture-and-performance-of-micro-frontends.html" %}

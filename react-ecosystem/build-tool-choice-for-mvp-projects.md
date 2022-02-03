# Build tool choice for MVP projects

Creating React app really doesn't need any fancy builder as you can do it by your self we just simple CDN, thus that approach can work for small exercises  or just playing with code , in real world we use building tools that facilitate the task of configuring the project bundling the app and managing 3'rd tiers libraries.

The most common choice is :

{% embed url="https://create-react-app.dev" %}

It was a very good build tool : it has a lot of integrations that is mature and solid for common business logic . but in modern days i remarked a swift shift to:&#x20;

{% embed url="https://vitejs.dev" %}

Like create-react-app it's a build tool created by [Evan You](https://evanyou.me) the creator of Vue.js.

It's by far faster then create react up as it uses [Rollup](https://rollupjs.org/guide/en/) under the hood against the MegaZord [webpack](https://webpack.js.org) used by Create-react-app .

{% embed url="https://www.youtube.com/watch?v=DkGV5F4XnfQ" %}

For all my personal small projects i use Vite as it's blazing fast. but for more complex projects i will choose a framework like [next.js](https://nextjs.org) or [gatsby](https://www.gatsbyjs.com)  . For now let's stick with vite and JavaScript. and i will talk about my favorite stack in the **** [**react ecosystem**](broken-reference) section

You can read more about Vite comparison :

{% embed url="https://theodorusclarence.com/blog/vite-cra" %}

## Quick guide&#x20;

### Installation

Vite has various template to chose from as it's not specific to React.&#x20;

```
vanilla
vanilla-ts
vue
vue-ts
react
react-ts
preact
preact-ts
lit-element
lit-element-ts
svelte
svelte-ts
```

As in the fundamentals section we will use only JavaScript we will build our app by just running this command.

With NPM:

```
$ npm init vite@latest
```

With Yarn:

```
$ yarn create vite
```

You can also directly specify the project name and the template you want to use via additional command line options. For example, to scaffold a Vite + Vue project, run:

```
# npm 6.x
npm init vite@latest name-of-the-project --template react

# npm 7+, extra double-dash is needed:
npm init vite@latest name-of-the-project -- --template react

# yarn
yarn create vite name-of-the-project--template react

```

Then just go to your newly created project and install the dependencies and then run the project.

```
 cd name-of-the-project
 // npm 
 npm install
 npm run dev
 // yarn 
yarn
yarn dev
```

&#x20;I did choose react-grimoire as the name of the project but you can name what ever you please&#x20;

And here you go a react project ready to use . simple right ??

![](<../.gitbook/assets/Screenshot from 2022-01-29 16-40-29.png>)

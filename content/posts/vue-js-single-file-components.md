+++
title = "Vue.js Single File Components"
date = "2020-03-23"
draft = false
pinned = false
description = "Single File Components\n1:  Introduction  #Global definitions  #String templates  #No CSS support   #No build step\n2:  #Complete syntax highlighting  #Complete syntax highlighting   #Component-scoped CSS\n3:  What About Separation of Concerns?   #separation of concerns is not equal to separation of file types\n4:  Getting Started  #Example Sandbox  #For Users New to Module Build Systems in JavaScript  #Node Package Manager (NPM):   #Modern JavaScript with ES2015/16:   #For Advanced Users\n"
+++
<!--StartFragment-->

# Single File Components

## [Introduction](https://vuejs.org/v2/guide/single-file-components.html#Introduction "Introduction")

[Watch a free video lesson on Vue School](https://vueschool.io/lessons/introduction-to-single-file-components?friend=vuejs "Free Vue.js Single File Components lesson")

In many Vue projects, global components will be defined using`Vue.component`, followed by`new Vue({ el: '#container' })`to target a container element in the body of every page.

This can work very well for small to medium-sized projects, where JavaScript is only used to enhance certain views. In more complex projects however, or when your frontend is entirely driven by JavaScript, these disadvantages become apparent:

* **Global definitions**force unique names for every component
* **String templates**lack syntax highlighting and require ugly slashes for multiline HTML
* **No CSS support**means that while HTML and JavaScript are modularized into components, CSS is conspicuously left out
* **No build step**restricts us to HTML and ES5 JavaScript, rather than preprocessors like Pug (formerly Jade) and Babel

All of these are solved by**single-file components**with a`.vue`extension, made possible with build tools such as Webpack or Browserify.

Here’s an example of a file we’ll call`Hello.vue`:

[![Single-file component example (click for code as text)](https://vuejs.org/images/vue-component.png)](https://codesandbox.io/s/github/vuejs/vuejs.org/tree/master/src/v2/examples/vue-20-single-file-components)

Now we get:

* [Complete syntax highlighting](https://github.com/vuejs/awesome-vue#source-code-editing)
* [CommonJS modules](https://webpack.js.org/concepts/modules/#what-is-a-webpack-module)
* [Component-scoped CSS](https://vue-loader.vuejs.org/en/features/scoped-css.html)

As promised, we can also use preprocessors such as Pug, Babel (with ES2015 modules), and Stylus for cleaner and more feature-rich components.

[![Single-file component example with preprocessors (click for code as text)](https://vuejs.org/images/vue-component-with-preprocessors.png)](https://gist.github.com/chrisvfritz/1c9f2daea9bc078dcb47e9a82e5f7587)

These specific languages are only examples. You could as easily use Bublé, TypeScript, SCSS, PostCSS - or whatever other preprocessors that help you be productive. If using Webpack with`vue-loader`, it also has first-class support for CSS Modules.

### [What About Separation of Concerns?](https://vuejs.org/v2/guide/single-file-components.html#What-About-Separation-of-Concerns "What About Separation of Concerns?")

One important thing to note is that**separation of concerns is not equal to separation of file types.**In modern UI development, we have found that instead of dividing the codebase into three huge layers that interweave with one another, it makes much more sense to divide them into loosely-coupled components and compose them. Inside a component, its template, logic and styles are inherently coupled, and collocating them actually makes the component more cohesive and maintainable.

Even if you don’t like the idea of Single-File Components, you can still leverage its hot-reloading and pre-compilation features by separating your JavaScript and CSS into separate files:

```
<!-- my-component.vue -->
<template>
  <div>This will be pre-compiled</div>
</template>
<script src="./my-component.js"></script>
<style src="./my-component.css"></style>
```

## [Getting Started](https://vuejs.org/v2/guide/single-file-components.html#Getting-Started "Getting Started")

### [Example Sandbox](https://vuejs.org/v2/guide/single-file-components.html#Example-Sandbox "Example Sandbox")

If you want to dive right in and start playing with single-file components, check out[this simple todo app](https://codesandbox.io/s/o29j95wx9)on CodeSandbox.

### [For Users New to Module Build Systems in JavaScript](https://vuejs.org/v2/guide/single-file-components.html#For-Users-New-to-Module-Build-Systems-in-JavaScript "For Users New to Module Build Systems in JavaScript")

With`.vue`components, we’re entering the realm of advanced JavaScript applications. That means learning to use a few additional tools if you haven’t already:

* **Node Package Manager (NPM)**: Read the[Getting Started guide](https://docs.npmjs.com/packages-and-modules/getting-packages-from-the-registry)section about how to get packages from the registry.
* **Modern JavaScript with ES2015/16**: Read through Babel’s[Learn ES2015 guide](https://babeljs.io/docs/learn-es2015/). You don’t have to memorize every feature right now, but keep this page as a reference you can come back to.

After you’ve taken a day to dive into these resources, we recommend checking out[Vue CLI 3](https://cli.vuejs.org/). Follow the instructions and you should have a Vue project with`.vue`components, ES2015, Webpack and hot-reloading in no time!

### [For Advanced Users](https://vuejs.org/v2/guide/single-file-components.html#For-Advanced-Users "For Advanced Users")

The CLI takes care of most of the tooling configurations for you, but also allows fine-grained customization through its own[config options](https://cli.vuejs.org/config/).

In case you prefer setting up your own build setup from scratch, you will need to manually configure webpack with[vue-loader](https://vue-loader.vuejs.org/). To learn more about webpack itself, check out[their official docs](https://webpack.js.org/configuration/)and[Webpack Academy](https://webpack.academy/p/the-core-concepts).

<!--EndFragment-->
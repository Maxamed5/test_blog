+++
title = "*What I learned today  #Conditional Rendering"
date = "2020-02-28"
draft = false
pinned = false
image = "img/if_else_condition_vue.png"
description = "*What I learned today \n#Conditional Rendering\n\n1- V-if\n2- V-else\n3- V-else-if\n\n#Controlling Reusable Elements with Key\n\n4- V-show\n5- V-if VS V-show\n6- V-if with V-for"
footnotes = "v-if vs v-show\nv-if is “real” conditional rendering because it ensures that event listeners and child components inside the conditional block are properly destroyed and re-created during toggles.\n\nv-if is also lazy: if the condition is false on initial render, it will not do anything - the conditional block won’t be rendered until the condition becomes true for the first time.\n\nIn comparison, v-show is much simpler - the element is always rendered regardless of initial condition, with CSS-based toggling.\n\nGenerally speaking, v-if has higher toggle costs while v-show has higher initial render costs. So prefer v-show if you need to toggle something very often, and prefer v-if if the condition is unlikely to change at runtime."
+++
# Conditional Rendering 

> Conditional Rendering The directive v-if is used to conditionally render a block. The block will only be rendered if the directive’s expression returns a truthy value.
>
> ```
> <h1 v-if="awesome">Vue is awesome!</h1>
> ```
>
> It is also possible to add an “else block” with`v-else`:
>
>
>
> ![](img/if_else_condition_vue.png "Conditional Rendering Vue.js")
>
> ```
> <h1 v-if="awesome">Vue is awesome!</h1>
> <h1 v-else>Oh no 😢</h1>
> ```
>
> <!--StartFragment-->
>
> ### [Conditional Groups with`v-if`on`<template>`](https://vuejs.org/v2/guide/conditional.html#Conditional-Groups-with-v-if-on-lt-template-gt "Conditional Groups with v-if on \<template>")
>
> Because`v-if`is a directive, it has to be attached to a single element. But what if we want to toggle more than one element? In this case we can use`v-if`on a`<template>`element, which serves as an invisible wrapper. The final rendered result will not include the`<template>`element.
>
> <!--EndFragment-->
>
> ```
> <template v-if="ok">
>   <h1>Title</h1>
>   <p>Paragraph 1</p>
>   <p>Paragraph 2</p>
> </template>
> ```
>
> <!--StartFragment-->
>
> ### [`v-else`](https://vuejs.org/v2/guide/conditional.html#v-else "v-else")
>
> You can use the`v-else`directive to indicate an “else block” for`v-if`:
>
> <!--EndFragment-->
>
> ```
> <div v-if="Math.random() > 0.5">
>   Now you see me
> </div>
> <div v-else>
>   Now you don't
> </div>
> ```

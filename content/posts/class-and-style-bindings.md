+++
title = "Class and style Bindings."
date = "2020-02-27"
draft = false
pinned = false
image = "img/dynamic-style-and-class-in-vue-js.jpg"
description = "What I learned today \n\n Class and style Bindings.\n1- Binding HTML Classes.\n2- Object Syntax.\n3- Array Syntax with Components Binding inline styles.\n4- Object Syntax.\n5- Array Syntax.\n6- Auto-prefixing.\n7- Multiple Values."
+++
<!--StartFragment-->

# Class and Style Bindings

> *`A common need for data binding is manipulating an element’s class list and its inline styles. Since they are both attributes, we can usev-bindto handle them: we only need to calculate a final string with our expressions. However`*
>
> ```
> <div v-bind:class="{ active: isActive }"></div>
>
> <div
>   class="static"
>   v-bind:class="{ active: isActive, 'text-danger': hasError }"
> ></div>
>
> data: {
>   isActive: true,
>   hasError: false
> }
> <div class="static active"></div>
>
> <div v-bind:class="classObject"></div>
> data: {
>   classObject: {
>     active: true,
>     'text-danger': false
>   }
> }
>
> data: {
>   isActive: true,
>   error: null
> },
> computed: {
>   classObject: function () {
>     return {
>       active: this.isActive && !this.error,
>       'text-danger': this.error && this.error.type === 'fatal'
>     }
>   }
> }
> ```
>
> *`, meddling with string concatenation is annoying and error-prone. For this reason, Vue provides special enhancements whenv-bindis used withclassandstyle. In addition to strings, the expressions can also evaluate to objects or arrays.`*

# <!--EndFragment-->

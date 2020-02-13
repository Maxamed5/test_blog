+++
title = "What I learned today"
date = "2020-02-12"
draft = false
pinned = false
image = "img/2-vue-component-tree-large.jpeg"
description = "1#B1 - Lesson 28 - Defining Relative Clauses\n2#Components Basics\n\nBase Example\n\nReusing Components\n"
+++
**Components Basics**

**Base Example**

Here’s an example of a Vue component:

Components are reusable Vue instances with a name: in this case, <button-counter>. We can use this component as a custom element inside a root Vue instance created with new Vue:

Since components are reusable Vue instances, they accept the same options as new Vue, such as data, computed, watch, methods, and lifecycle hooks. The only exceptions are a few root-specific options like el.

**Reusing Components**

Components can be reused as many

```
// Define a new component called button-counter
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```

```
<div id="components-demo">
  <button-counter></button-counter>
</div>
new Vue({ el: '#components-demo' })
```

```
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```

 times as you want:

+++
title = "Vue.js Mixins"
date = "2020-03-20"
draft = false
pinned = false
image = "img/4ce1004df2.png"
description = "Vue.js Mixins\n1:  Basics  #Examples\n2:  Option Merging  #Examples\n3:   Global Mixin  #Examples\n4:  Custom Option Merge Strategies  Vue.config.optionMergeStrategies:  #Examples"
+++
<!--StartFragment-->

# Mixins

## [Basics](https://vuejs.org/v2/guide/mixins.html#Basics "Basics")

Mixins are a flexible way to distribute reusable functionalities for Vue components. A mixin object can contain any component options. When a component uses a mixin, all options in the mixin will be “mixed” into the component’s own options.

[Watch a video explanation on Vue Mastery](https://www.vuemastery.com/courses/next-level-vue/mixins "Mixins Tutorial")

Example:

```
// define a mixin object
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// define a component that uses this mixin
var Component = Vue.extend({
  mixins: [myMixin]
})

var component = new Component() // => "hello from mixin!"
```

## [Option Merging](https://vuejs.org/v2/guide/mixins.html#Option-Merging "Option Merging")

When a mixin and the component itself contain overlapping options, they will be “merged” using appropriate strategies.

For example, data objects undergo a recursive merge, with the component’s data taking priority in cases of conflicts.

```
var mixin = {
  data: function () {
    return {
      message: 'hello',
      foo: 'abc'
    }
  }
}

new Vue({
  mixins: [mixin],
  data: function () {
    return {
      message: 'goodbye',
      bar: 'def'
    }
  },
  created: function () {
    console.log(this.$data)
    // => { message: "goodbye", foo: "abc", bar: "def" }
  }
})
```

Hook functions with the same name are merged into an array so that all of them will be called. Mixin hooks will be called**before**the component’s own hooks.

```
var mixin = {
  created: function () {
    console.log('mixin hook called')
  }
}

new Vue({
  mixins: [mixin],
  created: function () {
    console.log('component hook called')
  }
})

// => "mixin hook called"
// => "component hook called"
```

Options that expect object values, for example`methods`,`components`and`directives`, will be merged into the same object. The component’s options will take priority when there are conflicting keys in these objects:

```
var mixin = {
  methods: {
    foo: function () {
      console.log('foo')
    },
    conflicting: function () {
      console.log('from mixin')
    }
  }
}

var vm = new Vue({
  mixins: [mixin],
  methods: {
    bar: function () {
      console.log('bar')
    },
    conflicting: function () {
      console.log('from self')
    }
  }
})

vm.foo() // => "foo"
vm.bar() // => "bar"
vm.conflicting() // => "from self"
```

Note that the same merge strategies are used in`Vue.extend()`.

## [Global Mixin](https://vuejs.org/v2/guide/mixins.html#Global-Mixin "Global Mixin")

You can also apply a mixin globally. Use with caution! Once you apply a mixin globally, it will affect**every**Vue instance created afterwards. When used properly, this can be used to inject processing logic for custom options:

```
// inject a handler for `myOption` custom option
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption
    if (myOption) {
      console.log(myOption)
    }
  }
})

new Vue({
  myOption: 'hello!'
})
// => "hello!"
```

Use global mixins sparsely and carefully, because it affects every single Vue instance created, including third party components. In most cases, you should only use it for custom option handling like demonstrated in the example above. It’s also a good idea to ship them as[Plugins](https://vuejs.org/v2/guide/plugins.html)to avoid duplicate application.

## [Custom Option Merge Strategies](https://vuejs.org/v2/guide/mixins.html#Custom-Option-Merge-Strategies "Custom Option Merge Strategies")

When custom options are merged, they use the default strategy which overwrites the existing value. If you want a custom option to be merged using custom logic, you need to attach a function to`Vue.config.optionMergeStrategies`:

```
Vue.config.optionMergeStrategies.myOption = function (toVal, fromVal) {
  // return mergedVal
}
```

For most object-based options, you can use the same strategy used by`methods`:

```
var strategies = Vue.config.optionMergeStrategies
strategies.myOption = strategies.methods
```

A more advanced example can be found on[Vuex](https://github.com/vuejs/vuex)‘s 1.x merging strategy:

```
const merge = Vue.config.optionMergeStrategies.computed
Vue.config.optionMergeStrategies.vuex = function (toVal, fromVal) {
  if (!toVal) return fromVal
  if (!fromVal) return toVal
  return {
    getters: merge(toVal.getters, fromVal.getters),
    state: merge(toVal.state, fromVal.state),
    actions: merge(toVal.actions, fromVal.actions)
  }
}
```

<!--EndFragment-->
+++
title = "Vuex  Form Handling"
date = "2020-04-14"
draft = false
pinned = false
description = "Form Handling  #v-model  #obj.message  #input or change event\nTwo-way Computed Property  \n"
+++
<!--StartFragment-->

# Form Handling

<!--EndFragment-->

<!--StartFragment-->

When using Vuex in strict mode, it could be a bit tricky to use`v-model`on a piece of state that belongs to Vuex:

```
<input v-model="obj.message">
```

Assuming`obj`is a computed property that returns an Object from the store, the`v-model`here will attempt to directly mutate`obj.message`when the user types in the input. In strict mode, this will result in an error because the mutation is not performed inside an explicit Vuex mutation handler.

The "Vuex way" to deal with it is binding the`<input>`'s value and call a method on the`input`or`change`event:

```
<input :value="message" @input="updateMessage">
```

```
// ...
computed: {
  ...mapState({
    message: state => state.obj.message
  })
},
methods: {
  updateMessage (e) {
    this.$store.commit('updateMessage', e.target.value)
  }
}
```

And here's the mutation handler:

```
// ...
mutations: {
  updateMessage (state, message) {
    state.obj.message = message
  }
}
```

### [\#](https://vuex.vuejs.org/guide/forms.html#two-way-computed-property)Two-way Computed Property

Admittedly, the above is quite a bit more verbose than`v-model`+ local state, and we lose some of the useful features from`v-model`as well. An alternative approach is using a two-way computed property with a setter:

```
<input v-model="message">
```

```
// ...
computed: {
  message: {
    get () {
      return this.$store.state.obj.message
    },
    set (value) {
      this.$store.commit('updateMessage', value)
    }
  }
}
```

<!--EndFragment-->
+++
title = "Vuex   Getters"
date = "2020-04-02"
draft = false
pinned = false
description = "Getters\n1:  Property-Style Access   #store.getters \n2:   Method-Style Access\n3:  The mapGetters Helper   #mapGetters "
footnotes = ""
+++
<!--StartFragment-->

Sometimes we may need to compute derived state based on store state, for example filtering through a list of items and counting them:

```
computed: {
  doneTodosCount () {
    return this.$store.state.todos.filter(todo => todo.done).length
  }
}
```

If more than one component needs to make use of this, we have to either duplicate the function, or extract it into a shared helper and import it in multiple places - both are less than ideal.

Vuex allows us to define "getters" in the store. You can think of them as computed properties for stores. Like computed properties, a getter's result is cached based on its dependencies, and will only re-evaluate when some of its dependencies have changed.

Getters will receive the state as their 1st argument:

```
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

### [\#](https://vuex.vuejs.org/guide/getters.html#property-style-access)Property-Style Access

The getters will be exposed on the`store.getters`object, and you access values as properties:

```
store.getters.doneTodos // -> [{ id: 1, text: '...', done: true }]
```

Getters will also receive other getters as the 2nd argument:

```
getters: {
  // ...
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
```

```
store.getters.doneTodosCount // -> 1
```

We can now easily make use of it inside any component:

```
computed: {
  doneTodosCount () {
    return this.$store.getters.doneTodosCount
  }
}
```

Note that getters accessed as properties are cached as part of Vue's reactivity system.

### [\#](https://vuex.vuejs.org/guide/getters.html#method-style-access)Method-Style Access

You can also pass arguments to getters by returning a function. This is particularly useful when you want to query an array in the store:

```
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
```

```
store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
```

Note that getters accessed via methods will run each time you call them, and the result is not cached.

### [\#](https://vuex.vuejs.org/guide/getters.html#the-mapgetters-helper)The`mapGetters`Helper

The`mapGetters`helper simply maps store getters to local computed properties:

```
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
    // mix the getters into computed with object spread operator
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```

If you want to map a getter to a different name, use an object:

```
...mapGetters({
  // map `this.doneCount` to `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```

<!--EndFragment-->
+++
title = "Vuex Mutations"
date = "2020-04-03"
draft = false
pinned = false
description = "Mutations\n1:  Commit with Payload\n2:  Object-Style Commit  #type property\n3:  Mutations Follow Vue's Reactivity Rules\n4:  Using Constants for Mutation Types\n5:  Mutations Must Be Synchronous\n6:  Committing Mutations in Components\n7:  On to Actions"
+++
<!--StartFragment-->

# Mutations

<!--EndFragment-->

<!--StartFragment-->

The only way to actually change state in a Vuex store is by committing a mutation. Vuex mutations are very similar to events: each mutation has a string**type**and a**handler**. The handler function is where we perform actual state modifications, and it will receive the state as the first argument:

```
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // mutate state
      state.count++
    }
  }
})
```

You cannot directly call a mutation handler. Think of it more like event registration: "When a mutation with type`increment`is triggered, call this handler." To invoke a mutation handler, you need to call`store.commit`with its type:

```
store.commit('increment')
```

### [\#](https://vuex.vuejs.org/guide/mutations.html#commit-with-payload)Commit with Payload

You can pass an additional argument to`store.commit`, which is called the**payload**for the mutation:

```
// ...
mutations: {
  increment (state, n) {
    state.count += n
  }
}
```

```
store.commit('increment', 10)
```

In most cases, the payload should be an object so that it can contain multiple fields, and the recorded mutation will also be more descriptive:

```
// ...
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

```
store.commit('increment', {
  amount: 10
})
```

### [\#](https://vuex.vuejs.org/guide/mutations.html#object-style-commit)Object-Style Commit

An alternative way to commit a mutation is by directly using an object that has a`type`property:

```
store.commit({
  type: 'increment',
  amount: 10
})
```

When using object-style commit, the entire object will be passed as the payload to mutation handlers, so the handler remains the same:

```
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

### [\#](https://vuex.vuejs.org/guide/mutations.html#mutations-follow-vue-s-reactivity-rules)Mutations Follow Vue's Reactivity Rules

Since a Vuex store's state is made reactive by Vue, when we mutate the state, Vue components observing the state will update automatically. This also means Vuex mutations are subject to the same reactivity caveats when working with plain Vue:

1. Prefer initializing your store's initial state with all desired fields upfront.
2. When adding new properties to an Object, you should either:

* Use`Vue.set(obj, 'newProp', 123)`, or
* Replace that Object with a fresh one. For example, using the[object spread syntax](https://github.com/tc39/proposal-object-rest-spread)we can write it like this:

  ```
  state.obj = { ...state.obj, newProp: 123 }
  ```

### [\#](https://vuex.vuejs.org/guide/mutations.html#using-constants-for-mutation-types)Using Constants for Mutation Types

It is a commonly seen pattern to use constants for mutation types in various Flux implementations. This allows the code to take advantage of tooling like linters, and putting all constants in a single file allows your collaborators to get an at-a-glance view of what mutations are possible in the entire application:

```
// mutation-types.js
export const SOME_MUTATION = 'SOME_MUTATION'
```

```
// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'

const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // we can use the ES2015 computed property name feature
    // to use a constant as the function name
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

Whether to use constants is largely a preference - it can be helpful in large projects with many developers, but it's totally optional if you don't like them.

### [\#](https://vuex.vuejs.org/guide/mutations.html#mutations-must-be-synchronous)Mutations Must Be Synchronous

One important rule to remember is that**mutation handler functions must be synchronous**. Why? Consider the following example:

```
mutations: {
  someMutation (state) {
    api.callAsyncMethod(() => {
      state.count++
    })
  }
}
```

Now imagine we are debugging the app and looking at the devtool's mutation logs. For every mutation logged, the devtool will need to capture a "before" and "after" snapshots of the state. However, the asynchronous callback inside the example mutation above makes that impossible: the callback is not called yet when the mutation is committed, and there's no way for the devtool to know when the callback will actually be called - any state mutation performed in the callback is essentially un-trackable!

### [\#](https://vuex.vuejs.org/guide/mutations.html#committing-mutations-in-components)Committing Mutations in Components

You can commit mutations in components with`this.$store.commit('xxx')`, or use the`mapMutations`helper which maps component methods to`store.commit`calls (requires root`store`injection):

```
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // map `this.increment()` to `this.$store.commit('increment')`

      // `mapMutations` also supports payloads:
      'incrementBy' // map `this.incrementBy(amount)` to `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // map `this.add()` to `this.$store.commit('increment')`
    })
  }
}
```

### [\#](https://vuex.vuejs.org/guide/mutations.html#on-to-actions)On to Actions

Asynchronicity combined with state mutation can make your program very hard to reason about. For example, when you call two methods both with async callbacks that mutate the state, how do you know when they are called and which callback was called first? This is exactly why we want to separate the two concepts. In Vuex,**mutations are synchronous transactions**:

```
store.commit('increment')
// any state change that the "increment" mutation may cause
// should be done at this moment.
```

<!--EndFragment-->
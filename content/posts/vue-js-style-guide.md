+++
title = "Vue.js  Style Guide"
date = "2020-03-26"
draft = false
pinned = false
description = "Style Guide\n1:  Rule Categories  #Priority A: Essential  #Priority B: Strongly Recommended   #Priority C: Recommended  #Priority D: Use with Caution \n2:  Priority A Rules: Essential (Error Prevention)  #Multi-word component names  #Component data  #Prop definitions"
+++
<!--StartFragment-->

# Style Guide

This is the official style guide for Vue-specific code. If you use Vue in a project, it’s a great reference to avoid errors, bikeshedding, and anti-patterns. However, we don’t believe that any style guide is ideal for all teams or projects, so mindful deviations are encouraged based on past experience, the surrounding tech stack, and personal values.

For the most part, we also avoid suggestions about JavaScript or HTML in general. We don’t mind whether you use semicolons or trailing commas. We don’t mind whether your HTML uses single-quotes or double-quotes for attribute values. Some exceptions will exist however, where we’ve found that a particular pattern is helpful in the context of Vue. 

Finally, we’ve split rules into four categories:

## [Rule Categories](https://vuejs.org/v2/style-guide/#Rule-Categories "Rule Categories")



### [Priority A: Essential](https://vuejs.org/v2/style-guide/#Priority-A-Essential "Priority A: Essential")

These rules help prevent errors, so learn and abide by them at all costs. Exceptions may exist, but should be very rare and only be made by those with expert knowledge of both JavaScript and Vue.

### [Priority B: Strongly Recommended](https://vuejs.org/v2/style-guide/#Priority-B-Strongly-Recommended "Priority B: Strongly Recommended")

These rules have been found to improve readability and/or developer experience in most projects. Your code will still run if you violate them, but violations should be rare and well-justified.

### [Priority C: Recommended](https://vuejs.org/v2/style-guide/#Priority-C-Recommended "Priority C: Recommended")

Where multiple, equally good options exist, an arbitrary choice can be made to ensure consistency. In these rules, we describe each acceptable option and suggest a default choice. That means you can feel free to make a different choice in your own codebase, as long as you’re consistent and have a good reason. Please do have a good reason though! By adapting to the community standard, you will:

1. train your brain to more easily parse most of the community code you encounter
2. be able to copy and paste most community code examples without modification
3. often find new hires are already accustomed to your preferred coding style, at least in regards to Vue

### [Priority D: Use with Caution](https://vuejs.org/v2/style-guide/#Priority-D-Use-with-Caution "Priority D: Use with Caution")

Some features of Vue exist to accommodate rare edge cases or smoother migrations from a legacy code base. When overused however, they can make your code more difficult to maintain or even become a source of bugs. These rules shine a light on potentially risky features, describing when and why they should be avoided.

## [Priority A Rules: Essential (Error Prevention)](https://vuejs.org/v2/style-guide/#Priority-A-Rules-Essential-Error-Prevention "Priority A Rules: Essential (Error Prevention)")

### [Multi-word component namesESSENTIAL](https://vuejs.org/v2/style-guide/#Multi-word-component-names-essential "Multi-word component names essential")

**Component names should always be multi-word, except for root`App`components, and built-in components provided by Vue, such as`<transition>`or`<component>`.**

This[prevents conflicts](http://w3c.github.io/webcomponents/spec/custom/#valid-custom-element-name)with existing and future HTML elements, since all HTML elements are a single word.

#### [](https://vuejs.org/v2/style-guide/#Bad "Bad")Bad

```
Vue.component('todo', {
  // ...
})
```

```
export default {
  name: 'Todo',
  // ...
}
```

#### [](https://vuejs.org/v2/style-guide/#Good "Good")Good

```
Vue.component('todo-item', {
  // ...
})
```

```
export default {
  name: 'TodoItem',
  // ...
}
```

### [Component dataESSENTIAL](https://vuejs.org/v2/style-guide/#Component-data-essential "Component data essential")

**Component`data`must be a function.**

When using the`data`property on a component (i.e. anywhere except on`new Vue`), the value must be a function that returns an object.

#### Detailed Explanation

#### [](https://vuejs.org/v2/style-guide/#Bad-1 "Bad")Bad

```
Vue.component('some-comp', {
  data: {
    foo: 'bar'
  }
})
```

```
export default {
  data: {
    foo: 'bar'
  }
}
```

#### [](https://vuejs.org/v2/style-guide/#Good-1 "Good")Good

```
Vue.component('some-comp', {
  data: function () {
    return {
      foo: 'bar'
    }
  }
})
```

```
// In a .vue file
export default {
  data () {
    return {
      foo: 'bar'
    }
  }
}
```

```
// It's OK to use an object directly in a root
// Vue instance, since only a single instance
// will ever exist.
new Vue({
  data: {
    foo: 'bar'
  }
}
```



<!--EndFragment-->
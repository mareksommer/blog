# watchers in Vue Composition API

To replace watch option in Composition API we use watch function. Which you have import from vue.

Watch function allows us to register watcher inside the setup function.

Watch function accepts two parameters.
1. Dependencies to watch
2. Callback function to be called when dependency changes. The callback function is automatically called by Vue with tow arguments - newValue and oldValue

Watcher can watch for multiple dependencies. In that case we define dependencies as an Array and args provided to callback function are also arrays containing all the dependency values.


```tsx
import { watch, ref} from 'vue';

export default {
  setup() {
    const number = ref(0);

    watch(number, function(newValue, oldValue) {
      console.log('newValue', newValue)
      console.log('oldValue', oldValue)
    })

    const secondNumber = ref(1)
    watch([number, secondNumber], function(newValues, oldValues) {
      console.log('new number', newValues[0])
      console.log('old number', oldValues[0])

      console.log('new secondNumber', newValues[1])
      console.log('old secondNumber', oldValues[1])
    })
  }
}

```

## props watcher

If we want to watch for changes in props value. We can either use props as dependecy, but in that case watcher will be called everytime any of the prop changes. It may or may not be what we want. If we want our watcher to be dependant only on one prop value. The we can't simly use props.someProp because props are refs so they are reactive but not the value itself. So we need to use the toRefs() function to make object with refs from props and assign the one prop value to the watcher.

```tsx 

import { watch, toRef } from 'vue';

export default {
  setup(props: { name: string, age: number }) {
    const { name } = toRefs(props)

    watch(name, function(newValue, oldValue) {
      console.log('newValue', newValue)
      console.log('oldValue', oldValue)
    })
  }
}

```
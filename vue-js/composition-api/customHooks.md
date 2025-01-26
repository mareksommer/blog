# Custom hooks - concept of reusing code across components in Composition API

Custom hooks are simply javascript functions that use Composition API and of course js code. That can be later reused in components.

## Example

```tsx
//custom hook useCounter.js
import { ref } from 'vue';

export default function useCounter(initCount = 0) {
  const counter = ref(initCount)

  const setCounter = function(value) {
    counter.value = value
  }

  //here we can return object or array; Array is in my opinion slightly better because in array destructing in component we can rename newly constructed variables more easily
  return [counter, setCounter]
}

//someComponent.vue
import useCounter from '../hooks/useCounter'

export default {
  setup() {
    const [counter, setCounter] = useCounter(1)
    ...
  }
}
```

We can resuse our custom hook in multiple components and we've got benefit over mixin, in that our hook accepts paramters. Beacause it is simple js function. This is declarative programming instead of imperative programming using mixins and Options API.

This is for me the biggest advatage of using Composition API. The reusability a readibily of custom hooks is much better that using mixins. Mixins in bigger apps starts to be tricky to maintain and understant where does which option comes from. Here we are using simple javascrpt functions, and this declarative approach resulst in cleaner easier to understand components code.

Custom hooks encourage developer to separate functionality that comes together into smaller units (hooks) and reuse them over the application.
# Provide/Inject functionality in Composition API

Provide, Inject are functions that we can import and use in Composition API.

Provide function accepts two arguments:
1. key: string - key identifier of provided value
2. value: any - the provided value

Inject functino accepts key: string arg - to define which provided value we want to access

```tsx 
import { provide, inject, ref } from 'vue';

export default {
  setup() {
    cosnt provideRefValue = ref('Some value')
    provide('someCustomProvideValue', provideRefValue) // we can pass ref() as provide value - it will keep its reactivity throught the app
  }
}

// some child component
export default {
  setup() {
    cosnt injectValue = inject('someCustomProvideValue') // its gonna be ref() object, keeping its reactivity
  }
}

```

> It is best practice to update injected value only in provide side of the application. To avoid confusion, when using provide/inject. In the inject part, think of the value as read only.
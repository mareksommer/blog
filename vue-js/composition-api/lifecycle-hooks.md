# Lifecycle hooks of the component in Composition API

## beforeCreate, created
The **beforeCreate** and **created** lifecycle hooks are in Composition API replaced by **setup** function itself. *The setup function is called at the same time as created lifecycle hook would be.*

##  beforeMount, mounted
For **beforeMount** and **mounted** lifecycle hooks, Composition API provides **onBeforeMount**, **onMounted** functions.

## beforeUpdate, updated
Composition API exposes functions **onBeforeUpdate** and **onUpdated**

## beforeUnmount, unmounted
Composition API exposes functions **onBeforeUnmount** and **onUnmounted**

## Usage example

```tsx

import { onMounted } from 'vue'

export default {
  setup function() {
    onMounted(function() {
      // this code will be run on mount event
      console.log('mounted')
    })
  }
}

```

## Lifecycle hooks compolete list:
- onBeforeMount
- onMounted
- onBeforeUpdate
- onUpdated
- onBeforeUnmount
- onUnmounted
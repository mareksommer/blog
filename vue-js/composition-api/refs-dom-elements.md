# Using Refs as referencies to DOM elements in Composition API

Equivalent of **$refs**from Options API is same **ref()** function as we know it from handling elementary state values.

```tsx
<template>
  <input type="text" ref="inputRef" />
</template>

import { ref } from 'vue';

<script setup>
  const inputRef = ref(null);

  function getInputValue() {
    // notice: inputRef.value points to the input DOM element, to access its value we have to chain another .value call
    return inputRef.value.value
  }

  return {
    inputRef
  }

</script>
```
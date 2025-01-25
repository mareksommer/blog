# Computed function

To provide computed like functinality in Composition API. Vue introduces computed function, which you have to import before using.

Computed accepts function as its argument.

Vue will automaticaly inspect the functino we provide to the computed function and keeps track of used arguments and its changes for us. To autmaticly coputed new return value when its dependencies change.

Computed function is Ref, you can access its value. But the value is read only. You cannot change it from outside.

```tsx
import { computed, ref } from 'vue';

<script setup>
  const firstName = ref('Marek')
  const lastName = ref('Sommer')

  const name = computed(function() {
    return `${firstName.value} ${lastName.value}`
  })

  return { name }
</script>
```
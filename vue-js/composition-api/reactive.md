# Reactive -  to store reactive objects

Reactive is feature of Composition API, which intent is to work with objects. It accepts only objects as its value.

Reactive allows us to work with state objects as regular javascript objects. With benefit of being reactive in Vue sence.

```tsx
import { reactive } from vue

<srcipt setup>
  const user = reactive({
    name: 'Marek',
    position: 'Web developer'
  })

  // for updates, we don't use .value property
  user.name = 'Marcus'
</script>
```
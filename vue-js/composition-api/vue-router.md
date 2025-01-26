# Vue Router

Vue router gives us hooks for Composition API. 
- useRouter - to access the router object
- useRoute - to access the object containing current router informations
- useLink

```tsx
import { useRouter, useRoute } from 'vue-router';

export default {
  setup() {
    const router = useRouter()
    router.push('/some-address')

    const currentRoute = useRoute()
    console.log('current route', currentRoute)
  }
}

```
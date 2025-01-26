# Accessing props in setup method of Composition API

Our props defined in props options are passed as argument of setup function.

> Vue adds props as argument of the Composition API setup function

Vue automatically setup the props arg for us, so we have always access to props. If there are none, props object is just empty object.

```tsx
<script>
  import { computed } from 'vue';
  export default {
    props: ['name'],
    setup(props) {
      const greetings = computed(function() {
        return `Hello ${props.name}`
      })

      return { greetings }
    }
  }
</script>

```
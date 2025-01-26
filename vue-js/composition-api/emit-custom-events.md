# Emiting custom events in Composition API

Vue automatically provides setup function with two arguments: **props** and **context**.

> context object param contains **attr**, **emit**, **slot** properties

```tsx
<script>
  export default {
    setup(props, context) {
      const args = { someAttr: 'value' }
      context.emit('custom-event', args) // equivalent to this.$emit('custom-event', args) in options API
    }
  }
</script>

```
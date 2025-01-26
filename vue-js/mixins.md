# Mixins

Mixins are concept of reusing code across multiple components using Options API.

To setup mixin, you prepare js file with code you want to share between components. It would be some part of components exported object, containing: methods, data, computed props, watchers, anything you want, exept for registered components. That can't be part of the mixin.
Then in the component, where you want to use mixin, you declare mixin option as array, where you put your mixins.

## Example

```tsx

// mixin: mixin-example.js
export default {
  data() {
    return {
      counter: 0
    }
  },
  methods: {
    link(e, link) {
      ...
    },
  }
}


// component using mixin
import someComponent from './someComponent.vue'
import mixinExample from '../mixins/mixin-example.js'
export default {
  components: { someComponent },
  mixins: [mixinExample]
}
```

## Merging options

In case you define same option in mixin and in the component. Vue will merge the option. By option we meain data(), methods etc. If component defines same option as mixin, the components definition overwrites the mixin.

## Global mixins

We can also define global mixins, which will be used across the aplication in every component.
Global mixins are registered in app root file (main.js)

```tsx
//main.js
....
import App from './App.vue'
import globalMixin from '../mixins/global-mixin.js'

const app = createApp(App)

app.mixin(globalMixin)
....

```

## Disadvantages of mixins

> Mixins provides way to clean up code of the components, but with that comes, also cost of loosing visual control over what options are defined for the component. You have to inspect every used mixin, to find out where does come method or property comes from. With global mixins and merging. In large apps it can become tricky to debug and understand what is going on in the component. 
# Refs - replacement for data()

To use ref in the component you need to first import it and then use inside the components setup function.

> Ref is a function that creates reference to a reactive value.

```tsx
import { ref } from vue;

export default {
  setup() {
    // this will create reactive object, that Vue watch for changes
    const name = ref('Marek');

    // ref object stores its value in value prop. to update the ref we need to update its value property
    name.value = 'Marcus' 

    // setup function must return object containing all the values we want to be able to access in the template
    return { name }
  }
}
```

> We can use alternative declaration of setup function. <script setup></script> then we don't need to return object from setup function.

Ref suits best for storing simple values such as strings, booleans. It can be also used for storing reactive objects, but in that case you need to return whole object in return object of setup function. In order for Vue to be able to track changes in the object and update template.

> For storing comlex state as object, it's better to use **Reactive**

## Reactivity
> **Ref** and **Reactive** both creates reactive objects. Important to know is that Vue sees as reactive the whole objects. Not their values. That is the reason, why we have to always export whole objects not just partial object values.

Vue offers helper methods to find out if value is reactive or not. You can use **isRef()** and **isReactive()** to check if value is reactive or it is simple javascript value.

Another helper function Vue provides is toRefs(), that makes refs of each object property, that was passed to that function and returns object containing them.
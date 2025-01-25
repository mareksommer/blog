# Composition API - Big picture

**Composition API** was introduced in Vue version 3. The inspiration was clearly in React hooks.
The old way of defining components in Vue2 is called **Options API**.

Composition API is not meant to be replacement for Options API. You can still use Options API in Vue3 apps.

Compostion API has to be placed into components **setup function**.

## Benefits of Compostion API
The intent for introducing Composition API was to *enable writing more cohesive code where you find logic that belongs together in the same place together*. Second benefit of using Composition API is *better reusability of code between components*.
 
## Composition API replaces these options:
- data
- method
- computed
- watch
- lifecycle events
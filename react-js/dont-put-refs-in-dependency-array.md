# Don't put refs in dependency array

> **Important note:** useRef is similar to useState except changing the value doesn't trigger a re-render.

**TLDR**
> Change in ref value does not cause re-render the component. React does not keep track of **ref.current** value. Therefore adding **ref.current** value into dependency array is no use. Change in **ref.current** value doesn't fire hooks callback function.

React does not keep track of the **ref.current** value. Referencing and mutation of the value is up to you as developer. 

Referencing DOM nodes is just one of the usecases for **useRef** hook. But since it is so common. React will set the **current** value for you when you pass a **ref** prop to an DOM element.

What differentiates a **ref** from just a regular variable outside the component. Is that **useRef** ensures that the value is associated with a particular instance of a component.

The purpose of a dependency array is to let React run provided function again when some value of the dependency array changes, each render. React can't know that the value changed if a change doesn't trigger a render. 

## Example
In example bellow, we have basic counter button, that uses **useRef** hook to store the counter state. You can click the button how many times you want, but it will not fire rerender the component and it will not display updated counter value. The log inside **useEffect** will not be called also, just once for the initial render.

```tsx
function Counter() {
  const countRef = useRef(0)

  useEffect(() => {
    console.log(countRef.current)
  }, [countRef.current])

  const increment = () => (countRef.current += 1)
  return <button onClick={increment}>Click me {countRef.current}</button>
}
```

> Don't put abything that won't trigger a re-render when updated into the dependency array. 

> Don't expect any change in such values to result in the effect callback getting called. If you need the callback to be called when those things change, then put it in **useState** (or **useReducer**).

## Conclusion

You shouldn't list a ref in your useEffect dependency array, because it's an indication that you want the effect callback to re-run when a value is changed, but you're not notifying React when that change happens. 

If you don't want to re-run callback when the the value is changed, then don't put in the dependency array. If you want to re-run when value changes use **useState** or **useReducer** instead.
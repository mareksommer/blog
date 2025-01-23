# flushSync
React state updates happens in batches. It is more effective for React to wait until bigger chunk of your code is proccessed and then to rerender all the state updates in one render. Than to rerender right when state update occurs.

This can sometimes lead to problems, when you relies on state update and rerender, and forget that this happens asynchroniously. 

If you need to be sure that some state update will happen before your next actions. You need to force React to update state synchronously just when it comes across your state update.

This is the purpose of flushSync function from react-dom package. To force React to flush any pending work and update the DOM synchronously.


## Example
In the code below, you can see example of usage flushSync. 

Component called MyComponent renders html button element that, when clicked display the input field. We also want to set focus on displayed input, but if you use setShow to udpate the state, this will happen some time after the focus() method call on inputRef is fired. So the focus method is fired before the elment is displayed and so the element after display will not be focused. To solve the issue we need to force React to update the state directly when we call setShow in onClick event handler. We accomplish that by using flushSync function.

```tsx
import { flushSync } from 'react-dom'

function MyComponent() {
  const inputRef = useRef<HTMLInputElement>(null)
  const [show, setShow] = useState(false)

  return (
    <div>
      <button
        onClick={() => {
          flushSync(() => {
            setShow(true)
          })
          inputRef.current?.focus()
        }}
      >
        Show
      </button>
      {show ? <input ref={inputRef} /> : null}
    </div>
  )
}
```
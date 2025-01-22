# useSyncExternalStore hook

To synchronize external state with state managed by React app we use useSyncExternalStore hook.

## Basic API

```tsx
const snapshot = useSyncExternalStore(
	subscribe,
	getSnapshot,
	getServerSnapshot, // optional
)
```

- **subscribe** is a function that takes a callback and returns a cleanup function. The callback is called whenever the external store changes to let React know it should call **getSnapshot** to get the new value.
- **getSnapshot** is a function that returns the current value of the external store.
- **getServerSnapshot** is an optional function that returns the current value of the external store from the server. This is useful for server-side rendering and rehydration. If you don't provide this function, then React will render the nearest Suspense boundary fallback on the server and then when the client hydrates, it will call getSnapshot to get the current value.

## Example

Example would be, component that displays your current location, via geolocation API. The geolocation API is not part of React, so it is not aware of its state. To synchronize internal React state with geolocation API. We need to use **useSyncExternalStore** hook.

```tsx
import { useSyncExternalStore } from 'react'

type LocationData =
	| { status: 'unavailable'; geo?: never }
	| { status: 'available'; geo: GeolocationPosition }
// this variable is our external store!
let location: LocationData = { status: 'unavailable' }

// React will use this function to synchronize its state with outside world
function subscribeToGeolocation(callback: () => void) {
  //the watchPosition is part of browsers Geolocatoin API and is used to register a handler function that will be called automatically each time the position of the device changes.
	const watchId = navigator.geolocation.watchPosition((position) => {
		location = { status: 'available', geo: position }
		callback()
	})
  // cleanup function
	return () => {
		location = { status: 'unavailable' }
		return navigator.geolocation.clearWatch(watchId)
	}
}

function getGeolocationSnapshot() {
	return location
}

function MyLocation() {
	const location = useSyncExternalStore(
		subscribeToGeolocation,
		getGeolocationSnapshot,
	)
	return (
		<div>
			{location.status === 'unavailable' ? (
				'Your location is unavailable'
			) : (
				<>
					Your location is {location.geo.coords.latitude.toFixed(2)}
					{'°, '}
					{location.geo.coords.longitude.toFixed(2)}
					{'°'}
				</>
			)}
		</div>
	)
}

```
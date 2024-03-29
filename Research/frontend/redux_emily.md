# Why Redux?

Redux is a state management library for JavaScript applications to manage the state of applications in a predictable way.
It provides simplier, maintainable code and makes debugging easier.
It is used in conjunction with React and other JavaScript frameworks.
To use Redux Toolkit in a React application, you can follow these steps:

1. Install the Redux Toolkit library using npm or yarn.
2. Create a Redux store using the 'configureStore' function provided by Redux Toolkit.
3. Use the 'Provider' component from the react-redux library to make the Redux store available to the rest of your application.
4. Use the 'useSelector' and 'useDispatch' hooks from 'react-redux' to access the state and dispatch actions in your components.

An example code snippet:

```javascript
import { configureStore } from '@reduxjs/toolkit'
import { Provider, useSelector, useDispatch } from 'react-redux'

// Define a new Redux slice using 'createSlice()' function
const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
  },
})

// Create a Redux store using 'configureStore()' function
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
  },
})

// Wrap your app in the 'Provider' component from the 'react-redux' library  to make the Redux store available
function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  )
}

// Use the 'useSelector()' and 'useDispatch()' hooks to access the state and dispatch actions to and from the Redux store
function Counter() {
  const count = useSelector((state) => state.counter.value)
  const dispatch = useDispatch()

  return (
    <div>
      <button onClick={() => dispatch(counterSlice.actions.increment())}>
        Increment
      </button>
      <span>{count}</span>
      <button onClick={() => dispatch(counterSlice.actions.decrement())}>
        Decrement
      </button>
    </div>
  )
}
```

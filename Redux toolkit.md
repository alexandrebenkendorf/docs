

# Redux Tookit

[Tutorial](https://medium.com/stackanatomy/redux-is-dead-long-live-redux-toolkit-11dd79e89993)

## Step 1: Install Packages

Install via npm

```
npm i @reduxjs/tookit react-redux
```

Via Create React App 

```
npx create-react-app my-app --template redux
```

## Step 2: Create & Initialize Store

Create file `store.js` in `src` folder and add the following code in it:

```
import { configureStores } from '@reduxjs/tookit'

export default configureStore({
	reducer: {} // add reducers here
})
```

The `configureStore` here replaces the original `createStore` from Redux. Unlike `createStore`, `configureStore` from Redux Toolkit not only creates a store, but it can also accept reducer functions as arguments and automatically sets up the Redux DevTools Extension for easy debugging.


## Step 3: Provide Store in React app


In our `index.js`file, we import the `Provider`and our `store.js`like so:

```
import store from './store'
import { Provider } from 'react-redux' 

ReactDOM.render(
	<Provider store={store}>
		<App />
	</Provider>,
	document.getElementById('root')
)
```

## Step 4: Write Reducers and Actions

```
import { createSlice } from '@reduxjs/toolkit'

export const counterSlice = createSlice({
	name:'counter',
	initialState:{
		value: 0
	},
	reducers:{
		increase: (state) => {
			state.value += 1
		},
		decreace: (state) => {
			state.value -= 1
		}
	}
})

// each case under reducers becomes an action
export const { increase, decrease } = counterSlice.actions

export default counterSlice.reducer

```

## Step 5: Import Reducer to Store

In the `store.js` add the reducers

```
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from '.counterSlice'

export default configureStore({
	reducer:{
		counter: counterReducer
	}
})
```

## Step 6: Use

```
import { useSelector, useDispatch } from 'react-redux'
import { decrease, increase } from './counterSlice'

export const Counter = () =>{
	const count = useSelector((state)=>state.counter.value)
	// in our slice, we provided the name property as 'counter'
	// and the initialState with a 'value' property
	// thus to read our data, we need useSelector 
	// to return the state.counter.value
	
	const dispatch = useDispatch()
	
	
	return (
		<div>
			<p>{count}</p>
			<button onClick={()=> dispatch(increase())}>Increase</button>
			<button onClick={()=> dispatch(decrease())}>Decrease</button>
		</div>
	)
}


```


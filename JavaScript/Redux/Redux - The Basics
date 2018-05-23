# Redux - The Basics

## The Building Blocks
### Action

- JSON Object
- Needs to have a `type` property that indicates the type of action being performed
- If the application grows in its complexity, it's better to define the types as string constants and also consolidate them into a separate module

### Action Creator

- Exactly as name suggests - functions that create Actions
```javascript
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  };
}
```
- Avoid conflating the terminology between Action and Action Creator
- Unlike Flux, Action Creators in Redux does not dispatch the Actions. Need to explicitly call the `dispatch()` function.
- You can create **Bound Action Creator** that will create and dispatch the Actions at once
```javascript
const boundAddTodo = text => dispatch(addTodo(text));
```
- `dispatch()` is often called by some sort of a helper rather than directly, like `connect()` from [react-redux](https://github.com/reactjs/react-redux)
- You can use `bindActionCreator()` to bind many Action Creators to a `dispatch()` function

### Reducer

- Reducers define *how* states should change in response to Actions. Remember Actions only define *what* happened.
- A Reducer is a **pure function** that takes the previous state and an action, and returns the new state.

### Store
- Holds the State and allows other parts of the application to access the state with `store.getState()`
- Allows dispatching of Actions via `store.dispatch(action)` which the Reducers will then change the state accordingly
- Registers listeners and returns a callback that will handle the unregistering of the listeners via `store.subscribe(listener)`

## The Data Flow

1. Dispatch an action to the Store
2. The store will pass on the action to the root reducer along with the current State
3. Root reducer will slice up the State and pass on the action to its children reducers, which in turn will be handling its bit of state
4. After all of the reducers in the tree have processed the action and changed its share of the state as needed, the store will be returned the new State
5. Any listeners subscribing to the store can call `store.getState()` to access the updated State and do whatever they need to do - (log? or rerender the UI)


## Topics to look up
- ref in react
- using bind in render creates a new function every time a component is re-rendered in react - which is quite frequent

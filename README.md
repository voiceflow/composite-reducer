Composite Reducer
=========================

[![npm version](https://img.shields.io/npm/v/composite-reducer.svg?style=flat-square)](https://www.npmjs.com/package/composite-reducer)
[![npm downloads](https://img.shields.io/npm/dm/composite-reducer.svg?style=flat-square)](https://www.npmjs.com/package/composite-reducer)

[What are Reducers?](https://css-tricks.com/understanding-how-reducers-are-used-in-redux/)

Allows reducers for specific properties of a state - better organization for reducers of complex or deeply nested objects.

> Works well with state management solutions such as [Redux](https://redux.js.org/) or [React Context](https://reactjs.org/docs/context.html) + [useReducer](https://reactjs.org/docs/hooks-reference.html#usereducer) hook.

Similar to the [`combineReducers`](https://redux.js.org/api/combinereducers) function in redux. But instead of combining many equal top level reducers, has a main reducer and attaches other reducers for properties of the main state.

## Why?
Say there is a state that looks like this:
```
{
    name: "voiceflow",
    type: "startup",
    settings: {
        website: "voiceflow.com"
    }
}
```
If a reducer is created for this state, to change the `website`, I would need a dedicated action to update it, and construct a new state with something messier like this: 
```
{   
    ...state, 
    settings: { 
        ...state.settings, 
        website: action.payload 
    }
}
``` 

With `composite-reducer`, the `settings` sub-state can be abstracted into it's own dedicated reducer, separate from the main one.
```
const reducer = compositeReducer(mainReducer, { 
    settings: settingsReducer 
});
```
The dedicated reducer updates/works with a smaller, more concise state.

The main reducer can still act on the property if it has to.

Along with [`combinedReducer`](), this encourges the overall reducer to be cleaner/better organized.

## Example

```
import compositeReducer from 'composite-reducer';

const mainReducer = (state, action) => {
    // do reducer stuff here
    return state;
};
const propertyOneReducer = (state, action) => {
    // state is in the shape of propertyOne
    // do reducer stuff here
    return state;
};

const propertyTwoReducer = (state, action) => {
    // state is in the shape of propertyTwo
    // do reducer stuff here
    return state;
};

const reducer = compositeReducer(mainReducer, {
    propertyOne: subpropertyOneReducer,
    propertyTwo: subpropertyTwoReducer,
})
```

## Installation

To use `composite-reducer`, install it as a dependency:

```bash
# If you use npm:
npm install composite-reducer

# Or if you use Yarn:
yarn add composite-reducer
```

This assumes that you’re using a package manager such as [npm](http://npmjs.com/).
## License

[MIT](LICENSE.md)

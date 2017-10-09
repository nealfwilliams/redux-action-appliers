## Redux Action Appliers
This library is a utility to make testing redux actions simpler.  Essentially, it exposes an interface that 
accepts an initial state and a sequence of action creator calls.  The action creators will wrapped in a specified reducer 
call and called sequentially, iteratively updating the passed initial state.  The array of subsequent states will be returned 
in reverse order, starting with the final state (returned after the last action is passed to the reducer).

## Installation                                         
This package is available via npm.
```
npm install --save redux-action-appliers
yarn add redux-action-appliers
```

## Usage

#### Example: 
```javascript
import { ChainedActionApplier } from 'redux-action-appliers';

const initialState = {
  value: 'INITIAL'
};

const simpleActionCreator = (value) => ({
   type: 'SIMPLE_ACTION_CREATOR',
   value
});

const simpleReducer = (state, action) => {
  return {value: action.value}
};

const actionCreators = {
  simpleActionCreator
};

let applier = new ChainedActionApplier(actionCreators, simpleReducer);

let [state3, state2, state1] = applier.apply(
  initialState,
  {name: 'simpleActionCreator', args=['test1']},
  {name: 'simpleActionCreator', args=['test2']},
  {name: 'simpleActionCreator', args=['test3']},
);

state3.value === 'test3'; // true
state2.value === 'test2'; // true
state1.value === 'test1'; // true
```

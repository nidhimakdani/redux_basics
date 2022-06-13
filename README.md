# Getting Started with Create React App
REDUX - LEARNINGS - Following tutorial of dipesh malvia (YouTube - https://youtu.be/0W6i5LYKCSI) (author NIDHI MAKDANI)
Steps- 
1. npx create-react-app redux_app
2. npm i axios and  npm i react-router-dom
3. remove boiler plate code 
delete files (From public folder - logo,manifest and robots.txt and from src folder App.test.js, index.css,logo.svg,reportWebVirtuals.js,setupTests.js and remove the reportWebVitals() from index.js) Now we can see clear screen 
4.Remove <header>to</header> from app.js file and just write Hello Now we can see simple hello written on sceen 
5.Intall redux using command - npm install redux react-redux

Now Creating Folder Structure for redux !
-in src folder

1.containers (gonna contain all the components)

2.redux (files related to redux )
under redux folder create three mode folders 
1.reducer 
2.actions - productActions.js
3.constants - action-types.js

NOW LET'S CREATE ACTION TYPES FIRST IN ACTION TYPE FILE WE'LL ADD THIS CODE 
action-types.js 

export const ActionTypes = {
    SET_PRODUCTS : "SET_PRODUCTS",
    SELECTED_PRODUCT : "SELECTED_PRODUCTS",
    REMOVE_SELECTED_PRODUCT: "REMOVE_SELECTED_PRODUCT",
}

NOW IN PRODUCT ACTION FILE WE NEED TO CREATE THREE ACTIONS CODE IS GIVEN BELOW 
productActions.js

import { ActionTypes } from "../constants/action-types"
export const setProducts = (products) => {
    return{
        type: ActionTypes.SET_PRODUCTS,
        payload : products, 
    }
}
export const selectedProduct = (product) => {
    return{
        type: ActionTypes.SELECTED_PRODUCT,
        payload : product, 
    }
}

//THIRD ONE WE"LL CREATE LATER 

NOW GO TO REDUCER FOLDER AND CREATE FILE index.js AND productReducer.js 
in productReducer.js file we are gonna create REDUCER REDUCER always takes initial state and action as parameter 
productReducer.js 

    import { ActionTypes } from "../constants/action-types"

    const initialState = {
        products:[{
            id: 1,
            title:"Nidhi",
            category : " Programmer"
        }]
    }

    export const productReducer = (state = initialState , action,{type,payload}) => {
        switch(type){
            case ActionTypes.SET_PRODUCTS:
                return state;
            default :
                return state;
        }
    }

while creating application there is gonna be multiple reducer so we have to combine all that reducer in index.js 
index.js 

import { combineReducers } from 'redux';
import { productReducer } from './productReducer';

const reducer = combineReducers({
    allProducts : productReducer, 
})

export default reducer 

TILL NOW WE HAVE CREATED THE ACTIONS WE HAVE CREATED THE ACTION TYPES AND WE HAVE CREATED AND COMBINED REDUCERS 

now go to store.js file src->store.js 

create store takes multiple argument 
arg1 - reucer 
arg2 - middleweare (we are not using in his app)
arg3 - state in our case {} empty state 

now too see ou redux app is working or not in browser we have to add extention (window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()) put it as 4th argument 

store.js
import { legacy_createStore as createStore } from "redux";
import reducer from "./redux/reducer/index"

const store = createStore(reducer,{},window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());

export default store; 

WHEN YOU GO TO INSPECT AND CHECK THERE IS NO STORE BECAUSE OUR REACT APPLICATION IS NOT LINKED WITH REDUX TO LINK THAT FILE WITH REDUX IN MAIN index.js FILE ADD THIS CODE 

import { Provider } from "react-redux"
import store from "./store"

< Provider store={store}><App /> </Provider>

your index.js gonna look like this 

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { Provider } from "react-redux";
import store from "./redux/store";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);


NOW YOU CAN SEE THE DATA IN INSPECT REDUX NOW WHAT IF WE WANT TO ACCESS THAT DATA SO LET'S DO THAT ![Capture](https://user-images.githubusercontent.com/50043246/173302076-868449ed-aad3-451e-aca5-a0bc5c34a5f6.PNG)


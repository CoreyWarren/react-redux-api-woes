# react-redux-api-woes
Problem solving API woes in React/Redux.

## Relevant components:

* React

* Redux

* createAsyncThunk()

* createSlice()

* useDispatch()

* useEffect()

#

1) Did you export your createAsyncThunk const out of your .js file which contains your 'get' or 'post' function? (i.e.: Does your getProducts createAsyncThunk() function get exported?)

2) After exporting your createAsyncThunk, did you import it properly into your index.js or App.js or StorePage.js?

3) After importing there, did you create your useEffect function inside of App.js or your relevant containing page file (i.e.: StorePage.js)?

```js
useEffect(() => {
    //dispatch(checkAuth());
  }, []);

```

4) Inside your useEffect function, within your dispatching code, did you remember to add ellipses to your action inside the dispatcher?

```js
//useEffect(() => {
    dispatch(checkAuth());
  //}, []);
```

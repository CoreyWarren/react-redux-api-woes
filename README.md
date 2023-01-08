# react-redux-api-woes
Problem solving API woes in React/Redux.

## Relevant components:

* React

* Redux

* createAsyncThunk()

* createSlice()

* useDispatch()

* useEffect()

# Getting 'Actions' and API Data to actually show up on your page and in your Redux debugger

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

5) If you're not doing 'extraReducers', then ensure that you are properly using your slices (i.e.: userSlice, productSlice) and their proper formatting with your version of react.

```js
//...
reducers: {
    resetRegistered: state => {
      state.registered = false;
    },
  },

  extraReducers: builder => {
    builder
      // registration:
      .addCase( register.pending, state => {
          // Do what we need to the state within this reducer
          // Because we have immer, we can adjust the state directly
          //  instead of returning data.
          state.loading = true; // loading is used for spinners/progress indicators
      })
      .addCase( register.fulfilled, state => {
        // 'fulfilled' means everything was successful
        // so we can set this user to be registered.
        // they will later be redirected to the login page.
        state.loading = false;
        state.registered = true;
      })
      .addCase( register.rejected, state => {
        state.loading = false;
      })
     }
//...

6) For complex JSON data, while it generally should be as simplified as possible if you can help it, there are ways to map that data into an array of objects and interpret those objects.

```js
const StorePage = () => {
    const dispatch = useDispatch();

    useEffect(() => {
        dispatch(getProducts());
    }, [])

    const {products, loading} = useSelector(state => state.products);
    if(products == null) {
        return(
        <h1> Loading... </h1>
        )
    } else {
        const products_array = products.map(item => {
            const { title, description, image_preview, base_cost } = item;
            return {
                title,
                description,
                image_preview,
                base_cost
            };
        });
       return (
       <div className="list_item">
            Title: {products_array[0].title}
            Desc: {products_array[0].description}
            Image: {products_array[0].image_preview}
            Base Cost: {products_array[0].base_cost}
        </div>
        );
    }
}
       

```

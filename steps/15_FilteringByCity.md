## Steps
1. Create a `<SideBar />` component that will render a vertical sidebar (or you can do a horizontal bar if you prefer).
2. Add a `<Link />` for each city in your sidebar. The links should go to `?query={"city": "<your_city_name>"}` (where `<your_city_name>` matches the value in the select dropdown in your `<AddProperty />` component).
3. Modify your `<Properties />` component so it renders `<SideBar />`.
4. When you click on a `<Link />`, the URL in the address bar will update, and we want to trigger the `<Properties />` component to update (because it has been passed new props by React Router). We want to hook into this update in order to make a new request to the API. In order to achieve this, we need to use two extra hooks in the Properties component: the `useLocation()` hook from `react-router-dom` and a second `useEffect()` hook.
5. The `useEffect()` hook should listen to any changes of the prop `search` that is given by `useLocation()` and make a new request to the API whenever that prop changes. You should form your request URL using the query string in the address bar. Set the `properties` state using the response.

## 1 - Create a `<SideBar />` component that will render a vertical sidebar (or you can do a horizontal bar if you prefer).
Without the walkthrough.

## 2 - Add a `<Link />` for each city in your sidebar. The links should go to `?query={"city": "<your_city_name>"}` (where `<your_city_name>` matches the value in the select dropdown in your `<AddProperty />` component).

You will encounter a problem here if you try and do:

```jsx
<Link to="/?query={"city": "<your_city_name>"}">
```

The problem is that we're using curly braces as strings. A way around this is either to type the curly brace inside a JS string:

```jsx
<Link to={`/?query={"city": "Exeter"}`}>
```

## 3 - Modify your `<Properties />` component so it renders `<SideBar />`.

Without the walkthrough.

## 4 - When you click on a `<Link />`, the URL in the address bar will update, and we want to trigger the `<Properties />` component to update (because it has been passed new props by React Router). We want to hook into this update in order to make a new request to the API. In order to achieve this, we need to use two extra hooks in the `<Properties />` component: the `useLocation()` hook from `react-router-dom` and a second `useEffect()` hook.

```jsx
// Properties.js
import React, { useState, useEffect } from "react";
import { useLocation } from "react-router-dom";

...
useEffect(() => {}, []);
```

## 5 - The `useEffect()` hook should listen to any changes of the prop `search` that is given by `useLocation()` and make a new request to the API whenever that prop changes. You should form your request URL using the query string in the address bar. Set the `properties` state using the response.

Because we are using `react-router-dom` in our application and the `Properties` component is rendered by a `Route` component, we can access some helpful props that can help us manage the browser history. One of those is `props.location.search`. 

We could access this `prop` by passing `props` to the `<Properties />` component, however `react-router-dom` gives us an out of the box hook that does just that - the `useLocation()` hook. If we destructure `search` from `useLocation()` that gives us back the query string e.g: `?query={"city":"Exeter"}`. 

This query string is how we also filter down data on the Surreal Estate API - if we passed in that example, we'd only get back properties with a city of `Exeter`. Let's build our `useEffect()` hook to make another request only when there are changes in the query param:

```jsx
// Properties.js
 const { search } = useLocation();
 useEffect(() => {
    
 }, [search]);
```

Notice how we are passing a second argument to the `useEffect()` hook, the `search` prop which we get by destructing it from a call to `useLocation()`. A React component re-renders every time props *or* state change and upon each re-render this hook will check if this re-render was caused by `search` changing. If yes, it will run any code inside the inline function, otherwise it will do nothing. 

Finally, lets build our `axios` request to use the query string in `search` and `setProperties` upon success:

```jsx
// Properties.js
const { search } = useLocation();
useEffect(() => {
  axios.get(`http://localhost:4000/api/v1/PropertyListing${search}`)
    .then(({ data }) => setProperties(data))
    .catch(err => console.error(err));
}, [search]);
```

## Recommended Reading

* [MDN: Browser History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)
* [React Router Location](https://reactrouter.com/en/main/hooks/use-location)

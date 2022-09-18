## Steps
1. Add [qs](https://www.npmjs.com/package/qs) to your dependencies.
2. Add two `<Link />` elements to the `<SideBar />` component for sorting properties by price, first one for ascending and second for descending sorting.
3. In `SideBar.js`, create a function called `buildQueryString` that takes 2 parameters: `operation` (e.g. `sort` or `query`) and `valueObj` (e.g. `{ city:'Exeter' }` or `{ price:-1 }`). This function will make a query string and merge it into any existing query string in the URL bar.
4. Inside the `buildQueryString()` function you need to do the following:
  - Use `qs` to `parse` the current query string (remember you can use `useLocation()` from `react-router-dom`!) into an object. You'll need to set the option of `ignoreQueryPrefix` to `true` so that qs ignores the `?` when it parses the string into an object.
  - Create a new object using the object you just created (spread it) and add another key/value pair where the key is your `operation` variable, and the value is your `valueObj` variable.   
  - Use `qs` to `stringify()` the object and return the result. You'll need to set the option of `addQueryPrefix` to `true` (so `?` gets prepended) and `encode` to `false` (preserve the curly brace characters).
5. Modify your `<Link />` `to` props so the path comes from the `buildQueryString()` function you just created.

## 1 - Add [qs](https://www.npmjs.com/package/qs) to your dependencies.

Without the walkthrough.

## 2 - Add two `<Link />` elements to the `<SideBar />` component for sorting properties by price, first one for ascending and second for descending sorting.

Without the walkthrough.

## 3 - In `SideBar.js`, create a function called `buildQueryString()`** that takes 2 parameters: `operation` (e.g. `sort` or `query`) and `valueObj` (e.g. `{ city:'Exeter' }` or `{ price:-1 }`). This function will make a query string and merge it into any existing query string in the URL bar.

**this function should be created in `SideBar.js`, but not inside component `<SideBar />`.

```js
const buildQueryString = (operation, valueObj) => {

}
```

## 4 - Inside the `buildQueryString()` function you need to do the following:

### Use `qs` to `parse` the current query string (`location.search`) into an object. You'll need to set the option of `ignoreQueryPrefix` to `true` so that qs ignores the `?` when it parses the string into an object.


```js
import {useLocation} from 'react-router-dom';
import qs from 'qs';
...

const buildQueryString = (operation, valueObj) => {
  const {  search  } = useLocation();

  const currentQueryParams = qs.parse(search, { ignoreQueryPrefix: true });
}
```

Above we get the current query string e.g 

```js
?query={"city":"Exeter"}
```

and parse it into an object:

```js
{
  query: '{"city":"Exeter"}'
}
```

We have to tell `qs` to omit the `?` otherwise it won't ignore it and it'll include it in the parameter name (`ignoreQueryPrefix` set to `true` does that for us).

### Create a new object using the object you just created (spread it) and add another key/value pair where the key is your `operation` variable, and the value is your `valueObj` variable.   

```js
const buildQueryString = (operation, valueObj) => {
  ...

  const newQueryParams = {
    ...currentQueryParams,
    [operation]: JSON.stringify(valueObj)
  }
}
```

Here we take all the key/value pairs from the `currentQueryParams` object and spread them out into a new object. Then we add a new key/value pair to that object (if the key already existed in `currentQueryParams` then it is overridden). We use `JSON.stringify()` to convert `valueObj` from an object:

```js
{
  city: 'Exeter'
}
```

To a string:

```js
'{"city":"Exeter"}'
```

### Use `qs` to stringify the object and return the result. You'll need to set the option of `addQueryPrefix` to `true` (so `?` gets prepended) and `encode` to `false` (preserve the curly brace characters).

Now we have an object with all of the necessary URL parameters, we can use `qs` to convert it to a query string which we can then use as a link:

```js
const buildQueryString = (operation, valueObj) => {
  ...
  
  return qs.stringify(newQueryParams, { addQueryPrefix: true, encode: false });
}
```

This takes the `newQueryParams` object and turns it into a string like: `query={"city":"Exeter"}&sort={"price":1}`. The `addQueryPrefix` option ensures that `?` gets prepended to this string.

## 5 - Modify your `<Link />` `to` props so the path comes from the `buildQueryString()` function you just created.

```jsx
<Link to={buildQueryString('query', { city: 'Exeter' })}>Exeter</Link>
```

```jsx
<Link to={buildQueryString('sort', { price: -1 })}>Price Descending</Link>
```
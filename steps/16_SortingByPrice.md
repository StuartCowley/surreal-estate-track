Just as it's the APIs job to query our results, it's also its job to sort them as we specify. This is done with `?sort={"<field_to_sort_by>":1}` (1 is sort ascending, -1 is sort descending). 

![Sort by price](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/price.png)

There's one small spanner in the works for this one...if you link to `?sort={"price":1}` then you can't link to a city. We therefore need to find a way to combine the query parameters so we have a query string like: `?query={"city":"Exeter"}&sort={"price": 1}`. 

## To complete this challenge, you will need to:
* Add [qs](https://www.npmjs.com/package/qs) to your dependencies.
* Add two `<Link />` elements to the `<SideBar />` component for sorting properties by price, first one for ascending and second for descending sorting.
* In `SideBar.js`, create a function called `buildQueryString` that takes 2 parameters: `operation` (e.g. `sort` or `query`) and `valueObj` (e.g. `{ city:'Exeter' }` or `{ price:-1 }`). This function will make a query string and merge it into any existing query string in the URL bar.
* Inside the `buildQueryString()` function you need to do the following:
  - Use `qs` to `parse` the current query string (remember you can use `useLocation()` from `react-router-dom`!) into an object. You'll need to set the option of `ignoreQueryPrefix` to `true` so that qs ignores the `?` when it parses the string into an object.
  - Create a new object using the object you just created (spread it) and add another key/value pair where the key is your `operation` variable, and the value is your `valueObj` variable.   
  - Use `qs` to `stringify()` the object and return the result. You'll need to set the option of `addQueryPrefix` to `true` (so `?` gets prepended) and `encode` to `false` (preserve the curly brace characters).
* Modify your `<Link />` `to` props so the path comes from the `buildQueryString()` function you just created.

## Recommended Reading
* [`qs` node module](https://www.npmjs.com/package/qs)
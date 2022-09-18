## Steps

1. Create a search form inside your `<SideBar />` component which should consist of a text `<input>` and a submit `<button>`. The text `<input>` should be tied to a field in your state (`query` or `search` would be good field names) - refer back to the [AddProperty step](https://platform.manchestercodes.com/module/frontend/further-react/?pageId=8TqoTDrAlvkzxelfwDuP) if you are unsure about this. On form submission, a `handleSearch()` function should be called on your component.
2. Inside the `handleSearch()` function you should call your `buildQueryString()` function, passing in `'query'` as your first argument and `{ title: { $regex: <search query here> } }` as your second argument. Note that `<search query here>` will be replaced with the value of your text `<input>`, which should come from the state that you set earlier. Assign the result of invoking `buildQueryString()` to a variable.
3. Use the `useNavigate()` hook from `react-router-dom` to programatically change the URL to your new query string returned from the `buildQueryString()` function.
4. Give this a test run in your browser to check everything is working A-OK. You should notice that it isn't currently possible to search **and** filter by city.
5. Modify your `buildQueryString()` function so it supports more than one `query` key. Hint: you can achieve this by spreading one level deeper.

## 1 - Create a search form inside your `<SideBar />` component which should consist of a text `<input>` and a submit `<button>`. The text `<input>` should be tied to a field in your state (`query` or `search` would be good field names) - refer back to the [AddProperty step](https://platform.manchestercodes.com/module/frontend/further-react/?pageId=8TqoTDrAlvkzxelfwDuP) if you are unsure about this. On form submission, a `handleSearch()` function should be called on your component.

```jsx
const [query, setQuery] = useState("");
```

```jsx
<form onSubmit={handleSearch}>
  <input 
    type="text" 
    value={query} 
    onChange={(e) => setQuery(e.target.value)}
  />
  <button type="submit">Search</button>
</form>
```

```jsx
const handleSearch = event => {
  event.preventDefault();
}
```

There are no new concepts being introduced here so if you are unsure of anything then please go through the ["Adding Properties" step](https://platform.manchestercodes.com/module/frontend/further-react/?pageId=8TqoTDrAlvkzxelfwDuP) again.

If you wanted to be really fancy, you could use a Font Awesome icon in place of the `Search` text on the button above.

## 2 - Inside the `handleSearch()` function you should call your `buildQueryString()` function, passing in `'query'` as your first argument and `{ title: { $regex: <search query here> } }` as your second argument. Note that `<search query here>` will be replaced with the value of your text `<input>`, which should come from the state that you set earlier. Assign the result of invoking `buildQueryString()` to a variable.

```js
const handleSearch = event => {
  ...

  const newQueryString = buildQueryString('query', { title: { $regex: query } });
}
```

## 3 - Use the `useNavigate()` hook from `react-router-dom` to programatically change the URL to your new query string returned from the `buildQueryString()` function.

```js
import { Link, useLocation, useNavigate } from "react-router-dom";

const SideBar = () => {
  ...
  const navigate = useNavigate();

  const handleSearch = event => {
    ...

    navigate(newQueryString);
  }
  ...
}
```

We mentioned previously that React Router routes from one page to another without page loads by adding a new item to the browser's history using HTML5's history API. The `<Link/>` component takes care of this for us when we want to link from one page to another, but in this event we want to programatically change the URL based on a form submission. Fortunately, React Router gives our component the `useNavigate` hook which allows us to push a new item into the browser's history. By pushing the new query string into the history, our address bar will update and our component will update, making a new request to the API based on the new query string.

## 4 - Give this a test run in your browser to check everything is working A-OK. You should notice that it isn't currently possible to search **and** filter by city.

Without the walkthrough.

## 5 - Modify your `buildQueryString()` function so it supports more than one `query` key. Hint: you can achieve this by spreading one level deeper.

Before:

```js
const buildQueryString = (operation, valueObj) => {
  const { search } = useLocation();

  const currentQueryParams = qs.parse(search, { ignoreQueryPrefix: true });

  const newQueryParams = {
    ...currentQueryParams,
    [operation]: JSON.stringify(valueObj)
  }

  return qs.stringify(newQueryParams, { addQueryPrefix: true, encode: false });
}
```

After:

```js
const buildQueryString = (operation, valueObj) => {
  const { search } = useLocation();

  const currentQueryParams = qs.parse(search, { ignoreQueryPrefix: true });

  const newQueryParams = {
    ...currentQueryParams,
    [operation]: JSON.stringify({
      ...JSON.parse(currentQueryParams[operation] || '{}'),
      ...valueObj,
    }),
  };

  return qs.stringify(newQueryParams, { addQueryPrefix: true, encode: false });
};
```

This is probably the scariest piece of JavaScript you will have encountered (and probably will encounter) throughout the whole course so please don't freak out if you don't understand it or can't get your head around it.

Previously we just took the `{ title: { $regex: '<search query>' } }` object and assigned it as a JSON string on our `operation` key, so effectively this was happening:

```js
const newQueryParams = {
  ...currentQueryParams,
  query: '{"title":{"$regex":"<search query>"}}'
}
```

The problem we now face is if we add a `query` for `city`, then the above `query` key gets overriden (aka we can't do both simultaneously). We therefore go one level deeper. First thing's first, we create a new object:

```js
const newQueryParams = {
  ...currentQueryParams,
  [operation]: JSON.stringify({})
}
```

Then we parse any existing value for the key into an object (remember, it's currently a JSON string):

```js
const newQueryParams = {
  ...currentQueryParams,
  [operation]: JSON.stringify({
    ...JSON.parse(currentQueryParams[operation] || '{}')
  })
}
```

Note that `JSON.parse` has to be passed a valid JSON string (at a bare minimum a string of an empty object literal). If `currentQueryParams[operation]` is `undefined` here then we fall back to an empty JSON object.

Assuming `currentQueryParams[operation]` looked like this:

```js
{"city":"Exeter"}
```

It would parse it into a JS object:

```js
{
  city: 'Exeter'
}
```

We spread this object out into our new object so everything at this stage would actually be:

```js
const newQueryParams = {
  ...currentQueryParams,
  query: JSON.stringify({
    city: 'Exeter'
  })
}
```

And then we spread out our new `valueObj` underneath:

```js
const newQueryParams = {
  ...currentQueryParams,
  [operation]: JSON.stringify({
    ...JSON.parse(currentQueryParams[operation] || '{}'),
    ...valueObj
  })
}
```

Which would effectively do this:

```js
const newQueryParams = {
  ...currentQueryParams,
  query: JSON.stringify({
    city: 'Exeter',
    title: {
      $regex: '<search query>'
    }
  })
}
```

This would then be stringified to:

```js
const newQueryParams = {
  query: '{"city":"Exeter","title":{"$regex":"<search query"}}'
}
```
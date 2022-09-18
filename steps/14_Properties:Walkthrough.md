## Steps

1. Your `<Properties />` component will be stateful.
2. Set initial state of `properties` to an empty array.
3. Add a [`useEffect()` hook](https://reactjs.org/docs/hooks-reference.html#useeffect) method to the component.
4. Inside the `useEffect()` hook, make an Axios GET request to the API endpoint responsible for retrieving `PropertyListings`.
5. When the Axios Promise resolves, destructure the `data` object from the response object and set your `properties` state to the `data` object.
6. Use a hook to initialise state for alert and set it to `{message: ""}`
7. If the Axios Promise rejects, set the `message` in `alert` state to a useful error message.
8. Inside the `render()` method, map over the `properties` state, and pass each each key/value pair from each property listing to the `<PropertyCard />` component as props (you should now be able to see any properties you've added).
9. Render an `<Alert />` with the message you stored in state (you can test this by killing your API process).
10. Style your component (you might need to wrap each `<PropertyCard />` component in div tags) so that `<PropertyCards />` display in a grid.

## 1 - Your `<Properties />` component will be stateful.

Without the walkthrough.

## 2 - Set initial state of `properties` to an empty array.

You can do this by having a `const initialState` to store all the initial state for your component:

```jsx
const initialState = {
  properties: [],
}
```
```jsx
const [properties, setProperties] = useState(initialState.properties);
```

Or you can bypass the `const initialState`:

```jsx
const [properties, setProperties] = useState([]);
```
Don't forget to destructure the `useState()` hook from `react`!

## 3 -  Add a `useEffect()` hook method to the component.
For this you will need to destructure the `useEffect()` hook from `react`.

Immediately below the `useState()` hook we are going to use our `useEffect()` hook. Notice how we do not destructure any values from it like we do with `useState()`, we simply invoke the function. 

```jsx
useEffect(() => {}, [])
```

`useEffect()` takes two parameters - an inline function and an array of props that upon changing will trigger the function to rerun. We are using an empty array `[]` here, therefore not watching for any changing props, as we only want this hook to run once when the component initialises or mounts.

## 4 - Inside the `useEffect()` hook, make an Axios GET request to the API endpoint responsible for retrieving PropertyListings.

We won't give too much guidance here, other than this is very similar to how you made the POST request previously, just this time you don't need to specify any data in the request. You will need to look up your API documentation to find the correct endpoint.

[Axios Example](https://github.com/axios/axios#example)

Make sure you write the axios request inside the inline function which is `useEffect()` first parameter:

```jsx
useEffect(() => {
  // write axios request here
}, [])

```
## When the Axios Promise resolves, destructure the `data` object from the response object and set your `properties` state to the `data` object.

```js
axios.get(...)
  .then(({ data }) => setProperties(data))
```

This could equally be written without any destructuring of the response object:

```js
axios.get(...)
  .then((response) => setProperties(response.data))
```

See [Destructuring Function Arguments](https://davidwalsh.name/destructuring-function-arguments).

## 6 - Use a hook to initialise state for alert and set it to `{message: ""}`

Without the walkthrough.

## 7 - If the Axios Promise rejects, set the message in alert state to a useful error message.

Again not too much guidance here. In the resolve (`.then`) you have set some state. You just need to set some state if the Promise rejects (i.e. in a `.catch`).

## 8 - Inside the `render()` method, map over the `properties` state, and pass each each key/value pair from each property listing to the `<PropertyCard />` component as props (you should now be able to see any properties you've added).

```jsx
{properties.map(property => (
  <PropertyCard key={property._id} {...property} />
))}
```

In React, you can spread props using the spread operator. The `<PropertyCard key={property._id} {...property} />` above is the same as doing:

```jsx
<PropertyCard 
  key={property._id} 
  title={property.title} 
  bathrooms={property.bathrooms} 
  bedrooms={property.bedrooms} 
  type={property.type}
  email={property.email}
  city={property.city}
/>
```

See: [Spread Attributes](https://gist.github.com/sebmarkbage/07bbe37bc42b6d4aef81#spread-attributes).

Remember: when rendering arrays of components, each component has to have a unique `key` prop. We know each `key` will be unique here because we're using the unique identifier assigned to each document when added to the database by the API.

## 9 - Render an `<Alert />` with a message letting the user know there was a problem retrieving the properties (you can test this by killing your API process).

Without the walkthrough. Refer back to your `<AddProperty />` component if you get stuck.

## 10 - Style your component (you might need to wrap each `<PropertyCard />` component in `<div>` tags) so that `<PropertyCards />` display in a grid.

```jsx
<div className="properties">
  {properties.map((property) => (
    <div key={property._id} className="item">
      <PropertyCard {...property} />
    </div>
  ))}
</div>
```

```css
.properties {
  padding: 0.5rem;
}

.properties > .item {
  display: inline-block;
  width: 33.33%;
  padding: 0.5rem;
  box-sizing: border-box;
}
```
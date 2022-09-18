## Steps

1. Pass the `userID` state in the `<App />` component to the `<Properties />` component via the `<Route />` that renders this component.
2. In the `<Properties />` component, pass the `userID` prop down to the `<PropertyCard >` component as a prop.
3. Add a "Save" button to your `<PropertyCard />` component. It should only show if `userID` is truthy.
4. In your `<Properties />` component, create a method on the class called `handleSaveProperty()`. It should have a parameter of `propertyId`.
5. Inside the `handleSaveProperty()` method, make a HTTP request to create a new Favourite (you'll need to look up the API documentation to see which request type to use, which endpoint to call and what data you'll need to send). **Note: If you add `?populate=propertyListing` to your request URL, you will get back the property listing in place of the propertyListing _id in your response.**
6. Pass the `handleSaveProperty()` method to `<PropertyCard />` as a prop called `onSaveProperty`.
7. In the `<PropertyCard />` component, call the `onSaveProperty()` method when the "Save" button is clicked, passing in the `_id` of the property as an argument.
8. Try out the "Save" button. Verify using Postman that a Favourite has been added.

## 1 - Pass the `userID` state in the `<App />` component to the `<Properties />` component via the `<Route />` that renders this component.

```jsx
<Route path="/" element={<Properties userID={userID} />} />
```

Since elements rendered by a `<Route />` component are defined in the same way we always return components, props can be passed in the usual way.

## 2 - In the `<Properties />` component, pass the `userID` prop down to the `<PropertyCard />` component as a prop.

Without the walkthrough.

## 3 - Add a "Save" button to your `<PropertyCard />` component. It should only show if `userID` is truthy.

```jsx
{userID && (
  <button
    type="button"
    className="save"
  >
    <i className="fas fa-star" />Save
  </button>
)}
```

## 4 - In your `<Properties />` component, create a function on the class called `handleSaveProperty()`. It should have a parameter of `propertyId`.

Without the walkthrough.

## 5 - Inside the `handleSaveProperty()` function, make a HTTP request to create a new Favourite (you'll need to look up the API documentation to see which request type to use, which endpoint to call and what data you'll need to send).

Find the endpoint in the API docs for creating a Favourite:

![Favourite endpoint](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/favourite_endpoint.png)

Here we can identify that we need to make a `POST` request to `/Favourite` (appended to our API base URL), and that the data we need to send looks like so:

```json
{
  "propertyListing": "<_id of the property>",
  "fbUserId": "<logged in user's ID>"
}
```

Remember, you don't need to pass an `_id` - it's standard for APIs to generate unique identifiers for each document in the database.

Here's what the request looks like:

```js
axios.post('http://localhost:4000/api/v1/Favourite', {
  propertyListing: propertyId,
  fbUserId: userID,
});
```

## 6 - Pass the `handleSaveProperty()` function to `<PropertyCard />` as a prop called `onSaveProperty`.

Without the walkthrough.

## 7 - In the `<PropertyCard />` component, call the `onSaveProperty()` method when the "Save" button is clicked, passing in the `_id` of the property as an argument.

You'll need to destructure `_id` and `onSaveProperty` in your function parameters:

```jsx
const PropertyCard = ({
  _id,
  title,
  bedrooms,
  bathrooms,
  price,
  email,
  type,
  city,
  onSaveProperty,
  userID,
}) => (
  ...
)
```

And then call the `onSaveProperty()` using the `onClick` event handler on your Save anchor tag:

```jsx
<button
  type="button"
  onClick={() => onSaveProperty(_id)}
  className="save"
>
```

## 8 - Try out the "Save" button. Verify using Postman that a Favourite has been added.

Again, you can use the API documentation to look up the endpoint for this.

**Note: If you add `?populate=propertyListing` to your request URL, you will get back the property listing in place of the propertyListing _id in your response.**

![Postman: Favourites](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/postman_favourites.png)
**Note: If you don't have `Favourite` endpoints in your API documentation, then please pull down the latest API and restart your server.**

Now we're going to let the user save a property to their favourites. The user will have to be logged in to see the "Save" `<button>`, and when they save a property a call will be made to the API to add a `Favourite`. Be sure to have a look at the API documentation for `Favourite` before you go on.

![Save properties](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/save.png)

## To complete this challenge, you will need to:

- Pass the `userID` state in the `<App />` component to the `<Properties />` component via the `Route` that renders this component.
- In the `<Properties />` component, pass the `userID` prop down to the `<PropertyCard >` component as a prop.
- Add a "Save" button to your `<PropertyCard />` component. It should only show if `userID` is truthy.
- In your `<Properties />` component, create a method on the class called `handleSaveProperty()`. It should have a parameter of `propertyId`.
- Inside the `handleSaveProperty()` method, make a HTTP request to create a new Favourite (you'll need to look up the API documentation to see which request type to use, which endpoint to call and what data you'll need to send). **Note: If you add `?populate=propertyListing` to your request URL, you will get back the property listing in place of the propertyListing _id in your response.**
- Pass the `handleSaveProperty()` method to `<PropertyCard />` as a prop called `onSaveProperty`.
- In the `<PropertyCard />` component, call the `onSaveProperty()` method when the "Save" button is clicked, passing in the `_id` of the property as an argument.
- Try out the "Save" button. Verify using Postman that a Favourite has been added.

## Recommended Reading
* [Pass props to a component rendered by React Router](https://tylermcginnis.com/react-router-pass-props-to-components/)
In this component, you'll take advantage of React's `useEffect()` hook and Axios to bring in property listings from the API and render `<PropertyCard />` components for each one.

![Properties](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/Properties.png)

## To complete this challenge, you will need to:
* Your `<Properties />` component will be stateful.
* Set initial state of `properties` to an empty array.
* Add a [`useEffect()` hook](https://reactjs.org/docs/hooks-reference.html#useeffect) method to the component.
* Inside the `useEffect()` hook, make an Axios GET request to the API endpoint responsible for retrieving `PropertyListings`.
* When the Axios Promise resolves, destructure the `data` object from the response object and set your `properties` state to the `data` object.
* Use a hook to initialise state for alert and set it to `{message: ""}`
* If the Axios Promise rejects, set the `message` in `alert` state to a useful error message.
* Inside the `render()` method, map over the `properties` state, and pass each each key/value pair from each property listing to the `<PropertyCard />` component as props (you should now be able to see any properties you've added).
* Render an `<Alert />` with the message you stored in state (you can test this by killing your API process).
* Style your component (you might need to wrap each `<PropertyCard />` component in div tags) so that `<PropertyCards />` display in a grid.

## Recommended Reading

* [React Blog: Update on Async Rendering](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html)
* [Axios Documentation](https://github.com/axios/axios)
* [Destructuring Function Arguments](https://davidwalsh.name/destructuring-function-arguments)
* [Axios Example](https://github.com/axios/axios#example)
* [Destructuring Function Arguments](https://davidwalsh.name/destructuring-function-arguments)
* [Spread Attributes](https://gist.github.com/sebmarkbage/07bbe37bc42b6d4aef81#spread-attributes)
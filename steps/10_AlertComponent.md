You should at this stage have a form that adds new properties into the database. One thing missing though is we don't actually let the user know this operation was successful. We also don't factor in that it might not be successful - for example the API might be down.

In this step, we're going to create an `<Alert />` component:

![Error](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/error.png)

![Success](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/success.png)

It will take 2 props: 

- `message` a string of the text to display,
- `success` a boolean, alert will be green if `true` by default, but red if `false` (which means there was an error).

This is a fairly straightforward presentational component, so no excuses for not testing on this one!

## To complete this challenge, you will need to:
* Write a test for the `<Alert />` component for a failed action (error): `<Alert message="Error!" />`. It should check for a DOM node that contains the "Error!" content and assert the text of the node is `Error!`.
* Write the code to make this test pass. Use the error example above as a guideline for how this should look (you might also want to render a dummy `Alert` inside your `<AddComponent />` render so you can visualise it).
* Write a test for the `<Alert />` component for a successful action: `<Alert message="Success!!!" success />`. It should check for a DOM node with the "Success!!!" content and assert the text is `Success!!!`.
* Write the code that makes this test pass.
* Ensure your component is styled so that error messages show up in a red box, and success messages show up in a green box. Test as you go to ensure you haven't broken anything.
* Add `prop-types` validation to the component
* Add some extra initial state to `<AddProperty />`:

```jsx
{
  ...,
  alert: {
    message: "",
    isSuccess: false,
  },
}
```

* In the `handleAddProperty()` function, set the above state again (we want to clear any error/success messages before each re-submit of the form so they don't persist.)
* When your Axios Promise resolves (`.then()`) then set the `isSuccess` state to true and set the `message` to a helpful string for the user.
* When your Axios Promise rejects (`.catch()`) keep the isSuccess state as `false` and set the `message` to a helpful string for the user. Note that to cause an error so you can test this, just kill your API process - this will result in a network error.
* Render the `<Alert />` inside your form. It should only show if message is truthy.
* Write a test for when `message` is not truthy it does not render the component.
* Add a snapshot test to all of the three possible `<Alert />` UI scenarios: "error", "success" and "no message".

## Recommended Reading
* [React - JSX In Depth: Props Default to “True”](https://reactjs.org/docs/jsx-in-depth.html#props-default-to-true)
* [CSS Selector that applies to elements with two classes](https://stackoverflow.com/a/3772305)
* [The basics of destructuring props in React](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477)
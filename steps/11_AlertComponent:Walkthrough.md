## Steps

1. Write a test for the `<Alert />` component for a failed action (error): `<Alert message="Error!" />`. It should check for a DOM node that contains the "Error!" content and assert the text of the node is `Error!`.
2. Write the code to make this test pass. Use the error example above as a guideline for how this should look (you might also want to render a dummy `<Alert />` inside your `<AddComponent />` render so you can visualise it).
3. Write a test for the `<Alert />` component for a successful action: `<Alert message="Success!!!" success />`. It should check for a DOM node with the "Success!!!" content and assert the text is `Success!!!`.
4. Write the code that makes this test pass.
5. Ensure your component is styled so that error messages show up in a red box, and success messages show up in a green box. Test as you go to ensure you haven't broken anything.
6. Add `prop-types` validation to the component
7. Add some extra initial state to `<AddProperty />`:

```jsx
{
  ...,
  alert: {
    message: "",
    isSuccess: false,
  },
}
```

8. In the `handleAddProperty()` function, set the above state again (we want to clear any error/success messages before each re-submit of the form so they don't persist.)
9. When your Axios Promise resolves (`.then()`) then set the `isSuccess` state to true and set the `message` to a helpful string for the user.
10. When your Axios Promise rejects (`.catch()`) keep the isSuccess state as `false` and set the `message` to a helpful string for the user. Note that to cause an error so you can test this, just kill your API process - this will result in a network error.
11. Render the `<Alert />` inside your form. It should only show if message is truthy.
12. Write a test for when `message` is not truthy it does not render the component.
13. Add a snapshot test to all of the three possible `<Alert />` UI scenarios: "error", "success" and "no message".


## 1 - Write a test for the `<Alert />` component for a failed action (error): `<Alert message="Error!" />`.
It should check for a DOM node that contains the "Error!" content and assert the text of the node is string `Error!`.

If you haven't already got a `__tests__` or `tests` folder then please go ahead and make one now inside your `/src` directory. Inside create a `components` directory, and inside create a file `Alert.test.js` (so you should have `src/tests/components/Alert.test.js`).

Import in the necessary dependencies:

```js
import React from "react";
import { render } from "@testing-library/react";
import Alert from "../../components/Alert";
```

Remember, you aren't making the `<Alert />` component yet - you expect this test to fail.

Now create a new test:

```js
test('displays an error message', () => {

});
```

Use `react-testing-library` to render the component, passing in a `message` prop with the message we'll assert against:

```js
const component = render(<Alert message="Error!" />);
```

Then we are going to search for the DOM node that contains the error. The `getByText()` method is made available by invoking `render()` and it is going to come useful in looking for DOM nodes that contain certain text. In our case, we want to look for a DOM node that has the text "Error!"

```
const alertMessageNode = component.getByText("Error!")
```

`alertMessageNode` now contains markup found on the DOM that has text content which matches the string `Error!`. We then use the DOM text property [`textContent`](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) to write our expectation that the text of that DOM node is indeed "Error!":

```js
expect(alertMessageNode.textContent).toBe('Error!');
```

Now run your tests.

Note that this test can be written in a DRYer way, by [destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) `getByText` from the result of invoking `render()`:

```js
const { getByText } = render(<Alert message="Error!" />);
```

And we can use a [regex pattern](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) like `/Error/` which matches to any string that contains "Error" (regardless of what comes before or after). This does not change the result of the test in any way, just makes our test easier to read. This test written by using destructuring and a regex will then look like the code below - such a pattern is well used in the `react-testing-library` documentation! 

```js
test("displays an error message", () => {
  const { getByText } = render(<Alert message="Error!" />);

  expect(getByText(/Error/).textContent).toBe("Error!");
});

```

## 2 - Write the code to make this test pass.
Use the error example above as a guideline for how this should look (you might also want to render a dummy `<Alert />` inside your `<AddComponent />` render so you can visualise it).

Ideally what we want to do here is to create the component going solely by the test. When we pass the test, we can modify the aesthetic of our component etc. in knowledge that we have the test to fall back on.

You might feel confident enough to do this step on your own, in which case stop reading and go do that! Otherwise continue.

We know that (for now) this component won't need state so we want to make it a simple function, and that this component will take a prop of `message` that will be rendered between opening and closing tags of an HTML element with the classname `.alert`. Let's see how that looks:

```jsx
import React from 'react';

const Alert = ({ message }) => (
  <div className="alert">
    {message}
  </div>
);

export default Alert;
```

In a presentational component, React passes one argument to the function - the object `props`. Here we destructure `props` to get the prop `message`, which we then render inside `<div>` tags.

## 3 - Write a test for the `<Alert />` component for a successful action: `<Alert message="Success!!!" success />`.
It should check for a DOM node with the "Success" content and assert the text contains `Success` string.

```js
test("displays a success message", () => {
  const { getByText } = render(<Alert message="Success!!!!" success />);

  expect(getByText(/Success/).textContent).toBe("Success!!!!");
});
```

What is the difference between this test and our other test? It is a `success` prop:

```jsx
<Alert message="Success!!!" success />
```

When you pass a prop without assigning a value (as with `success` above), it's the equivalent of assigning `prop={true}` so the above is really short for:

```jsx
<Alert message="Success!!!" success={true} />
```

It's just a nice bit of extra syntactic sugar we get with JSX. 

## 4 - Write the code that makes this test pass.

```jsx
import React from 'react';

const Alert = ({ message, success }) => {
  return (
    <div className={`alert alert-${success ? "success" : "error"}`}>
      {message}
    </div>
  );
};

export default Alert;
```

A couple of things have changed here:

* In addition to the `message` prop, we've also destructured a `success` prop.
* We've changed the class name to a JSX expression with a template literal string inside. Inside this template literal we have another JavaScript expression of a ternary. We always have the class name `.alert`, but depending if `success` is truthy or not we add class `.alert-success` or `.alert-error`.

## 5 - Ensure your component is styled so that error messages show up in a red box, and success messages show up in a green box. Test as you go to ensure you haven't broken anything.

Please attempt this one on your own. Use the CSS guidance above to assist you. 

## 6 - Add `prop-types` validation to the component
If you followed the steps to install the Airbnn Style Guide and Prettier you probably can see both destructured props in the `<Alert />` component being highlighted in VSCode with:

`message is missing in props validation`

`success is missing in props validation`

To fix this we need to install the `prop-types` package in our project. We use `prop-types` to document the intended types of properties passed to components. React will check props passed to components against those definitions, and warn in development if they don’t match.

```plaintext
npm install --save prop-types
```

Notice that `prop-types` is installed as a regular project dependency and not a dev dependency as it will be needed when we come to build and bundle our project for deployment.

We then import the `prop-types` module into `Alert.js`:

```jsx
import PropTypes from "prop-types";
```

And use it just before we export our component. Note the different capitalisation used here, `propTypes` is an object we're appending to `Alert` comprising two key value pairs, keys being the props we are passing into our component and the values the types that PropTypes package exposes:

```jsx
Alert.propTypes = {
  message: PropTypes.string.isRequired,
  success: PropTypes.bool,
};
```

Let's see what is happening here - our two props have different types: `string` and `boolean`. `message` also has an extra property `isRequired` indicating that the component needs it in order to render correctly. On the other hand, `success` is only used for success messages making it optional. 

You might now see VSCode highlighting the `success` propType with:

`propType success is not required, but has no corresponding defaultProps declaration.`

To fix this we need to add a `defaultProps` property to `Alert`, and then assign a default value to `success`. This value will be used when we do not pass `success` into our component. As the absence of a prop is equivalent to `prop={false}`, the default value of `success` is `false`. 

```jsx
Alert.defaultProps = {
  success: false,
};
```

## 7 - Add some extra initial state to `<AddProperty />`:

Here's the extra state that needs adding:

```jsx
{
  ...,
  alert: {
    message: '',
    isSuccess: false,
  },
}
```

Add `alert` as key to `const initialState = { fields: { ... }, alert: { ... } }`

And then below the `fields` state hook, add a second hook to manage the state of alert:

```jsx
const [alert, setAlert] = useState(initialState.alert);
```

## 8 - In the `handleAddProperty()` method, set the above state again 
We want to clear any error/success messages before each re-submit of the form so they don't persist.

Right after your `event.preventDefault()`:

```jsx
setAlert({ message: "", isSuccess: false });
```

## 9 - When your Axios Promise resolves (`.then()`) then set the `isSuccess` state to true and set the `message` to a helpful string for the user.

```js
axios.post(...)
 .then(() =>
   setAlert({
     message: "Property Added",
     isSuccess: true,
   })
 )
```

## 10 - When your Axios Promise rejects (`.catch()`) keep the `isSuccess` state as `false` and set the `message` to a helpful string for the user. 
Note that to cause an error so you can test this, just kill your API process - this will result in a network error.

```js
axios.post(...)
  .then(...)
  .catch(() =>
    setAlert({
      message: "Server error. Please try again later.",
      isSuccess: false,
    })
  );
```

## 11 - Render the `<Alert />` inside your form. It should only show if message is truthy.

We've put this inside the `<form>` tag for stylistic reasons but position it where you think is best suited for the aesthetic you're going for:

```jsx
<Alert message={alert.message} success={alert.isSuccess} />
```

We mention that we should only render `<Alert />` if `message` is truthy, so how can we handle this logic? We have a couple of options available to us, but before we look into them lets remember that:

a) We only want to render `<Alert />` if there is a `message`,
b) `message` is of type string,
c) `Boolean` values for strings are:  

```
Boolean("any string")  // evaluates to `true` aka a truthy value
```
```
Boolean("") // evaluates to `false` aka a falsy value
```

### Option 1
Handle this logic in the parent component `<AddProperty />` by using a conditional expression when we render Alert inside the form. Notice how we need to wrap the `<Alert />` component in `()` and the whole expression in `{}`.

```jsx
// AddProperty.js
{alert.message && (
   <Alert message={alert.message} success={alert.isSuccess} />
)}
```

### Option 2
Handle this logic inside the child component `<Alert />`. We do not change `<Alert />` inside the form and so leave it like:

```jsx
// AddProperty.js
<Alert message={alert.message} success={alert.isSuccess} />
```

Instead we can handle the conditional rendering of `<Alert/>` by writing an `if(){}` just before the return statement inside `Alert.js`

```
// Alert.js
if (!message) return null;
```

This reads as `if not truthy message return null`. If the whole `if` statement evaluates to `true`, the component execution stops here and renders `null` to React's virtual DOM. If it evaluates to false, it will be bypassed and the component returns normaly. The component should now look like:

```jsx
const Alert = ({ message, success }) => {
  if (!message) return null;

  return (
    <div className={`alert alert-${success ? "success" : "error"}`}>
      {message}
    </div>
  );
};
```

### Option 1 vs Option 2
Both approaches produce the same results, with the main differences lying on:

- who controls the render of the component - their parent (option 1) or itself (option 2), 

- readability - many consider *option 2* easier to read 

- testing - when using a per component testing strategy *option 2* is easier to test

- reusability - we can use `<Alert />` in other components without having to worry about how to control it. It is enough to pass a "message" prop for it to conditionally render.

## 12 - Write a test for when `message` is not truthy it does not render the component 
To write this test we are going to use the "Option 2" above and `asFragment()` instead of `getByText()`. In `react-testing-library`, `asFragment()` gives us a nice DOM slice that corresponds to the React component we're testing

We start by writing a new test and destructuring the `asFragment()` method from the result of rendering `<Alert />` :

```js
test("does not render an error or a success message if message props is empty", () => {
  const { asFragment } = render(<Alert message="" />);
});
```

Notice how the prop `message` passed into `<Alert />` is an empty string. We are certain that no markup should be rendered when `message=""`, so we are simply going to create a snapshot test based on the result of invoking `asFragment()`

```js
const alert = asFragment();
```

What do you think the `const alert` will contain? We expect no markup to be rendered, in this case an empty `<Fragment />`. The best way to assert this is to use the `toMatchSnapshot()` from the `jest` framework. We can set our expectation like:

```js
expect(alert).toMatchSnapshot();
```

The first time the test runs, jest will grab a stringified DOM representation of `alert` and save it under a folder `_snapshots_`. Snapshots are a great (and quick) way of creating tests that validate markup 

Run your tests and head to `_snapshots/Alert.test.snap.js` to see what we mean. 

Snapshots do not capture visual changes made by CSS but they do capture everything else, including markup and CSS classes used in a component. They are a very useful tool whenever you want to make sure your UI does not change unexpectedly but they shouldn't be the only type of tests we use. More on snapshot testing [here](https://jestjs.io/docs/en/snapshot-testing).

## 13 - Add a snapshot test to all of the three possible `<Alert />` UI scenarios: "error", "success" and "no message".
For "no message" we added this snapshot on the example before. For "error" we can do this by adding `asFragment` to the properties destructured from rendering `<Alert />`and then adding an extra expectation:

```js
const { getByText, asFragment } = render(<Alert message="Error!" />);
```
```js
expect(asFragment()).toMatchSnapshot();
```

For "success" you can use the example above and add a snapshot test to the `displays a success message` test!
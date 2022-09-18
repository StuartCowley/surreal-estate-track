Single Sign On (SSO) in a nutshell is having one login for multiple applications. You've probably used it yourself any time you've signed into a website with Google or Facebook. Fortunately, both of these companies offer Single Sign On to developers. We're going to use Facebook's JavaScript API to implement SSO into our application. Fortunately, there's a React module that will help us with this: [react-facebook-login](https://github.com/keppelen/react-facebook-login).

![Facebook login](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/facebook.png)

## To complete this challenge, you will need to:
* Add the `<FacebookLogin />` component to your `<NavBar />`:
  - Don't use the `onClick` handler. 
  - Set the `callback` prop to call `onLogin`. 
  - Register for a Facebook dev account in order to get an `appId`
  - Your `<NavBar />` component will expect `onLogin` to be passed as a prop.
* In `<App />`, add initial state of `userID` and set it to `""`.
* Create a `handleLogin()` function and pass it down as a prop to the `<NavBar />` component. Call this prop `onLogin` to match the prop name your `<NavBar />` component expects.
* Your `handleLogin()` method will get passed a `response` parameter, which will get passed an object containing data about the user. Inspect this response object to find the user ID, and update the `userID` state accordingly.
* Pass the `userID` state as a prop (named `userID`) to `<NavBar />`.
* Inside `<NavBar />`, if the `userID` prop has a truthy value, then show a sign out button with the text "Sign Out" (it doesn't need to do anything yet), otherwise show the `<FacebookLogin />` component.
* Add an `onClick` handler to your sign out button. It should call `onLogout`. Your `<NavBar />` component should expect to be passed a prop of `onLogout`.
* Create a `handleLogout()` function in your `<App />` component. It doesn't need to have any parameters. Pass it down to `<NavBar />` as a prop (named `onLogout`).
* Inside the `handleLogout()` function, [logout of Facebook](https://developers.facebook.com/docs/reference/javascript/FB.logout/) using the `window.FB` object. When clicked, you should see the button alternate between "Login with Facebook" and "Sign Out". Note that in React, you can use `window.FB` instead of `FB` to stop your linter from erroring (`FB` is a global variable stored on the window object).

## Recommended Reading

* [react-facebook-login](https://github.com/keppelen/react-facebook-login)
* [Facebook Logout](https://developers.facebook.com/docs/reference/javascript/FB.logout/)
* [Stack Overflow - Working with Facebook login](https://stackoverflow.com/questions/39800216/working-with-facebook-login-from-localhost#:~:text=You%20need%20to%20register%20as,be%20able%20to%20access%20it.)
* [Using HTTPS in development](https://create-react-app.dev/docs/using-https-in-development/)
* [Facebook for Developers](https://developers.facebook.com/)

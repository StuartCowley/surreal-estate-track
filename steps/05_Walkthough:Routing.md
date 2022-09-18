### List of tasks
1. Add `react-router-dom` to your project's dependencies.

2. Wrap your `<App />` component inside the [`<BrowserRouter />`](https://reactrouter.com/en/main/router-components/browser-router) component.

3. Create a `<Properties />` component. For now, it should be a presentational component that renders a `<div>` with the contents "Properties Page".

4. Create a `<AddProperty />` component. For now, it should be a presentational component that renders a `<div>` with the contents "Add Property Page".

5. Inside your `<App />` component, underneath the `<NavBar />`, render a [`<Routes />`](https://reactrouter.com/en/main/components/routes) component.

6. Inside the `<Routes />` statement, add a new [`<Route />`](https://reactrouter.com/en/main/route/route) component. It should have a `path` prop set to `/` (for when the user is on the homepage). It should render the `<Properties />` component - see [element](https://reactrouter.com/en/main/route/route#element).

7. Add another `<Route />` component for when the user visits the path `add-property`. This time it should render the `<AddProperty />` component.

8. Inside the `<NavBar />` component, import in the [`<Link />`](https://reactrouter.com/en/main/components/link) component.

9. Swap your `<a>` elements for `<Link />` elements. Add a `to` prop to the `<Link />` element wrapping "View Properties" and set it's value to `/`. Set your other `<Link />`'s `to` prop to `add-property`.

10. Everything should still look okay in your browser now. You might need to look at changing the text [color](https://www.w3schools.com/cssref/pr_text_color.asp) and [text-decoration](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration) in the `.navbar-links-item` CSS class to get the appearance you want.

11. Give the links a go. If everything has been done correctly then they should alternate between your `<Properties />` and `<AddProperty />` components without reloading the page.

## 1 - Add `react-router-dom` to your project's dependencies.

Do this without the walkthrough. 💪

*Hint:* use `npm install react-router-dom`

## 2 - Wrap your `<App />` component inside the `<BrowserRouter />` component.

The `<BrowserRouter />` component instructs React Router to use HTML5's History API to handle navigation. We wrap the outermost component, also known as the entry point of our application, so that routing is available in all application components.

In `src/index.js`, [destructure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) `BrowserRouter` from the `react-router-dom` package:

```jsx
import { BrowserRouter } from 'react-router-dom';
```

And wrap the `<App />` component passed to `root.render()` method inside the `<BrowserRouter />` component:

```jsx
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

## 3 - Create a `<Properties />` component. 
For now, it should be a presentational component that renders a `<div>` or Fragment with the contents "Properties Page".

```jsx
import React from "react";

const Properties = () => <div>Properties Page</div>;

export default Properties;
```

You could have also used a React `<Fragment />` here. Think what typical React problem using `<Fragment />` can solve? If you aren't familiar with [`Fragment`](https://reactjs.org/docs/fragments.html) it essentially wraps our JSX children in the same way a `div` does, but without rendering a pointless empty div to the DOM. It can be represented as `<Fragment></Fragment>` or by the shorthand `<></>`

## 4 - Create a `<AddProperty/>` component. 
For now, it should be a presentational component that renders a `<div>` with the contents "Add Property Page".

Do this without the walkthrough. 💪

## 5 - Inside your `<App />` component, underneath the `<NavBar />`, render a `<Routes />` [component](https://reactrouter.com/en/main/components/routes).

Don't forget to import `Routes` from `react-router-dom`.

```jsx
...

<NavBar />
<Routes></Routes>

...
```

The `<Routes />` component houses all of our routes, its purpose is to match the given child routes to the current location.

## 6 - Inside the `<Routes />` statement, add a new `<Route />` [component](https://reacttraining.com/react-router/web/api/Route).

Don't forget to import `Route` from `react-router-dom`.

The `<Route />` component should have two props:

 - `path` set to `/`,
 - `element` should point to the `<Properties />` component .

```jsx
<Routes>
  <Route path="/" element={Properties} />
</Routes>

```

You should have a linter error here on `Properties`. We'll leave you to fill in the missing puzzle piece. 

## 7 - Add another `<Route />` component for when the user visits the path `/add-property`. 
This time it should render the `<AddProperty />` component.

Do this without the walkthrough. 💪

## 8 - Inside the `<NavBar />` component, import in the `<Link />` component from `react-router-dom`.

There is a code example of how to do this on the [`<Link />` documentation](https://reactrouter.com/en/main/components/link).

## 9 - Swap your `<a>` elements for `<Link />` elements. 
Add a `to` prop to the `<Link />` element wrapping "View Properties" and set it's value to `/`. Set your other `<Link />`'s `to` prop to `add-property`.

Example:

```jsx
<Link className="item" to="/">View Properties</Link>
```

## 10 - Try it out in the browser

If everything has been done correctly then they should alternate between your `<Properties />` and `<AddProperty />` components without seeing the page reload. You should see text underneath the `<NavBar/>` changing from "Properties Page" to "Add Property Page".

Do take time here to tinker with your CSS and ensure everything looks aesthetically pleasing.
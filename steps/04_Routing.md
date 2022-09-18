Surreal Estate will be a Single Page Application (SPA). Normal browser behaviour is to click a link, which in turn makes a new request to the server, and a new page loads in the browser. With a SPA, you do one request to the server to load in your application. Any page changes are merely an illusion - JavaScript re-writes the contents of the DOM for each page which allows you to change pages without the page loads or server requests. You can still make AJAX requests from within a SPA to get more data from the server when you need it, just as you did with the Weather app to get forecasts.

There is one problem with this SPA approach, which is that the URL shown in the address bar won't change as you change pages because you aren't actually changing the page. This is where React Router comes in - it uses HTML5's [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API) to manipulate your browser history. When you visit a new page, it adds that page to the top of your history and as such the URL in the address bar changes. Because this is a JavaScript API, this still happens without page loads. Another fundamental aspect of React Router is that it can map a browser path to a React component. For example, if your web application was deployed online with the address https://randomthings.com and a user visited https://randomthings.com/guestbook then you could use React Router to specify that the `/guestbook` path should render a Guestbook component, and that `/contact` should render a `<Contact />` component.

For this task you are going to:

* Import React Router into your project

* Add routes for the homepage and the add property page

* Incorporate `<Link />` components into your `<NavBar />`.

Please read the React Router documentation linked in the steps below. It's written very well, and will give your more insight into what it is the components actually do.

## To complete this challenge, you will need to:

- Add `react-router-dom` to your project's dependencies.

- Wrap your `<App />` component inside the [`<BrowserRouter />`](https://reactrouter.com/en/main/router-components/browser-router) component.

- Create a `<Properties />` component. For now, it should be a presentational component that renders a `<div>` with the contents "Properties Page".

- Create a `<AddProperty />` component. For now, it should be a presentational component that renders a `<div>` with the contents "Add Property Page".

- Inside your `<App />` component, underneath the `<NavBar />`, render a [`<Routes />`](https://reactrouter.com/en/main/components/routes) component.

- Inside the `<Routes />` statement, add a new [`<Route />`](https://reactrouter.com/en/main/route/route) component. It should have a `path` prop set to `/` (for when the user is on the homepage). It should render the `<Properties />` component - see [element](https://reactrouter.com/en/main/route/route#element).

- Add another `<Route />` component for when the user visits the path `add-property`. This time it should render the `<AddProperty />` component.

- Inside the `<NavBar />` component, import in the [`<Link />`](https://reactrouter.com/en/main/components/link) component.

- Swap your `a` elements for `<Link />` elements. Add a `to` prop to the `<Link />` element wrapping "View Properties" and set it's value to `/`. Set your other `<Link />`'s `to` prop to `add-property`.

- Everything should still look okay in your browser now. You might need to look at changing the text [color](https://www.w3schools.com/cssref/pr_text_color.asp) and [text-decoration](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration) in the `.navbar-links-item` CSS class to get the appearance you want. 

- Give the links a go. If everything has been done correctly then they should alternate between your `<Properties />` and `<AddProperty />` components without reloading the page.

## Recommended Reading

* [React Router Documentation](https://reactrouter.com/en/v6.3.0/api)

* [React Router Installation](https://reactrouter.com/en/v6.3.0/getting-started/installation)

* [React Router Overview](https://reactrouter.com/en/main/start/overview)

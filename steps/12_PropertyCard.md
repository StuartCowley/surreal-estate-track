Using your knowledge from the Weather app, you're going to make a `<PropertyCard />` component (no walkthrough for this step) - this component will be what shows up in the properties listing grid. Ours looks like:

![PropertyCard](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/PropertyCard.png)

(Note that we've gone with 100% width - inside a grid this width will be restricted to the width of a column).

Your component will be passed props of:

```plaintext
title
type
bathrooms
bedrooms
price
city
email
```

**You should approach this in a test-driven manner**. Write a different test for each prop passed to the card: use `react-testing-library` methods exposed by rendering the `<PropertyCard />` component passing in each prop to the component with a mock value, and then assert that the correct value has been rendered (try and think in advance and perhaps draw down on paper what you think your component is going to look like so you can use `react-testing-library` methods effectively). Again, when you want to try out the component in the browser, render it inside one of your existing components and pass it some dummy props (the `<Properties />` component could be a good shout!).

All of the graphics above are Font Awesome icons - any styling has been done with CSS.

Stuck?

* Read the walkthrough for the last step
* [Weather App: Testing Components](https://platform.manchestercodes.com/module/frontend/react-basics/?pageId=3xVuX3xZK9qqSGoD3e8N)
* [React Testing Library Cheat Sheet](https://testing-library.com/docs/react-testing-library/cheatsheet)
* [Common mistakes with React Testing Library](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)

## Recommended Reading

* [mailto Links](https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_link_mailto)
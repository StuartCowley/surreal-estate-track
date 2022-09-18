This is what we are looking to achieve by the end of this section:

![NavBar](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/nav-bar.png)

-------------------------------

## Steps:

1. Create a `<NavBar />` component which renders a `<div>`, and import it into your `<App />` component. This is useful as it'll enable you to preview any changes you make to it by running the application with `npm start`.

2. Create a `navbar.css` file in `/styles` and import it into your component.

3. Add a `navbar` class with some styling (we've given ours a white background and a grey [bottom border](https://www.w3schools.com/cssref/pr_border-bottom.asp)) and add it to the `<div>` in your `<NavBar />` component.

4. Inside the `<div>` in the <NavBar /> component, add an image for the logo:

![Surreal Logo](https://mcrcodes.s3.eu-west-2.amazonaws.com/course/surreal-estate/logo.png). 

✔️ You might want to add some CSS styling to this to reduce the size of the image 😱

5.  Add an [unordered list](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul) inside the `<div>` and give it a class name of `navbar-links`. Use this class selector to style the list so it doesn't have any margins or padding. 

6. Add two list elements to your `<ul>` and give them a class name of `navbar-links-item`. Each list item will be a hyperlink, one with the text "View Properties" and the other with "Add a Property". In your CSS, style these list items by using the `navbar-links-item` class selector so they:
  * have no margin 
  * have some padding (we leave you to experiment)
  * display as an inline-block.

👏 You now have two items for your navigation!  

## Recommended Reading

* [CSS Display Properties](https://medium.com/@DaphneWatson/css-display-properties-block-inline-and-inline-block-how-to-tell-the-difference-7d3a1e6e3051)
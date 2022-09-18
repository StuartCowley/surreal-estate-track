The `<AddProperty />` component will be a form where we'll create a new property. We'll eventually tie it up to an API, but for now we're just concerned with the user interface (UI).

You should read the [React Forms documentation](https://reactjs.org/docs/forms.html) before you go any further. There aren't many applications out there that don't use forms, so don't rush through this step.

The field names for a property are as follows:

* `title` - the property tagline
* `type` - what type of property it is...flat, terrace etc.
* `bedrooms` - number of bedrooms
* `bathrooms` - number of bathrooms
* `price` - cost of property
* `city` - where property is based
* `email` - email of person to contact

## To complete this challenge, you will need to:

1. Give a `className` prop with a value of `"add-property"` to outer `<div>` of the `<AddProperty />` component. If using a `<Fragment />`, replace it with a `<div>` and remove the unused `Fragment` import.
2. Create a new `add-property.css` file and import it into your component.
3. Style your `.add-property` CSS selector to give it some padding.
4. Inside the `<div>`, add a `<form>` tag. 
5. Inside the `<form>` tag, add a `<button>` with a `type` prop of `submit`. The button should have text "Add" inside.
6. At the top of your component, create a `const` named `initialState` with a key `fields` set to the following object:

  ```jsx
  {
    title: ''
  }
  ```
7. Initialise the component state by importing `useState` and set it like so:

  ```jsx
const [fields, setFields] = useState(initialState.fields);
  ```

8. Create the `handleAddProperty()` function inside the Component wrapper function. You can write this as an arrow function or not (we prefer arrow functions as they don't have their own `this` property, which comes useful when working with older versions of React. More on `this` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)).
9. Add a single parameter of `event` to `handleAddProperty()`. Inside you should call `event.preventDefault()` to halt the default form submission behaviour, and then below log out `fields` to the console.
10. Give a prop of `onSubmit` to the form and set the value to `handleAddProperty`.
11. If you view your page in the browser now and click the "Add" button, you should see `{ title: '' }` logged out to the console.
12. Inside the `<form>` tag above your `<button>`, add an `<input>`. It should have an `id` prop set to `title`, a `name` prop set to `title`, a `value` prop set to `fields.title` (the state you set earlier), and an `onChange` handler set to a `handleFieldChange()` function. It should also have a `label` prop with the corresponding [`htmlFor`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label) prop set to the `id` of the field referenced, in this case it will be `title`.
13. Create the `handleFieldChange()` function. Make it an arrow function and should have a parameter of `event`.
14. Inside the `handleFieldChange()` function, set the state of the field being updated. `event.target.name` will give you the input name (in this case: `title`) and `event.target.value` will give you the current value of the `<input>`. You want to update the `event.target.name` of the `fields` state, updating its value. You will have to get down and dirty with the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) here.
15. Add a `city` field to your initial `fields` state with a value of `'Manchester'`. `Manchester` will be the default option we wish to show in our city dropdown.
16. Add a `select` element. It should have an `id` prop of `city`, a `name` prop of `city`, a value prop of `fields.city` and an `onChange` prop of `handleFieldChange` (see the similarities between this and the input from before). Don't forget to give it a `<label>` with the corresponding `htmlFor` prop.
17. Give the `<select>` element some `<option>` elements as children. Each should have a `value` prop. The `<label>` for each select `<option>` will be passed as a child to the `<option>` element. Here are the values and text you will need for the `city` select:

| Value          | Text           |
|----------------|----------------|
| Manchester     | Manchester     |
| Leeds          | Leeds          |
| Sheffield      | Sheffield      |
| Liverpool      | Liverpool      |

18. Add the other fields (repeating the above steps: add field state + add `<input>`/`<select>`). All are `<input>`s apart from "Type" which is another `<select>` dropdown. Think about the appropriate `<input>` types to use. The options for the "Type" field are:

| Value          | Text           |
|----------------|----------------|
| Flat           | Flat           |
| Detached       | Detached       |
| Semi-Detached  | Semi-Detached  |
| Terraced       | Terraced       |
| End of Terrace | End of Terrace |
| Cottage        | Cottage        |
| Bungalow       | Bungalow       |

19. Fill out your form and click the "Add" button. If you've done everything correctly then you should see an object logged out to the console which has key/value pairs matching your `<input>`/`<select>` names and values.
20. Give your inputs `<label>`s and `placeholders` to make it clearer to the user what each field is for (`<label>` should inform what information should be provided, when `placeholder` in which format, including capitalisation or usage of special characters, like "john.smith@email.co.uk"). Use CSS to style your form fields. Don't be afraid to wrap them in `<div>` elements to use margins and padding to space everything out a bit!

## 1 - Give a `className` prop with a value of `"add-property"` to outer `<div>` of the `<AddProperty />` component. If using a `<Fragment />`, replace it with a `<div>` and remove the unused `Fragment` import.

Do this without the walkthrough. 💪

## 2 - Create a new `add-property.css` file and import it into your component.

Do this without the walkthrough. 💪

## 3 - Style your `.add-property` CSS selector to give it some padding.

Do this without the walkthrough. 💪

## 4 - Inside the `<div>`, add a `<form>` tag.

Do this without the walkthrough. 💪

## 5 - Inside the `<form>` tag, add a `<button>` with a `type` prop of `"submit"`. The button should have text "Add" inside.

Do this without the walkthrough. 💪

## 6 - At the top of your component, create a `const` named `initialState` with a key `fields` set to the following object:

```jsx
{
  title: ''
}
```

This will look like: 

```jsx
const initialState = {
  fields: {
    title: "",
  },
};
```

## 7 - Initialise the component state by importing `useState` and set it like so:

```jsx
const [fields, setFields] = useState(initialState.fields);
```

Lets first import `useState` destructuring it next to where we import `React` like: 

```jsx
import React, { useState } from "react";
```

Below where we declared the `const initialState` we  can then initialise our component state by using `useState()` like:

```jsx
const [fields, setFields] = useState(initialState.fields);
```

Here we are using a function that the React library makes available to us so that we can keep track of component state. Functions that start with `use` in React are commonly called `hooks`. The hook `useState()` takes an argument which is an object. Notice how this is exactly what `initialState.fields` is. The expression `[fields, setFields]` to the left means that we are [destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) the result of invoking `useState()` and assigning it to two constants - one is the current value of state at any given moment (which we named `fields`) and the second is another function (which we named `setFields()`), function which will allow us to change the value of `fields`, ie, the value of state.

We could have written the above as:

```jsx
const state = useState(initialState.fields); // returns an array of two items
const fields = state[0]; 
const setFields = state[1];
```

This means that `useState()` function signature is that it will return an array with at least two elements, the first being the value of state at any given time and the second the function that allows that state to be changed. Notice how much less verbose it is to use destructuring!

## 8 - Create the `handleAddProperty()` function inside the Component wrapper function. 
You can write this as an arrow function or not (we prefer arrow functions as they don't have their own `this` property, which comes useful when working with older versions of React. More on `this` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)).

You can create this function immediately after where we use the `useState` hook.

```jsx
const handleAddProperty = () => {}
```

## 9 - Add a single parameter of `event` to `handleAddProperty()`. Inside you should call `event.preventDefault()` to halt the default form submission behaviour, and then below log out `fields` to the console.

We start by adding an `event` parameter to our function

```jsx
const handleAddProperty = (event) => {};
```

Then we can invoke `event.preventDefault()` to prevent the browser default behaviour when a button of type "Submit" is pressed, which is to submit the form by making a network call and refresh the page. We will submit the values in this form but without refreshing the page!

```jsx
 const handleAddProperty = (event) => {
   event.preventDefault();
 };
```

And in order to check everything is working as we go, we'll add a `console.log()` which will output `fields`, which is the state we initialised by passing the value of the `initialState.fields` to the hook `useState()`:

```jsx
const handleAddProperty = (event) => {
  event.preventDefault();
  console.log(fields);
};
```

## 10 - Give a prop of `onSubmit` to the form and set the value to `handleAddProperty`.

We do this by adding a prop to our form tag and making it equal to `{}`. 

```jsx
<form onSubmit={}>
  // ...
</form>
```

Curlies in JSX imply that we will be using Javascript instead of markup, in this case we want to tell the form to use the function `handleAddProperty` when submitting. This is also called `binding` the `onSubmit` prop to the `handleAddProperty` function:

```jsx
<form onSubmit={handleAddProperty}>
  // ...
</form>
```

Notice that we are not invoking (calling) the `handleAddProperty` by adding the double parenthesis `()` when binding it to `onSubmit`. What we are trying to achieve here is a chain of events:

1 - Button (of type submit) is clicked >> 
2 - Which triggers the `onSubmit` prop on the form >>
3 - `onSubmit` is bound to the function `handleAddProperty` >> 
4 - Bound function `handleAddProperty` is called. 


## 11 - If you view your page in the browser now and click the "Add" button, you should see `{ title: '' }` logged out to the console.

Do this without the walkthrough. 💪

## 12 - Inside the `<form>` tag above your button, add an `<input>`. 

It should have an `id` prop set to `title`, a `name` prop set to `title`, a value prop set to `fields.title` (the state you set earlier), and an onChange handler set to a `handleFieldChange` function. It should also have a `<label>` with the corresponding [`htmlFor`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label) prop set to the `id` of the field referenced, in this case it will be `title`.

```jsx
<label htmlFor="title">
  Title
  <input
    id="title"
    name="title"
    value={fields.title}
    onChange={handleFieldChange}
  />
</label>
```

Each time this field is changed (a.k.a. a character is typed inside of it), the `handleFieldChange` function which is bound to the `onChange` event handler will be called. This method will set the `fields.title` state to the current value of the input. We say that this therefore is a _controlled input_ - that is an input where the value always comes from state, and the value is updated programatically in an event handler (in this case `handleFieldChange`).

## 13 - Create the `handleFieldChange` function. Make it an arrow function and should have a parameter of `event`.

Do this without the walkthrough. 💪

## 14 - Inside the `handleFieldChange` function, set the state of the field being updated. 
`event.target.name` will give you the input name (in this case: `title`) and `event.target.value` will give you the current value of the input. You want to update the `event.target.name` of the `fields` state, updating its value. You will have to get down and dirty with the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) here.

This looks like so:

```jsx
const handleFieldChange = (event) => {
  setFields({ ...fields, [event.target.name]: event.target.value });
};
```

This might look a bit frightening so we'll break it down a little:

```jsx
setFields({ ... });
```

You should be familiar with the `setFields` function. It takes key value pair(s) state to update. Here we update the `fields` state:

```jsx
setFields({});
```

The above would overwrite the `fields` object setting it to a new empty object. If we had several key/value pairs inside `fields` (which we will), then they would all be overwritten. There's a way around this which is to _spread_ out all the existing key value pairs into the new object:

```jsx
setFields({...fields});
```

This is like taking the following object:

```jsx
{
  title: '',
}
```

Removing the curly braces, and slotting the key/value pair: `title: ''` into the new object.

Then underneath we can overwrite a specific key/value pair:

```jsx
setFields({
  ...fields,
  title: '',
});
```

The above would ensure `title` was always an empty string. If we wanted to set `title` to the input value, we could use `event.target.value` (the target of the event was the text input because that's what triggered the event, so we're just asking for that DOM element's `value` attribute):

```jsx
setFields({
  ...fields,
  title: event.target.value,
});
```

This would effectively update the `fields.title` state without deleting any other key/value pairs inside the `fields` state. However, we want to use this helper on our other inputs too, so we don't want to use `title` specifically here. Instead we can use the `name` attribute on the input:

```jsx
setFields({
  ...fields,
  [event.target.name]: event.target.value,
});
```

We can use the above square bracket notation to dynamically interpolate a key name.

Below is another way how this logic can be written:

```
const handleFieldChange = (event) => {
  const changedField = event.target.name;
  const newValue = event.target.value;
  setFields({ ...fields, [changedField]: newValue });
};
```

You should now be able to use this on any HTML form element that has a `name` attribute, and whose value can be retrieved on `event.target.value`.

## 15 - Add a `city` field to your initial `fields` state with a value of `'Manchester'`. It will be the default option we wish to show in our city dropdown.

Do this without the walkthrough. 💪

## 16 - Add a `<select>` element. It should have an `id` prop of `city`, a `name` prop of `city`, a `value` prop of `fields.city` and an `onChange` prop of `handleFieldChange` (see the similarities between this and the `<input>` from before). Don't forget to give it a `<label>` with the corresponding `htmlFor` prop.

This should look similar to the `<input>` element we rendered before:

```jsx
<label htmlFor="city">
  <select id="city" name="city" value={fields.city} onChange={handleFieldChange} />
</label>
```

## 17 - Give the `<select>` element some `<option>` elements as children. Each should have a `value` prop. The text for each select `<option>` will be passed as a child to the `<option>` element. Here are the values and text you will need for the `city` select:

| Value          | Text           |
|----------------|----------------|
| Manchester     | Manchester     |
| Leeds          | Leeds          |
| Sheffield      | Sheffield      |
| Liverpool      | Liverpool      |

We'll give you the first 2:

```jsx
<select id="city" name="city" value={fields.city} onChange=handleFieldChange}>
  <option value="Manchester">Manchester</option>
  <option value="Leeds">Leeds</option>
</select>
```

Now finish adding the others. With a select, the value is always that of the selected `option` element.

## 18 - Add the other fields (repeating the above steps: add field state + add `<input>`/`<select>`). All are `<input>`s apart from "Type" which is another `<select>` dropdown. Think about the appropriate `<input>` types to use. The options for the "Type" field are:

| Value          | Text           |
|----------------|----------------|
| Flat           | Flat           |
| Detached       | Detached       |
| Semi-Detached  | Semi-Detached  |
| Terraced       | Terraced       |
| End of Terrace | End of Terrace |
| Cottage        | Cottage        |
| Bungalow       | Bungalow       |

Do this without the walkthrough. 💪

## 19 - Fill out your form and click the "Add" button.

If you've done everything correctly then you should see an object logged out to the console which has key/value pairs matching your `<input>`/`<select>` names and values:

![Property object](https://mcrcodes.s3.eu-west-2.amazonaws.com/course/surreal-estate/propertyObj.png)

## 20 - Give your inputs `<label>`s and `placeholders` to make it clearer to the user what each field is for (`<label>` should inform what information should be provided, when `placeholder` in which format, including capitalisation or usage of special characters, like "john.smith@email.co.uk"). Use CSS to style your form fields. Don't be afraid to wrap them in `<div>` elements to use margins and padding to space everything out a bit!

Do this without the walkthrough. 💪
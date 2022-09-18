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

* Give a `className` prop with a value of `"add-property"` to outer `<div>` of the `<AddProperty />` component. If using a `Fragment`, replace it with a `<div>` and remove the unused `Fragment` import.
* Create a new `add-property.css` file and import it into your component.
* Style your `.add-property` CSS selector to give it some padding.
* Inside the `<div>`, add a `<form>` tag. 
* Inside the `<form>` tag, add a `<button>` with a `type` prop of `submit`. The `<button>` should have text "Add" inside.
* At the top of your component, create a `const` named `initialState` with a key `fields` set to the following object:

  ```jsx
  {
    title: ''
  }
  ```
* Initialise the component state by importing `useState` and set it like so:

  ```jsx
        const [fields, setFields] = useState(initialState.fields);
  ```

* Create the `handleAddProperty()` function inside the Component wrapper function. You can write this as an arrow function or not (we prefer arrow functions as they don't have their own `this` property, which comes useful when working with older versions of React). More on `this` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).
* Add a single parameter of `event` to `handleAddProperty()`. Inside you should call `event.preventDefault()` to halt the default form submission behaviour, and then below log out `fields` to the console.
* Give a prop of `onSubmit` to the `form` and set the value to `handleAddProperty`.
* If you view your page in the browser now and click the "Add" button, you should see `{ title: '' }` logged out to the console.
* Inside the `<form>` tag above your `<button>`, add an `<input>`. It should have an `id` prop set to `title`, a `name` prop set to `title`, a value prop set to `fields.title` (the state you set earlier), and an onChange handler set to a `handleFieldChange()` function. It should also have a `<label>` with the corresponding [`htmlFor`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label) prop set to the `id` of the field referenced, in this case it will be `title`.
* Create the `handleFieldChange()` function. Make it an arrow function and should have a parameter of `event`.
* Inside the `handleFieldChange()` function, set the state of the field being updated. `event.target.name` will give you the input name (in this case: `title`) and `event.target.value` will give you the current value of the input. You want to update the `event.target.name` of the `fields` state, updating its value. You will have to get down and dirty with the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) here.
* Add a `city` field to your initial `fields` state with a value of `"Manchester"`. It will be the default option we wish to show in our city dropdown.
* Add a `<select>` element. It should have an `id` prop of `city`, a `name` prop of `city`, a value prop of `fields.city` and an `onChange` prop of `handleFieldChange` (see the similarities between this and the `<input>` from before). Don't forget to give it a `<label>` with the corresponding `htmlFor` prop.
* Give the `<select>` element some `<option>` elements as children. Each should have a `value` prop. The text for each select `<option>` will be passed as a child to the `<option>` element. Here are the values and text you will need for the `city` select:

| Value          | Text           |
|----------------|----------------|
| Manchester     | Manchester     |
| Leeds          | Leeds          |
| Sheffield      | Sheffield      |
| Liverpool      | Liverpool      |

* Add the other fields (repeating the above steps: add field state + add `<input>`/`<select>`). All are `<input>`s apart from "Type" which is another `<select>` dropdown. Think about the appropriate `<input>` types to use. The options for the "Type" field are:

| Value          | Text           |
|----------------|----------------|
| Flat           | Flat           |
| Detached       | Detached       |
| Semi-Detached  | Semi-Detached  |
| Terraced       | Terraced       |
| End of Terrace | End of Terrace |
| Cottage        | Cottage        |
| Bungalow       | Bungalow       |

* Fill out your form and click the "Add" button. If you've done everything correctly then you should see an object logged out to the console which has key/value pairs matching your `<input>`/`<select>` names and values.
* Give your inputs `<label>`s and `placeholders` to make it clearer to the user what each field is for (`<label>` should inform what information should be provided, when `placeholder` in which format, including capitalisation or usage of special characters, like "john.smith@email.co.uk"). Use CSS to style your form fields. Don't be afraid to wrap them in `<div>` elements to use margins and padding to space everything out a bit!

## Recommended Reading

* [MDN: input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
* [MDN: select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)
* [React: Forms](https://reactjs.org/docs/forms.html)
* [React: Components and Props](https://reactjs.org/docs/components-and-props.html)
* [Difference between `name` and `id` in form inputs](https://stackoverflow.com/questions/1397592/difference-between-id-and-name-attributes-in-html#:~:text=The%20ID%20of%20a%20form,contained%20in%20the%20value%20attribute.)
* [Set value to currency in input type number](https://stackoverflow.com/a/14651044)
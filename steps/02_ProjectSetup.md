## To complete this challenge, you will need to start by setting it up:

✅ Create a new app by running the command:

```bash
npx create-react-app surreal-estate
```

Using `npx` means that we avoid installing a local version of `create-react-app` in our machine and instead we use the latest available version of `create-react-app` in the `npm` registry. It also completes a few other tasks for us:

  * Creates a project directory for us (in this case `surreal-estate`)  
  * Adds all tooling plus a `Hello World` React project 
  * Installs our project dependencies (`node_modules`) automatically, so that we do not need to run `npm i` in our project directory

✅ Now that we have basic boilerplate installed in our computer we need to check this installation works correctly:

- Check the project starts by running one of these commands (stick to either `npm` or `yarn` for all node modules commands):

```plaintext
npm start
```

```plaintext
yarn start
```

- Check the test pass by running:

```plaintext
npm test
```

```plaintext
yarn test
```
You might need to choose to `A. Run all tests` in the Jest dialogue box.

✅ Then we need to update this boilerplate - this means removing all files, markup and styles that are irrelevant to our project. We suggest the following setup:

### 1. `/public` folder
- delete all files except for `index.html`
- update `index.html` to not use the favicon we just deleted and the manifest, deleted all comments and updated meta tags and page title

### 2. `/src` folder
- Remove the `serviceWorker.js`, `reportWebVitals.js` and SVG file.
- Update the entry point to our application `index.js` by removing references to the service worker, reportWebVitals and comments.
- Update `App.js` so that it does not use and render the SVG we just deleted.

💡 If you run the application now with `npm start` what do you see? The application should run correctly with no errors on the console and, as expected, the React logo is not being rendered. Can you see the favicon we have deleted though? If yes this will happen due to browser caching. If you open ` http://localhost:3000` in another browser you will see the favicon is not being rendered.

### 3. Tidy up the file structure in the `/src` folder

At Manchester Codes we prefer a folder structure where we keep components, their styles and tests separate so we create three folders inside `/src`:

* components
* tests
* styles

and then move `App.js`, `App.test.js` and `App.css` to them correspondingly (`App.css` should also be renamed to `app.css`). The root of the `/src` folder contains now only `index.js`, `index.css` and the `setupTests.js`, which is a configuration file that powers our test suite.
  
💡 The relative import paths in the files we've just moved will, most likely, need updating! An easy way to do this is to follow the **Failed to compile** errors presented when we run our application via `npm start` or `yarn start`.

### 4. Delete  markup and styles for `<App />` and create a simple `<h2>` displaying the words `Surreal Estate`. 
In `app.css` delete all styles.

### 5. Run your tests. 
The only test in our test suite is failing. 🤔 Can you explain why this is happening?

💡 Our test suite is looking for a piece of markup which contains the text "Learn React". This has been deleted when we changed the markup to "Surreal Estate". 

✔️ Try and re-write the test so that it looks for a piece of markup which contains the text that is now relevant.

### 6. Initialise a git repo.
Stage, commit and push your work. Don't forget to commit and push your work frequently and consistently with meaningful messages 👌.

### 7. [Add a Google font](https://fonts.google.com/)
You can select as many styles as you want - choose the `Embed` tab to have access to the instructions on how to add the font to a project. We encourage you to use the `@import` method in `index.css` instead of using a `<script>` tag. Update the styling for `<body>` element in your `index.css`, replacing all the fonts brought in by `create-react-app` boilerplate with the font of your choice. We used the Nunito font.

✔️ Also delete the styling that is being applied to `<code>` markup elements.

### 8. Add additional styling to the `body` element
Set `margin` and `padding` to 0, and a light grey background.

### 9. Add the [Airbnb style guide](https://airbnb.io/javascript/)
For our project we will be using the Airbnb style guide, which in many quarters is considered the standard for developing React applications.

In any other project we would start by installing `eslint` as one of of dev dependencies however, since we are using `create-react-app` this dependency is already included. We do need to install a few other though:

```plaintext
    "eslint-config-airbnb": "^19.0.4",
    "eslint-plugin-import": "^2.26.0",
    "eslint-plugin-jsx-a11y": "^6.5.1",
    "eslint-plugin-react": "^7.30.0",
    "eslint-plugin-react-hooks": "^4.5.0"

```

We can do this by writing on the command line:

```plaintext
npm i -D  eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks
```

This will install a set of `eslint` plugins that support Airbnb Style Guide. We also need to add a configuration file `.eslintrc.json` to the root of your project with the following content:

```json
{
    "env": {
        "browser": true,
        "es6": true
    },
    "extends": [
        "plugin:react/recommended",
        "airbnb"
    ],
    "globals": {
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
    },
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": 2018,
        "sourceType": "module"
    },
    "plugins": [
        "react"
    ],
    "rules": {
    }
}
```

The configuration above represents the standard Airbnb style guide, eg, this is the code style we would use if we were to be working in the Airbnb dev team. However there's a few contentious points like the enforcing of the strict use of `.jsx` files for JSX (instead of being able to use either `.jsx` or `.js` (highly debated - have a look [here](https://github.com/airbnb/javascript/issues/1235)). 

In a nutshell, it goes like:  

- React team: you have the freedom, ✅ go forth using `.js` files for JSX components!
- Airbnb team: no ❌ 👎 🙅🏻‍♀️

At Manchester Codes we decided to side with freedom and the React team (after all they *are* the React team) and we're going to overwrite that rule and a couple more by editing the `rules{}` key in the file `.eslintrc` you just created (and saved, we hope) to:
 
```json
  "rules": {
    "no-underscore-dangle": [0],
    "react/jsx-props-no-spreading": [0],
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".js", ".jsx"]
      }
    ],
    "react/function-component-definition": [
      2,
      {
        "namedComponents": "arrow-function"
      }
    ]
  }
```

Besides allowing us freedom to use `.js` or `.jsx` extensions, we are also allowing ourselves to use prop spreading like `{...props}` and `underscore dangles` as we will use a variable named `_id` further on the track. We are also enforcing the use of ES6 arrow functions for named components.

This is a good example of how to change specific rules when using a popular style guide as a standard. When working in a team these standards should be agreed in advance so that there is consistency across a code base. 

One last thing, as we will be using `jest` and the style guide is agnostic regarding testing framework - we need to add an extra key/value pair of `"jest": true` to `.env` key in `.eslintrc` so that our linter knows how to handle `jest` global variables like `describe`, `test`, etc.

```json
  "env": {
    "browser": true,
    "es2020": true,
    "jest": true
  }

```

### 10. Install Prettier.
We strongly recommend the use of Prettier with VSCode as it helps with keeping to the style guide without much effort. If you do not have it installed in VSCode there is this great [guide](https://medium.com/javascript-in-plain-english/set-up-react-js-with-eslint-prettier-and-airbnb-cc015363a7c7)

If you already use Prettier with VSCode, just install a few dependencies with `npm i -D prettier eslint-config-prettier eslint-plugin-prettier` and then update the `extends` in the `.eslintrc` file with:

```json
"extends": [ "airbnb", "plugin:prettier/recommended" ]
```

You shouldn't see any linting errors but if you do try closing VSCode and opening it again so it's forced to read any changes to the configuration files.

### 11. Last but not the least, update the `Readme`!

## Recommended Reading

- [:zap: Components](https://hackmd.io/s/ryKpNrWKV)

- [React Fragments](https://reactjs.org/docs/fragments.html)

- [MDN: CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

- [0to255: #000](http://www.0to255.com/000)
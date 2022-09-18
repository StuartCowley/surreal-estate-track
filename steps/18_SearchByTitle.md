![Search](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/search.png)

So far we've explored how we can filter results from the Surreal Estate API with the `query` query parameter, and sort them with the `sort` query parameter. Now we need to use the `query` query parameter to search. We can do so like so:

```js
?query={"title":{"$regex":"<search_query_here>"}}
```

Previously we have filtered like so:

```js
?query={"city":"Exeter"}
```

When we pass an object with a `$regex` key, we say instead "match the given value (in this case `<search_query_here>`) against part of the field's value. So if we did:

```js
?query={"title":{"$regex":"bungalow"}}
```

Then we'd get back all properties with the word `bungalow` in the title. Note that this isn't very advanced search functionality, but will suffice for not overcomplicating this track too much. Large organisations will more likely use something like Elastic Search to handle their search operations.

What you need to do is to create a search form that - when submitted - programatically (without the `<Link />` component) changes the URL to include your search query. A spanner in the works is that you will still need to be able to filter search results by city, so you will need to find a way of combining `query` objects inside your `buildQueryString` method so that the following is possible:

```js
?query={"city":"Exeter","title":{"$regex":"bungalow"}}
```

## To complete this challenge, you will need to:
* Create a search form inside your `<SideBar />` component which should consist of a text `<input>` and a submit `<button>`. The text `<input>` should be tied to a field in your state (`query` or `search` would be good field names) - refer back to the [AddProperty step](https://platform.manchestercodes.com/module/frontend/further-react/?pageId=8TqoTDrAlvkzxelfwDuP) if you are unsure about this. On form submission, a `handleSearch()` function should be called on your component.
* Inside the `handleSearch()` function you should call your `buildQueryString()` function, passing in `'query'` as your first argument and `{ title: { $regex: <search query here> } }` as your second argument. Note that `<search query here>` will be replaced with the value of your text `<input>`, which should come from the state that you set earlier. Assign the result of invoking `buildQueryString()` to a variable.
* Use the `useNavigate()` hook from `react-router-dom` to programatically change the URL to your new query string returned from the `buildQueryString()` function.
* Give this a test run in your browser to check everything is working A-OK. You should notice that it isn't currently possible to search **and** filter by city.
* Modify your `buildQueryString()` function so it supports more than one `query` key. Hint: you can achieve this by spreading one level deeper.

## Useful Documentation
 - [querying an API generated with express-restify-mongoose](https://florianholzapfel.github.io/express-restify-mongoose/#query)
- [MongoDB query operators](https://docs.mongodb.com/manual/reference/operator/query/)
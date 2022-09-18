For this project, you'll be using an API that we've developed for the course. This is a walkthrough-only step where we'll get the API running, and we'll make some sample HTTP requests to it.

Clone down the [surreal-estate-api](https://github.com/MCRcodes/surreal-estate-api) repository and follow the instructions in the README to "Run in a container".

** Note **
You can check if you already have `docker-compose` installed by writing on a terminal window `docker-compose --version`

In a new terminal tab, change directory into the API folder and run `docker-compose up`. This process fires up a local express server connected to a remote MongoDB database, so you'll need to keep this process running (don't close the tab).

💡 Did you get this error when bring docker container up?

```plaintext
ERROR: for surreal-estate-api_express-app_1  Cannot start service express-app: driver failed programming external
connectivity on endpoint surreal-estate-api_express-app_1 (6c4ab9630051beb9ad4e9c3dfa5091a70fd82e151b019a64723eb438f0f0ee1c): 
Bind for 0.0.0.0:4000 failed: port is already allocated
```
It means something else is using that port. To solve this problem open `docker-compose.yaml` (in `surreal-estate-api` directory) and change `4000` to other port, then run `docker-compose up` again. **Remember to use the right port in the following steps** in that case.

Visit [http://localhost:4000/api-docs](http://localhost:4000/api-docs) in your browser to view the API documentation - keep this tab open as we'll be referencing it later:

![Swagger](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/swagger.png)

** Note **
There is a chance your API might be running on a different port to `4000`. In order to check in which port your API is running, head to the terminal tab where docker compose is running and look for the line below, where <PORT NUMBER> is the port where the API is running:

```plaintext
express-app_1  | Surreal Estate API is running on :<PORT NUMBER>
```

Download and install [Postman](https://www.getpostman.com/) if you haven't done it before. Postman allows us to make requests to an API and view any response data that comes back.

** Note **
If you've completed the backend module you will be familiar with Postman and how to use it! You probably want to skim this page if that is the case.

Open Postman. On the landing screen click the 'X' to close the modal:

![Postman Landing](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/postman_landing.png)

We want to create a new property listing, so head back to [your API documentation](http://localhost:4000/api-docs). We have the following endpoints:

![Endpoints](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/endpoints.png)

Click on the POST endpoint:

![POST endpoint](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/post.png)

Here you can see the fields that a property listing can have and the types associated with those fields:

```json
{
  "_id": "string",
  "title": "string",
  "type": "string",
  "bedrooms": 0,
  "bathrooms": 0,
  "price": 0,
  "city": "string",
  "email": "string"
}
```

We can see here that a property listing can have a title, type, city and email, which are all strings, and bedrooms, bathroom and price, which are all numbers. We can use Postman or JavaScript to send a JSON object matching the above interface to the endpoint `/PropertyListing`. However, we first need to know what the _base URL_ is - that is the URL we prepend to the endpoint. You can find that at the top of the documentation:

![Base URL](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/baseurl.png)

So our full request URL will be `http://localhost:4000/api/v1/PropertyListing`, and we will be making a POST request.

Lets head back to Postman:

![Postman](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/postman.png)

At the top you have the HTTP request type dropdown and an address bar to create a new request:

![Request Bar](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/requestbar.png)

Choose POST from the dropdown, and enter your request URL. Don't click Send just yet - we still have to specify the data we want to send across.

Below the request bar, select the `Body` tab:

![Body](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/body.png)

We want to send raw data (essentially text) so choose the `raw` radio button. A dropdown should appear on the right with a selected option of `Text`. Change it to `JSON (application/json)`:

![JSON](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/json.png)

You should now be familiar with JSON - it stands for JavaScript Object Notation, and it's essentially a JavaScript object represented as a string that can be sent to and retrieved from servers.

Now take the fields object from earlier and copy it into the editor:

![Editor](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/editor.png)

Remove the `_id` field - ID fields traditionally get created by the API  so we don't need to worry about specifying this. 

Change the values of your other fields (ensuring you use the correct type) and then click the `Send` button.

You should see a successful response (indicated by `201 Created`) below:

![Response](https://s3.eu-west-2.amazonaws.com/mcrcodes/course/surreal-estate/response.png)

Notice how this response has an `_id` field despite us not specifying one.

## Your turn

* Make a GET request to retrieve this property back from the API. Use the API docs to choose the appropriate endpoint. Note that you will swap `{propertyListingId}` for the `_id` value of the property.

* Add another property.

* Make a GET request to retrieve all properties.

* Delete your first property (DELETE request).

* Update the title of your remaining property (PATCH request). Note that in a PATCH request you only have to send the fields over you wish to update, not the whole object. You specify the property ID in the request URL, so this doesn't need to be part of the object either.
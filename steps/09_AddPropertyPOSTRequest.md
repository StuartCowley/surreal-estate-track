You've got your add property form in place with the data ready to be sent off to the API, and you should now have made some example requests. Now you'll use [Axios](https://github.com/axios/axios) to make those requests inside of the browser.

It's important that you get used to reading documentation, so we're leaving this step completely up to you. You can find the Axios documentation [here](https://github.com/axios/axios/blob/master/README.md) - there are a couple of examples on how to make requests. Refer back to the Surreal Estate API documentation (previous step) if you can't remember the HTTP request type or the URL you need to make the request to.

The only hint we will give is that you are already logging out the data you need to send inside of the `handleAddProperty()` method on the `<AddProperty />` component. You should swap this `console.log()` out for your Axios request.

The Axios request call returns a Promise object. In order to verify a successful/unsuccessful request, you should use the this promise, logging out the response object or error object (if there is one) to the console. You should also verify the property has been added in Postman.

## Recommended Reading

* [Axios Documentation](https://github.com/axios/axios)
* [YouTube: How to use Axios with React](https://www.youtube.com/watch?v=oQnojIyTXb8)
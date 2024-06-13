---
title: "Learning to make a Temperature Converting API using Express.js"
date: 2022-06-12T00:00:06+05:30
description: "One of the first few tasks of the internship I recently got, was to develop a simple RESTful API which converted a given temperature from Farhenheit to Celsius and vice versa"
---
One of the first few tasks of the internship I recently got, was to develop a simple RESTful API which converted a given temperature from Farhenheit to Celsius and vice versa. 
{{<figure src="https://i.morioh.com/8c8203b86e.png">}}

The choice of technology was left up to me. Having worked with **Node and Express.js** before, I decided it would be convenient for me to work on the API using these. It would be easier developing an understanding over the API structure and its nuances, without having to worry about learning the syntax of a new language.

### How I learned developing the API
Developing an API was a new and challenging task for me since I'd never worked on one before.
Multiple Google searches and YouTube videos later, I was able to...  <br> <br>
...differentiate between a GET and POST request.  
<br>
Understanding the different types of requests and how they behave with the data is essential. The API I'm working with mainly operates on these two requests -
1. **GET** - to retrieve data from the server at the specified source
2. **POST** - to create or update data on the server at the specified source  

{{<figure src="https://s3-us-west-2.amazonaws.com/assertible/blog/swagger-petstore-store-endpoints.png">}}

#### Basic API Structure
Our API takes in temperature value as a *request* parameter, and gives us the converted value as a *response*.  
We specify two endpoints for the different conversions
- Celsius to Fahrenheit (.../CtoF)
- Fahrenheit to Celsius (.../FtoC)  
  ...or we could go bonkers and add Kelvin conversions too.

The code is structured something like this - 

Importing the *Express.js* Node module into our file and specifying the port at which to host our server.
```js
/* index.js */
const express = require("express");
const app = express();
const PORT = 8080;
app.use(express.json());

// Listen for requests at the specified PORT
app.listen(PORT, () => console.log(`Listening at localhost:${PORT}`));

```

Using `express.json()` essentially allows our server to parse the JSON which comes in the request body, or we're met with an error which says
```powershell
TypeError: Cannot read properties of undefined (reading '<object>')
```
(I learnt this the hard way, struggling with this one line of code for a few hours as my API refused to accept JSON in the request). <br><br>
Before adding code for the conversion, let's test a simple request to our API to make sure everything's A-OK.

Implementing a simple GET request to the API -
```js
/* index.js */
app.get('/', (req, res) => {
  res.send('A-Ok')
})
```
Let's run the server using ```node index.js``` and then fire up Postman to check the call to our API -
{{<figure src="https://user-images.githubusercontent.com/70942982/173202113-c30f9f4d-6228-47bb-b0b9-1f085a65b154.png" class="center-image">}}

Great, everything works.

#### Temperature Conversions

Let's add code for the conversion now. Even though the demonstration at hand is a small example, we'll split it into two files for cleaner and maintainable code at scale.

```js
/* index.js */
app.use('/FtoC', FtoC)
app.use('/CtoF', CtoF)
```
Taking the first line as an example to explain what's going on here.  
This piece of code tells our server to handle all requests which are received at the endpoint `/FtoC`, using our Express router `FtoC`, which is provided as a callback function.  
For this ⬆️ to work, we need to first make our router functions in a separate file and then import the router in `index.js`.

##### Router Function

```js
/* tempConverter/FtoC.js */
const router = require('express').Router();
```
Here we're creating an Express router instance to handle the requests received.

And then we handle our GET request which contains the value for temperature in the request body - 
```js
/* tempConverter/FtoC.js */
router.get('/', (req, res) => {
  let reqF = req.body.fahrenheit
  let resC = (reqF - 32) * 5/9

  res.status(200).send({
    "enteredFahrenheit": `${ reqF }`,
    "calculatedCelsius": `${ resC }`
  })
})
module.exports = router
```
<center><sup><sub>(note that we could make it either a POST request or a GET request for this task since we are just computing a value from the request parameter and returning it as a response)</sub></sup></center>

We are storing the Fahrenheit value from the request body into a variable `reqF` (stands for 'Request Fahrenheit'), performing the required calculation for Celsius conversion and storing it into the variable `resC` (stands for 'Response Celsius').  <br><br>
We're then sending a response back from the server -  a JSON object which contains Fahrenheit value entered and the output Celsius value. <br><br>


##### Important Note to Self
It took me a while to understand why we were taking `'/'` as the request route, instead of `/FtoC` in our router file.
That's because `index.js` is pointing our callback function to `/FtoC` already.
```js
/* index.js */
app.use('/FtoC', FtoC)
```
which makes `/FtoC` the root endpoint for our router function. Hence we specify `'/'` as the route for our router function to operate on.  <br><br>

Before we test the API, we need to import our router function into `index.js`.

```js
/* index.js */
const FtoC = require('./tempConverter/FtoC')
```

### Testing the API
The code in `tempConverter/FtoC.js` tells us we need a Fahrenheit object in our request body.

Let's make the GET request to `localhost:8080/FtoC` using Postman with

```json
{
    "fahrenheit": -40
}
```
in the request body.

{{<figure src="https://user-images.githubusercontent.com/70942982/173204187-a3703fa6-269e-49de-b87d-4b04c2ebbe7c.png" class="center-image">}}

We're getting the output Celsius value equal to the input Fahrenheit value at -40. This tells us two things.
1. Our API is working as expected!
2. Fun fact : Fahrenheit and Celsius are equal at -40.

Similarly, the code for Celsius to Fahrenheit conversion would require us to create a router function in a new file, and then importing the router in our `index.js` file, specifying the endpoint and callback function.

# Web Servers // Express // Middleware

**What it means to be a server?**

To serve a correct response to all requests

http://localhost:8000

It points to your own machine. "Look at this website at your own machine"
"8000": port

Request is a long object full of information
But have two main information
`url` and `method` *request.method* and *request.url*
Is the action I want (method) on which resource (url)


## Express

`app.get('/', callback function)`
`app.get('/toronto', another callback function)`


The callback function can render the page from the file
`app.render('toronto')`
*where toronto is the file name*

You can code an **app.get** for each ROUTE

*npm install express* DON'T FORGET TO INSTALL THE PACKAGE

This method helps us to separate our **control logic** from our **html**


`app.set("view engine", "ejs")`

**-----------------------------------------------------------------------**

## Express Made Easy

```javascript
const express = require('express')                      //Hiring the Manager
const app = express()

app.use('/', function(req, res, next) {                 //Customer got shirt and shoes?
  console.log('Request: ', req);                        //Otherwise they can't be seated
  console.log('Response: ', res);                       //If they want to sit at the bar, are they old enough?
  next();
});

app.get('/', function (req, res) {                      //Taking an Order
  res.send('Hello World!');
};

app.listen (3000, function () {                         //Open for business
  console.log('Example app listening on port 3000!')
})
```

### Require Statemens (Hiring the manager)

* Need NPM to install the package
* Use **require** statement to load the module
* Need a variable to hole your Express application

```javascript
const app = express();
```

### Middleware

* Allow you to take action on any incoming requests and modify it before sending back a response
* Start with **app.use()**

### Routing (Taking an Order)

* Allow us to script specific actions based on the **path**
* GET, POST, PUT and DELETE
* GETs do no modify or add to your database. THey just retrieve information based on specific parameters

```javascript
app.get('/table/:amount', function (req, res) {
  var party = req.params.amount
  res.send('We are searching for your table for '+party+'!');
})
```

### Ports (Open for business)

* Since your server can handle many types of restaurants at once, ou need to tell it where each script should run

**-----------------------------------------------------------------------**

# Class






# HTTP & API

## Class

`HTTP` it's a protocol on how to exchange information.

### Web Server and Web Client

A client request a resource, the server that has the resource respond and send the information.

The resource is represented by the URL (Uniform Resource Locator)


http: protocol
www: host
example.com: domain
80, 88: port (need to specify only when different from the standard)
/hello: path
?words: parameters (optional)

### TCP/IP

A collection of protocols that we can use for different scenarios.

`TCP`: transport control protocol
TCP is responsible for taking all the data that is going to be transfered, label it, and guarantee that is being delivered in the right order.

`IP`: Internet protocol
IP is resposible for adressess, making sure the packages gets to the right destination.

---
### HTTP Fundamentals

`DNS`: Domain Name Service/System

Most common HTTP responses: 200, 204, 301, 304, 403, 404, 500

** HTTP Methods/Verbs**

* GET (Read): request data from a server. Data could be html, images, videos, etc
* POST (Create): send data from the browser to the server. Ex: registration form
* PUT & PATCH (Update)
* DELETE (Delete)

### API Endpoints

`API`: application program interface

Lots of data can be behind the wall and the API let's part of it to be accessible.

**Example**

```javascript
var request = require('request');
var fs = require('fs'); //required to manipulate files inside your system
var query = process.argv.slice(2);

request("<URL>" + query, function (error, response, body){
  if (error){
    console.log(error) ;
    return;
  }
  if (response.statusCode === 200) {
    var data = JSON.parse(body);
    // console.log(data) ;

    var woeid = data.[0].woeid;

    request("URL" + woeid + "/", function(error, response, body){
      if (error) {
        console.log(error);
        return
      }
      if (response.statusCode === 200) {
        var weatherData = JSON.parse(body);
        console.log(weatherData.consolidated_weather[0].the_temp) ;
        console.log(weatherData.consolidated_weather[0].humidity) ;

        var pathIcon = "<URL>" + weatherData.consolidated_weather[0].weather_state_abr + ".ico"
        //...
      }
    })
  }
});
```


## Anatomy of an HTTP Transaction

https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/


### Create the Server

```javascript
const http = require('http');

const server = http.createServer((request, response)) => {
  //magic happens here
}
```

In fact, the **Server** objet returned by **createServer** is an **EventEmitter**, and what we have here is just shorthand for creating a *server* object and then adding the listener later.


```javascript
const server = http.createServer();
server.on('request', (request, response) => {
  // the same kind of magic happens here
});
```
In order to actually serve requests, the **listen** method needs to be called on the server object. In most cases, all you'll need to pass to *listen* is the port number you want the server to listen on.

** ------------------------------------------------------------------------------------------------------------ **


### Method, URL and Headers

When handling a request, the first thing you'll probably want to do is look at the metod and URL, so that appropriate actions can be taken.


```javascript
const {method, url} = request;
```

* Method: is a normal HTTP method/verb
* URL: is the full URL without the server, protocol or port

Headers are also not far away. They're in their own object on *request* caleed *headers*.

```javascript
const {headers} = request;
const userAgent = headers['user-agent'];
```

* Note here that all headers are represented in lower-case only, regardless of how the client actually sent them

** ------------------------------------------------------------------------------------------------------------ **


### Request Body

When receiving a *post* or *put* request, the request body might be important to your application.


```javascript
let body = [];
request.on('data', (chunk) => {
  body.push(data);
})
      .on('end', () => {
        body = Buffer.concat(body).toString();
        //at this point, 'body' has the entire request body stored in it as a string
});
```

** ------------------------------------------------------------------------------------------------------------ **


### A Quick Thing About Errors

Since the *request* object is a **ReadableStream**, it's also an **EventEmitter** and behaves like one when an error happens

**If you don't have a listener for that event, the error will be *thrown*, which could crash your Node.js program**

```javascript
request.on('error', (err) => {
  //this prnts the error message and stack trace to 'stderr'
  console.log(err.stack);
});
```

** ------------------------------------------------------------------------------------------------------------ **


### HTTP Status Code

If you don't bother setting it, the HTTP status code on a response will always be 200.

```javascript
response.statusCode = 404;
```








```javascript

```
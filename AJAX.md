# AJAX

AJAX is a developer's dreams, because you can

* Read data from a web server - after the page has loaded
* Update a web page without reloading the page
* Send data to a web server - in the background


AJAX uses a combination of:

* A browser built-in `XML Http Request` object
* JavaScript and HTML DOM (to display or use the data)

**How AjAX Works**

1. An event occurs in a web page (the page is loaded, a button is clicked)
2. An XML Http Request object is created by JavaScript
3. The XML Http Request object sends a request to a web server
4. The server processes the request
5. The server sends a response back to the web page
6. The response is read by JavaScript
7. Proper action (like page update) is performed by JavaScript


## XMLHttpRequest Object Methods

* new XMLHttpRequest()                  Creates a new XMLHttpRequest object
* abort()                               Cancels the current request
* getAllResponseHeaders()               Returns header information
* getResponseHeader()                   Returns specific header information
* open(method, url, async, user, psw)   Specifies the request
                                        *method*: the request type GET or POST
                                        *url*: the file location
                                        *async*: true (asynchronous)
                                        *user*: optional user name
                                        *psw*: optional password
* send()                                Sends the request to the server. Used for GET requests
* send(string)                          Sends the request to the server. Used for POST requests
* setRequestHeader()                    Adds a label/value pair to the header to be sent

## XMLHttpRequest Object Properties

* onreadystatechange                    Defines a function to be called when the readyState property changes
* readyState                            Holds the status of the XMLHttpRequest
                                        *0*: request not initialized
                                        *1*: server connection established
                                        *2*: request received
                                        *3*: processing request
                                        *4*: request finished and repsonse is ready
* responseText                          Returns the response data as a string
* responseXML                           Returns the response data as XML data
* status                                Returns the status-number of a request
                                        *200*: OK
                                        *403*: Forbidden
                                        *404*: Not found
* statusText                            Returns the status-text (eg OK or Not found)

## Send a Request to a Server

We use the `open()` and `send()` methods of the **XMLHttpRequest** object

```javascript
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```

* open(method, url, async, user, psw)   Specifies the request
                                        *method*: the request type GET or POST
                                        *url*: the file location
                                        *async*: true (asynchronous)
                                        *user*: optional user name
                                        *psw*: optional password
* send()                                Sends the request to the server. Used for GET requests
* send(string)                          Sends the request to the server. Used for POST requests


## GET Requests

```javascript
xhttp.open("GET", "demo_get.asp", true);
xhttp.send();
```

In the example above, you may get a cached result. To avoid this, add a unique ID to the URL

```javascript
xhttp.open("GET", "demo_get.asp?t=" + Math.random(), true);
xhttp.send();
```

If you want to send information witht he `GET` method, add the information to the URL

```javascript
xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford", true);
xhttp.send();
```

## POST Requests

A simple `POST` request

```javascript
xhttp.open("POST", "demo_post.asp", true);
xhttp.send();
```

To POST data like an HTML form, add an HTTP header with `setRequestHeader`. Specify the data you want to send in the `send()` method:

```javascript
xhttp.open("POST", "ajax_test.asp", true);
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhttp.send("fname=Henry&lname=Ford");
```

* setRequestHeader()                    Adds a label/value pair to the header to be sent
                                        *header*: specifies the header name
                                        *value*: specifies the header value




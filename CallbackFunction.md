# Callback Function

https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced?fbclid=IwAR0ItyZAz_7u9v9iHIy9gRB8uAvBatboQ8dKtfIIFqzO0UzCAPcolIOR7ck

## Definition
A callback is a function that is to be exectured after another function has finished executing.

In JavaScript, functions are objects. Because of this, functions can take functions as arguments, and can be returned by other functions. Functions that do this are called higher-order functions. Any function that is passed as an argument is called a callback function.

## Why do we need Callbacks?
Because Javascript is an event driven language, which means, that instead of waiting for a response before moving on, JS will keep executing while listening for other events.

```javascript
function first(){
  console.log(1);
}

function second(){
  console.log(2);
}

first();
second();

-> 1
-> 2
```

But what if "function first" took a while to be evaluated?

```javascript
function first(){
  // Simulate a code delay
  setTimeout( function(){
    console.log(1);
  }, 500 );
}

function second(){
  console.log(2);
}

first();
second();

-> 2
-> 1
```

So why show you this? Because you can;t just call one function after another and hope they execute in the right order.
->Callbacks are a way to make sure certain code doesn't execute until other code has already finished execution.<-

##Create a Callback

```javascript
function doHomework(subject) {
  alert(`Starting my ${subject} homework.`);
}

doHomework('math');

-> Alerts: Starting my math homework.
```

Now let's add in our callback.

```javascript
function doHomework(subject, callback) {
  alert(`Starting my ${subject} homework.`);
  callback();
}

doHomework('math', function() {
                      alert('Finished my homework');
                    }
          );
```

But callback functions don't always have to be defined in our function call.
They can be defined elsewhere in our code like this:

```javascript
function doHomework(subject, callback) {
  alert(`Starting my ${subject} homework.`);
  callback();
}
function alertFinished(){
  alert('Finished my homework');
}
doHomework('math', alertFinished);
```














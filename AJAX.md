# AJAX

AJAX = Asynchronous JavaScript and XML
A concept or methodoogy using JavaScript

JavaScript ->
1. Dynamicism on the page
2. ????

AJAX
Loading the page in the smallest....

AJAX as a function: fetching content, communicating with the server asynchronously.

```javascript
const title = 'Good Morning lighthouse';
const clickHandler = () => console.log('I have been clicked')

$(document).ready(() => {
  setTimeout( () => {

    const h2 = `<h2 onclck='clickHandler()'>${title}</h2>`

    $(`.title`).html(h2)

  }, 2000)

})
```

XHR = XML HTTP Request = object with error information



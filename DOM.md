# DOM

DOM = Document Object Model

Events can be triggered on any part of a document, whether by a user's interaction or by the browser.

## Listening for DOM events

In JavaScript, we can listen to events using this:

```JavaScript

element.addEventListener(<event-name>, <callback>, <use-capture>);

```

* `event-name` (string) This is the nam eor type of event that you would like to listen to (click, mousedown, touchstart, transitionEnd, etc).
* `callback` (function) This function gets called when the event happens. The **event** object, containing data abou the event, is passed as the first argument.
* `use-capture` (boolean) This decalres whether the callback should be fired in the "capture" phase.

*Example*

```JavaScript
var element = document.getEelementByID('element');

function callback() {
  alert('Hello');
}

// Add listener
element.addEventListener('click', callback);
```

### Maintaining Callback Context

```JavaScript
var element = document.getElementById('element');

var user = {
  firstname: 'Wilson',
  greeting: function() {
    alert('My Name is ' + this.firstname)
  }
};

// Attach user.greeting as a callback
element.addEventListener('click', user.greeting);

// alert => 'My name i undefined'
```

When we pass the `greeting` function to the `addEventListener` method, we are only passing a reference to the function; the context of `user` is not passed with it.
Internaly, the callback is called in the context of `element`, which means that `this` refers to `element`, not to `user`.
Therefore, `this.firstname` is undefined.



**Solution: Function.Prototype.Bind**

_.bind()_  method generate a new function (`bound`) that will always run in the give context. We then pass that function as the callback to `.addEventListener()`.

```javascript
// Overwrite the original function with one bound to the context of 'user'
user.greeting = user.greeting.bind(user);

// Attach the bound usergreeting as a callback
button.addEventListener('click', user.greeting);
```

### The Event Object

We can use this object to access a wealth of information about the event that has occurred:
* `type` (string) this is the name of the event
* `target` (node) this is the dom node where the event originated
* `currentTarget` this is the DOM node that the event callback is currently firing on
* `bubbles` (boolean) this indicates wheher this is a "bubbling" event
* `preventDefault` (function) this prevents any default behavior from ocurring
* `stopPropagation` (function) this prevents callbacks from being fired on any nodes further along the event chain.
* `stopImmediatePropagation` (function) this prevents any callbacks from being fired on any nodes further along


### Event Phases

In short, the event flows from the document's root to the target (ie capture phase), the fires on the event target (target phase), ten flows back to the document's root.

* Capture Phase
The event starts its journey at the root of the document, working its way down through each layer of the DOM.
The job of the capture phase is to build the propagation path, which the event will travel back through in the bubbling phase.

* Target Phase
The event fires on the target node, before reversing and retracing its steps, propagatins back to the outermost document level.

* Bubbling Phase
After an event has fired on the arget, it doesn't stop there. It bubbles up (or propagates) through the DOM until it reaches the document's root.
The majorit of, but not all, events bubble. When events do not bubble, it is usually for a good reason.

### Delegate Event Listeners

Delegate event listeners are a more convenient and performant way to listen for event on a large number of DOM nodes using a single event listener.

For example, if a list contais 100 items we would have to add 100 separate event listeners.
Instead of listening for the `click` event on each element, we listen for it on the parent `<ul>` element. When an `<li>` is clicked, then the event bubbles up to the `<ul`> triggering the callback.

example

```javascript
var list = document.querySelectio('ul');

list.addEventListener('click', function(event) {
  var target = event.target;

  while (target.tagName !== 'LI') {
    target = target.parentNode;
    if (target === list) return;
  }

  // do stuff here
})
```

If you are using JQuery, you can seamlessly uuse event delegation by passing a selector as the second parameter to the `.on()` method

```javascript
// Not using event delegation
$('li').on('click', function(){});

// Using event delegation
$('ul').on('click', 'li', function(){});


let keypress = document.addEventListener("keypress", (event) => {
  console.log("KeyPress");
});


let keydown = document.addEventListener("keydown", (event) => {
  console.log("KeyDown");
});


let keyup = document.addEventListener("keyup", (event) => {
  console.log("KeyUp");
});
```
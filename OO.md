# Introduction to Object Oriented Programming

**What is Object Orientation?**

Is a way of writing code that encourages modularity and reduces duplication through the user of *objects*.

Programming langues that are *predominantly* OO:

- C++
- C#
- Java
- Python
- Ruby
- PHP
- Swift
- Objective-C

! Conclusion !

* OO is a software development paradigm
* OO is a popular way to solve code organization, re-use and modularity
* OO is very important to learn due to its popularity
* JS is nto strictly OO in the way that Java or Ruby are
* Functional Programming is an alternative paradigm, and one that JavaScript also encourages

## Simple OOP in JS

In JS variables look like this

```javascript
const dogSound = 'woof';
let dogBreed = 'shih tzu';
```

Functions look like this

```javascript
function speak() {
    console.log(`${dogBreed} says ${dogSound}`);
}
```

and objects looks like this

```javascript
const dog = {
    sond: 'woof',
    dogBreed: 'shih tzu',
    speak: function() {
        console.log(`${dogBreed} says ${dogSound}`);
    }
}
```

In OO we use objects to group related variables and functions together to keep our code more organized.

An object is a little bundle of information, also known as **state**.
Each property that an object has, can represent the state of that object.

An object is not just state, an object also has some stuff it can do known as behaviour. This behaviour takes the form of **methods**.

## This

Just like in normal english, *this* means nothing without context. The value of *this* is determined at the tome of the call
and depends on how and where it was called.

All we really need to know for OO in JavaScript, is that when you use *this* inside a method, *this* refers
to the **object** that the method was called on.

```javascript
const dog = {
    sound:'woof'
    function speak () {
        console.log(this.sound);
    }
}

dog.speak();
// woof
```

```javascript
const dog = {
  sound: "woof",
  speak: function() {
    console.log(this.sound);
  },
  teachMeSomething: function() {
    if (dog === this) {
      console.log('dog === this');
    }
    this.speak();
  }
};
// dog === this
// woof
```

## Using objects

`Express Response`

In Express, we write endpoint handlers that take two arguments, a *request* and a *response*.

```javascript
app.get('/', (request, response) => {
    response.status() // to set the status of the response
    response.set() // to set outgoing headers of the response
    response.json() // to send an objet as JSON in the response-body
    response.get() // to see what headers we've already set
    response.locals;
    response.headersSent;
})
```

So, again, we have these thigs called *objects* that fit into variables. They have some methods and properties, some internal state.

Not all objects have all of these things, but the idea of bundling up some methods and some state into a single "thing" is what makes an objects an object (in the sense of "object-oriented)

`! Conclusion !`

In the context of object orientation, an object is a little bundle of information.
Actually, it's not just information (aja "state"); an object also has some stuff it can do (aka "behavirou")

OO bundles (groups) together related *state* and *logic* into an object that can be passed around as a single entity.

## A Quick Disclaimer About Classes in JS

JS's object system is based on another pattern known as *prototypes*, not *classes*.

JavaScript mimics the behaviour of class-based or *classical* OOP languages now.

> Classes and Instances

Classes are blueprints. It has all details and instructions to build a house, but it's not a house.

We can create as many houses as we want. Each house will be separate from the other one. Completely unique houses, but all based on the same blueprint.

In OOP, *classes* are blueprints (templates) that we use to create *instances* of objects. A class describes what the object is going to be and we
can create new objects using the class.

To create a class, you use the **class** keyword with the name of the class

```javascript
class Pizza {

}
```
- The class name should always be a noun
- The first letter should always be capitalized

To create a new object from the class, we use the **new** keyword

```javascript
let pizza1 = new Pizza();
let pizza2 = new Pizza();
```
*pizza1* and *pizza2* are pizza objects. These objects are both instances of the same class. 

```javascript
pizza1 === pizza2 // false
```

> Methods and Properties


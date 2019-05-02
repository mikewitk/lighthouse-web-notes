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

```javascript
class Pizza {

  constructor() {
    this.toppings = ["cheese"];
  }
  
  addTopping(topping) {
    this.toppings.push(topping);
  }
}
```

You can add a method to a class with the following syntax:

```javascript
class SomeClass {
  methodName(parameters) {
    // this is a method
  }
}
```

To add properties to a class, simply use *this* keyword followed by the property name, then assign it a value

```javascript
class SomeClass {
  someMethod() {
    this.hello = "hi"; // Created a property called hello
  }
}
```

Any pizza object created from this *Pizza* class will have its own version  of these properties and methods.
This means we can call the **addTopping()** method on *pizza1* without affecting *pizza2*.

> Introduction to *Constructor*

*Constructor* is a special kind of method that gets executed when an object instance is created from a class.

This is a great place to setup default state for new instances.

> Customizing the Constructor

Every class can have a **single constructor method** that will get called when an instance of that class is created.

Since it's a method, we can also **pass values to the constructor method**.

```javascript
class Pizza {
  
  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addToppings(topping) {
    this.toppings.push(topping);
  }
}
```

## Inheritance

With inheritance, we can build a new class based on existing class.

Now there is a general Person class that contains the shared code. Student and Mentor inherit behaviour and state information from Person using the keyword extends. They also have their own code that reflects behaviour and information only pertaining to themselves.

Student and Mentor are subclasses of the Person class, since they are extensions of that class. Person is the superclass in this relationship

```javascript
// This class represents all that is common between Student and Mentor
class Person {
  // moved here b/c it was identical
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // moved here b/c it was identical
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}
class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}

class Mentor extends Person {
  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }
}
```

## Method Overriding

Sometimes you want a subclass to have similar but slightly different behaviour to its superclass.

> Solution 1: Methor Override

```javascript
// Superclass
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// Subclass
class Mentor extends Person {
  // Completely re-define the bio method since it has more to say
  bio() {
    return `I'm a mentor at Lighthouse Labs. My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// The Student class doesn't need to define bio since it can just use the one from Person

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

While this is indeed a step in the right direction, it isn't ideal because we are repeating the logic.

> Super

OOP languages allow subclasses to have a reference on the parent class. This is usually done via the **super** keyword, and JavaScript
supports it too

```javascript
// Super class
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

## Getters and Setters

Getters and setters are special methods that are used to get the value of a property or set the value of a property.

There are many reasons you might want to use getters and setters in your app.

Let's go over two main reasons right now:

* Validating data before assigning it to a property
* Computing a value on the fly instead of simply pulling it out of a property

**VALIDANTE DATA**

Using a setter method instead of setting the size property directly, we can have the object validate the value before it gets set.

```javascript
// setSize now includes data validation
  setSize(size) {
    if (size === 's' || size === 'm' || size === 'l') {
      this.size = size;
    }
    // else we could throw an error, return false, etc.
    // We choose here to ignore all other values!
```

**COMPUTED VALUE**

We could create a property to keep track of the price of a pizza. Every time the size or toppings change, we could just update this price property. But that involves constantly keeping track of the price. It would be easier to just compute the price of the pizza when it's needed.

```javascript
class Pizza {

  // ...

  getPrice() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + (this.toppings.length * toppingPrice);
  }
}

// DRIVER CODE
let pizza = new Pizza();
pizza.getPrice();
```

**PRIVATE PROPERTIES**

Now that we have our getter and setter methods in place, we want to make sure that no one accesses the properties directly.

The way we do this in JavaScript is by adding an _ to the beginning of the property name. So this.size becomes this._size. 
Adding an _ doesn't change the behaviour, it just tells other developers not to access the property directly.

> A Better way *get* and *set*

```javascript
class Pizza {

  // ...

  // replace our custom getters / setters with these ones!
  get price() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + this.toppings.length * toppingPrice;
  }

  set size(size) {
    if (size === 's' || size === 'm' || size === 'l') {
      this._size = size;
    }
  }
}
```

The only new things here are the **get** and **set** keywords in front of the getter and setter methods. 
The main difference we get from using these is that price and size will now be accessed as if they 
were **value properties instead of method properties**. This gives us a slightly nicer interface:

```javascript
let pizza = new Pizza();

pizza.price;      // instead of getPrice()
pizza.size = 's'; // instead of setSize(size)
```

`! CONCLUSION ! `

We explored the concept of **getters** and **setters** and how to use the **get** and **set** keywords in JS.

Setters allow us to validate data vefore assigning it to a property and getters allow us to compute a value on the fly instead of simply pulling it out of a property.

The **get** and **set** keywords just make our object's interface more simple.

ß
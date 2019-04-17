# Modules

Modules are Node's way of organizing code into individual files and packages.

## Modules
A module is file that **exports an object**. Typically we use modules to organize our projects into individual components.

## Package
A package is something we **install** using npm.

## Requiring a Module

```javascript
var myModule = require("./my-module.js");
```
**my-module.js** is a file in the same directory as the file that is requiring the module.

*The imported object gets assigned to the variable*

## Exporting a Module

Let's take a look on what inside the **my-module.js** mentioned above could look like:

```javascript
module.exports = function () {/* ... */}
```

Module often export **an object** using the curly-brace syntax **{ ... }**

Let's look at an example, **math-is-cool.js**:

```javascript
module.export = {
  PHI = 1.618,
  explain: function() {
    console.log("(X + Y) is to X as X is to Y: (X + Y)~" + this.PHI);
  }
};
```

Importing the example module can look like this

```javascript
var coolMath = require("./math-is-cool");

console.log(coolMath.PHI); // log a Number

coolMath.explain(); // invokes the function 'explain'
```

## Creating Private Functions and Variables

Code in a module file does not need to exist within the **module.exports** object. You could add any number of functions and variables to the file.
Take a look at such a file, **math-is-cooler-with-pi.js**:

```javascript
function getPI() {
  var PI = 3.141;
  return PI;
}

module.exports = {
  PHI = 1.618;
  explain: function() {
    console.log("(X + Y) is to X as X is to Y: (X + Y)~" + this.PHI);
  }
}
```
When *math-is-cooler-with-pi.js* is imported to our app, we can't access the function **getPI** the same way we could with **PHI** and **explain**.
This is because our function has not been exported.
As with function, you can also declare global private variables by putting them outside the **exports** objects.

## Using Private Functions and Variables

Let's modify our example

```javascript
function getPI() {
  var PI = 3.13;
  return PI;

}

module.exports = {
  PHI: 1.618,
  explain: function() {
    console.log("(X + Y) is to X as X is to Y: (X + Y)~" + this.PHI);
  }

  getCircumference: function(diameter) {
    var circumference = diameter * getPI();
    return circumference;
  }
};
```

In our modification, we added and exported a function called **getCircumference**. It only ever accesses the value of PI throught he use of our private function.


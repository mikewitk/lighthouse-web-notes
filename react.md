# REACT

React is a client-side JavaScript library first created at Facebook.

In **React** there is just one pattern: the **COMPONENT**.
Every app is a component, and components may be assembled from other components.

**Usually, a component's job is to get or manage data, and then present that data.**

# Webpack

Webpack among other things, allows us to write our client-side JavaScript code in mutiple files, Webpack then minify the code and put it all into one file.

# Babel

Babel is a powerful library for translating JavaScript into different Javascript.
What it does is lets us use the latest ES6 features in our code, and then creates browser-friendly ES5.

## React -> Writing JSX

JSX stands for **JavaScript** with **XML**

JSX it's not meant to be read by the browser. So we will write some JSX code, use babel to *translate* it into JavaScript, then have the browser interpret the plain JavaScript file.

> RULES

1. ALL JSX elements must either consist of an **opening *and* closing** tag, or be **self closing**

```javascript
//GOOD
const openAndClose = (<div>This content is contained in this div</div>);

const selfClosing = (<img src='https://http.cat/200'/>);

//BAD
const thisIsNotOkay = (<img>);
```

2. The next tag to close must match the last one to open

```javascript
//GOOD
const correctOrder = (<em><strong>Content</strong></em>);
const anotherCorrectOrder = (<strong><em>Content</em></strong>);

//Bad
const outOfOrder = (<em><strong>Content</em></strong>);
const alsoOutOfOrder = (<strong><em>Content</strong></em>);
```

3. Any JSX expression assigned to a variable or returned from a function must have **one** root tag

```javascript
//GOOD
const validOneRoot = (<div><p>Totally cool to have more than one child element, though</p></div>);

//BAD
const notOkay = (<div></div><p></p>);
```

4. HTML comment won't work

```javascript
//GOOD
const correctComment = (<div>{/* Correct Commet */}</div>);

//BAD
const thisIsNotValid = (,div>{<!-- Bad Comment --></div>});
```

5. White space is totally cool

```javascript
const thisIsValid = (<div><span>Content</span></div>);

const thisIsTheSameAsAbove = (<div>
  <span>Content</span>
</div>);
```

`! CONCLUSION !`

JSX elements are just syntactic sugar over the *React.createElement()* method. It makes our code nicer to write, and is the preferred way of creating React Components.

## React -> Props

```html
<h1 id="main-title">Title</h1>
```
*h1* **HTML element** with an *id* **attribute** set to "main-title"

```html
<h1 id='main-title'>Title</h1>
```
*h1* **React element** with its *id* **prop** set to 'main-title'

Props and attributes have a lot in common, but there is one **huge** difference between them:

- HTML attributes can only take in **strings**.
- Props accepts all sorts of **values, objects, arrays, and functions**.

## React -> className

In React, to refer to a class attribute of a HTML tag we use **className**.
```javascript
<p className='jumbotron'></p>
```

### React -> className -> Style

In JSX *inline* styles are the preferred way of styling an element.

There are three important differences between HTML and JSX inline style:

1. We write styles as object with **key-value pairs**
2. We write every props in **camel case** (backgroundColor)
3. We pass the styles object to the *style* prop using **curly braces**

```javascript
//So this:
<span style="background-color: lime">Hi</span>

//Becomes
const styleObject = { backgroundColor: 'lime' };
<span style={{styleObject}}>Hi</span>
```

## React -> Dynamic Content

One of the expressive powers of JSX is as a templating language.
The idea is that we have some data, we feed it through a template, and we have markup that comes out.
We could think of a template as **function** that takes *data in* and spits *markup out*

Here's how we put dynamic content in our markup, specifically, the current date and time.

```javascript
const root = document.getElementById('root');

ReactDOM.render(
  (<h1 className='blue'>
    {new Date().toString()}
  </h1>),
  root
);
```

Here's the list of things that React will render:

* Strings
* Numbers (including NaN, which will show up as NaN)
* Valid JSX expressions
* Arrays containing strings, numbers, and valid JSX expressions

And here's what React will ignore as if it never happened:

* true and false
* undefined and null
* functions

Anything else will raise an error.

### React -> Dynamic Content -> Making a Template

So, if we have the following HTML:

```javascript
<div class='profile'>
  <img style='max-width: 100%' src='http://joelshinness.com/assets/img/avatars/avatar_square_sm.jpg'/>
  <p>Joel Shinness</p>
  <p><small>Web Development Instructor</small></p>
</div>
```
Then the data being displayed could be represented as the following object:

```javascript
const data = {
  name: 'Joel Shinness',
  title: 'Web Development Instructor',
  photoUrl: 'http://joelshinness.com/assets/img/avatars/avatar_square_sm.jpg'
}
```
Then the template would be something like:

```javascript
const markup = (<div className='profile'>
  <img
    style={{maxWidth: '100%'}}
    src={data.photoUrl}/>
  <p>{data.name}</p>
  <p><small>{data.title}</small></p>
</div>);
```

## React -> Logic and Looping

### React -> Logic and Looping -> Conditional Inclusion / Exclusion

```javascript
function makeCard(dataItem) {
  let warningLabel = undefined;
  if(dataItem.warning){
    warningLabel = (
      <p className="warning">🤨{dataItem.warning}</p>
      );
  }
  return <div className="card">{warningLabel}</div>; // <-- Line 8
};

const root = document.getElementById("root");
ReactDOM.render(
  <div>
    {makeCard({})}
    {makeCard({ warning: "Problem!" })}
  </div>,
  root
);
```

> For the case "makeCard({}) line 8 of the code won't be rendered because JSX ignores: **true, false, null, and undefined**.

### React -> Logic and Looping -> Condition && (OnlyIfTrue)

We can reduce the amount of code by using logical operators **||** and **&&**.

```javascript
const makeCard = dataItem => {
  const warningLabel = dataItem.warning && (
    <p className="warning">🤨{dataItem.warning}</p>
  );

  return <div className="card">{warningLabel}</div>;
};
```
* If **data.warning** is a truthy string, then we'll include that bit of JSX.
* If **data.warning** is *undefined*, *false*, or an empty string, then it will be promptly ignored by React.

### React -> Logic and Looping -> Conditional Switch

What if we want to include some markup if something is true, and something else if it's false?

```javascript
function makeCard(dataItem) {
  const warningLabel = dataItem.warning && (
    <p className="warning">🤨{dataItem.warning}</p>
  );

  let userLabel;
  if(dataItem.user){
    userLabel = (
      <p className='logged-in'>👋 Hello, {dataItem.user.name}</p>
    );
  } else {
    userLabel = (
      <p className='not-logged-in'>🖐 You are not logged in.</p>
    );
  }

  return (
    <div className="card">
      {warningLabel}
      {userLabel}
    </div>
  );
};

const data1 = {};
const data2 = {
  warning: "Your account may expire soon!",
  user: {
    name: "Jeff"
  }
};

const root = document.getElementById("root");
ReactDOM.render(
  <div>
    {makeCard(data1)}
    {makeCard(data2)}
  </div>,
  root
);

// You are not logged in.

// Your account may expire soon!
// Hello, Jeff
```

### React -> Logic and Looping -> Condition ? (IfTrue) : (IfFalse)

```javascript
function makeCard(dataItem) {
  const warningLabel = dataItem.warning && (
    <p className="warning">🤨{dataItem.warning}</p>
  );

  const userLabel = dataItem.user ? (
    <p className='logged-in'>👋 Hello, {dataItem.user.name}</p>
  ) : (
    <p className='not-logged-in'>🖐 You are not logged in.</p>
  );
```

### React -> Logic and Looping -> Looping

In EJS, we used **for** or **.forEach(fn)** to iterate over an array or object and perform some **instruction** on each member.
In React, we are **composing** pieces rather than just running instructions, so here, we want to take an array of data and **get an array of JSX expressions**.

We can do that by using **Array.prototype.map**

Transform an array of data:
```javascript
["🍺", "🍷", "🍸"]
```

Into an array of JSX expressions:
```javascript
[<p>🤗</p>, <p>"💩"</p>, <p>"🍺"</p>]
```

Using map:
```javascript
emojis.map((emoji) => {
  return <p>{emoji}</p>
});
```

Example
```javascript
const data1 = {
  emojis: ["☕️", "🍩"]
};

const data2 = {
  emojis: ["🍺", "🍷", "🍸"]
};

function makeCard(dataItem) {

  const emojiListItems = dataItem.emojis.map( (emoji) => {
    return (<li>{emoji}</li>);
  });

  return (
    <div className="card">
      <ul>{emojiListItems}</ul>
    </div>
  );
};

const root = document.getElementById("root");
ReactDOM.render(
  <div>
    {makeCard(data1)}
    {makeCard(data2)}
  </div>,
  root
);

// * ☕️
// * 🍩

// * 🍺
// * 🍷
// * 🍸
```

`! UNIQUE "KEY" PROP !`

When we are dealing with data that has unique IDs, we can add the id to the element using a **key** prop, and React will be satisfied. It uses this information for performance purposes in its never-ending quest to do as few DOM updates as possible.

```javascript
const emojiListItems = dataItem.emoji.map((emoji) => {
  return (<li key={emoji}>{emoji}</li>);
});
```

**PS:** It only works here because our emojis are unique. **Keys need to be unique**

## React -> DOM Events

With React, we add listeners directly by passing functions to certain props. In the following example, we will pass an **alertFn** function to a **button** component using its **onClick** prop.

```javascript
function alertFn() {
  alert('This alert, tho, amirite?');
}

const buttonWithListener = (
  <button onClick={alertFn}>
    Click Me!
  </button>);

ReactDOM.render(buttonWithListener, root);
```

`When the button is clicked, the function will get called`

Like regular event listeners, they take an **event** as an argument, and unless the function is already bound to a specific object, the keyword **this** will refer to the **DOM element** that had the listener.

```javascript
function onSubmit(event) {
}

const form = (<form onSubmit={onSubmit}>
    <div>
      <input name='email' type='email' placeholder='Email'/>
    </div>
    <div>
      <input name='password' type='password' placeholder='Password'/>
    </div>
    <div><input type='submit' value='Log In'/></div>
  </form>);
```

1. As with any submit form, the first step is to prevent default behavior

```javascript
function onSubmit(event) {
  event.preventDefault();
}
```

2. The form is the **target** of the event object. If the inputs have name attributes, then we can get them

```javascript
function onSubmit(event) {
  event.preventDefault();
  const form = event.target;
  const emailInput = form.elements.email;
  const passwordInput = form.elements.password;

  alert(`Your email is ${emailInput.value} and your password is ${passwordInput.value}`);

  //reset inputs
  emailInput.value = passwordInput.value = '';
}
```

## React and ReactDOM

When we want to use React in the browser, we have to include two libraries:

* React: the library for creating views.
* ReactDOM: the library used to actually render the UI in the browser.

We can include these into your project in a few different ways.

1. Script Tags

Using normal script tags, we can include both libraries in your HTML file.
```javascript
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
```

2. Require

If we are using webpack, and we like ES5, we can require the two libraries into our JavaScript file.
```javascript
var React = require('react');
var ReactDOM = require('react-dom');
```

3. Import

If we are using webpack, and we want to use ES6 features, we can import the two libraries into our JavaScript file. 
**This is the preferred way of doing things**, so most examples will do look like this:
```javascript
import React from "react";
import ReactDOM from "react-dom";
```
`The reason that there are two libraries instead of one, is so that the core react library doesn't have to be tied to the browser. This means that we can use the react library on any platform, like mobile. In the browser, we have to include react and react-dom. On mobile, we have to include react and react-native. The react library is the same, but the rendering library changes.`

### React and ReactDOM -> Render

```javascript
const greeting = <h1>Hello!</h1> // This uses the React Library
const root = document.getElementById("root"); // Vanilla JS
ReactDOM.render(greeting, root); // ReactDOM does the rendering
```
**ReactDom.render()** takes two parameters
1. a React element
2. The element in DOM where React will render the element to

## React and ReactDOM -> Classes

* If we want to make a bunch of objects that have the same behaviour, we can create a class that provides a blueprint:
```javascript
class Shark {
}

const finn = new Shark();
console.log(finn);
// CONSOLE: Shark {}
```
* We can add constructors that lets us add some information about a specific object.
```javascript
class Shark {
  constructor(name) {
    this.name = name;
  }
}
const finn = new Shark('Finn');
console.log(finn);
//CONSOLE: Shark {name: 'Finn'}
```
* We can add new behaviours to the class with **methods**. There are functions added to the class that can reference the instance with **this**.
```javascript
class Shark {
  constructor(name){
    // Add the name to the shark object.
    this.name = name;
    this.position = {x: 0, y: 0};
    console.log('This', this);
    // CONSOLE: This Shark { name: 'Finn', position: { x: 0, y: 0 } }
  }
  /* SWIM METHODS */
  swimRight(){
    this.position.x += 1;
  }
  swimLeft(){
    this.position.x -= 1;
  }
  swimUp(){
    this.position.y += 1;
  }
  swimDown(){
    this.position.y -= 1;
  }
}
const finn = new Shark('Finn');
console.log('Finn', finn);
// CONSOLE: Finn Shark { name: 'Finn', position: { x: 0, y: 0 } }
finn.swimRight();
console.log('Finn After Swim', finn);
// CONSOLE: Finn After Swim Shark { name: 'Finn', position: { x: 1, y: 0 } }
```
* If we have one class that has a lot of behaviour we like, and we want to make a more specialized version, we can **extend** the class
```javascript
class Shark {
  constructor(name){
    // Add the name to the shark object.
    this.name = name;
    this.position = {x: 0, y: 0};
    console.log('This', this);
    // CONSOLE: This Shark { name: 'Finn', position: { x: 0, y: 0 } }
  }
  /* SWIM METHODS */
  swimRight(){
    this.position.x += 1;
  }
  swimLeft(){
    this.position.x -= 1;
  }
  swimUp(){
    this.position.y += 1;
  }
  swimDown(){
    this.position.y -= 1;
  }
}

const finn = new Shark('Finn');
console.log('Finn', finn);
// CONSOLE: Finn Shark { name: 'Finn', position: { x: 0, y: 0 } }
finn.swimRight();
console.log('Finn After Swim', finn);
// CONSOLE: Finn After Swim Shark { name: 'Finn', position: { x: 1, y: 0 } }

class LaserShark extends Shark {
  shoot(){
    console.log('PEW PEW!');
  }
}

const laserFinn = new LaserShark('Laser Finn');
// CONSOLE: This LaserShark { name: 'Laser Finn', position: { x: 0, y: 0 } }
console.log('Laser Finn', laserFinn);
// CONSOLE: Laser Finn LaserShark { name: 'Laser Finn', position: { x: 0, y: 0 } }

laserFinn.shoot();
// CONSOLE: PEW PEW!
```

There are a number of ways to describe the relationship between **Shark** and **LaserShark**:

* **LaserShark** extends **Shark**
* **LaserShark** inherits from **Shark**
* **LaserShark** is a *subclass* of **Shark**
* **Shark** is the superclass of **LaserShark**
* **LaserShark** is a child class of **Shark**
* **Shark** is the parent class of **LaserShark**
* Every instance of **LaserShark** is an instance of **Shark**
* Anything that is true of a **Shark** is true of a **LaserShark**
* The child class may have behaviour that doesn't exist in the parent class. **LaserShark**s can shoot, but regular **Shark**s can't.

* You may **override** a parent class method in a child class. That means that any instance of the child class will use the overridden version instead of the original version.
```javascript
class Shark {
  constructor(name){
    // Add the name to the shark object.
    this.name = name;
    this.position = {x: 0, y: 0};
    console.log('This', this);
    // CONSOLE: This Shark { name: 'Finn', position: { x: 0, y: 0 } }
  }
  /* SWIM METHODS */
  swimRight(){
    this.position.x += 1;
  }
  swimLeft(){
    this.position.x -= 1;
  }
  swimUp(){
    this.position.y += 1;
  }
  swimDown(){
    this.position.y -= 1;
  }
}

const finn = new Shark('Finn');
console.log('Finn', finn);
// CONSOLE: Finn Shark { name: 'Finn', position: { x: 0, y: 0 } }
finn.swimRight();
console.log('Finn After Swim', finn);
// CONSOLE: Finn After Swim Shark { name: 'Finn', position: { x: 1, y: 0 } }

class LaserShark extends Shark {
  shoot(){
    console.log('PEW PEW!');
  }
  /* LASER SHARKS ARE FASTER! */
  swimRight(){
    this.position.x += 2;
  }
  swimLeft(){
    this.position.x -= 2;
  }
  swimUp(){
    this.position.y += 2;
  }
  swimDown(){
    this.position.y -= 2;
  }
}

const laserFinn = new LaserShark('Laser Finn');
// CONSOLE: This LaserShark { name: 'Laser Finn', position: { x: 0, y: 0 } }
console.log('Laser Finn', laserFinn);
// CONSOLE: Laser Finn LaserShark { name: 'Laser Finn', position: { x: 0, y: 0 } }

laserFinn.shoot();
// CONSOLE: PEW PEW!

laserFinn.swimRight();
console.log('Laser Finn After Swim', laserFinn);
// CONSOLE: Laser Finn After Swim LaserShark { name: 'Laser Finn', position: { x: 2, y: 0 } }
```

* If you have overriden the constructor, you can access the parent's class's constructor with **super**
```javascript
class Shark {
  constructor(name){
    // Add the name to the shark object.
    this.namelol = name;
    this.position = {x: 0, y: 0};
    console.log('This', this);
    // CONSOLE: This Shark { name: 'Finn', position: { x: 0, y: 0 } }
  }
  /* SWIM METHODS */
  swimRight(){
    this.position.x += 1;
  }
  swimLeft(){
    this.position.x -= 1;
  }
  swimUp(){
    this.position.y += 1;
  }
  swimDown(){
    this.position.y -= 1;
  }
}

const finn = new Shark('Finn');
console.log('Finn', finn);
// CONSOLE: Finn Shark { name: 'Finn', position: { x: 0, y: 0 } }
finn.swimRight();
console.log('Finn After Swim', finn);
// CONSOLE: Finn After Swim Shark { name: 'Finn', position: { x: 1, y: 0 } }

class LaserShark extends Shark {
  constructor(namelol, laserSound){
    super(namelol);
    this.laserSound = laserSound;
  }
  shoot(){
    console.log(`${this.namelol}: ${this.laserSound}!`);
  }
  /* LASER SHARKS ARE FASTER! */
  swimRight(){
    this.position.x += 2;
  }
  swimLeft(){
    this.position.x -= 2;
  }
  swimUp(){
    this.position.y += 2;
  }
  swimDown(){
    this.position.y -= 2;
  }
}

const laserFinn = new LaserShark('Laser Finn', 'PEW PEW');

// CONSOLE: Laser Finn LaserShark {
//  name: 'Laser Finn',
//  position: { x: 0, y: 0 },
//  laserSound: 'PEW PEW' }

console.log('Laser Finn', laserFinn);
// CONSOLE: Laser Finn LaserShark {
//  name: 'Laser Finn',
//  position: { x: 0, y: 0 },
//  laserSound: 'PEW PEW' }

laserFinn.shoot();
// CONSOLE: Laser Finn: PEW PEW!

laserFinn.swimRight();
console.log('Laser Finn After Swim', laserFinn);
// CONSOLE: Laser Finn After Swim LaserShark {
//  name: 'Laser Finn',
//  position: { x: 2, y: 0 },
//  laserSound: 'PEW PEW' }
```

## React and ReactDOM -> Crafting Components Intro

In React, there's just one architectural pattern: the **Component**.

Let's build a simple CityList app. The output HTML will be like this:
```html
<div>
  <p>Here are some cities</p>
  <ul>
    <li>Vancouver</li>
    <li>Toronto</li>
  </ul>
</div>
```
And we want that to be rendered to the HTML by this line:

```javascript
const root = document.getElementById('root');

ReactDOM.render(
  (<CityList/>),
  root);
```

Where do we start? Well, to create our own components, we can make a new class that extends React.Component.
```javascript
class CityList extends React.Component {
}
```
That means that we're bringing in all the behaviour of **React.Component**, or as we said before:

*Everything that is true of **React.Component** is also true of CityList, unless we specify otherwise.*

Any subclass of **React.Component** will need to implement a **render()** method, and the **render()** method needs to return a valid JSX expression.

Now that we're creating components, the JSX may be some combination of HTML tags and React components. And for now, we can just have it return HTML.
```javascript
class CityList extends React.Component {
  render(){
    return (<div>
      <p>Here are some cities</p>
      <ul>
       <li>Vancouver</li>
       <li>Toronto</li>
     </ul>
   </div>);
  }
}
```

`All component class names must begin with a capital letter. JSX treats tags that begin with lower case letters differently than those that begin with upper case letters.`

Let's put in some more components that have some data or meaning. For now, we can at least make some **CityListItems**

```javascript
const root = document.getElementById('root');

class VancouverCityListItem extends React.Component {
  render(){
    return (<li>Vancouver</li>);
  }
}

class TorontoCityListItem extends React.Component {
  render(){
    return (<li>Toronto</li>);
  }
}

class CityList extends React.Component {
  render(){
    return (<div>
      <p>Here are some cities</p>
      <ul>
        <VancouverCityListItem/>
        <TorontoCityListItem/>
      </ul>
   </div>);
  }
}

ReactDOM.render(
  (<CityList/>),
  root);
```
`! CONCLUSION !`

A custom component extends the **Component** class in React, and, at the very least, implements the **render()** method. The **render()** method must return a JSX expression. Once we've created or included a component, we're able to use it in our JSX as we would with an HTML element.

## React and ReactDOM -> Props (again)

Wouldn't it be great if we could just create a single, reusable **CityListItem** component and pass it the name of the city when we use it?

Props to the rescue:
```javascript
const vancouver = (<CityListItem city='Vancouver'/>);
const toronto = (<CityListItem city='Toronto'/>);
```
Let's rebuild our program again with this more generalized Component, and pass the correct information to it.
```javascript
const root = document.getElementById('root');

class CityListItem extends React.Component {
  render(){
    return (<li>{this.props.city}</li>);
  }
}

class CityList extends React.Component {
  render(){
    return (<div>
      <p>Here are some cities</p>
      <ul>
        <CityListItem city='Vancouver'/>
        <CityListItem city='Toronto'/>
      </ul>
   </div>);
  }
}

ReactDOM.render(
  (<CityList/>),
  root);
```

### React and ReactDOM -> Props -> Array of Props

Of course, we still have the city components hard-coded into our render function. Let's do this in a more data-driven way, using props again. We'll start with an array of city names:
```javascript
const cityNames = ['Vancouver', 'Toronto'];
```
Then we'll use .map to create an array of "CityListItem />"s from our cityNames array.
```javascript
const cityNames = ['Vancouver', 'Toronto'];
const cityListItems = cityNames.map( (cityName) => {
  return (<CityListItem city={cityName}/>);
});
```
And we can embed that array of CityListItem elements directly into the return value of the render function.
```javascript
class CityList extends React.Component {
  render(){
    const cityNames = ['Vancouver', 'Toronto'];
    const cityListItems = cityNames.map((cityName) => {
      return (<CityListItem city={cityName}/>);
    });

    return (<div>
      <p>Here are some cities</p>
      <ul>{cityListItems}</ul>
   </div>);
  }
}
```

In fact, let's make it even more dynamic, and pass this array as a prop to CityList.
```javascript
const cityNames = ['Vancouver', 'Toronto'];

class CityList extends React.Component {
  render(){ 
    const cityListItems = this.props.cityNames.map((cityName) => {
      return (<CityListItem city={cityName}/>);
    });

    return (<div>
      <p>Here are some cities</p>
      <ul>{cityListItems}</ul>
   </div>);
  }
}

ReactDOM.render(
  (<CityList cityNames={cityNames}/>),
  root);
```

## React and ReactDOM -> State

Unlike *props*, which are passed into the component from outside, a component is responsible for creating and managing its own **state**.

There are two things we can do with state

1. We can read the state at any time with **this.state**
2. We can set **this.state =** in a component's constructor to define the initial state

Let's take a look at an example:
```javascript
import React from "react";
import ReactDOM from "react-dom";

class CountReader extends React.Component {
  render() {
    let timesOrTime = "times";
    if (this.props.count === 1) {
      timesOrTime = "time";
    }
    return (
      <span>
        {this.props.count} {timesOrTime}
      </span>
    );
  }
}

class Incrementer extends React.Component {
  constructor(props) {
    super(props);

    // Set the initial state
    this.state = { count: 0 };

    // Increment the state count
    this.increment = () => {
      const oldCount = this.state.count;
      this.setState({ count: oldCount + 1 });
    };
  }
  render() {
    return (
      <p>
        {/* Change state in response to user action */}
        <button onClick={this.increment}>Increment</button>
        {/* Display the current state */}
        &nbsp;
        <CountReader count={this.state.count} />
      </p>
    );
  }
}

ReactDOM.render(<Incrementer />, document.getElementById("root"));
```

This incrementer should:
1. Start with an initial count of 0
2. Increase the count by 1 every time the button is clicked
3. Update the UI to represent the current count, every time the count changes.

Let analyze one by one

**1. Start with an initial count of 0**
```javascript
class Incrementer extends React.Component {
  constructor(props){
    super(props); // SUPER IMPORTANT!  IF YOU LEAVE THIS OUT, STUFF BREAKS!
    this.state = {count: 0};
  }
  render(){
    return (<p>
      <button>Increment</button>
      <span>{this.state.count}</span>
    </p>);
  }
}
```
In the components constructor, we are going to set any initial data on the state property. We can then read from the state when we render the component.

When we override the constructor of a component, we *must* call **super()** with the components props. This is because we are inheriting from **React.Component** and we need to make sure that the **React.Component**'s constructor is always called.

**2. Increase the count by 1 every time the button is clicked**
```javascript
class Incrementer extends React.Component{
  constructor(props){
    super(props);
    // Set the initial state
    this.state = {count: 0};
    this.increment = this.increment.bind(this);
  }
  // Increment the state count
  increment() {
    this.setState((previousState) => {
      return {count: previousState.count + 1}
    });
  }
  render(){
    return (<p>
      {/* Change state in response to user action */}
      <button onClick={this.increment}>Increment</button>
      {/* Display the current state */}
      <span>{this.state.count}</span>
    </p>);
  }
}
```
Every time someone clicks the "Increment" button, we will call the **increment** method. The increment method will then call **setState** to update the current state of the component. **setState** accepts a function that will receive the **previousState** and return the new state as an object.

**3. Update the UI to represent the current count, every time the count changes.**

Calling **setState()** will always lead to the component being re-rendered. When the component is re-rendered, the span will display the value of **this.state.count**, which is now 1 more than it used to be.

`! CONCLUSION !`

A component has two sources of data: the **state** and the **props**.

* State is a component's own cache of data, which it manages. It cannot be directly read or changed by any other component, regardless of whether that other component is a parent, child, or sibling to this component.
* Props are sent from parent to child. A child element cannot change the props they are sent, though the parent may change the props sent.
* A component may send data from its state to a child component's props.

The one-way data flow from parent to child is a big part of React's philosophy, and how it manages to be so efficient.

# REACT CLASS

* **Rule 1**: always import react (and Component);

```javascript
import react, {Component} from 'react';
```

* **Rule 2**: Classes are your componeents. They will extend Component
```javascript
class App extends Component {

}
```

* **Rule 3**: All components MUST!!!! have a render() function
```javascript
class App extends Component {
  render (
    return {
      
    }
  )
}
```
* **Rule 4**: If component is in a different file, ALWAYS export that component
```javascript
export default App;
```

* **Rule 5**: Always wrap your JSX into one single element
```javascript
class App extends Component {
  render (
    return {
     <div>
     /* Anything in between */
     </div>
    }
  )
}
```

* Rule 6: There are things called constructors and it has state
```javascript
class App extends Component {
  constructor {
    super(props);
    this.state = { number: 0 }
  }

  number = 0 => {
    let x = this.state.number;
    x++;
    this.setState( { number: x } );
  }
}
```

# REACT BREAKOUT

## React -> Lifecycle Methods

React has a mechanism that lets us write as if we're replacing all the DOM every time, but React is smart enough to pick and choose so that it can perform as few DOM operations as it needs to.
This mechanism is the **Virtual DOM**.

In order to understand wha tthe Virutal DOM does, we have to walk through the three major steps in a component's lifecycle: Mounting, Updating, and Unmounting.

Lifecycle methods are methods that we can add to the Component class that will be classed at different times.

### React -> Lifecycle Methods -> Mounting

When a component is added to the DOM or its parent.

### React -> Lifecycle Methods -> Unmounting

When a component is removed from the Virtual DOM

### React -> Lifecycle Methods -> Updating

When a component's props or state changes

**Don't use *this.setState* in the *render()* function.**

### React -> Lifecycle Methods -> componentDidMount()

componentDidMount() is to React what the "document.ready" is to jQuery. It starts running stuff *after* it's available on the DOM.

That makes this the ideal place to do two big things:

* Trigger async acitons that we want to do when this component is created
* Target the DOM imperatively for any of the following
  - Add global event listeners
  - Draw on canvas
  - Start animation timers
  - Listen to notifications sources
  - Run any other imperative browser APIs


> OBJECT DESTRUCTURING

This
```javascript
const person = {
  firstName: 'Joel',
  lastName: 'Shinness'
};
// THIS
const firstName = person.firstName;
const lastName = person.lastName;

// IS EQUAL TO THIS
const { firstName, lastName } = person;
```

# React CLASS


# REACT

React is a client-side JavaScript library first created at Facebook.

In **React** there is just one pattern: the **COMPONENT**.
Every app is a component, and components may be assembled from other components.

Usually, a component's job is to get or manage data, and then present that data.

# Webpack

Webpack among other things, allows us to write our client-side JavaScript code in mutiple files, Webpack then minify the code and put it all into one file.

# Babel

Babel is a powerful library for translating JavaScript into different Javascript.
What it does is lets us use the latest ES6 features in our code, and then creates browser-friendly ES5.

## Writing JSX

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

## Props

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

> Classes

In React, to refer to a class attribute of a HTML tag we use **className**.
```javascript
<p className='jumbotron'></p>
```

> Style

In JSX *inline* styles are the preferred way of styling an element.

There are three important differences between HTML and JSX inline style:

1. We write styles as object with **key-value pairs**
2. We write every property in **camel case** (backgroundColor)
3. We pass the styles object to the *style* prop using **curly braces**

```javascript
//So this:
<span style="background-color: lime">Hi</span>

//Becomes
const styleObject = { backgroundColor: 'lime' };
<span style={{styleObject}}>Hi</span>
```

## Dynamic Content

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

## MAKING A TEMPLATE

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

## Logic and Looping

> Conditional Inclusion / Exclusion

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

* Line 8 of the code won't be rendered because JSX ignores: **true, false, null, and undefined**.

> Condition && (<OnlyIfTrue/>)

We can reduce the amount of code by using logical operators *||* and *&&*.

```javascript
const makeCard = dataItem => {
  const warningLabel = dataItem.warning && (
    <p className="warning">🤨{dataItem.warning}</p>
  );

  return <div className="card">{warningLabel}</div>;
};
```
* If **data.warning** is a truthy string, then we'll include that bit of JSX.
* If **data.warning** is *undefined*, *false*, or an empty string, then it will be promplty ignore by React.

> Conditional Switch

What if we want to include some markup if somethins is true, and something else if it's false?

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

> Condition ? *<IfTrue/>) : (<IfFalse/>)

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

> Looping

In EJS, we used **for** or **.forEach(fn)** to iterate over an arry or object and perform some **instruction** on each member.
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

  const emojiListItems = dataItem.emojis.map((emoji) => {
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

! UNIQUE "KEY" PROP !

When we are dealing with data that has unique IDs, we can add the id to the element using a **key** prop, and Reac will be satisfied. It uses this information for performance purposes in its never-ending quest to do as few DOM updates as possible.

```javascript
const emojiListItems = dataItem.emoji.map((emoji) => {
  return (<li key={emoji}>{emoji}</li>);
});
```

**PS:** It only works here because our emojis are unique. **Keys need to be unique**


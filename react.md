# REACT

React is a client-side JavaScript library first created at Facebook.

In **React** there is just one pattern: the **COMPONENT**.
Every app is a component, and components may be assembled from other components.

usually, a component's job is to get or manage data, and then present that data.

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

JSX elements are just syntactic sugar over the *React.createElement()* method. It makes ou code nicer to write, and is the preferred way of creating React Components.

## Props

```html
<h1 id="main-title">Title</h1>
```
*h1* **HTML element** with an *id* **attribute** set to "main-title"

```html
<h1 id='main-title'>Title</h1>
```
*h1* **React element** with its *id* **prop** set to 'main-title'

Props and attributes have a lot in common, but there is one **8*huge** difference between them:

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
The idea is that we have some data, we feed it through a template, annd we jave markup that comes out.
We could think of a template as **function** that takes *data in* and spits *markup out*


# Clean Code

## JavaScript Style Guide

### Types

1. Primitives: when you access a primite ype you work directly on its value.

* string
* number
* boolean
* null
* undefined
* symbol

2. Complex: when you access a complex type you work on a reference to its value

* object
* array
* function

### References

1. Use `const` for all your references. This ensures that you can't reassign your referenceses, which can lead to bugs and difficlt to comprehend code.

2. If you must reassign references, use `let` instead of `var`.

3. Note that both `let` and `const` are block-scoped

```javascript
//const and let only exist in the blocks they are defined in.
{
  let a = 1;
  let b = 3;
}
console.log(a); // Reference error
console.log(b); // Reference error
```

### Objects

1. Use the lyteral syntax for object creation

```javascript
// bad
const item = new Object();

// good
const item = {};
```

2. Use computed property names when creating objets with dynamic property names

3. Use object method shorthand

```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

4. Use property value shorthand. It is shorter and descriptive

```javascript
const LukeSkywalker = "Luke Skywalker";

// bad
const obj = {
  LukeSkywalker: LukeSkywalker,
};

// good
const obj = {
  LukeSkywalker,
};
```

5. Group your shorthand properties at the beginning of your object declaration

6. Only quote properties tat are invalid identifiers. In general we consider it subjectively easier to read.

```javascript
// bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

// good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

7. Do no call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.
These methods may be shadowed by properties on the object in question.

8. Prefer the object spread operator over `Object.assign` to shallow-copy objects. Use the object rest operator to get a new object with certain properties ommited.

```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

### Arrays

1. Use the literal syntax for array creaiton

```javascript
// bad
const items = new Array();

// good
const items = [];
```

2. Use `array.push` instead of direct assignment to add item to an array.

3. Use array spreads `...` to copy arrays.

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

4. To convert an iterable object to an array, use spreads `...` instead of `Array.from`.

5. Use `Array.from` for converting an array-like object to an array.

6. Use `Array.from` instead of spread `...` for mapping over iterables, because it avoids creating an intermediate array.

7.  Use return statements in array method callbacks. It is ok to omit the return if the function body consists of a single statement returning an expression without side effects.

8. Use line breaks after open and before close array brackets if an array has mutiple lines

```javascript
// bad
const arr = [
  [0, 1], [2, 3], [4, 5],
];

const objectInArray = [{
  id: 1,
}, {
  id: 2,
}];

// good
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [
  {
    id: 1,
  },
  {
    id: 2,
  },
];
```

### Destructuring

1. Use object destructuring when accessing and using multiple properties of an object.
Destructuring saves you from creating temporary references for those properties.

2. Use arrau destructuring

```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;

console.log(first) ; // 1
```

3. Use object destructuring for multiple return values, not array destructuring.
You can add new properties over time or change the order of things without breaking call sites

```javascript
// bad
function processInput(input) {
  // then a miracle occurs
  return [left, right, top, bottom];
}

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);

// good
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom };
}

// the caller selects only the data they need
const { left, top } = processInput(input);
```

### Strings

1. Use single quotes `' '` for strings.

2. Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.
Broken strings are painful to work with and mkae code less searchable.

```javascript
// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';

// good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

3. When programatically building up strings, use template strings instead of concatenation.

```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

4. Never use `eval()` on a string, it open too many vulnerabilities

5. Do not unnecessarily escape characters in strings

```javascript
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

### Functions

1. Use named function expressions instead of function declarations

```javascript
// bad
function foo() {
  // ...
}

// bad
const foo = function () {
  // ...
};

// good
// lexical name distinguished from the variable-referenced invocation(s)
const short = function longUniqueMoreDescriptiveLexicalFoo() {
  // ...
};
```

2. Wrap immediately invoked function expression in parentheses.

```javascript
// immediately-invoked function expression (IIFE)
(function () {
  console.log('Welcome to the Internet. Please follow me.');
}());
```

3. Never declare a function in a non-function block (`if`, `while`, etc). Assign the function to a variable instead.

4. Never name a parameter `arguments`. This will take precedence over the `arguments` object that is fiven to every function scope.

5. Never reassign parameters

```javascript
// bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

// good
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```
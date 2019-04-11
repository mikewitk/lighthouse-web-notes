# ES6

## Template Literal or String Interpolation

Template literals allow us to simplify the string concatenation process while being faster and using up less computer memory.

```javascript
var name = 'Alice';
console.log(`Hello, ${name}!`) ; // logs: Hello, Alice!
```

**NOTES**

1. The string **name** is being injected directly into the final string
2. Instead of using single or double quotes, we need to use **back ticks**
3. **Placeholders** -> `${expression}`

`Another example`

```javascript
var a = 5;
var b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b}.`);
// "Fifteen is 15 and
// not 20."
```

`You can also use for multi-line strings`

```javascript
`string text line 1
string text line 2`
```

## Variable Declarations with Let and Const

### Let

While **var** creates a variable scoped within its nearest parent function, **lets** scopes the variable to the nearest block, this includes **for** loops, **if** statements, and others.

### Const

Follow the same scoping rules as **let**.

**ES6 Conventions**

* Use **const** by default
* Use **let** if you have to rebind a variable


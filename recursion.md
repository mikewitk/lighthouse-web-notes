# RECURSION

Is an alternative to traditional looping that allows you to do the same thing, just in a slightly different way.

Let's take an example: counting all even numbers from 0 to 12.

```javascript
let number = 0;

while (number <= 12) {
    console.log(number);
    number +=2;
}
```

Using recursion we have the following:

```javascript
function countEvenToTwelve(number) {
    if (number <= 12) {
        console.log(number);
        countEvenToTwelve(number + 2);
    }
}
countEvenToTwelve(0);
```
Recursion in a nutshell: a function that call itself until it doesn't.

Our countEvenToTwelve function will continue to call itself as long as *number <= 12* so as soon as *number . 12* the function will no longer call itself.
Every recursive function **must** stop calling itself at some point.

- We refer to *number <= 12* as a **recursive case**, because as long as this is true, the function will continue to call itself.
- We refer to *number > 12* as a **base case**. If this is true, the function will not call itself.

*A function must have at least one recursive case and at least one base case in order to be recursive*.

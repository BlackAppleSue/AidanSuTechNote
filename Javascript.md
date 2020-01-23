# Javascript Common Questions
 
 1. Event Bubbling & Event Capturing & Event Delegation (eventPhase)
```mermaid
sequenceDiagram
div ->> ul: Event Capturing
Note right of div: div.addEventListener<BR>('click', handler, true)
ul->>li: Event Capturing
li->> ul: Event Bubbling
ul-x div : Event Bubbling
Note right of div: event.<BR>stopPropagation()
```
## Function Scope

 - principle of least privilege

```
function foo(a) {
  var b = 2;

  function bar() {
    // ...
  }

  var c = 3;
}

foo(2);

console.log(a); // ReferrenceError
console.log(b); // ReferrenceError
console.log(c); // ReferrenceError

bar(); // ReferrenceError
```
```
function doSomething(a) {
  var b;
  b = a + doSomethingElse(a * 2);

  console.log(b * 3);

  function doSomethingElse(a) {
    return a - 1;
  }
}

doSomething(2); // 15

function doSomethingElse(a) {
  return a - 2;
}
```
## Function Declaration vs Function Expression

function declaration

```
function foo() {
  var a = 3;
  console.log(a); // 3
}

foo();

```

function expression

```
var foo = function bar() {
  var a = 3;
  console.log(a); // 3
};

foo();

```
## Immediately Invoked Function Expression, IIFE
```
(function foo() {
  var a = 3;
  console.log(a); // 3
})();

foo(); // foo is not defined
```
```
(function() {
  var a = 3;
  console.log(a); // 3
})();
```
## Block Scope
{ ... }
```
var foo = true;

if (foo) {
  const bar = foo * 2;
  console.log(bar); // 2
}

console.log(bar); // ReferenceError
```
```
{
  let i;
  for (i = 0; i < 10; i++) {
    console.log(i);
  }
}

console.log(i); // ReferenceError: i is not defined
```
## hoisting
```
console.log(a); // predict ReferenceError: a is not defined, but is undefined
var a = 10;
```
```
var a ;
console.log(a); // undefined 
a = 5;
```
let 與 const 確實有 hoisting，與 var 的差別在於提升之後，var 宣告的變數會被初始化為 undefined，而 let 與 const 的宣告不會被初始化為 undefined，而且如果你在「賦值之前」就存取它，就會拋出錯誤。

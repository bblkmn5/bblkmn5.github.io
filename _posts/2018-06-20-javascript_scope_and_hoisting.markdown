---
layout: post
title:      "Javascript: Scope and Hoisting"
date:       2018-06-20 15:25:26 +0000
permalink:  javascript_scope_and_hoisting
---


Scope and hoisting are two very important terms to know when learning about the Javascript programming language.

A **scope** is defined as the runtime environment where context is placed within the code. It is important to understand when defining and using variables. The outer-most scope is named the **global scope**. Variables defined in the global scope are accessible by all smaller, or **local**, scopes. Conversely, variables, functions, or objects defined in a local scope are only accessible within that scope. However, when a local scope has another function nested inside of it, the outer scope variables become accessible to the smaller scope.

 For example:
```
function newFunct(){
   var localVar = 1;
   console.log(`Hello, my favorite number is ${localVar}`)
}

newFunct()  //Hello, my favorite number is 1

console.log(localVar) //returns error of not defined

```

As shown above, trying to call the local variable outside of the function it is defined in (`newFunct()`) results in an error of not defined. However, if `localVar` is defined in the global scope, while keeping the local scoped variable the same, the result is different, and gives a more expected response:

```
var localVar = 2;

function newFunct(){
   var localVar = 1;
   console.log(`Hello, my favorite number is ${localVar}`);
}

newFunct()  //Hello, my favorite number is 1

console.log(localVar) //2
```

Even more interesting is when a variable is not defined in the local scope, but is used as an expression. The end result (using the code above, with no local variable definition):

```
newFunct() //Hello, my favorite number is 2
console.log(localVar) //2
 ```
 
 This leads into the topic of hoisting.
 
 
**Hoisting** is the process of moving all declared variables to the top of the current scope. However, any values given to these variables are not hoisted. Therefore, a variable has to be given a value before it can be used in the scope, but only if it has not been defined in a higher scope. In addition, a variable's value will be undefined if called before it has a value. This is different from not defined, as the variable is declared when hoisted.

Let's return to the example above, with a twist:

```
var localVar = 2;

function newFunct(){
   console.log(`Hello, my favorite number is ${localVar}`);
	 var localVar = 5;
}

newFunct()  //Hello, my favorite number is undefined

console.log(localVar) //2

```

As you can see, because of hoisting, `localVar` was still declared. However, as it is defined after the `console.log`, it was not given a value. If `localVar` was not defined after the `console.log`, or if it was just given a new value (with `localVar = 5` instead of `var localVar = 5`), the result would have been different.

In addition, when a function is assigned to a variable (a function expression), it behaves differently then when it is declared as a statement. Function expressions, just like regular variable declarations, are hoisted to the top of the scope, while the assignment stays in the place it is defined.


### Var, Let, and Const <- Hoisting and Scope

**Var** is available in all versions of Javascript, and is an older syntax. It allows for defining variables that can be changed later. For example, to define a variable, you would use `var new = 1;` when giving a new value to the same variable, you would use `new = 2;`, giving the `new` variable a different value. In addition, `var` is not **block-scoped**, meaning if defined in a local scope, it will change the global scope's assigned value. `Var` expressions are hoisted to the top of the current scope, but are given a value of undefined if called before the variable is defined within a block of code. As a result, it is considered bad use, because it can completely change the value of a variable if defined in another place in the code. No errors are shown if this occurs.
					 
**Let** is a new syntax from ES6, and allows for the definition of  a variable that can be changed later. Unlike `var`, `let` is **block-scoped**. As a result, when a `let`-defined variable is called, it gives the value of the scope in which it is called.
`Let`, like `var`, is hoisted in the scope it is defined. However, `let` is not given a value of undefined, but instead gives a `ReferenceError` of not defined. This is to prevent variable declarations after variable references (initializing). Finally, `let` will show an error if another variable is defined with the same name. This makes it easier for debugging, and gives less errors to worry about!

The final variable-defining syntax is `const`. **Const** allows for defining a variable that can NOT be changed later. This is best when declaring a variable that you want to stay constant (const = constant). `Const` behaves just like `let`; it is **block-scoped**, giving the current scopes' value when called, and is hoisted but not defined. It is best practice to declare all variables as `const`, then change to `let` if you want value to be changed.


### Function name() vs function() <- Hoisting

Two types of function syntax are named functions and unnamed, or anonymous, functions:

```
var namedFunction = function test (a, b) {}  // named function
var unnamedFunction = function (a, b) {}  // unnamed function
```

**Named functions** are hoisted to the top of the scope, while **anonymous functions** are not. Named functions are also easier to debug, as the name of the function appears in the error, rather than as an anonymous function. However, in post ES6, both named and unnamed functions have name properties set. 


Two types of functions in Javascript are **function expressions** and **function declarations**. 

**Function expressions** are functions that are declared to a variable. Function expressions are only defined when the line of declaration is reached. As shown below, a call to`testFunction()` results in an error, because the function has not been defined at that time (not hoisted!):

 ```
 testFunction()        //TypeError:  testFunction is not a function
 
 var testFunction = function() { 
        console.log("Hello")
	 }
```
	 
Alternatively, a **function declaration** is a function that is executed as soon as the entire script is loaded. As a result, it is hoisted to the top of the scope and can be called at any time within the code: 
	 
```
testFunctionTwo()      // "Hello Again"

function testFunctionTwo() { 
	console.log("Hello Again")
}
```

### What makes an arrow function different?
An **arrow function** `=>` is a short-hand way of writing a new function. With one variable, an arrow function is simply written as `variableName => {}`. When using zero or multiple variables, parenthesis are required. For example, `(hello, moto) => {}`, and `() => {}`.

An arrow function allows for the movement of `this` towards an inner scope. This means that an arrow function does NOT have it's own `this` defined. This is ideal for the use of classes in Javascript, providing an invaluable resource for passing a newly created instance of a class. 

However, arrow functions are not ideal for all situations. Arrow functions cannot be used as a constructor function, and do not have a prototype property. They are most ideal for situations where you will only use the function once.


After researching scope, hoisting, and other commonly-used Javascript terms, I feel much more confident in my understanding of Javascript, and am excited to keep learning.


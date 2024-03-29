# Execution context
![](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/8cd25270-8259-4c58-b0d5-fc393105c4ff)

- Global Execution Context: This is the default or base execution context. Variables and functions that are not inside any function are part of the global execution context. In the diagram, the global execution context initializes variables n, square1, square2, and a function square.

- Function Execution Context: This is created each time a function is invoked or called. In the diagram, the function square is called twice with different arguments (5 and 8), creating separate execution contexts for each call. Each function execution context shows memory allocation and code execution, calculating the square of the input numbers.

- Call Stack: This is the stack data structure that stores all the execution context objects in a LIFO (Last In, First Out) manner. When a function is called, a new execution context is created and added (pushed) to the call stack. When the function returns, its execution context is removed (popped) from the stack. In the diagram, after each function execution, the context is destroyed, returning control to the global context.

- Variable and Function Hoisting: In the global execution context, variables are initially set to undefined and functions are fully defined. This is due to a JavaScript mechanism called hoisting.

- Execution: The code part shows sequential line-by-line code execution including variable assignments and function calls. After the entire code execution is done, the global context will be destroyed.


# Hoisting
Hoisting in JavaScript refers to the behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase, before the code is executed. This means that you can use a variable or a function in your code before it's declared.

However, it's important to note that only the declarations are hoisted, not the initializations. Let's look at examples for both variables and functions:

- Variable Hoisting
```js
console.log(x); // Output: undefined
var x = 5;
console.log(x); // Output: 5

```
In the above example, the variable x is hoisted to the top of its scope during compilation. So, even though we try to access it before the declaration, it doesn't throw an error. The first console.log(x) outputs undefined because only the declaration is hoisted, not the assignment.

- Function Hoisting:
```js
foo(); // Output: "Hello, I'm foo!"

function foo() {
  console.log("Hello, I'm foo!");
}
```

In this example, the function foo is hoisted to the top of its scope. So, when we call foo() before its declaration, it works without an error.

However, hoisting does not work the same way with function expressions:
```js
bar(); // TypeError: bar is not a function

var bar = function() {
  console.log("Hello, I'm bar!");
};

```

In this case, the variable bar is hoisted, but it's initialized with undefined. Attempting to call bar() before the assignment results in a TypeError because bar is not yet a function.


#### Global execution context creation in call stack
![Screenshot 2024-01-09 182659](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/2271af17-9754-45de-8f59-e5ba62deef41)

#### function invoke creates Local execution context inside Global execution context

![Screenshot 2024-01-09 182725](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/6f26e3dc-65c8-4730-99e3-6e0b40c3ba20)

#### Once the control reaches back to Global execution context, local execution context will be removed from call stack

![Screenshot 2024-01-09 182752](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/ccb398e7-fe20-40d6-bae8-0107e30e5aa4)

#### Same thing repeats with the another function call also

![Screenshot 2024-01-09 182810](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/fa6604b7-b272-4418-b6f2-8f014dee21ac)
![Screenshot 2024-01-09 182839](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/2fcf6c80-4b5b-4e6e-82a6-9d40ef8e7e54)
![Screenshot 2024-01-09 183028](https://github.com/MuraliAirody/JavaScript_Learning_series/assets/71452201/bed2c315-8c7d-4d14-8990-8c8e2029d930)



# window 

In a browser environment, when the global execution context is created, it indeed creates a global object, which is typically referred to as window. In this context, window and this both refer to the global object, so window === this is true.

However, within a function execution context, the value of this depends on how the function is called. If a function is a regular function invocation, then this inside the function refers to the global object (window in the browser). However, if the function is a method of an object , the value of this can be different.
```js
console.log(window === this); // true

function exampleFunction() {
  console.log(this === window); // true
}

exampleFunction(); // When called as a regular function, this is the global object

const obj = {
  method: function() {
    console.log(this === obj); // true
  }
};

obj.method(); // When called as a method of an object, this is the object itself

```
**javascript is loosely typed language**

# The Scope Chain, 🔥Scope & Lexical Environment

In JavaScript, the concepts of Scope Chain, Scope, and Lexical Environment are fundamental to understanding how the language handles variables and functions. Here’s a brief explanation of each:

**Scope**: Scope refers to the visibility of variables or functions to the executing code1. In JavaScript, a variable or function is visible to the executing code if it is there in the current lexical environment or in the lexical-environment-chain of the enclosing function1. There are three types of scopes in JavaScript:

**Global Scope**: Variables or functions declared at the top of the code, i.e., in the global space, are said to be in the Global Scope. We can access these variables or functions from anywhere inside our code.
**Local/Function Scope**: When a variable is defined within a function or block, it has a local scope. This means that it can only be accessed within that function or block.
**Block Scope**: ES6 introduced the let and const keywords, which allow variables to have block scope. This means that variables defined within a block of code (such as within an if statement or a for loop) can only be accessed within that block.
**Scope Chain**: The Scope Chain is the hierarchy of scopes that will be searched in order to find a function or variable. It is the process in which the JavaScript engine searches for the value of the variables in the scope of the functions. However, the search is in a lexical manner.

**Lexical Environment**: The Lexical Environment is the local memory with the lexical environment of its parent (lexical parent - where actually parent physically present in the codes). The chain of the lexical environment references is known as the scope chain. The scope chain defines whether a variable or function is present inside the scope or not.

# let and const ,🔥 Temporal Dead Zone

In JavaScript, let and const are both used for variable declaration, but they have some differences in terms of behavior and scope. Both let and const were introduced in ECMAScript 6 (ES6) to provide block-scoped variables, as opposed to var, which is function-scoped.

Here's a brief overview of each:

let: Variables declared with let can be reassigned but are block-scoped. This means they are only accessible within the block in which they are defined or declared.
Example:

```javascript
{
    let x = 10;
    console.log(x); // 10
}
```
console.log(x); // ReferenceError: x is not defined
const: Variables declared with const are block-scoped like let, but they cannot be reassigned. However, it's important to note that for objects and arrays declared with const, their properties or elements can still be modified.
Example:

```javascript
const y = 5;
y = 10; // TypeError: Assignment to constant variable

const obj = { foo: 'bar' };
obj.foo = 'baz'; // This is allowed
console.log(obj.foo); // 'baz'
```
Now, regarding the Temporal Dead Zone (TDZ): This is a behavior specific to let and const. It's the period between entering a scope (starting from the top of the scope) and the actual declaration of a variable. During this time, accessing the variable will result in a ReferenceError. This is to enforce block scoping rules and to make it clear that the variable exists but isn't yet initialized.

Example:

```javascript
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 10;
```
In this example, even though x is declared later in the code, accessing it before the declaration results in a ReferenceError due to the Temporal Dead Zone.

# BLOCK SCOPE & Shadowing in JS 🔥

```js
{
    var a = 20
    let b = 10
    const c = 100
    console.log(a)
    console.log(b)
    console.log(c)
}
    console.log(a)
    console.log(b)
    console.log(c)

```
How call stack works 
```

Block
  b: <value unavailable>
  c: <value unavailable>
Script
  b: 10
  c: 100
Global
  a: 20
```

Block Scope: Block scope refers to the visibility and accessibility of variables within a block of code, typically delimited by curly braces {}. In JavaScript, variables declared with let and const have block scope, meaning they are only accessible within the block in which they are defined. This is in contrast to variables declared with var, which have function scope.
Example:

```javascript
{
    let x = 10;
    console.log(x); // 10
}
console.log(x); // ReferenceError: x is not defined
```
In this example, the variable x is scoped to the block within the curly braces.

Shadowing: Shadowing occurs when a variable with the same name as one in a higher scope is declared in a nested scope. The inner variable "shadows" the outer one, meaning that references to the variable name within the inner scope will refer to the inner variable, effectively hiding the outer one.
Example:

```javascript
let x = 10;

{
    let x = 20;
    console.log(x); // 20
}

console.log(x); // 10
```
In this example, the outer variable x is shadowed by the inner variable x within the block. Inside the block, x refers to the inner variable with the value 20, while outside the block, x refers to the outer variable with the value 10


 # Closures in JS 🔥
 A closure in JavaScript is a combination of a function and the lexical environment within which that function was declared. This lexical environment consists of any local variables that were in scope at the time the closure was created. Closures allow functions to maintain access to these variables even after they have exited the scope in which they were defined.

Here's a simple example to illustrate a closure:

```javascript
function outerFunction() {
  let outerVariable = 'I am from the outer function';
  
  function innerFunction() {
    console.log(outerVariable);
  }
  
  return innerFunction;
}
```

const innerFunc = outerFunction();
innerFunc(); // Output: "I am from the outer function"
In this example, innerFunction is defined within outerFunction and has access to the outerVariable even after outerFunction has finished executing. This happens because innerFunction forms a closure over the scope of outerFunction, capturing its lexical environment.

Closures are powerful because they allow for data encapsulation and the creation of private variables and functions. They are commonly used in scenarios such as creating factory functions, implementing module patterns, and handling asynchronous operations.

It's worth noting that closures also play a crucial role in event handling and callback mechanisms in JavaScript. When a callback function is passed to another function and executed later, it maintains access to the variables in its lexical scope, forming a closure. This enables asynchronous operations to work with data from their surrounding context.


```js
function main(){
    for(var i =1;i<6;i++){
        function sub(i){
            setTimeout(()=>{
            console.log(i)
        },i*1000)
        }
        sub(i)
    }
}

main()
```

# 🔥Interview Questions 📝📝

### **function statement / function declaration**
This is a way to define a function in JavaScript using the function keyword followed by the function name, parameters (if any), and the function body.
```js
function add(a, b) {
    return a + b;
}
```

### **function expression**
This is another way to define a function where the function is assigned to a variable. Function expressions do not have to have a name, but they can.
```js
const multiply = function(a, b) {
    return a * b;
};
```

### **Anonymous function**
An anonymous function is a function without a name. Anonymous functions are often used as arguments to other functions or assigned to variables.
```js
setTimeout(function() {
    console.log('This is an anonymous function.');
}, 1000);
```

### **named function expression**
This is a function expression that has a name. The name is only accessible within the function itself and is useful for recursion and stack traces.
```js
const factorial = function factorial(n) {
    return n <= 1 ? 1 : n * factorial(n - 1);
};
```

### **difference between parameter and agrguments**
Parameters are the variables declared in the function definition. They represent the values that the function expects to receive.
Arguments are the actual values passed to the function when it is called. They match up with the parameters defined in the function.
```js
function greet(name) { // 'name' is a parameter
    console.log(`Hello, ${name}!`);
}
greet('Alice'); // 'Alice' is an argument
```

### **first class function and arrow function**
In JavaScript, functions are treated as first-class citizens, which means they can be assigned to variables, passed as arguments to other functions, returned from other functions, and stored in data structures.
```js
const add = function(a, b) {
    return a + b;
};
const result = add(2, 3);
```
Arrow functions are a concise way to write function expressions in JavaScript. They have a shorter syntax compared to regular function expressions and do not bind their own this value.
```js
const multiply = (a, b) => a * b;
```

### **what is callback function in javascript**
A callback function is a function passed as an argument to another function, which is then invoked inside the outer function to complete some kind of action or operation.
Callback functions are commonly used in asynchronous programming to handle tasks like fetching data from a server, responding to user events, or executing code after a time delay.
They allow for non-blocking behavior, enabling JavaScript to perform tasks asynchronously without halting the execution of other code.

### **javascript is synchronous single threaded language**
JavaScript is indeed single-threaded, meaning it can only execute one piece of code at a time.
This means that code is executed sequentially from top to bottom in the order it appears in the script.
### **blocking the main thread**
Blocking the main thread refers to situations where long-running synchronous operations prevent other code from executing, leading to unresponsive user interfaces.
Heavy computations, long-running loops, or synchronous network requests can all block the main thread and degrade the user experience.

```js
// Example of blocking the main thread with a long-running loop

// Function to simulate a long-running task
function longRunningTask() {
    // Simulate a task that takes a significant amount of time
    const endTime = Date.now() + 5000; // 5 seconds
    while (Date.now() < endTime) {
        // Do nothing, just loop for 5 seconds
    }
    console.log("Long-running task completed");
}

// Function to demonstrate blocking behavior
function blockMainThread() {
    console.log("Starting long-running task...");
    longRunningTask();
    console.log("Main thread unblocked!");
}

// Call the blocking function
blockMainThread();
console.log("Main thread continues...");

```

### **power of callbacks**
Callbacks provide a powerful mechanism for handling asynchronous operations in JavaScript.
They allow for code to be executed once an asynchronous task completes, enabling developers to write efficient and responsive applications.
Callbacks are a fundamental building block for many asynchronous patterns in JavaScript, including event handling, AJAX requests, and timers.

### **deep about event listeners**
Event listeners are functions that are invoked in response to a specific event occurring in the browser, such as a mouse click, key press, or page load.
They are used to create interactive web pages by responding to user actions.
Event listeners can be attached to DOM elements using methods like addEventListener, allowing developers to define custom behavior for various user interactions.
### **clouser demo with event listeners**
Closures are functions that have access to variables from their containing scope even after the parent function has finished executing.
In the context of event listeners, closures are often used to maintain state or access variables from the surrounding scope.
For example, a closure might be used to keep track of a counter or store data associated with a specific event listener.
```js
function createCounter() {
    let count = 0;

    function incrementCounter() {
        count++;
        console.log("Counter incremented to:", count);
    }

    function decrementCounter() {
        count--;
        console.log("Counter decremented to:", count);
    }

    // Return an object with methods to increment and decrement the counter
    return {
        increment: incrementCounter,
        decrement: decrementCounter
    };
}

// Create a counter using the createCounter function
const counter = createCounter();

// Add event listeners to buttons to increment and decrement the counter
document.getElementById("incrementBtn").addEventListener("click", counter.increment);
document.getElementById("decrementBtn").addEventListener("click", counter.decrement);

```
### **scope demo with event listeners**
Scope in JavaScript refers to the visibility and lifetime of variables and functions.
When working with event listeners, it's important to understand how scope affects the availability of variables and functions.
Variables declared inside a function are only accessible within that function's scope, unless closures are used to capture them.
### **garbage collection and removeEventlisteners**
Garbage collection is the process by which JavaScript automatically frees up memory by removing objects that are no longer in use or referenced.
When removing event listeners, it's important to ensure that all references to the listener function are removed to prevent memory leaks.
Failing to remove event listeners can prevent the associated DOM elements from being garbage collected, leading to memory leaks and potential performance issues.


# Blocking Main Thread

```js
 console.log("start);

 setTimeout(()=>{
  console.log("callback)
 },5000);

 let startTime  = new Date().getTime();
 let endTime = startTime;

 while(endTime<startTime + 10000){ //10s delay
    endTime = new Date().getTime();
 }

 console.log("End")
```
- console.log("start);: This prints "start" to the console, indicating the beginning of execution.

- setTimeout(() => { console.log("callback") }, 5000);: This schedules a callback function to be executed after a delay of 5000 milliseconds (5 seconds). However, it doesn't block the main thread; instead, it sets up a timer that will trigger the callback function asynchronously after the specified delay.

- let startTime = new Date().getTime();: This captures the current time in milliseconds as the start time.

- let endTime = startTime;: Initializes endTime with the same value as startTime.

- while (endTime < startTime + 10000) { ... }: This initiates a while loop that runs until 10 seconds have passed from the startTime. The loop continuously updates endTime with the current time until the condition endTime < startTime + 10000 evaluates to false. During this loop, the main thread is actively engaged in checking the condition and updating endTime, causing it to be blocked.

console.log("End"): Once the loop condition is met, indicating that 10 seconds have passed, this line prints "End" to the console.

**Explanation of blocking the main thread:**
The main thread is blocked primarily by the while loop (while (endTime < startTime + 10000) { ... }). During this loop, the thread continuously checks the condition endTime < startTime + 10000 and updates endTime. Since this loop doesn't yield control back to the event loop, it monopolizes the main thread's execution, preventing any other code, including asynchronous tasks like the setTimeout callback, from being executed until the loop completes.

Due to this blocking behavior, even though there's an asynchronous setTimeout scheduled to execute after 5 seconds, its execution is delayed until the main thread becomes available after the loop completes. Hence, you may observe "callback" being logged to the console after "End", not after 5 seconds from the "start" message as intended by the setTimeout.

# Function Currying
Currying is a functional programming technique where a function that takes multiple arguments is transformed into a sequence of functions, each taking a single argument. This allows for more flexible and modular code. Here's a basic explanation and example in JavaScript:

```javascript
// Original function taking multiple arguments
function add(x, y, z) {
  return x + y + z;
}

// Curried version of the function
function curriedAdd(x) {
  return function(y) {
    return function(z) {
      return x + y + z;
    };
  };
}

// Example usage
console.log(add(1, 2, 3)); // Outputs: 6

const curried = curriedAdd(1)(2)(3);
console.log(curried); // Outputs: 6
```

In the above example, curriedAdd takes the first argument x and returns a function that takes the second argument y, which in turn returns a function that takes the third argument z. This allows you to call curriedAdd with one argument at a time.

Currying can make functions more flexible and composable, as you can partially apply arguments to create new functions with preset values. This is particularly useful in scenarios where you want to reuse a function with some of its arguments pre-determined.

<details>
<summary><b>Currying offers several advantages in real-world scenarios:</b></summary>

- Partial Application: Currying allows you to create specialized versions of a function by partially applying its arguments. This can be particularly useful when you have a function with many arguments and you frequently need to use it with some arguments fixed. It simplifies the creation of specialized functions on-the-fly.

- Code Reusability: Currying promotes code reuse by allowing you to create specialized functions from a more general one. Instead of defining multiple functions with similar behavior but different arguments, you can define a single function and curry it to create variations as needed.

- Modularity: Currying encourages modular programming. By breaking down functions into smaller, single-purpose functions, you can compose them more easily to build complex behavior. Each curried function can focus on a single aspect of the overall functionality, making the code easier to understand and maintain.

- Functional Composition: Currying fits well with functional programming principles like composition. Composing functions becomes more natural when each function takes only one argument. This allows you to chain functions together more easily, creating pipelines of transformations.

- Flexibility: Currying allows for greater flexibility in function invocation. You can choose to provide arguments one at a time or provide all arguments at once, depending on the context and requirements of your application.

</details>
<hr>

# Callback Hell

Callback hell, also known as "pyramid of doom," refers to the situation in asynchronous programming where code becomes difficult to read and maintain due to nested callbacks. It occurs when multiple asynchronous operations are chained together in a nested structure, leading to deeply nested callback functions.

**Callback hell can make code:**

- Hard to read: The deeply nested structure makes it challenging to understand the flow of execution and the relationships between different parts of the code.

- Hard to maintain: Adding, removing, or modifying operations becomes difficult and error-prone due to the complex nesting.

- Error-prone: Error handling becomes cumbersome, and it's easy to introduce bugs, especially when dealing with asynchronous code.

```js
fetchUserDetails(userId, function(userDetails) {
  // Process user details
  // Nested callback for fetching cart items
  fetchCartItems(userId, function(cartItems) {
    // Process cart items
    // Nested callback for payment processing
    processPayment(userDetails, cartItems, function(paymentResult) {
      // Handle payment result
      // Nested callback for order confirmation
      confirmOrder(userDetails, cartItems, orderDetails, function(orderConfirmation) {
        // Handle order confirmation
      });
    });
  });
});

```
# JAVASCRIPT CONCEPTS

---

- [JAVASCRIPT CONCEPTS](#javascript-concepts)
  - [WHAT IS JAVASCRIPT?](#what-is-javascript)
  - [THE JAVASCRIPT ENGINE AND RUNTIME](#the-javascript-engine-and-runtime)
    - [JS Engine](#js-engine)
    - [CALL STACK](#call-stack)
    - [HEAP](#heap)
    - [COMPILATION VS. INTERPRETATION LANGUAGES](#compilation-vs-interpretation-languages)
    - [JIT IN JAVASCRIPT](#jit-in-javascript)
    - [WEB APIs](#web-apis)
    - [Callback Queue](#callback-queue)
  - [EXECUTION CONTEXT AND THE CALL STACK](#execution-context-and-the-call-stack)
    - [What is an execution context?](#what-is-an-execution-context)
    - [What's inside an execution context?](#whats-inside-an-execution-context)
    - [Call stack](#call-stack-1)
  - [SCOPE AND SCOPE CHAIN](#scope-and-scope-chain)
    - [Scope Concepts](#scope-concepts)
    - [Global Scope](#global-scope)
    - [Function Scope](#function-scope)
    - [Block Scope (ES6)](#block-scope-es6)
    - [Scope Chain](#scope-chain)
    - [Scope chain vs. Call stack](#scope-chain-vs-call-stack)
    - [Summary](#summary)
  - [Hoisting in JavaScript](#hoisting-in-javascript)
    - [Temporal Dead Zone, Let and Const](#temporal-dead-zone-let-and-const)
      - [Hoisting](#hoisting)
  - [THE THIS KEYWORD](#the-this-keyword)
    - [Method call](#method-call)
    - [Regular function call](#regular-function-call)
    - [Arrow function call](#arrow-function-call)
    - [Event listener](#event-listener)
  - [Primitives vs. Objects (Primitive vs. Reference Types)](#primitives-vs-objects-primitive-vs-reference-types)
    - [Primitives Summary](#primitives-summary)
    - [Objects Summary](#objects-summary)
    - [Objects](#objects)

---

## WHAT IS JAVASCRIPT?

**Short answer:** JavaScript is a high-level, object-oriented, multi-paradigm programming language.

**Long answer:** JavaScript is a high-level, prototype-based object-oriented, multi-paradigm, interpreted or just-in-time compiled, dynamic, single-threaded, garbage-collected programming language with first-class functions and a non-blocking event loop concurrency model.

Destructuring the long answer:

- **High-level:** JavaScript is a high-level programming language. This means that it is easy to read and write, and it is close to human languages. It is also easy to understand and learn. Low-level programming languages on the other end are closer to machine languages and are harder to read and write (the developer has to manage memory and other resources manually).
- **Garbage-collected:** JavaScript is a garbage-collected language. This means that the developer does not have to manage memory manually. The garbage collector takes care of that. The garbage collector is a program that runs in the background and frees up memory when it is not being used anymore.
- **Interpreted or just-in-time compiled:** JavaScript is an interpreted language. This means that the code is not compiled into machine code before it is executed. Instead, the code is compiled line by line while it is being executed. This is also called just-in-time compilation. The advantage of this is that the developer does not have to compile the code before it is executed. The disadvantage is that the code runs slower than compiled code. Visit [just-in-time compilation](#jit-in-javascript) for more info.
- **Multi-paradigm:** JavaScript supports multiple programming paradigms. This means that it supports different ways of programming. For example, it supports object-oriented programming, functional programming, and procedural programming.
  - Procedural programming is when the code is written as a sequence of steps.
  - Functional programming is when the code is written as a sequence of functions.
  - Object-oriented programming is when the code is written as a sequence of objects.
- **Prototype-based:** JavaScript is a prototype-based language. This means that objects in JavaScript are based on prototypes. A prototype is a blueprint for an object. It is used to create new objects. For example:

  | Array |
  | --- |
  | Array.prototype.push |
  | Array.prototype.indexOf |

  ```javascript
    const arr = [1, 2, 3];
    arr.push(4); // arr is now [1, 2, 3, 4]
    const hasZero = arr.indexOf(0) > -1; // hasZero is false
    ```

    How does this happen? The prototype is the Array prototype object, the array inherits methods from to type as it is built from the prototype itself. Take for example a car, it has a prototype, the prototype is the car itself, and the car inherits methods from the prototype as it is built from the prototype itself.

- **First-class functions:** JavaScript supports first-class functions. This means that functions in JavaScript are treated like any other variable. Functions can be passed as arguments to other functions, returned by other functions, and assigned to variables.
- **Dynamic**: JavaScript is a dynamic language. This means that the data types are not set when the code is written. Instead, the data types are set when the code is executed. This is also called type coercion. For example:

  ```javascript
    let x = 1;
    x = 'hello';
  ```

  In the example above, the variable `x` is set to the number `1`. Then, the variable is set to the string `'hello'`. This is possible because JavaScript is a dynamic language. The data type is set when the code is executed, not when it is written, some consider this a weakness of JavaScript, though there's **TypeScript** to help with that.

- **Single-threaded:** JavaScript is a single-threaded language. This means that only one command can be executed at a time. This is also called synchronous execution. For example:

  ```javascript
    console.log('Hello');
    console.log('World');
  ```

  In the example above, the code is executed line by line. The first line is executed, then the second line is executed. This is possible because JavaScript is a single-threaded language. The code is executed line by line, one command at a time.

- **Non-blocking event loop concurrency model:** JavaScript has a non-blocking event loop concurrency model. This means that the code is executed line by line, one command at a time. However, if a function takes a long time to execute, the code execution is not blocked. Instead, the code execution continues. When the function is done executing, the result is returned. This is also called asynchronous execution. For example:

  ```javascript
    console.log('Hello');
    setTimeout(() => {
      console.log('World');
    }, 1000);
  ```

  In the example above, the code is executed line by line, one command at a time. The first line is executed, then the second line is executed. However, the second line is not executed immediately. Instead, the second line is executed after 1 second. This is possible because JavaScript has a non-blocking event loop concurrency model. The code is executed line by line, one command at a time. However, if a function takes a long time to execute, the code execution is not blocked. Instead, the code execution continues. When the function is done executing, the result is returned.

---

## THE JAVASCRIPT ENGINE AND RUNTIME

### JS Engine

A JavaScript engine is a program that executes JavaScript code. It translates the code written in a high-level language into machine code that can be run on a computer.

JavaScript engines are an important part of modern web browsers, as they allow web pages to execute JavaScript code. When you visit a website that uses JavaScript, your web browser downloads the JavaScript code and runs it on your computer using a JavaScript engine.

There are several JavaScript engines in use today, including the V8 engine developed by Google and used in the Chrome browser, and the Spider Monkey engine developed by Mozilla and used in the Firefox browser.

![Call Stack & Heap Description](https://i.imgur.com/EEb5hMN.png)

### CALL STACK

Where our code is executed using execution context. See [execution context](#execution-context-and-the-call-stack) and [call stack](#call-stack-1) for more info.

### HEAP

In JavaScript, the heap is a region of memory that is used to store objects and data structures. It is separate from the call stack, which is used to store the current execution state of the program.

The heap is used to store objects that are created dynamically at runtime, such as objects that are created using the `new` operator or objects that are created using the literal syntax (e.g. `{}` or `[]`). The heap is also used to store data structures that are created using the `new` operator, such as arrays or maps.

The heap is managed by the JavaScript engine, and objects in the heap are subject to garbage collection when they are no longer being used. Garbage collection is the process by which the JavaScript engine identifies and removes objects from the heap that are no longer being used by the program. This helps to free up memory and improve the performance of the program.

The heap is an important aspect of the way JavaScript works, and is used by many other programming languages as well. It is separate from the stack, which is used to store the current execution state of the program and is managed by the JavaScript engine to ensure that objects and data structures are efficiently used and managed in memory.

### COMPILATION VS. INTERPRETATION LANGUAGES

**Compilation:** Entire code is converted into machine code at once, and written to a binary file that can be executed by a computer.
![Compilation Process](https://i.imgur.com/k4tbNsN.png)

**Interpretation:** The interpreter runs through the source code and executes it line by line.
![Interpretation Process](https://i.imgur.com/n2iyTwm.png)

The compilation process is way faster than the interpretation one.

Javascript uses **JIT** (Just-in-time) compilation (mix between Compilation & Interpretation)
![Just in Time Process](https://i.imgur.com/FHhwpuc.png)

### JIT IN JAVASCRIPT

![The processes behind JIT in Javascript](https://i.imgur.com/z7CTSTL.png)

The code first is parsed into AST (abstract syntax tree) - it splits up each line of code into pieces that are meaningful to the language - like const/function keywords, and saves all of those pieces into the tree in a structured way while checking for syntax errors at the same time.

Then comes compilation, which takes the generated AST and compiles it into machine code, then the machine code gets executed right away. It doesn't stop at that moment, javascript will execute a very unoptimized machine code at first, but during execution, the machine code is optimized and recompiled during the execution.

### WEB APIs

![Web APIs](https://i.imgur.com/ynjjDyC.png)

- DOM,
- Timers,
- Fetch API, ...

What are they? They are not part of the JS language, they are part of the browser, and they are not part of the JS engine. (Functionalities provided to the engine, accessible on the window object. (e.x: window.setTimeout))

### Callback Queue

![Callback Queue](https://i.imgur.com/FVJmbgD.png)

Callback functions, for e.x, when an event is called (e.x an onClick), the callback function is put into the callback queue. Then, when the stack is empty, the callback function is passed to the stack so that it can be executed. And this happens due to the event loop, it takes callback functions from the callback queue and puts them into the call stack so they can be executed.

---

## EXECUTION CONTEXT AND THE CALL STACK

### What is an execution context?

After compilation, a so-called global execution context is created for the top-level code (code that is not inside any function), after that is finished, the execution of top-level code inside global EC happens, and only then does the execution of functions happens while waiting for callbacks. (e.x: click event callback)

Exactly one global execution context (EC) happens, that is for top-level code. But, an execution context is created per each function. (for each function call, a new execution context is created)

### What's inside an execution context?

- Variable environment:
  - let,
  - const,
  - var declarations,
  - functions,
  - arguments object (not in arrow functions)),
- The scope chain,
- `this` keyword (not in arrow functions)
  All of this is generated during the "creation phase", right before execution.

Arrow functions don't have the arguments object & this keyword, they can instead use them from their closest regular function parent.

```javascript
const name = 'ItsYeWolfie';

const first = () => {
  let a = 1;
  const b = second(7, 9);
  a = a + b;
  return a;
};

function second(x, y) {
  var c = 2;
  return c;
}

const x = first();
```

| Scope chain: [global] | Scope chain: [first, global] | Scope chain: [second, first, global] |
| --------------------- | ---------------------------- | ------------------------------------ |
| **name:** ItsYeWolfie     | **a:** 1                         | **c:** 2                                 |
| **first:** function       | **b:** unknown                   | **arguments:** {0: 7, 1: 9}              |
| **second:** function      |
| **x:** unknown            |

Arguments are an array of all the arguments passed into the function. (not in arrow functions)

How will the engine keep track of the order of execution of functions? It will use a data structure called the call stack.

### Call stack

LIFO (Last In First Out) data structure, where the last function that gets pushed into the stack is the first one to be popped out of the stack when the execution is finished.

It is as if you bought pizzas together with your friends, and you put them on a table to keep track of who bought which pizza. The last pizza you bought is the first one you eat, and the first pizza you bought is the last one you eat.

For example in the code above, the call stack will look like this:

```javascript
global execution context
x calls first()
first()
first() calls second()
second()
```

![Call stack](https://i.imgur.com/R51TLgU.png)

So the first function that gets popped out of the stack is second(), then first(), then x, and finally the global execution context.
What does this mean? It means that the execution of the code happens in the same order as the functions are called. (first `x`, then `first`, then `second`)
This is called synchronous execution, and it is the default behavior of javascript, it will do one thing at a time, in the order that it is written, and it will wait for the execution of the current function to finish before moving on to the next one (the functions which were called are put into the call stack, and when they are finished, they are popped out of the stack). The only exception to this are asynchronous functions, which will be explained later.

---

## SCOPE AND SCOPE CHAIN

### Scope Concepts

The scope is the visibility of variables. (where can we access a certain variable?) How our program's variables are organized and accessed. "Where can we access a certain variable?", "Where do we have access to a certain variable?" or "Where was a certain variable defined in the code?"

- **Lexical scope:** A function that is lexically within another function gets access to the scope of the outer function. (e.x: a function defined inside another function has access to the variables of the outer function)

- **Scope:** Space or environment in which a certain variable is declared, that determines its accessibility. (visibility).
  - There are three types of scope:
    - Global scope
    - Function scope
    - Block scope
- **Scope of a variable:** Region of your code where you have access to a certain variable.

### Global Scope

```javascript
const name = 'ItsYeWolfie';
const job = 'Fellow';
const year = 2001;
```

- Global scope is the default scope in javascript.
- It is the outermost scope in javascript. (outside of any function or block)
- Variables defined in the global scope are accessible from anywhere in the code.

### Function Scope

```javascript
function calcAge(birthYear) {
  const age = 2022 - birthYear;
  return age;
}

console.log(age); // ReferenceError: age is not defined
```

- Variables defined inside a function are not accessible from outside the function.
- Also called a local scope, because the variables are only accessible inside the function.

### Block Scope (ES6)

```javascript
if (year >= 2001 && year <= 2021) {
  const century = true;
  var millenial = true;
}

console.log(century); // ReferenceError: century is not defined
console.log(millenial); // true
```

- Variables defined inside a block are not accessible from outside the block.
- However, variables defined with the `var` keyword are accessible from outside the block.
- Variables defined with the `let` and `const` keywords are not accessible from outside the block.
- Functions defined inside a block are not accessible from outside the block, (they are also block-scoped), at least in strict mode.

### Scope Chain

```javascript
const name = 'ItsYeWolfie';

function first() {
  const age = 2022 - 2001;

  if (age >= 22) {
    const decade = true;
    var millenial = true;
  }

  function second() {
    const job = 'Fellow';
    console.log(
      `${name} is a ${age}-year old ${job}. Is he a millenial? ${millenial}`
      // ItsYeWolfie is a 21-year old Fellow. Is he a millenial? false
    );

    console.log(decade); // ReferenceError: decade is not defined
  }

  second();
}

first();
```

At first sight, the scopes might look like this:

| Global Scope      | first() Scope | second() Scope |
| ----------------- | ------------- | -------------- |
| name: ItsYeWolfie | age: 21       | job: Fellow    |

The secret is that every scope has access to the variables of all its parent scopes. This is called the scope chain. That means that the second() function has access to the variables of the first() function, and the first() function has access to the variables of the global scope. How does this work? The second `scope()` will look for the variable it needs in its scope, and if it doesn't find it there, it will look in the scope of its parent, and so on, until it finds the variable it needs, or it reaches the global scope, and if it doesn't find the variable there, it will throw a `ReferenceError`.

This is called the **variable lookup**, and it is how the javascript engine finds the value of a variable, this only works **upwards**, it will **_never look downwards_**, so the `second()` function will never have access to the variables of a `third()` function.

The `millennial` variable is accessible from the `second()` function, because it is defined by the `var` keyword (which is exempt from the block scope), and the `decade` variable is not accessible from the `second()` function, because it is defined by the `const` keyword (which is not exempt from the block scope) - **var** is function scoped, **let** and **const** are block scoped.

The final scope chain will look like this:

| Global Scope      | first() Scope     | if block Scope    | second() Scope    |
| ----------------- | ----------------- | ----------------- | ----------------- |
| name: ItsYeWolfie | age: 21           | age: 21           | age: 21           |
|                   | millenial: true   | millenial: true   | millenial: true   |
|                   | name: ItsYeWolfie | name: ItsYeWolfie | name: ItsYeWolfie |
|                   |                   |                   | job: Fellow       |

Due to lexical scope, the `if-else` cannot access the `job` variable, because it is defined in the `second()` function, which is not a parent of the `if-else` block, they are merely siblings.

### Scope chain vs. Call stack

```javascript
const a = 'ItsYeWolfie';
first();

function first() {
  const b = 'Hello';
  second();

  function second() {
    const c = 'Hey!';
    third();
  }
}

function third() {
  const d = 'Hi';
  console.log(a + b + c + d);
  // ReferenceError
}
```

The call stack will look like this:

| Call stack |
| ---------- |
| third()    |
| second()   |
| first()    |
| global     |

| Global EC (Variable Environment - VE) | first() EC       | second() EC | third() EC |
| ------------------------------------- | ---------------- | ----------- | ---------- |
| a: ItsYeWolfie                        | b: Hello         | c: Hey!     | d: Hi      |
| first: function                       | second: function |             |            |
| third: function                       |                  |             |            |

Order of execution: global -> first -> second -> third (order in which the functions are called)

The scope chain will look like this:

| Global Scope     | first() Scope    | second() Scope   | third() Scope   |
| ---------------- | ---------------- | ---------------- | --------------- |
| a: ItsYeWolfie   | b: Hello         | c: Hey!          | d: Hi           |
| first: function  | second: function | b: Hello         | a: ItsYeWolfie  |
| second: function | a: ItsYeWolfie   | second: function | first: function |
|                  | first: function  | a: ItsYeWolfie   | third: function |
|                  | third: function  | first: function  |
|                  |                  | third: function  |

That shows that the code above will throw a `ReferenceError`, as `b` and `c` are not defined in the `third()` function, and the `third()` function is not a parent of the `first()` function, they are merely siblings.

### Summary

- Scope determines the accessibility (visibility) of variables. It asks the question "Where can we access a certain variable?", "Where do variables live?".
- There are 3 types of scope: global scope, function scope and block scope.
- Variables defined in the global scope are accessible from anywhere in the code.
- Only `let` and `const` are block-scoped, and `var` is function-scoped.
- In JavaScript, we have lexical scope, which means that scope is defined by the placement of functions and blocks in the code, not by where the functions and blocks are called.
- Every scope always has access to the variables of its parent scope, but not the other way around.
- When a variable is not in the current scope, the scope chain is used to look for the variable in the parent scope, and so on, until the variable is found, or the global scope is reached, and if the variable is not found in the global scope, a `ReferenceError` is thrown.
- The scope chain is a one-way street, it goes from the current scope to the global scope, but not the other way around.
- The scope chain in a certain scope is equal to adding together all the variable environments of all the parent scopes.
- The scope chain has nothing to do with the order in which functions are called, it has to do with the order in which functions are written in the code.

Check [this](scoping.js) for practice.

---

## Hoisting in JavaScript

**Hoisting** is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. Inevitably, this means that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

**Before execution,** the code is scanned for variable declarations and for each variable, a new property is created in the Variable Environment Object. **After that, the code is scanned for function declarations, and for each function, a new property is created in the Variable Environment Object.**

|                                 | Hoisted? | Initial value               | Scope                  |
| ------------------------------- | -------- | --------------------------- | ---------------------- |
| function declaration            | Yes      | function                    | Block(Strict)/Function |
| var variable                    | Yes      | undefined                   | Function               |
| let and const variables         | No       | unitialized,TDZ             | Block                  |
| function expressions and arrows | No       | Depends if var or let/const | Block                  |

### Temporal Dead Zone, Let and Const

```javascript
const myName = 'ItsYeWolfie';

if (myName === 'ItsYeWolfie') {
  console.log(`${myName} is a ${job}`); // ReferenceError: Cannot access 'job' before initialization
  const age = 2022 - 2001;
  console.log(age);
  const job = 'Fellow';
  console.log(x); // ReferenceError: x is not defined
}
```

The code above will throw a `ReferenceError` because the `job` variable is in the temporal dead zone, and the `x` variable is not defined.

- Because it is a safer way to declare variables because it prevents us from using variables before they are declared. It makes it easier to avoid and catch errors. Accessing a variable before it is declared is a common mistake, and it is a common source of bugs and should be avoided.
- Makes const variables more useful, because they are now immutable, and we can't accidentally change them.

#### Hoisting

**If hoisting brings a lot of problems, why is it still a thing?**

- _It is a feature of JavaScript, and it is not going to be removed._
- Using functions before the actual declaration.
- var hoisting is just a side effect of how the JavaScript engine works, and it is not a good practice to use it.

Visit [this](hoisting.js) for practice and further reading & understanding.

## THE THIS KEYWORD

`this` keyword is a special variable that is created for every execution context (every function). It is not assigned a value until a function where it is defined is called. It takes the value of (points to) the "owner" of the function in which `this` keyword is used.

**`this` keyword is not static. It depends on how the function is called, and its value is only assigned when the function is called.**

If we set for example `x = 5`, and then we call `console.log(this.x)`, `this` keyword will point to the **global object**, which is the `window` object in the browser, and the `global` object in Node.js.

Let's analyze four different ways of calling a function, and see how `this` keyword behaves in each case.

### Method call

```javascript
const myObj = {
  name: 'ItsYeWolfie',
  birthYear: 2001,
  calcAge: function () {
    console.log(this);
    console.log(2022 - this.birthYear);
  },
};

myObj.calcAge(); // this = myObj
```

In the code above, `this` keyword points to the object that is calling the method, in this case, the `myObj` object, and `this.birthYear` is equal to `myObj.birthYear`, which is `2001`.

### Regular function call

```javascript
const myObj = {
  name: 'ItsYeWolfie',
  birthYear: 2001,
};

const calcAge = function () {
  console.log(this);
  console.log(2022 - this.birthYear);
};

calcAge(); // this = undefined
```

In the code above, `this` keyword is undefined, because the `calcAge()` function is a regular function call and not a method call. (This applies only for strict mode, in non-strict mode, `this` keyword will point to the global object, which is the `window` object in the browser, and the `global` object in Node.js.)

### Arrow function call

```javascript
const myObj = {
  name: 'ItsYeWolfie',
  birthYear: 2001,
  calcAge: function () {
    console.log(this);
    console.log(2022 - this.birthYear);

    const isMillenial = () => {
      console.log(this);
      console.log(this.birthYear >= 1981 && this.birthYear <= 1996);
    };

    isMillenial();
  },
};

myObj.calcAge(); // this = myObj
```

In the code above, `this` keyword points to the object that is calling the method, in this case, the `myObj` object, and `this.birthYear` is equal to `myObj.birthYear`, which is `2001`. Arrow functions do not get their own `this` keyword, they simply use `this` keyword of the function they are written in.

### Event listener

```javascript
const myObj = {
  name: 'ItsYeWolfie',
  birthYear: 2001,
};

const calcAge = function () {
  console.log(this);
  console.log(2022 - this.birthYear);
};

document.querySelector('.btn').addEventListener('click', calcAge); // this = undefined
```

In the code above, `this` keyword is undefined, because the `calcAge()` function is a regular function call and not a method call. (The strict mode applies just the same, in non-strict mode, `this` keyword will point to the global object, which is the `window` object in the browser, and the `global` object in Node.js.)

There are other ways to fix this, but the most common ways are:

- Using the `new` keyword.
- Using the `call()` method.
- Using the `apply()` method.
- Using the `bind()` method.

They will be explained way down below.

See [this](this.js) for practice and further reading & understanding.

## Primitives vs. Objects (Primitive vs. Reference Types)

In JavaScript, there are two types of data types: primitives and objects.

What are the primitive data types?

- Number
- String
- Boolean
- Undefined
- Null
- Symbol (ES2015)
- BigInt (ES2020)

What are the object data types?

- Object literals
- Arrays
- Functions
- Many more...

How do they differ? It's how they are stored in the computer's memory.

If we recall from the previous chapters, the computer's memory is divided into two parts: the stack and the heap. The call stack is where the function calls are stored, and the heap is where the objects are stored. On the other hand, the primitive data types are stored in the stack, that means the primitive types are stored in the execution context in which they are declared. Let's find out how they differ.

Primitive values example:
```javascript
let age = 21;
let oldAge = age;
age = 22;
console.log(age); // 22
console.log(oldAge); // 21
```

When we create a primitive value, it is stored in the stack, and the variable `age` points to that value. When we create another variable `oldAge` and assign it the value of `age`, the value of `age` is copied and stored in the stack, and the variable `oldAge` points to that value. When we change the value of `age`, the value of `oldAge` remains the same, because it is a copy of the value of `age`, and it is stored in the stack.

In technical details: Javascript will first create a so-called unique identifier with the variable name, then a piece of memory will be allocated with a certain address, for e.x `0x001`, and then the value will be stored in that memory address. The identifier points to that memory address, not the value itself. When we assign a variable to another variable, the value is copied, and the identifier points to the same memory address. It will look as if `oldAge` is a copy of `age`, but it is not. When we reassign the value of `age`, a new memory address will be allocated, and the identifier will point to that new memory address (`0x002`) - which will hold the value of 31. Now, with reference types, it is a bit different.

![Call Stack of age & oldAge](https://i.imgur.com/awy3ElR.png)

Reference values example:
```javascript
const me = {
  name: 'ItsYeWolfie',
  age: 21,
};

const friend = me;
friend.age = 27;
console.log('Friend:', friend); // Friend: { name: 'ItsYeWolfie', age: 27 }
console.log('Me:', me); // Me: { name: 'ItsYeWolfie', age: 27 }
```

When we create an object, it is stored in the heap, and the variable `me` points to that object. When we create another variable `friend` and assign it the value of `me`, the value of `me` is not copied, but the identifier points to the same memory address. When we change the value of `friend.age`, the value of `me.age` also changes, because they point to the same memory address.

In technical details: JavaScript will create an unique identifier with the variable name `me`, which will point to a memory address, for e.x `0x003`, and then the object's reference will be stored in that memory address. In other words, the piece of memory in the call stack has a refernece to the piece of memory in the heap, which holds the `me` object. Next, we create a new variable `friend`, which will point to the same memory address as `me`, which is `0x003`, with that, we have the understanding that the `friend` object is the exact same object as the `me` object. When we change the value of `friend.age`, the value of `me.age` also changes, because we are changing the value of the object that is stored in the heap, we are not changing the value of the memory address's vaue in the stack.

How will this look in the whole picture?

Stack memory:
| Identifier | Memory Address | Value |
|------------|----------------|-------|
| age        | 0x001          | 21    |
| oldAge     | 0x002          | 21    |
| me         | 0x003          | D30F  |
| friend     | 0x003          | D30F  |

Heap memory:
| Memory Address | Value |
|----------------|-------|
| D30F           | { name: 'ItsYeWolfie', age: 21 } |

To summarize:

### Primitives Summary

- Primitives are **immutable**.
- Primitives are **copied by their value** (they are saved into their place in memory, in the stack).
- Primitives are **passed by value**.

### Objects Summary

- Objects are **mutable**.
- Objects are **copied by their reference** (they are saved into their place in memory, in the heap).
- Objects are **passed by reference**.

For further understanding, let's see some examples.


```javascript
let lastName = 'Wolfie';
let oldLastName = lastName;
lastName = 'Wolf';
console.log(lastName, oldLastName); // Wolf Wolfie
```

In the code above, we can see that the `oldLastName` variable is a copy (a new variable) of the `lastName` variable, and when we change the `lastName` variable, the `oldLastName` variable is not affected.

### Objects



```javascript
const jane = {
  firstName: 'Jane',
  lastName: 'Williams',
  age: 27,
};

const marriedJane = jane;

marriedJane.lastName = 'Davis';

console.log('Before marriage:', jane); // Before marriage: {firstName: "Jane", lastName: "Davis", age: 27}
console.log('After marriage:', marriedJane); // After marriage: {firstName: "Jane", lastName: "Davis", age: 27}
```

In the code above, we can see that the `marriedJane` object is a reference to the `jane` object, and when we change the `lastName` property of the `marriedJane` object, we are also changing the `lastName` property of the `jane` object.

In details: It didn't create a new object in the heap, it just created a new variable that points to the same object in the stack that holds the reference to the object in the heap. In the stack, they both hold the same reference to the object in the heap. Whenever we change the object in the heap, both objects will be affected. This is the reason why we can't change the `marriedJane` object, which is declared as a `const`, and as we know, `const` variables can't be changed. However, what needs to be constant is the value in the stack, and in this case, it is the reference to the object in the heap, which we aren't changing, but the object in the heap itself. It doesn't have to do anything with the `const` keyword, it is just how objects work. What we can't do is to assign a completely different object to the `marriedJane` variable, for example if we do:

```javascript
marriedJane = {}; // Uncaught TypeError: Assignment to constant variable.
```

We are trying to assign a completely different object to the `marriedJane` variable, which is declared as a `const`, and as we know, `const` variables can't be changed.

What if we wanted to copy the object, so that we could change one of them without changing the other one? We can do that by using the `Object.assign()` method.

```javascript
const jane = {
  firstName: 'Jane',
  lastName: 'Williams',
  age: 27,
};

const marriedJane = Object.assign({}, jane);

marriedJane.lastName = 'Davis';

console.log('Before marriage:', jane); // Before marriage: {firstName: "Jane", lastName: "Williams", age: 27}
console.log('After marriage:', marriedJane); // After marriage: {firstName: "Jane", lastName: "Davis", age: 27}
```

In the code above, we can see that the `marriedJane` object is a copy of the `jane` object, and when we change the `lastName` property of the `marriedJane` object, we are not changing the `lastName` property of the `jane` object.

In detail: It created a new object in the heap, and it created a new variable that points to the new object in the stack. In the stack, they both hold a different reference to the object in the heap. Whenever we change the object in the heap, only the object that we changed will be affected. However, there is still a problem, because using this technique of `Object.assign()` will only work for the first level of the object, if we have an object inside the object, then the inner object will still be the same, it will point to the same place in memory, it only creates a shallow copy, not a deep clone of the object.
To put it into an example:

```javascript
const jane = {
  firstName: 'Jane',
  lastName: 'Williams',
  age: 27,
  family: ['Bob', 'Emily', 'John'],
};

const marriedJane = Object.assign({}, jane);

marriedJane.lastName = 'Davis';
marriedJane.family.push('Mary');

console.log('Before marriage:', jane); // Before marriage: {firstName: "Jane", lastName: "Williams", age: 27, family: Array(4)}
console.log('After marriage:', marriedJane); // After marriage: {firstName: "Jane", lastName: "Davis", age: 27, family: Array(4)}
```

In the code above, we can see that the `marriedJane` object is a copy of the `jane` object, and when we change the `lastName` property of the `marriedJane` object, we are not changing the `lastName` property of the `jane` object. However, when we change the `family` property of the `marriedJane` object, we are also changing the `family` property of the `jane` object, which is a deeply nested object, the `Object.assign()` did not really behind the scenes copy it to the new object. In essence, both the object's `family` property are pointing to the same place in memory, and when we change one of them, we are also changing the other one. A deep clone is what would be needed in this case, and there are many ways to do that, but the most common ways are:

- Using the `JSON.parse()` and `JSON.stringify()` methods.
- Using the `lodash` library.

They will be explained way down below.

# 📂 JavaScript Functions - Complete Guide

![05 JavaScript Functions](https://img.shields.io/badge/JavaScript_Functions-f7df1e?style=for-the-badge&logo=javascript&logoColor=black)

![Function Basics](https://img.shields.io/badge/Function-Basics-blue?style=for-the-badge)

![Advanced Concepts](https://img.shields.io/badge/Advanced-Concepts-purple?style=for-the-badge)

![Higher Order Functions](https://img.shields.io/badge/Higher_Order-Functions-success?style=for-the-badge)

***

## 📚 Table of Contents

- [🌟 What are Functions?](#-what-are-functions)
- [📝 Function Declarations](#-function-declarations)
- [🔧 Function Expressions](#-function-expressions)
- [➡️ Arrow Functions](#️-arrow-functions)
- [📦 Parameters and Arguments](#-parameters-and-arguments)
- [⚙️ Default Parameters](#️-default-parameters)
- [🔄 Rest Parameters](#-rest-parameters)
- [📤 Spread Operator](#-spread-operator)
- [🎯 Higher-Order Functions](#-higher-order-functions)
- [🔁 Callbacks](#-callbacks)
- [⚡ IIFE (Immediately Invoked Function Expressions)](#-iife-immediately-invoked-function-expressions)
- [✅ Best Practices](#-best-practices)
- [📝 Summary](#-summary)
- [💻 Code Examples Summary](#-code-examples-summary)
- [🔗 References](#-references)

***

## 🌟 What are Functions?

**Functions** are reusable blocks of code designed to perform specific tasks [web:3][web:7]. They are fundamental building blocks in JavaScript that help organize code, avoid repetition, and make programs more modular and maintainable [web:8]. Functions can accept inputs (parameters), process data, and return outputs (results) [web:21].

### 🎯 Key Features

- **Reusability**: Write once, use multiple times
- **Modularity**: Break complex problems into smaller, manageable pieces
- **First-class citizens**: Can be assigned to variables, passed as arguments, and returned from other functions [web:8]
- **Scope isolation**: Create private variables and prevent global namespace pollution [web:13]
- **Multiple syntax options**: Declarations, expressions, and arrow functions [web:3][web:7]

### 🏗️ Function Architecture

```
┌────────────────────────────────────────────────────────────┐
│                    JavaScript Functions                    │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  ┌─────────────────────┐      ┌─────────────────────┐      │
│  │   Function Types    │      │   Function Features │      │
│  ├─────────────────────┤      ├─────────────────────┤      │
│  │ • Declarations      │      │ • Parameters        │      │
│  │ • Expressions       │      │ • Return Values     │      │
│  │ • Arrow Functions   │      │ • Closures          │      │
│  │ • IIFE              │      │ • Hoisting          │      │
│  │ • Anonymous         │      │ • Scope             │      │
│  └─────────┬───────────┘      └─────────┬───────────┘      │
│            │                            │                  │
│            └────────────┬───────────────┘                  │
│                         │                                  │
│              ┌──────────▼───────────┐                      │
│              │   Function Execution │                      │
│              │   • Call             │                      │
│              │   • Apply            │                      │
│              │   • Bind             │                      │
│              └──────────────────────┘                      │
└────────────────────────────────────────────────────────────┘
```

***

## 📝 Function Declarations

**Function declarations** define named functions using the `function` keyword [web:19]. They are hoisted to the top of their scope, meaning they can be called before they are defined in the code [web:19][web:22].

### 🔍 Syntax and Structure

```javascript
// Basic syntax
function functionName(parameters) {
    // Function body
    return value;
}
```

### 💻 Code Examples

```javascript
// Example 1: Simple function declaration
function greet() {
    console.log('Hello, World!');
}
greet(); // Output: Hello, World!

// Example 2: Function with parameters
function add(a, b) {
    return a + b; // Returns the sum of a and b
}
const result = add(5, 3); // Call function with arguments 5 and 3
console.log(result); // Output: 8

// Example 3: Function with multiple operations
function calculateArea(length, width) {
    const area = length * width; // Calculate area
    console.log(`Area: ${area}`); // Log the result
    return area; // Return the calculated value
}
calculateArea(10, 5); // Output: Area: 50

// Example 4: Hoisting demonstration
sayHello(); // ✅ Works! Function declarations are hoisted
function sayHello() {
    console.log('Hello from hoisted function!');
}
// Output: Hello from hoisted function!

// Example 5: Function with conditional logic
function isEven(number) {
    if (number % 2 === 0) { // Check if number is divisible by 2
        return true; // Return true for even numbers
    } else {
        return false; // Return false for odd numbers
    }
}
console.log(isEven(4)); // Output: true
console.log(isEven(7)); // Output: false

// ❌ Common Mistakes:
// Mistake 1: Forgetting return statement
function multiply(x, y) {
    x * y; // Missing return - function returns undefined
}
console.log(multiply(3, 4)); // Output: undefined

// Mistake 2: Missing parameters
function divide(a, b) {
    return a / b;
}
console.log(divide(10)); // Output: NaN (b is undefined)
```

### 📊 Hoisting Behavior

| Aspect | Function Declaration | Function Expression |
|--------|---------------------|---------------------|
| **Hoisting** | ✅ Fully hoisted [web:19][web:22] | ❌ Not hoisted [web:19][web:22] |
| **Call Before Definition** | ✅ Allowed [web:22] | ❌ Throws error [web:22] |
| **Scope** | Function or global | Block scope (let/const) [web:19] |
| **Anonymous** | ❌ Must have name [web:7] | ✅ Can be anonymous [web:7] |

***

## 🔧 Function Expressions

**Function expressions** define functions as part of an expression, typically by assigning them to variables [web:7][web:19]. Unlike declarations, they are not hoisted and cannot be called before they are defined [web:19][web:22].

### 🔍 Syntax and Structure

```javascript
// Basic syntax
const functionName = function(parameters) {
    // Function body
    return value;
};
```

### 💻 Code Examples

```javascript
// Example 1: Named function expression
const greet = function sayHi() {
    console.log('Hello from function expression!');
};
greet(); // Output: Hello from function expression!

// Example 2: Anonymous function expression
const subtract = function(a, b) {
    return a - b; // Subtract b from a
};
console.log(subtract(10, 4)); // Output: 6

// Example 3: Function expression in variable
const square = function(num) {
    return num * num; // Calculate square of number
};
console.log(square(5)); // Output: 25

// Example 4: Hoisting demonstration - ERROR
// multiplyNums(3, 4); // ❌ ReferenceError: Cannot access before initialization
const multiplyNums = function(x, y) {
    return x * y;
};
console.log(multiplyNums(3, 4)); // ✅ Output: 12

// Example 5: Function expression as callback
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(function(num) {
    return num * 2; // Double each number
});
console.log(doubled); // Output: [2, 4, 6, 8, 10]

// Example 6: Conditional function assignment
const userRole = 'admin';
const getPermissions = userRole === 'admin' 
    ? function() { return 'Full access'; } // Admin permissions
    : function() { return 'Limited access'; }; // User permissions
console.log(getPermissions()); // Output: Full access
```

### 🔄 Declaration vs Expression Comparison

```
┌──────────────────────────────────────────────────────────┐
│              Function Declaration                        │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  function myFunc() {                                     │
│      return "I am hoisted!";                             │
│  }                                                       │
│                                                          │
│  ✅ Hoisted to top                                       │
│  ✅ Can call before definition                           │
│  ✅ Must have a name                                     │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│              Function Expression                         │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  const myFunc = function() {                             │
│      return "I am not hoisted!";                         │
│  };                                                      │
│                                                          │
│  ❌ Not hoisted                                          │
│  ❌ Cannot call before definition                        │
│  ✅ Can be anonymous                                     │
└──────────────────────────────────────────────────────────┘
```

***

## ➡️ Arrow Functions

**Arrow functions** provide a concise syntax for writing function expressions using the `=>` arrow notation [web:3][web:5]. They were introduced in ES6 and offer shorter syntax while having different behavior with the `this` keyword [web:3][web:7].

### 🔍 Syntax Variations

```javascript
// Basic syntax forms
() => expression                    // No parameters
param => expression                 // Single parameter (no parentheses needed)
(param) => expression              // Single parameter (with parentheses)
(param1, param2) => expression     // Multiple parameters
() => { statements }               // Multiple statements (requires return)
```

### 💻 Code Examples

```javascript
// Example 1: Basic arrow function
const greet = () => {
    console.log('Hello from arrow function!');
};
greet(); // Output: Hello from arrow function!

// Example 2: Single parameter (no parentheses)
const square = num => num * num; // Implicit return for single expression
console.log(square(4)); // Output: 16

// Example 3: Multiple parameters
const add = (a, b) => a + b; // Implicit return
console.log(add(5, 3)); // Output: 8

// Example 4: Multiple statements (explicit return)
const calculateDiscount = (price, discount) => {
    const discountAmount = price * (discount / 100); // Calculate discount
    const finalPrice = price - discountAmount; // Subtract discount
    return finalPrice; // Explicit return required with braces
};
console.log(calculateDiscount(100, 20)); // Output: 80

// Example 5: Returning objects (requires parentheses)
const createUser = (name, age) => ({
    name: name, // Object property
    age: age,   // Object property
    isActive: true // Default property
});
console.log(createUser('Alice', 25)); 
// Output: { name: 'Alice', age: 25, isActive: true }

// Example 6: Arrow function with array methods
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2); // Concise syntax
console.log(doubled); // Output: [2, 4, 6, 8, 10]

// Example 7: Filtering with arrow function
const evenNumbers = numbers.filter(n => n % 2 === 0); // Keep even numbers
console.log(evenNumbers); // Output: [2, 4]

// Example 8: IIFE with arrow function
(() => {
    console.log('Immediately invoked arrow function!');
})();
// Output: Immediately invoked arrow function!

// ❌ Common Mistakes:
// Mistake 1: Forgetting return with curly braces
const multiply = (a, b) => {
    a * b; // Missing return statement
};
console.log(multiply(3, 4)); // Output: undefined

// Mistake 2: Incorrect object return
const makeObj = () => { name: 'John' }; // ❌ Treated as code block
console.log(makeObj()); // Output: undefined
// ✅ Correct way:
const makeObjCorrect = () => ({ name: 'John' });
console.log(makeObjCorrect()); // Output: { name: 'John' }

// Mistake 3: Arrow functions are not hoisted
// sayHi(); // ❌ ReferenceError
const sayHi = () => console.log('Hi');
```

### 📊 Arrow Function Syntax Comparison

| Parameters | Syntax | Example | Output |
|------------|--------|---------|--------|
| **None** | `() => expression` | `() => 'Hello'` | Returns "Hello" |
| **One** | `param => expression` | `x => x * 2` | Doubles input |
| **One (parentheses)** | `(param) => expression` | `(x) => x * 2` | Doubles input |
| **Multiple** | `(p1, p2) => expression` | `(x, y) => x + y` | Sums inputs |
| **Block body** | `() => { statements }` | `() => { return 1; }` | Returns 1 |

### 🔄 Traditional vs Arrow Function

```
┌──────────────────────────────────────────────────────────┐
│            Traditional Function Expression               │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  const add = function(a, b) {                            │
│      return a + b;                                       │
│  };                                                      │
│                                                          │
│  ✅ Can use 'this' binding                               │
│  ✅ Can be constructor                                   │
│  ✅ Has arguments object                                 │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│                Arrow Function (ES6)                      │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  const add = (a, b) => a + b;                            │
│                                                          │
│  ✅ Shorter syntax                                       │
│  ✅ Implicit return                                      │
│  ✅ Lexical 'this' binding                               │
│  ❌ Cannot be constructor                                │
│  ❌ No arguments object                                  │
└──────────────────────────────────────────────────────────┘
```

***

## 📦 Parameters and Arguments

**Parameters** are variables listed in the function definition, while **arguments** are the actual values passed to the function when it is called [web:21]. Understanding the distinction is crucial for effective function design [web:21].

### 🔍 Key Concepts

```javascript
// Parameters are defined in function signature
function exampleFunc(param1, param2) { // param1, param2 are parameters
    return param1 + param2;
}

// Arguments are passed when calling the function
exampleFunc(5, 10); // 5, 10 are arguments
```

### 💻 Code Examples

```javascript
// Example 1: Basic parameters and arguments
function introduce(name, age) { // name, age are parameters
    console.log(`My name is ${name} and I am ${age} years old.`);
}
introduce('Alice', 25); // 'Alice', 25 are arguments
// Output: My name is Alice and I am 25 years old.

// Example 2: Too few arguments (undefined parameters)
function greet(firstName, lastName) {
    console.log(`Hello ${firstName} ${lastName}`);
}
greet('John'); // lastName is undefined
// Output: Hello John undefined

// Example 3: Too many arguments (extras ignored)
function add(a, b) {
    return a + b; // Only uses first two arguments
}
console.log(add(1, 2, 3, 4, 5)); // Extra arguments 3, 4, 5 are ignored
// Output: 3

// Example 4: Using the arguments object (traditional functions)
function sum() {
    let total = 0; // Initialize total
    for (let i = 0; i < arguments.length; i++) { // Loop through arguments
        total += arguments[i]; // Add each argument to total
    }
    return total;
}
console.log(sum(1, 2, 3, 4, 5)); // Output: 15
console.log(sum(10, 20)); // Output: 30

// Example 5: Arguments object is array-like (not real array)
function showArguments() {
    console.log(typeof arguments); // Output: object
    console.log(Array.isArray(arguments)); // Output: false

    // Convert to real array
    const argsArray = Array.from(arguments);
    console.log(Array.isArray(argsArray)); // Output: true
}
showArguments(1, 2, 3);

// Example 6: Arrow functions don't have arguments object
const arrowSum = () => {
    console.log(arguments); // ❌ ReferenceError: arguments is not defined
};
// arrowSum(1, 2, 3); // This will throw error

// Example 7: Primitive vs Reference parameters
function modifyPrimitive(num) {
    num = 100; // Changes local copy only
    console.log(`Inside function: ${num}`); // Output: Inside function: 100
}
let x = 50;
modifyPrimitive(x);
console.log(`Outside function: ${x}`); // Output: Outside function: 50

function modifyObject(obj) {
    obj.name = 'Changed'; // Modifies original object
    console.log(`Inside function: ${obj.name}`); // Output: Inside function: Changed
}
let person = { name: 'Original' };
modifyObject(person);
console.log(`Outside function: ${person.name}`); // Output: Outside function: Changed
```

### 📊 Parameters vs Arguments

| Aspect | Parameters | Arguments |
|--------|-----------|-----------|
| **Definition** | Variables in function declaration [web:21] | Actual values passed to function [web:21] |
| **Location** | Function signature | Function call |
| **Purpose** | Define what function expects | Provide actual data |
| **Count** | Fixed (defined once) | Variable (can differ per call) |
| **Example** | `function(a, b)` | `myFunc(5, 10)` |

***

## ⚙️ Default Parameters

**Default parameters** allow you to initialize function parameters with default values if no argument is provided or if `undefined` is passed [web:18][web:21]. This feature was introduced in ES6 and prevents errors from missing arguments [web:18].

### 🔍 Syntax

```javascript
// Basic syntax
function functionName(param1 = defaultValue1, param2 = defaultValue2) {
    // Function body
}
```

### 💻 Code Examples

```javascript
// Example 1: Basic default parameter
function greet(name = 'Guest') { // Default value 'Guest' if no argument
    console.log(`Hello, ${name}!`);
}
greet(); // Output: Hello, Guest!
greet('Alice'); // Output: Hello, Alice!

// Example 2: Multiple default parameters
function calculatePrice(price = 0, tax = 0.1, discount = 0) {
    const taxAmount = price * tax; // Calculate tax
    const finalPrice = price + taxAmount - discount; // Calculate final price
    return finalPrice;
}
console.log(calculatePrice()); // Output: 0 (all defaults)
console.log(calculatePrice(100)); // Output: 110 (price=100, tax=0.1, discount=0)
console.log(calculatePrice(100, 0.15)); // Output: 115 (custom tax)
console.log(calculatePrice(100, 0.1, 20)); // Output: 90 (all custom)

// Example 3: Default parameter with expressions
function createUser(name = 'Anonymous', id = Date.now()) {
    return { // Return user object
        name: name,
        id: id, // Default is current timestamp
        created: new Date()
    };
}
console.log(createUser()); 
// Output: { name: 'Anonymous', id: 1705123456789, created: 2026-01-12T... }
console.log(createUser('John'));
// Output: { name: 'John', id: 1705123456790, created: 2026-01-12T... }

// Example 4: Using undefined triggers default
function showMessage(msg = 'Default message') {
    console.log(msg);
}
showMessage(undefined); // Output: Default message (undefined triggers default)
showMessage(null); // Output: null (null does NOT trigger default)
showMessage(''); // Output: (empty string, does NOT trigger default)

// Example 5: Default parameters referencing other parameters
function buildUrl(protocol = 'https', domain, path = '/') {
    return `${protocol}://${domain}${path}`; // Construct URL
}
console.log(buildUrl(undefined, 'example.com')); 
// Output: https://example.com/
console.log(buildUrl('http', 'example.com', '/about'));
// Output: http://example.com/about

// Example 6: Function as default parameter
function getDefaultName() {
    return 'Default User'; // Function to generate default
}
function register(username = getDefaultName()) {
    console.log(`Registered: ${username}`);
}
register(); // Output: Registered: Default User
register('Alice'); // Output: Registered: Alice

// Example 7: Required parameters using default
function requiredParam() {
    throw new Error('Missing required parameter!'); // Throw error
}
function createAccount(username = requiredParam(), email = requiredParam()) {
    return { username, email }; // Create account object
}
console.log(createAccount('john', 'john@example.com')); 
// Output: { username: 'john', email: 'john@example.com' }
// createAccount(); // ❌ Error: Missing required parameter!
// createAccount('john'); // ❌ Error: Missing required parameter!

// Example 8: Default parameters with arrow functions
const multiply = (a = 1, b = 1) => a * b; // Default both to 1
console.log(multiply()); // Output: 1
console.log(multiply(5)); // Output: 5
console.log(multiply(5, 3)); // Output: 15

// ❌ Common Mistakes:
// Mistake 1: Using non-undefined falsy values
function test(value = 'default') {
    console.log(value);
}
test(0); // Output: 0 (not 'default' - 0 doesn't trigger default)
test(false); // Output: false (not 'default')
test(''); // Output: (empty string, not 'default')
```

### 📊 Default Parameter Behavior

| Value Passed | Uses Default? | Example |
|-------------|---------------|---------|
| **Nothing (omitted)** | ✅ Yes [web:21] | `func()` |
| **undefined** | ✅ Yes [web:21] | `func(undefined)` |
| **null** | ❌ No [web:21] | `func(null)` |
| **0** | ❌ No | `func(0)` |
| **false** | ❌ No | `func(false)` |
| **Empty string** | ❌ No | `func('')` |

***

## 🔄 Rest Parameters

**Rest parameters** allow you to represent an indefinite number of arguments as an array [web:9]. They are denoted by three dots (`...`) followed by a parameter name and must be the last parameter in the function signature [web:9].

### 🔍 Syntax

```javascript
// Basic syntax
function functionName(param1, param2, ...restParams) {
    // restParams is an array of remaining arguments
}
```

### 💻 Code Examples

```javascript
// Example 1: Basic rest parameters
function sum(...numbers) { // Collect all arguments into numbers array
    let total = 0; // Initialize total
    for (let num of numbers) { // Loop through array
        total += num; // Add each number
    }
    return total;
}
console.log(sum(1, 2, 3)); // Output: 6
console.log(sum(1, 2, 3, 4, 5)); // Output: 15
console.log(sum()); // Output: 0 (empty array)

// Example 2: Rest parameters with other parameters
function introduce(firstName, lastName, ...hobbies) {
    console.log(`Name: ${firstName} ${lastName}`);
    console.log(`Hobbies: ${hobbies.join(', ')}`); // Join array into string
}
introduce('John', 'Doe', 'Reading', 'Gaming', 'Coding');
// Output: Name: John Doe
//         Hobbies: Reading, Gaming, Coding

// Example 3: Rest parameters are real arrays
function showType(...args) {
    console.log(Array.isArray(args)); // Check if real array
    console.log(args.length); // Array length property
    args.forEach(arg => console.log(arg)); // Use array method
}
showType(1, 2, 3);
// Output: true
//         3
//         1
//         2
//         3

// Example 4: Mathematical operations with rest
function multiply(multiplier, ...numbers) {
    return numbers.map(num => num * multiplier); // Multiply each by multiplier
}
console.log(multiply(2, 1, 2, 3, 4)); // Output: [2, 4, 6, 8]
console.log(multiply(5, 10, 20)); // Output: [50, 100]

// Example 5: Finding max with rest parameters
function findMax(...numbers) {
    if (numbers.length === 0) return undefined; // Handle empty case
    return Math.max(...numbers); // Spread array to Math.max
}
console.log(findMax(5, 2, 9, 1, 7)); // Output: 9
console.log(findMax()); // Output: undefined

// Example 6: Rest parameters with destructuring
function processData(action, ...items) {
    const [first, second, ...rest] = items; // Destructure items array
    console.log(`Action: ${action}`);
    console.log(`First: ${first}, Second: ${second}`);
    console.log(`Rest: ${rest.join(', ')}`);
}
processData('Process', 'A', 'B', 'C', 'D', 'E');
// Output: Action: Process
//         First: A, Second: B
//         Rest: C, D, E

// Example 7: Rest parameters with arrow functions
const average = (...nums) => {
    if (nums.length === 0) return 0; // Avoid division by zero
    const sum = nums.reduce((acc, num) => acc + num, 0); // Sum all numbers
    return sum / nums.length; // Calculate average
};
console.log(average(10, 20, 30, 40)); // Output: 25
console.log(average(5, 15)); // Output: 10

// ❌ Common Mistakes:
// Mistake 1: Rest parameter not last
// function wrong(a, ...rest, b) {} // ❌ SyntaxError: Rest parameter must be last

// Mistake 2: Multiple rest parameters
// function wrong(...rest1, ...rest2) {} // ❌ SyntaxError: Multiple rest parameters

// ✅ Correct usage:
function correct(a, b, ...rest) { // Rest must be last
    console.log(`a: ${a}, b: ${b}, rest: ${rest}`);
}
correct(1, 2, 3, 4, 5); // Output: a: 1, b: 2, rest: 3,4,5
```

### 📊 Rest Parameters vs Arguments Object

| Feature | Rest Parameters | Arguments Object |
|---------|----------------|------------------|
| **Type** | Real array [web:9] | Array-like object |
| **Array Methods** | ✅ Available [web:9] | ❌ Not available |
| **Arrow Functions** | ✅ Works [web:9] | ❌ Not available |
| **Named** | ✅ Descriptive name | ❌ Always 'arguments' |
| **Partial Collection** | ✅ Can collect subset [web:9] | ❌ All arguments |
| **Modern** | ✅ ES6+ [web:9] | ❌ Legacy |

***

## 📤 Spread Operator

**The spread operator** (`...`) expands an iterable (like an array) into individual elements [web:9]. While it looks identical to rest parameters, it serves the opposite purpose - expanding instead of collecting [web:9].

### 🔍 Syntax

```javascript
// Spread in function calls
functionName(...array)

// Spread in array literals
[...array1, ...array2]

// Spread in object literals
{...object1, ...object2}
```

### 💻 Code Examples

```javascript
// Example 1: Spread in function calls
function add(a, b, c) {
    return a + b + c; // Sum three numbers
}
const numbers = [1, 2, 3];
console.log(add(...numbers)); // Spread array into arguments
// Output: 6 (equivalent to add(1, 2, 3))

// Example 2: Finding max/min with spread
const nums = [5, 2, 9, 1, 7, 4];
console.log(Math.max(...nums)); // Spread array to Math.max
// Output: 9
console.log(Math.min(...nums)); // Spread array to Math.min
// Output: 1

// Example 3: Combining arrays
const fruits = ['apple', 'banana'];
const vegetables = ['carrot', 'potato'];
const food = [...fruits, ...vegetables]; // Merge arrays
console.log(food); 
// Output: ['apple', 'banana', 'carrot', 'potato']

// Example 4: Copying arrays (shallow copy)
const original = [1, 2, 3];
const copy = [...original]; // Create new array with same elements
copy.push(4); // Modify copy
console.log(original); // Output: [1, 2, 3] (unchanged)
console.log(copy); // Output: [1, 2, 3, 4]

// Example 5: Adding elements while spreading
const baseArray = [2, 3, 4];
const extendedArray = [1, ...baseArray, 5, 6]; // Add elements before/after
console.log(extendedArray); // Output: [1, 2, 3, 4, 5, 6]

// Example 6: Spreading strings
const str = 'Hello';
const chars = [...str]; // Split string into characters
console.log(chars); // Output: ['H', 'e', 'l', 'l', 'o']

// Example 7: Spread with objects (ES2018+)
const person = { name: 'John', age: 30 };
const employee = { ...person, role: 'Developer' }; // Copy and add property
console.log(employee); 
// Output: { name: 'John', age: 30, role: 'Developer' }

// Example 8: Merging objects (later properties override)
const defaults = { theme: 'light', fontSize: 14 };
const userSettings = { fontSize: 16, language: 'en' };
const finalSettings = { ...defaults, ...userSettings }; // Merge with override
console.log(finalSettings); 
// Output: { theme: 'light', fontSize: 16, language: 'en' }

// Example 9: Spread with function and rest combined
function log(first, second, ...rest) {
    console.log(`First: ${first}`);
    console.log(`Second: ${second}`);
    console.log(`Rest: ${rest.join(', ')}`);
}
const args = [1, 2, 3, 4, 5];
log(...args); // Spread array into function arguments
// Output: First: 1
//         Second: 2
//         Rest: 3, 4, 5

// Example 10: Practical use - removing duplicates
const withDuplicates = [1, 2, 2, 3, 4, 4, 5];
const unique = [...new Set(withDuplicates)]; // Spread Set back to array
console.log(unique); // Output: [1, 2, 3, 4, 5]

// ❌ Common Mistakes:
// Mistake 1: Spreading non-iterables
// const num = 123;
// const arr = [...num]; // ❌ TypeError: num is not iterable

// Mistake 2: Confusing spread with rest
const example1 = (...args) => args; // REST - collects arguments
const example2 = (arr) => [...arr]; // SPREAD - expands array
```

### 🔄 Spread vs Rest Visualization

```
┌──────────────────────────────────────────────────────────┐
│                 REST PARAMETERS                          │
│              (Collects into Array)                       │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  function sum(...numbers) {                              │
│      // numbers = [1, 2, 3, 4, 5]                        │
│  }                                                       │
│                                                          │
│  Individual Args ──► ...numbers ──► Array                │
│   (1, 2, 3, 4, 5)                    [1,2,3,4,5]         │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│                SPREAD OPERATOR                           │
│             (Expands from Array)                         │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  const nums = [1, 2, 3];                                 │
│  add(...nums);                                           │
│                                                          │
│  Array ──► ...nums ──► Individual Args                   │
│  [1,2,3]               (1, 2, 3)                         │
└──────────────────────────────────────────────────────────┘
```

### 📊 Spread Operator Use Cases

| Use Case | Example | Result |
|----------|---------|--------|
| **Function Arguments** | `Math.max(...[1,2,3])` | 3 |
| **Array Concatenation** | `[...a, ...b]` | Combined array |
| **Array Copy** | `[...original]` | Shallow copy |
| **String to Array** | `[...'hello']` | ['h','e','l','l','o'] |
| **Object Merge** | `{...obj1, ...obj2}` | Merged object |

***

## 🎯 Higher-Order Functions

**Higher-order functions** are functions that either accept other functions as arguments, return functions as results, or both [web:8][web:11]. They enable powerful functional programming patterns in JavaScript [web:8].

### 🔍 Key Concepts

Higher-order functions treat functions as first-class citizens, allowing for more abstract and reusable code patterns [web:8][web:11].

### 💻 Code Examples

```javascript
// Example 1: Function accepting another function as argument
function greet(name, formatter) {
    const formattedName = formatter(name); // Call the formatter function
    console.log(`Hello, ${formattedName}!`);
}
const uppercase = (str) => str.toUpperCase(); // Formatter function
greet('alice', uppercase); // Pass function as argument
// Output: Hello, ALICE!

// Example 2: Function returning another function
function createMultiplier(factor) {
    return function(number) { // Return a new function
        return number * factor; // Closure - remembers factor
    };
}
const double = createMultiplier(2); // Creates doubling function
const triple = createMultiplier(3); // Creates tripling function
console.log(double(5)); // Output: 10
console.log(triple(5)); // Output: 15

// Example 3: Array.map() - Built-in higher-order function
const numbers = [1, 2, 3, 4, 5];
const squared = numbers.map(function(num) {
    return num * num; // Transform each element
});
console.log(squared); // Output: [1, 4, 9, 16, 25]

// Example 4: Array.filter() - Higher-order function
const ages = [12, 18, 25, 30, 16, 21];
const adults = ages.filter(function(age) {
    return age >= 18; // Keep only adults
});
console.log(adults); // Output: [18, 25, 30, 21]

// Example 5: Array.reduce() - Higher-order function
const nums = [1, 2, 3, 4, 5];
const sum = nums.reduce(function(accumulator, current) {
    return accumulator + current; // Sum all elements
}, 0); // Initial value is 0
console.log(sum); // Output: 15

// Example 6: Custom higher-order function for array processing
function applyOperation(arr, operation) {
    const result = []; // Store results
    for (let item of arr) {
        result.push(operation(item)); // Apply operation to each item
    }
    return result;
}
const numbers2 = [1, 2, 3, 4];
const doubled = applyOperation(numbers2, x => x * 2);
const squared2 = applyOperation(numbers2, x => x * x);
console.log(doubled); // Output: [2, 4, 6, 8]
console.log(squared2); // Output: [1, 4, 9, 16]

// Example 7: Function composition
function compose(f, g) {
    return function(x) { // Return composed function
        return f(g(x)); // Apply g first, then f
    };
}
const addOne = x => x + 1;
const multiplyByTwo = x => x * 2;
const addThenMultiply = compose(multiplyByTwo, addOne);
console.log(addThenMultiply(5)); // Output: 12 ((5 + 1) * 2)

// Example 8: setTimeout and setInterval (higher-order functions)
setTimeout(function() {
    console.log('Executed after 1 second');
}, 1000); // Accepts callback function
// Output: (after 1 second) Executed after 1 second

// Example 9: Custom forEach implementation
function forEach(array, callback) {
    for (let i = 0; i < array.length; i++) {
        callback(array[i], i, array); // Call callback with item, index, array
    }
}
forEach([1, 2, 3], function(item, index) {
    console.log(`Item ${index}: ${item}`);
});
// Output: Item 0: 1
//         Item 1: 2
//         Item 2: 3

// Example 10: Practical example - user authentication
function withAuth(fn) {
    return function(...args) { // Return wrapper function
        const isAuthenticated = true; // Check authentication
        if (isAuthenticated) {
            return fn(...args); // Execute original function if authenticated
        } else {
            console.log('Access denied!');
        }
    };
}
const deleteUser = (userId) => console.log(`Deleted user ${userId}`);
const secureDeleteUser = withAuth(deleteUser); // Wrap with authentication
secureDeleteUser(123); // Output: Deleted user 123
```

### 🏗️ Higher-Order Function Architecture

```
┌────────────────────────────────────────────────────────┐
│          Higher-Order Function Patterns                │
├────────────────────────────────────────────────────────┤
│                                                        │
│  Pattern 1: Function as Argument                       │
│  ┌──────────────────────────────────────┐              │
│  │  higherOrderFunc(callback)           │              │
│  │    ↓                                 │              │
│  │  callback executed inside            │              │
│  └──────────────────────────────────────┘              │
│                                                        │
│  Pattern 2: Function Returns Function                  │
│  ┌──────────────────────────────────────┐              │
│  │  higherOrderFunc()                   │              │
│  │    ↓                                 │              │
│  │  returns new function                │              │
│  │    ↓                                 │              │
│  │  newFunc() can be called later       │              │
│  └──────────────────────────────────────┘              │
│                                                        │
│  Pattern 3: Both (Accept & Return)                     │
│  ┌──────────────────────────────────────┐              │
│  │  higherOrderFunc(callback)           │              │
│  │    ↓                                 │              │
│  │  processes callback                  │              │
│  │    ↓                                 │              │
│  │  returns enhanced function           │              │
│  └──────────────────────────────────────┘              │
└────────────────────────────────────────────────────────┘
```

### 📊 Common Higher-Order Functions

| Function | Purpose | Example | Result |
|----------|---------|---------|--------|
| **map()** | Transform elements [web:11] | `[1,2].map(x => x*2)` | [2, 4] |
| **filter()** | Select elements [web:11] | `[1,2,3].filter(x => x>1)` | [2, 3] |
| **reduce()** | Accumulate value [web:11] | `[1,2,3].reduce((a,b) => a+b)` | 6 |
| **forEach()** | Iterate elements [web:11] | `[1,2].forEach(console.log)` | Logs items |
| **setTimeout()** | Delayed execution [web:8] | `setTimeout(fn, 1000)` | Calls fn after 1s |

***

## 🔁 Callbacks

**Callbacks** are functions passed as arguments to other functions and executed later [web:8]. They are fundamental to JavaScript's asynchronous programming model and event handling [web:8].

### 🔍 Key Concepts

Callbacks allow you to define what should happen after an operation completes, making them essential for handling asynchronous tasks [web:8].

### 💻 Code Examples

```javascript
// Example 1: Simple callback
function processData(data, callback) {
    console.log('Processing data...');
    const result = data.toUpperCase(); // Process data
    callback(result); // Execute callback with result
}
processData('hello', function(result) {
    console.log(`Result: ${result}`);
});
// Output: Processing data...
//         Result: HELLO

// Example 2: Callback with array methods
const numbers = [1, 2, 3, 4, 5];
numbers.forEach(function(number, index) { // Callback for each element
    console.log(`Index ${index}: ${number * 2}`);
});
// Output: Index 0: 2
//         Index 1: 4
//         Index 2: 6
//         Index 3: 8
//         Index 4: 10

// Example 3: Asynchronous callback with setTimeout
function fetchData(callback) {
    console.log('Fetching data...');
    setTimeout(function() { // Simulate async operation
        const data = { id: 1, name: 'Product' };
        callback(data); // Execute callback when done
    }, 2000);
}
fetchData(function(data) {
    console.log('Data received:', data);
});
// Output: Fetching data...
//         (after 2 seconds) Data received: { id: 1, name: 'Product' }

// Example 4: Error-first callback pattern (Node.js style)
function readFile(filename, callback) {
    setTimeout(function() {
        if (filename === 'valid.txt') {
            callback(null, 'File contents here'); // Success: error=null, data provided
        } else {
            callback(new Error('File not found'), null); // Error: error provided, data=null
        }
    }, 1000);
}
readFile('valid.txt', function(error, data) {
    if (error) {
        console.log('Error:', error.message);
    } else {
        console.log('Data:', data);
    }
});
// Output: Data: File contents here

// Example 5: Callback for event handling
function addEventListener(event, callback) {
    console.log(`Listening for ${event} event...`);
    // Simulate event trigger
    setTimeout(function() {
        callback({ type: event, timestamp: Date.now() }); // Call with event data
    }, 1000);
}
addEventListener('click', function(eventData) {
    console.log(`Event ${eventData.type} triggered at ${eventData.timestamp}`);
});
// Output: Listening for click event...
//         (after 1 second) Event click triggered at 1705123456789

// Example 6: Multiple callbacks (success and error)
function performOperation(shouldSucceed, onSuccess, onError) {
    setTimeout(function() {
        if (shouldSucceed) {
            onSuccess('Operation successful!'); // Call success callback
        } else {
            onError('Operation failed!'); // Call error callback
        }
    }, 1000);
}
performOperation(
    true,
    function(message) { console.log('Success:', message); },
    function(message) { console.log('Error:', message); }
);
// Output: Success: Operation successful!

// Example 7: Callback hell (pyramid of doom) - AVOID THIS
function step1(callback) {
    setTimeout(() => callback('Step 1 done'), 500);
}
function step2(callback) {
    setTimeout(() => callback('Step 2 done'), 500);
}
function step3(callback) {
    setTimeout(() => callback('Step 3 done'), 500);
}
// ❌ Nested callbacks - hard to read and maintain
step1(function(result1) {
    console.log(result1);
    step2(function(result2) {
        console.log(result2);
        step3(function(result3) {
            console.log(result3);
        });
    });
});
// Output: Step 1 done
//         Step 2 done
//         Step 3 done

// Example 8: Custom filter with callback
function customFilter(array, testCallback) {
    const filtered = []; // Store matching elements
    for (let item of array) {
        if (testCallback(item)) { // Test each item with callback
            filtered.push(item);
        }
    }
    return filtered;
}
const nums = [1, 2, 3, 4, 5, 6];
const evens = customFilter(nums, function(num) {
    return num % 2 === 0; // Callback tests if even
});
console.log(evens); // Output: [2, 4, 6]

// Example 9: Named vs anonymous callbacks
// Named callback (better for debugging)
function handleSuccess(data) {
    console.log('Success:', data);
}
processData('test', handleSuccess); // Named function reference

// Anonymous callback
processData('test', function(data) { // Anonymous function
    console.log('Success:', data);
});

// Example 10: Arrow function callbacks (modern syntax)
const items = [1, 2, 3, 4, 5];
const doubled = items.map(item => item * 2); // Arrow callback
console.log(doubled); // Output: [2, 4, 6, 8, 10]

items.forEach((item, index) => { // Arrow callback with multiple params
    console.log(`Item ${index}: ${item}`);
});
```

### 🔄 Callback Flow Diagram

```
┌────────────────────────────────────────────────────────┐
│              Callback Execution Flow                   │
├────────────────────────────────────────────────────────┤
│                                                        │
│  Step 1: Define callback function                      │
│  ┌──────────────────────────────────┐                  │
│  │  function myCallback(result) {   │                  │
│  │      console.log(result);        │                  │
│  │  }                               │                  │
│  └──────────────────────────────────┘                  │
│                  ↓                                     │
│  Step 2: Pass callback to higher-order function        │
│  ┌──────────────────────────────────┐                  │
│  │  processData(data, myCallback);  │                  │
│  └──────────────────────────────────┘                  │
│                  ↓                                     │
│  Step 3: Higher-order function processes               │
│  ┌──────────────────────────────────┐                  │
│  │  function processData(d, cb) {   │                  │
│  │      const result = transform(d);│                  │
│  │      cb(result); // Execute      │                  │
│  │  }                               │                  │
│  └──────────────────────────────────┘                  │
│                  ↓                                     │
│  Step 4: Callback executes with result                 │
│  ┌──────────────────────────────────┐                  │
│  │  console.log(result);            │                  │
│  └──────────────────────────────────┘                  │
└────────────────────────────────────────────────────────┘
```

### 📊 Callback Types

| Type | Description | Example |
|------|-------------|---------|
| **Synchronous** | Executes immediately [web:8] | `array.forEach(callback)` |
| **Asynchronous** | Executes later [web:8] | `setTimeout(callback, 1000)` |
| **Error-first** | First param is error [web:8] | `fs.readFile(file, callback)` |
| **Event handler** | Responds to events | `button.addEventListener('click', callback)` |

***

## ⚡ IIFE (Immediately Invoked Function Expressions)

**IIFE** (Immediately Invoked Function Expression) is a function that executes immediately after it's defined [web:13][web:14]. IIFEs are wrapped in parentheses and invoked with `()` at the end [web:13][web:14][web:17].

### 🔍 Syntax

```javascript
// Standard IIFE syntax
(function() {
    // Code executes immediately
})();

// Arrow function IIFE
(() => {
    // Code executes immediately
})();

// IIFE with parameters
(function(param) {
    // Use param
})(argument);
```

### 💻 Code Examples

```javascript
// Example 1: Basic IIFE
(function() {
    console.log('This runs immediately!');
})();
// Output: This runs immediately!

// Example 2: IIFE with arrow function
(() => {
    console.log('Arrow IIFE executed!');
})();
// Output: Arrow IIFE executed!

// Example 3: IIFE with parameters
(function(name) {
    console.log(`Hello, ${name}!`); // Use passed parameter
})('Alice');
// Output: Hello, Alice!

// Example 4: IIFE with return value
const result = (function(a, b) {
    return a + b; // Calculate and return
})(5, 3);
console.log(result); // Output: 8

// Example 5: IIFE for private variables (avoid global pollution)
(function() {
    const privateVar = 'I am private'; // Not accessible outside
    let counter = 0; // Private counter

    function increment() {
        counter++;
        console.log(`Counter: ${counter}`);
    }

    increment(); // Output: Counter: 1
    increment(); // Output: Counter: 2
})();
// console.log(privateVar); // ❌ ReferenceError: privateVar is not defined

// Example 6: Module pattern with IIFE
const calculator = (function() {
    let result = 0; // Private variable

    return { // Return public API
        add: function(x) {
            result += x;
            return this; // Allow chaining
        },
        subtract: function(x) {
            result -= x;
            return this;
        },
        getResult: function() {
            return result;
        }
    };
})();
calculator.add(10).add(5).subtract(3);
console.log(calculator.getResult()); // Output: 12
// console.log(result); // ❌ ReferenceError: result is not defined

// Example 7: IIFE for initialization code
const app = (function() {
    // Initialization code runs once
    console.log('App initializing...');
    const config = { theme: 'dark', version: '1.0' }; // Setup config
    console.log('Config loaded:', config);

    return {
        getConfig: () => config // Expose only what's needed
    };
})();
// Output: App initializing...
//         Config loaded: { theme: 'dark', version: '1.0' }

// Example 8: IIFE with named function (for debugging)
(function myIIFE() {
    console.log('Named IIFE - easier to debug');
    // Function name appears in stack traces
})();
// Output: Named IIFE - easier to debug

// Example 9: IIFE for loop variable isolation (ES5 pattern)
for (var i = 0; i < 3; i++) {
    (function(index) { // IIFE creates new scope for each iteration
        setTimeout(function() {
            console.log(`Iteration ${index}`);
        }, index * 1000);
    })(i); // Pass i as argument
}
// Output: Iteration 0 (immediately)
//         Iteration 1 (after 1s)
//         Iteration 2 (after 2s)

// Example 10: Alternative IIFE syntaxes
// Style 1: Parentheses around entire expression (most common)
(function() { console.log('Style 1'); })();

// Style 2: Parentheses around function only
(function() { console.log('Style 2'); }());

// Style 3: Unary operators (less common)
!function() { console.log('Style 3'); }();
+function() { console.log('Style 4'); }();
void function() { console.log('Style 5'); }();

// Example 11: IIFE with async/await (modern)
(async () => {
    console.log('Start async operation');
    // Simulate async operation
    await new Promise(resolve => setTimeout(resolve, 1000));
    console.log('Async operation complete');
})();
// Output: Start async operation
//         (after 1 second) Async operation complete

// ❌ Common Mistakes:
// Mistake 1: Missing parentheses
// function() { console.log('Error'); }(); // ❌ SyntaxError

// Mistake 2: Trying to call IIFE again
const iife = (function() {
    return 'I run once';
})();
console.log(iife); // Output: "I run once" (it's the return value, not function)
// iife(); // ❌ TypeError: iife is not a function
```

### 🏗️ IIFE Structure Diagram

```
┌────────────────────────────────────────────────────────┐
│              IIFE Anatomy                              │
├────────────────────────────────────────────────────────┤
│                                                        │
│  (function() {        })();                            │
│   │        │          │ │                              │
│   │        │          │ └─ Invoking parentheses        │
│   │        │          └─── Closing parenthesis         │
│   │        └───────────── Function body                │
│   └────────────────────── Opening parenthesis          │
│                           (makes it expression)        │
│                                                        │
│  ┌─────────────────────────────────────┐               │
│  │  Step 1: Wrap function in ( )       │               │
│  │  (function() { ... })               │               │
│  └──────────┬──────────────────────────┘               │
│             ↓                                          │
│  ┌─────────────────────────────────────┐               │
│  │  Step 2: Add () to invoke           │               │
│  │  (function() { ... })()             │               │
│  └──────────┬──────────────────────────┘               │
│             ↓                                          │
│  ┌─────────────────────────────────────┐               │
│  │  Step 3: Executes immediately       │               │
│  │  Code runs, then function discarded │               │
│  └─────────────────────────────────────┘               │
└────────────────────────────────────────────────────────┘
```

### 📊 IIFE Benefits

| Benefit | Description | Use Case |
|---------|-------------|----------|
| **Avoid Global Pollution** | Variables stay private [web:13][web:17] | Module initialization |
| **Create Private Scope** | Encapsulate variables [web:13] | Data privacy |
| **Execute Immediately** | No need to call separately [web:14] | One-time setup |
| **Module Pattern** | Create public/private members [web:13] | Library design |
| **Variable Isolation** | Each invocation has own scope | Loop callbacks (ES5) |

***

## ✅ Best Practices

Following best practices ensures your JavaScript functions are efficient, maintainable, and easy to understand.

### 🎯 Function Design

- **Single Responsibility**: Each function should do one thing well and have a clear purpose
- **Descriptive Names**: Use verb-based names that describe what the function does (e.g., `calculateTotal`, `fetchUserData`)
- **Keep Functions Small**: Aim for functions that fit on one screen (typically 20-30 lines max)
- **Limit Parameters**: Use 3 or fewer parameters when possible; consider an options object for more
- **Return Early**: Use early returns to avoid deep nesting and improve readability

### 📝 Parameter Handling

- **Use Default Parameters**: Provide sensible defaults instead of checking for `undefined` [web:18][web:21]
- **Use Rest Parameters**: Prefer rest parameters over the `arguments` object [web:9]
- **Validate Inputs**: Check parameter types and values at the start of functions
- **Document Parameters**: Use JSDoc comments to describe expected parameter types and values
- **Avoid Mutating Parameters**: Don't modify objects passed as parameters unless intended

### ➡️ Arrow Functions

- **Use for Callbacks**: Arrow functions are perfect for short callback functions [web:3][web:5]
- **Avoid for Methods**: Don't use arrow functions as object methods (they don't bind `this`)
- **Implicit Return**: Use implicit returns for single expressions to keep code concise [web:5]
- **Parentheses for Objects**: Wrap object literals in parentheses when using implicit return [web:3]
- **Named Functions for Recursion**: Use named function expressions for recursive functions

### 🔁 Callbacks and Higher-Order Functions

- **Avoid Callback Hell**: Use Promises or async/await instead of deeply nested callbacks [web:8]
- **Use Named Callbacks**: Named functions are easier to debug than anonymous functions
- **Error Handling**: Always handle errors in asynchronous callbacks [web:8]
- **Use Built-in Methods**: Prefer `map`, `filter`, `reduce` over manual loops when appropriate [web:11]
- **Pure Functions**: Create functions without side effects when possible

### ⚡ IIFE Usage

- **Module Pattern**: Use IIFEs to create modules with private variables [web:13][web:17]
- **Avoid Global Variables**: Wrap code in IIFEs to prevent global namespace pollution [web:13]
- **Modern Alternative**: Consider ES6 modules instead of IIFEs for new projects [web:14]
- **Initialization Code**: Use IIFEs for one-time initialization that shouldn't run again [web:17]
- **Arrow IIFEs**: Use arrow function IIFEs for cleaner syntax in modern code [web:14]

### 🔧 General Guidelines

- **Use `const` for Functions**: Declare function expressions with `const` to prevent reassignment
- **Consistent Style**: Choose either function declarations or expressions and be consistent
- **Comment Complex Logic**: Explain why, not what - the code shows what
- **Test Edge Cases**: Always test with empty inputs, null, undefined, and boundary values
- **Performance Considerations**: Avoid creating functions inside loops unnecessarily

***

## 📝 Summary

- Functions are reusable blocks of code that can accept parameters and return values [web:3][web:7]
- **Function declarations** are hoisted and can be called before definition [web:19][web:22]
- **Function expressions** are not hoisted and must be defined before use [web:19][web:22]
- **Arrow functions** provide concise syntax with implicit returns and lexical `this` binding [web:3][web:5]
- **Parameters** are defined in function signatures while **arguments** are passed during calls [web:21]
- **Default parameters** provide fallback values when arguments are missing or undefined [web:18][web:21]
- **Rest parameters** collect multiple arguments into an array using `...` syntax [web:9]
- **Spread operator** expands arrays/objects into individual elements [web:9]
- **Higher-order functions** accept functions as arguments or return functions as results [web:8][web:11]
- **Callbacks** are functions passed to other functions for later execution [web:8]
- **IIFE** executes immediately upon definition, creating private scope and avoiding global pollution [web:13][web:14][web:17]

***

## 💻 Code Examples Summary

### Quick Reference Examples

**1. Function Declaration:**
```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet('Alice')); // Output: Hello, Alice!
```

**2. Function Expression:**
```javascript
const add = function(a, b) {
    return a + b;
};
console.log(add(5, 3)); // Output: 8
```

**3. Arrow Function:**
```javascript
const multiply = (a, b) => a * b;
console.log(multiply(4, 5)); // Output: 20
```

**4. Default Parameters:**
```javascript
const greet = (name = 'Guest') => `Hello, ${name}!`;
console.log(greet()); // Output: Hello, Guest!
```

**5. Rest Parameters:**
```javascript
const sum = (...numbers) => numbers.reduce((a, b) => a + b, 0);
console.log(sum(1, 2, 3, 4)); // Output: 10
```

**6. Spread Operator:**
```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];
console.log(arr2); // Output: [1, 2, 3, 4, 5]
```

**7. Higher-Order Function:**
```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(n => n * 2);
console.log(doubled); // Output: [2, 4, 6, 8]
```

**8. Callback:**
```javascript
function processData(data, callback) {
    callback(data.toUpperCase());
}
processData('hello', result => console.log(result));
// Output: HELLO
```

**9. IIFE:**
```javascript
(function() {
    const message = 'Runs immediately!';
    console.log(message);
})();
// Output: Runs immediately!
```

**10. Function Returning Function:**
```javascript
const createMultiplier = (factor) => (num) => num * factor;
const double = createMultiplier(2);
console.log(double(5)); // Output: 10
```

***

## 🔗 References

### Official Documentation
- [MDN Web Docs - Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [MDN Web Docs - IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)
- [JavaScript.info - Rest Parameters and Spread Syntax](https://javascript.info/rest-parameters-spread)

### Learning Resources
- [FreeCodeCamp - Callbacks and Higher-Order Functions](https://www.freecodecamp.org/news/callbacks-higher-order-functions-in-javascript/)
- [W3Schools - JavaScript Arrow Functions](https://www.w3schools.com/js/js_arrow_function.asp)
- [GeeksforGeeks - JavaScript Higher Order Functions](https://www.geeksforgeeks.org/javascript/javascript-higher-order-functions/)

### Advanced Topics
- [JavaScript Tutorial - Default Parameters](https://www.javascripttutorial.net/javascript-default-parameters/)
- [Dev.to - Function Declarations vs Expressions](https://dev.to/catherineisonline/function-declarations-function-expressions-2o5k)
- [JavaScript Tutorial - IIFE](https://www.javascripttutorial.net/javascript-immediately-invoked-function-expression/)

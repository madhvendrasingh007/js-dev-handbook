# 🚀 JavaScript Hoisting & Temporal Dead Zone (TDZ)

![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=flat-square&logo=javascript)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-orange?style=flat-square)
![Best Practices](https://img.shields.io/badge/Best%20Practices-Included-green?style=flat-square)

> **Understanding JavaScript's execution context behavior: Hoisting and the Temporal Dead Zone**

---

## 📋 Table of Contents

- [Theory](#-theory)
  - [What is Hoisting?](#what-is-hoisting)
  - [What is Temporal Dead Zone?](#what-is-temporal-dead-zone)
  - [How JavaScript Executes Code](#how-javascript-executes-code)
- [Architecture](#-architecture)
  - [Hoisting Process Visualization](#hoisting-process-visualization)
  - [Memory Allocation Phase](#memory-allocation-phase)
  - [Temporal Dead Zone Timeline](#temporal-dead-zone-timeline)
- [Code Examples](#-code-examples)
  - [Variable Hoisting (var, let, const)](#variable-hoisting-var-let-const)
  - [Function Hoisting](#function-hoisting)
  - [Temporal Dead Zone Examples](#temporal-dead-zone-examples)
  - [Class Hoisting](#class-hoisting)
- [Best Practices](#-best-practices)
- [Summary](#-summary)
- [References](#-references)

---

## 📚 Theory

### What is Hoisting?

**Hoisting** is JavaScript's default behavior of moving declarations to the top of their scope during the compilation phase, before code execution. This means you can use variables and functions before they appear to be declared in the code.

**Key Concepts:**
- Hoisting happens during the **creation phase** of the execution context
- Only **declarations** are hoisted, not **initializations**
- Different behavior for `var`, `let`, `const`, and function declarations
- Hoisting is a mental model to understand JavaScript's two-phase execution

**Real-World Context:**
Understanding hoisting helps you avoid bugs related to variable access timing and write more predictable code. It's especially important when working with legacy codebases using `var` or when debugging unexpected `undefined` values.

---

### What is Temporal Dead Zone?

The **Temporal Dead Zone (TDZ)** is the period between entering scope and the variable being declared where the variable cannot be accessed. During this time, any attempt to access the variable results in a `ReferenceError`.

**Key Concepts:**
- TDZ exists for `let`, `const`, and `class` declarations
- Starts at the beginning of the scope
- Ends when the variable declaration is reached
- Designed to catch errors and enforce better coding practices
- `var` does not have a TDZ (returns `undefined` instead)

**Real-World Context:**
The TDZ prevents you from using variables before they're properly initialized, catching potential bugs early. This makes modern JavaScript (`let`/`const`) safer than legacy `var` declarations.

---

### How JavaScript Executes Code

JavaScript execution happens in **two phases**:

1. **Creation Phase (Memory Allocation)**
   - Execution context is created
   - Variables and functions are stored in memory
   - `var` variables are initialized with `undefined`
   - `let`/`const` variables are uninitialized (TDZ)
   - Function declarations are fully hoisted

2. **Execution Phase**
   - Code is executed line by line
   - Variables are assigned their values
   - Functions are invoked

---

## 🏗️ Architecture

### Hoisting Process Visualization

```
┌─────────────────────────────────────────────────────────────┐
│                    SOURCE CODE (Written)                     │
├─────────────────────────────────────────────────────────────┤
│  console.log(a);        // Line 1                           │
│  console.log(b);        // Line 2                           │
│  console.log(c);        // Line 3                           │
│  var a = 10;            // Line 4                           │
│  let b = 20;            // Line 5                           │
│  const c = 30;          // Line 6                           │
└─────────────────────────────────────────────────────────────┘
                              ↓
                    COMPILATION PHASE
                              ↓
┌─────────────────────────────────────────────────────────────┐
│              HOW JAVASCRIPT INTERPRETS IT                    │
├─────────────────────────────────────────────────────────────┤
│  // CREATION PHASE - Memory Allocation                      │
│  var a = undefined;     // Hoisted & initialized            │
│  let b;                 // Hoisted but uninitialized (TDZ)  │
│  const c;               // Hoisted but uninitialized (TDZ)  │
│                                                              │
│  // EXECUTION PHASE - Line by line                          │
│  console.log(a);        // undefined                        │
│  console.log(b);        // ReferenceError (TDZ)             │
│  console.log(c);        // ReferenceError (TDZ)             │
│  a = 10;                // Assignment                       │
│  b = 20;                // TDZ ends, assignment             │
│  c = 30;                // TDZ ends, assignment             │
└─────────────────────────────────────────────────────────────┘
```

---

### Memory Allocation Phase

```
┌──────────────────────────────────────────────────────────────┐
│                    EXECUTION CONTEXT                          │
├──────────────────────────────────────────────────────────────┤
│  Memory Component (Variable Environment)                     │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  var declarations:    a = undefined                    │ │
│  │  let declarations:    b = <uninitialized> [TDZ]       │ │
│  │  const declarations:  c = <uninitialized> [TDZ]       │ │
│  │  function greet:      { entire function code }         │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                              │
│  Code Component (Thread of Execution)                        │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  Executes code line by line                            │ │
│  │  Variables get their actual values                     │ │
│  └────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
```

---

### Temporal Dead Zone Timeline

```
Scope Begins
    │
    ├─────────────────────┐
    │   TEMPORAL DEAD ZONE │  ← ReferenceError if accessed
    │   (Cannot access)    │
    ├─────────────────────┘
    │
let x = 10;  ← Declaration & Initialization
    │
    ├─────────────────────┐
    │   SAFE ZONE          │  ← Variable can be used
    │   (Can access x)     │
    └─────────────────────┘
```

**Detailed Timeline:**

| Phase | var | let/const | Function |
|-------|-----|-----------|----------|
| **Creation** | Hoisted & initialized (`undefined`) | Hoisted but uninitialized | Fully hoisted with definition |
| **Before Declaration Line** | Returns `undefined` | TDZ - ReferenceError | Can be called |
| **After Declaration Line** | Contains value | Contains value | Can be called |

---

## 💻 Code Examples

### Variable Hoisting (var, let, const)

```javascript
// Example 1: var hoisting behavior
console.log(x); // Output: undefined (not an error!)
var x = 5; // Declaration is hoisted, initialization is not
console.log(x); // Output: 5

// How JavaScript interprets it:
// var x = undefined;  // Hoisted to top
// console.log(x);     // undefined
// x = 5;              // Assignment happens here
// console.log(x);     // 5
```

```javascript
// Example 2: let hoisting with TDZ
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10; // let is hoisted but stays in TDZ until this line
console.log(y); // Output: 10

// Explanation:
// - let y is hoisted but uninitialized
// - Accessing before declaration = TDZ violation
// - TDZ ends when declaration line is reached
```

```javascript
// Example 3: const hoisting with TDZ
console.log(z); // ReferenceError: Cannot access 'z' before initialization
const z = 15; // const must be initialized when declared
console.log(z); // Output: 15

// Explanation:
// - const behaves like let regarding hoisting
// - const MUST be initialized at declaration
// - Cannot be reassigned later
```

```javascript
// Example 4: Comparison of all three
function demonstrateHoisting() {
  console.log(a); // undefined (var is initialized)
  console.log(b); // ReferenceError (let in TDZ)
  console.log(c); // ReferenceError (const in TDZ)
  
  var a = 1;   // var: hoisted and initialized to undefined
  let b = 2;   // let: hoisted but in TDZ
  const c = 3; // const: hoisted but in TDZ
}
```

---

### Function Hoisting

```javascript
// Example 5: Function declaration hoisting
greet(); // Output: "Hello World!" (works before declaration)

function greet() {
  console.log("Hello World!"); // Entire function is hoisted
}

// Explanation:
// - Function declarations are fully hoisted
// - Both name and body are available from the start
// - Can call function before its definition in code
```

```javascript
// Example 6: Function expression with var
sayHi(); // TypeError: sayHi is not a function

var sayHi = function() {
  console.log("Hi!"); // Function assigned to var
};

// Explanation:
// - var sayHi is hoisted and set to undefined
// - The function assignment happens at runtime
// - Calling undefined as a function causes TypeError
```

```javascript
// Example 7: Function expression with let/const
greetUser(); // ReferenceError: Cannot access 'greetUser' before initialization

const greetUser = function() {
  console.log("Hello User!"); // const is in TDZ
};

// Explanation:
// - const greetUser is hoisted but in TDZ
// - Cannot access before initialization
// - TDZ protection prevents usage before ready
```

```javascript
// Example 8: Arrow function hoisting
welcomeMessage(); // ReferenceError: Cannot access 'welcomeMessage' before initialization

let welcomeMessage = () => {
  console.log("Welcome!"); // Arrow functions follow let/const rules
};

// Explanation:
// - Arrow functions are treated as expressions
// - Follow the same TDZ rules as let/const
// - Must be declared before use
```

---

### Temporal Dead Zone Examples

```javascript
// Example 9: TDZ in block scope
{
  // TDZ starts here for 'temp'
  console.log(temp); // ReferenceError
  
  let temp = "value"; // TDZ ends here
  console.log(temp); // Output: "value"
}

// Explanation:
// - TDZ exists from block start to declaration
// - Each block scope has its own TDZ
// - Accessing variable in TDZ throws error
```

```javascript
// Example 10: TDZ with typeof operator
console.log(typeof undeclaredVar); // Output: "undefined" (no error)
console.log(typeof x); // ReferenceError: Cannot access 'x' before initialization

let x = 10; // x exists but is in TDZ

// Explanation:
// - typeof on truly undeclared variable returns "undefined"
// - typeof on TDZ variable throws ReferenceError
// - TDZ is stricter than var for error detection
```

```javascript
// Example 11: TDZ in function parameters
function multiply(a = b, b = 2) {
  // TDZ: 'b' used before it's declared in parameters
  return a * b;
}

multiply(); // ReferenceError: Cannot access 'b' before initialization

// Explanation:
// - Parameters are evaluated left to right
// - 'b' is in TDZ when used as default for 'a'
// - Order matters in parameter defaults
```

```javascript
// Example 12: TDZ with destructuring
let [a, b] = [1, 2]; // Both a and b are in TDZ until this line completes

console.log(a, b); // Output: 1 2

// Trying to access before:
// console.log(x); // ReferenceError
let [x, y] = [10, 20]; // TDZ for both x and y

// Explanation:
// - Destructuring follows same TDZ rules
// - All variables in destructuring are in TDZ
// - TDZ ends when entire statement completes
```

---

### Class Hoisting

```javascript
// Example 13: Class declaration hoisting
const instance = new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization

class MyClass {
  constructor() {
    this.name = "Class"; // Classes are hoisted but in TDZ
  }
}

// Explanation:
// - Class declarations are hoisted
// - They remain in TDZ like let/const
// - Must declare class before instantiation
```

```javascript
// Example 14: Class expression
const obj = new MyClassExpr(); // ReferenceError

const MyClassExpr = class {
  constructor() {
    this.value = 100; // Class expression follows const rules
  }
};

// Explanation:
// - Class expressions follow const/let hoisting
// - Subject to TDZ restrictions
// - Cannot instantiate before declaration
```

---

## ✅ Best Practices

### 1. **Always Declare Variables at the Top of Their Scope**
```javascript
// ❌ Bad Practice
function calculate() {
  result = x + y; // Accessing before declaration
  let x = 5;
  let y = 10;
  return result;
}

// ✅ Good Practice
function calculate() {
  let x = 5;       // Declare at top
  let y = 10;      // Clear initialization
  let result = x + y; // Use after declaration
  return result;
}
```

### 2. **Prefer `const` and `let` Over `var`**
```javascript
// ❌ Avoid var
var count = 0; // Function-scoped, confusing hoisting

// ✅ Use const for constants
const MAX_SIZE = 100; // Block-scoped, TDZ protection

// ✅ Use let for variables
let counter = 0; // Block-scoped, TDZ protection
```

### 3. **Declare Functions Before Using Them**
```javascript
// ❌ Relying on hoisting (confusing)
processData();

function processData() {
  // Complex logic
}

// ✅ Clear declaration order
function processData() {
  // Complex logic
}

processData(); // Called after declaration
```

### 4. **Avoid Accessing Variables in Their TDZ**
```javascript
// ❌ TDZ violation
if (true) {
  console.log(data); // ReferenceError
  let data = "info";
}

// ✅ Declare before use
if (true) {
  let data = "info";
  console.log(data); // Safe access
}
```

### 5. **Use Function Declarations for Top-Level Functions**
```javascript
// ✅ Function declaration (fully hoisted, clear intent)
function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0);
}

// ✅ Use const for function expressions (prevents reassignment)
const formatCurrency = (amount) => {
  return `$${amount.toFixed(2)}`;
};
```

### 6. **Be Careful with Default Parameters**
```javascript
// ❌ Parameter order issue
function greet(name = surname, surname = "Doe") {
  // 'surname' in TDZ when used for 'name'
  return `Hello ${name} ${surname}`;
}

// ✅ Correct parameter order
function greet(surname = "Doe", name = surname) {
  // 'surname' is initialized before use
  return `Hello ${name} ${surname}`;
}
```

### 7. **Understand Block Scope with let/const**
```javascript
// ❌ Unexpected behavior with var
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // All print 3
}

// ✅ Block scope with let
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // Prints 0, 1, 2
}
```

---

## 📝 Summary

### Key Takeaways

1. **Hoisting is JavaScript's behavior of moving declarations to the top during compilation:**
   - `var` declarations are hoisted and initialized to `undefined`
   - `let` and `const` declarations are hoisted but remain uninitialized (TDZ)
   - Function declarations are fully hoisted with their definitions
   - Only declarations are hoisted, not initializations or assignments

2. **The Temporal Dead Zone (TDZ) is a safety feature:**
   - Exists for `let`, `const`, and `class` declarations
   - Prevents access to variables before they're properly initialized
   - Starts at the beginning of scope and ends at the declaration line
   - Accessing variables in TDZ throws a `ReferenceError`

3. **Best practices for avoiding hoisting-related bugs:**
   - Prefer `const` and `let` over `var` for better scoping and TDZ protection
   - Declare all variables at the top of their scope
   - Initialize variables when you declare them
   - Understand the difference between function declarations and expressions
   - Be mindful of block scope and execution context

---

## 📖 References

1. **MDN Web Docs - Hoisting**  
   https://developer.mozilla.org/en-US/docs/Glossary/Hoisting

2. **JavaScript.info - Variable Scope and Hoisting**  
   https://javascript.info/closure#lexical-environment

3. **MDN Web Docs - Temporal Dead Zone**  
   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz

---

*Made with ❤️ for JavaScript developers | Understanding hoisting leads to better code*
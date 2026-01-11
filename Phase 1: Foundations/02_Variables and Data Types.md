# JavaScript Variables & Data Types 🎯

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![ES6+](https://img.shields.io/badge/ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Variables](https://img.shields.io/badge/Variables-4CAF50?style=for-the-badge)
![Data Types](https://img.shields.io/badge/Data%20Types-2196F3?style=for-the-badge)
![Type Coercion](https://img.shields.io/badge/Type%20Coercion-FF5722?style=for-the-badge)
![Hoisting](https://img.shields.io/badge/Hoisting-9C27B0?style=for-the-badge)
![Scope](https://img.shields.io/badge/Scope-00BCD4?style=for-the-badge)

## 📖 Overview

Variables are containers for storing data values, and data types determine what kind of values can be stored. JavaScript's dynamic typing allows variables to hold any type of value, making it flexible yet requiring careful handling. Understanding variable declarations, scoping rules, and type conversion is fundamental to writing robust JavaScript code.

## 📦 Variable Declarations

JavaScript offers three ways to declare variables: `var`, `let`, and `const`. Each has distinct characteristics that affect scope, reassignment, and hoisting behavior.

### Declaration Comparison

| Feature | `const` | `let` | `var` | Implicit |
|---------|---------|-------|-------|----------|
| **Introduced** | ES6 (2015) | ES6 (2015) | Pre-ES6 | Always existed |
| **Scope** | Block | Block | Function | Global |
| **Reassignable** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **Redeclarable** | ❌ No | ❌ No | ✅ Yes | N/A |
| **Hoisting** | Yes (TDZ) | Yes (TDZ) | Yes (undefined) | No |
| **Use Case** | Default choice | When reassignment needed | Legacy code only | ❌ Never use |

> **TDZ** (Temporal Dead Zone): Variables are hoisted but remain uninitialized and inaccessible until their declaration line

### Basic Declaration Example

```javascript
// const - Cannot be reassigned
const accountId = 12345;
// accountId = 54321; // ❌ TypeError: Assignment to constant variable

// let - Block-scoped and reassignable
let accountEmail = "user@example.com";
accountEmail = "newuser@example.com"; // ✅ Works

// var - Function-scoped (avoid in modern code)
var accountPassword = "pass123";
accountPassword = "newpass456"; // ✅ Works

// Implicit global (dangerous - never use)
accountCity = "Mumbai"; // ✅ Works but creates global pollution

// Undefined variable
let accountState; // Declared but not initialized
console.log(accountState); // undefined
```

## 🔄 Hoisting Behavior

Hoisting is JavaScript's default behavior of moving declarations to the top of their scope during compilation. This is unique compared to most programming languages.

### What is Hoisting?

```
┌─────────────────────────────────────────────────────────┐
│                  Hoisting Mechanism                     │
└─────────────────────────────────────────────────────────┘

        YOUR CODE                    JAVASCRIPT INTERPRETS IT
┌──────────────────────┐           ┌──────────────────────┐
│ console.log(x);      │           │ var x;               │
│ var x = 5;           │    →      │ console.log(x);      │
│                      │           │ x = 5;               │
└──────────────────────┘           └──────────────────────┘
    Returns: undefined               Declaration hoisted
```

### var Hoisting

```javascript
console.log(myVar); // undefined (not an error!)
var myVar = 5;
console.log(myVar); // 5

// JavaScript interprets this as:
var myVar; // Hoisted to top, initialized with undefined
console.log(myVar); // undefined
myVar = 5; // Assignment stays in place
console.log(myVar); // 5
```

### let and const Hoisting (Temporal Dead Zone)

```javascript
// TDZ - accessing before declaration causes error
console.log(myLet); // ❌ ReferenceError: Cannot access 'myLet' before initialization
let myLet = 10;

console.log(myConst); // ❌ ReferenceError: Cannot access 'myConst' before initialization
const myConst = 20;

// After declaration, they work normally
let validLet = 30;
console.log(validLet); // 30 ✅
```

### Function Hoisting

```javascript
// Function declarations are fully hoisted
sayHello(); // ✅ "Hello!" - Works before declaration

function sayHello() {
  return "Hello!";
}

// Function expressions follow variable hoisting rules
sayGoodbye(); // ❌ TypeError: sayGoodbye is not a function

var sayGoodbye = function() {
  return "Goodbye!";
};

// Arrow functions with const - TDZ applies
greet(); // ❌ ReferenceError: Cannot access 'greet' before initialization

const greet = () => {
  return "Greetings!";
};
```

### Hoisting: JavaScript vs Other Languages

```javascript
// ✅ JAVASCRIPT - Hoisting allows this
console.log(x); // undefined (no error)
var x = 5;

sayHello(); // "Hello!" (works perfectly)
function sayHello() {
  return "Hello!";
}
```

```c
// ❌ C/C++ - Strict declaration order
#include <stdio.h>
int main() {
    printf("%d", x); // Error: 'x' undeclared
    int x = 5;
    return 0;
}
```

```python
# ❌ PYTHON - No hoisting
print(x) # NameError: name 'x' is not defined
x = 5
```

```java
// ❌ JAVA - No forward references
public class Example {
    public static void main(String[] args) {
        System.out.println(x); // Compile Error
        int x = 5;
    }
}
```

## 🎯 Block Scope vs Function Scope

Scope determines where variables are accessible in your code.

```
┌─────────────────────────────────────────────────────────┐
│                    Scope Visualization                  │
└─────────────────────────────────────────────────────────┘

GLOBAL SCOPE
├── var globalVar (accessible everywhere)
│
└── FUNCTION SCOPE
    ├── var functionVar (accessible in function)
    │
    └── BLOCK SCOPE { }
        ├── let blockLet (only in this block)
        └── const blockConst (only in this block)
```

### Block Scope (let & const)

```javascript
if (true) {
  let blockScoped = "I'm trapped!";
  const alsoBlockScoped = "Me too!";
  var notBlockScoped = "I escaped!";

  console.log(blockScoped); // ✅ "I'm trapped!"
}

console.log(notBlockScoped); // ✅ "I escaped!" - var ignores block scope
console.log(blockScoped); // ❌ ReferenceError - let is block-scoped
console.log(alsoBlockScoped); // ❌ ReferenceError - const is block-scoped
```

### Function Scope (var)

```javascript
function testScope() {
  if (true) {
    var functionScoped = "Available in whole function";
    let blockOnly = "Only in this block";
  }

  console.log(functionScoped); // ✅ "Available in whole function"
  console.log(blockOnly); // ❌ ReferenceError
}

testScope();
console.log(functionScoped); // ❌ ReferenceError - not in global scope
```

### Practical Scope Example

```javascript
function demonstrateScope() {
  console.log(a); // undefined (var hoisted to function scope)
  // console.log(b); // ❌ ReferenceError (let in TDZ)

  if (true) {
    var a = 1; // Hoisted to function scope
    let b = 2; // Block scoped
    console.log(a, b); // 1, 2 ✅
  }

  console.log(a); // 1 ✅ - accessible due to function scoping
  // console.log(b); // ❌ ReferenceError - b is block-scoped
}

demonstrateScope();
```

## 🏷️ Primitive Data Types

JavaScript has 7 primitive data types that store single values directly in memory.

```
┌────────────────────────────────────────────────────────┐
│              Primitive Data Types (7)                  │
├────────────────────────────────────────────────────────┤
│  String  │  Number  │  Boolean  │  Undefined  │  Null  │
│  Symbol  │  BigInt                                     │
└────────────────────────────────────────────────────────┘
```

### String

Represents textual data enclosed in quotes.

```javascript
// String declaration - three ways
const singleQuote = 'Hello';
const doubleQuote = "World";
const templateLiteral = `Hello ${singleQuote}`; // Template literals support interpolation

// String properties and methods
const message = "JavaScript";
console.log(message.length); // 10 - length property
console.log(message.toUpperCase()); // "JAVASCRIPT"
console.log(message.charAt(0)); // "J"
console.log(message.includes("Script")); // true

// Multi-line strings with template literals
const multiLine = `This is
a multi-line
string`;
```

### Number

Represents both integers and floating-point numbers.

```javascript
// Number types
const integer = 42;
const float = 3.14159;
const negative = -100;
const exponential = 2.5e6; // 2500000

// Special numeric values
const infinity = Infinity; // Positive infinity
const negInfinity = -Infinity; // Negative infinity
const notANumber = NaN; // Not a Number (result of invalid math)

// Number operations
console.log(10 / 0); // Infinity
console.log("text" / 2); // NaN
console.log(0.1 + 0.2); // 0.30000000000000004 - floating-point precision issue
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
```

### Boolean

Represents logical true/false values.

```javascript
// Boolean values
const isActive = true;
const isComplete = false;

// Boolean from comparisons
const isGreater = 10 > 5; // true
const isEqual = "hello" === "world"; // false

// Boolean in conditions
if (isActive) {
  console.log("User is active"); // Executes if true
}

// Boolean conversion
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("text")); // true
console.log(Boolean("")); // false
```

### Undefined

Represents a variable that has been declared but not assigned a value.

```javascript
// Undefined scenarios
let notAssigned; // Declared but not initialized
console.log(notAssigned); // undefined

function noReturn() {
  // No return statement
}
console.log(noReturn()); // undefined

const obj = { name: "John" };
console.log(obj.age); // undefined - property doesn't exist
```

### Null

Represents intentional absence of any value.

```javascript
// Null - explicitly setting "no value"
let emptyValue = null; // Intentionally empty
console.log(emptyValue); // null

// null vs undefined
let notSet; // undefined - unintentional absence
let cleared = null; // null - intentional absence

console.log(typeof notSet); // "undefined"
console.log(typeof cleared); // "object" - historical JavaScript bug!

// Checking for null
if (cleared === null) {
  console.log("Value is explicitly null");
}
```

### Symbol (ES6)

Creates unique identifiers that are guaranteed to be unique.

```javascript
// Symbol creation - always unique
const id1 = Symbol("id");
const id2 = Symbol("id");
console.log(id1 === id2); // false - each Symbol is unique

// Symbols as object keys (hidden from normal iteration)
const user = {
  name: "Alice",
  [id1]: 123 // Symbol as property key
};

console.log(user.name); // "Alice"
console.log(user[id1]); // 123
console.log(Object.keys(user)); // ["name"] - Symbol key not included

// Use case: Avoid property name collisions
const EMAIL = Symbol("email");
const obj = {
  [EMAIL]: "user@example.com"
};
```

### BigInt (ES2020)

Represents integers larger than Number.MAX_SAFE_INTEGER.

```javascript
// BigInt for very large numbers
const regularNumber = 9007199254740991; // MAX_SAFE_INTEGER
const tooBig = 9007199254740992; // Loses precision

// BigInt declaration - add 'n' suffix
const bigNumber = 9007199254740991n;
const anotherBig = BigInt("99999999999999999999");

// BigInt operations
console.log(bigNumber + 100n); // ✅ Works
// console.log(bigNumber + 100); // ❌ TypeError - cannot mix BigInt and Number

// Comparison works
console.log(10n === 10); // false - different types
console.log(10n == 10); // true - loose equality
console.log(10n > 5); // true - comparison works
```

## 🔄 Type Conversion & Coercion

JavaScript converts types automatically (coercion) or manually (conversion).

```
┌─────────────────────────────────────────────────────────┐
│            Type Conversion Flow                         │
└─────────────────────────────────────────────────────────┘

    EXPLICIT                        IMPLICIT
   (Manual)                       (Automatic)
       ↓                               ↓
  Number("123")                   "5" + 5
  String(123)         ←→          "5" - 2
  Boolean(0)                      "5" * "2"
```

### Explicit Conversion

```javascript
// String conversion
const num = 123;
const str = String(num); // "123"
const alsoStr = num.toString(); // "123"
console.log(typeof str); // "string"

// Number conversion
const strNum = "456";
const converted = Number(strNum); // 456
const parsed = parseInt("789px"); // 789 - parses until non-digit
const floatParsed = parseFloat("3.14abc"); // 3.14

console.log(Number("hello")); // NaN - invalid conversion
console.log(Number(true)); // 1
console.log(Number(false)); // 0
console.log(Number(null)); // 0
console.log(Number(undefined)); // NaN

// Boolean conversion
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("text")); // true
console.log(Boolean("")); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
```

### Implicit Coercion

```javascript
// String coercion with +
console.log("5" + 5); // "55" - number coerced to string
console.log("Hello" + " " + "World"); // "Hello World"
console.log("Value: " + 100); // "Value: 100"

// Numeric coercion with -, *, /
console.log("10" - 5); // 5 - string coerced to number
console.log("20" * 2); // 40
console.log("100" / 10); // 10
console.log("5" - "2"); // 3

// Boolean coercion in conditions
if ("text") { // Non-empty string → true
  console.log("Truthy value");
}

// Comparison coercion
console.log("5" == 5); // true - loose equality (coerces types)
console.log("5" === 5); // false - strict equality (no coercion)
console.log(null == undefined); // true - special case
console.log(null === undefined); // false - different types
```

### Truthy and Falsy Values

JavaScript coerces values to boolean in conditional contexts.

```javascript
// ❌ FALSY VALUES (only 8)
console.log(Boolean(false)); // false
console.log(Boolean(0)); // false
console.log(Boolean(-0)); // false
console.log(Boolean(0n)); // false - BigInt zero
console.log(Boolean("")); // false - empty string
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN)); // false

// ✅ TRUTHY VALUES (everything else)
console.log(Boolean(true)); // true
console.log(Boolean(1)); // true
console.log(Boolean(-1)); // true
console.log(Boolean("text")); // true
console.log(Boolean("0")); // true - non-empty string
console.log(Boolean("false")); // true - non-empty string
console.log(Boolean([])); // true - empty array
console.log(Boolean({})); // true - empty object
console.log(Boolean(function(){})); // true - any function
```

### Practical Truthy/Falsy Example

```javascript
function checkValue(val) {
  if (val) {
    console.log(`${val} is truthy`);
  } else {
    console.log(`${val} is falsy`);
  }
}

checkValue("hello"); // "hello is truthy"
checkValue(""); // " is falsy"
checkValue(42); // "42 is truthy"
checkValue(0); // "0 is falsy"
checkValue(null); // "null is falsy"
checkValue(undefined); // "undefined is falsy"
checkValue([]); // "[] is truthy" - empty arrays are truthy!
```

## 🎨 Type Checking

```javascript
// typeof operator
console.log(typeof "hello"); // "string"
console.log(typeof 42); // "number"
console.log(typeof 42n); // "bigint"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null); // "object" ⚠️ - historical bug!
console.log(typeof Symbol()); // "symbol"
console.log(typeof {}); // "object"
console.log(typeof []); // "object" - arrays are objects
console.log(typeof function(){}); // "function"

// Better null check
const value = null;
console.log(value === null); // true ✅ - correct way

// Array check
console.log(Array.isArray([])); // true ✅
console.log(Array.isArray({})); // false
```

## 🏗️ Architecture Overview

```
┌──────────────────────────────────────────────────────────┐
│          JavaScript Variable & Type System               │
└──────────────────────────────────────────────────────────┘

                    SOURCE CODE
                         ↓
            ┌────────────────────────┐
            │   COMPILATION PHASE    │
            │  - Variable hoisting   │
            │  - Scope creation      │
            │  - TDZ initialization  │
            └───────────┬────────────┘
                        ↓
            ┌────────────────────────┐
            │   EXECUTION PHASE      │
            └───────────┬────────────┘
                        ↓
        ┌───────────────┴───────────────┐
        ↓                               ↓
┌───────────────┐             ┌───────────────┐
│ MEMORY HEAP   │             │  CALL STACK   │
│               │             │               │
│ Objects       │             │ Execution     │
│ Arrays        │             │ Contexts      │
│ Functions     │             │               │
└───────────────┘             └───────────────┘
        ↓                               ↓
┌───────────────────────────────────────────┐
│         VARIABLE STORAGE                  │
├───────────────────────────────────────────┤
│  Primitives → Stack (value)               │
│  Objects → Heap (reference in stack)      │
└───────────────────────────────────────────┘
```

## ✅ Best Practices

- **Always use `const` by default** - prevents accidental reassignment and signals intent
- **Use `let` only when reassignment is needed** - like loop counters or accumulators
- **Never use `var` in modern code** - avoid scope confusion and hoisting issues
- **Never use implicit globals** - always declare variables with const/let
- **Declare variables at the top of their scope** - improves readability
- **Use meaningful, descriptive names** - `userEmail` not `ue` or `x`
- **Initialize variables when declaring** - avoid undefined values
- **Use strict equality (`===`)** - prevents unexpected type coercion
- **Understand truthy/falsy for conditionals** - but be explicit when needed
- **Check types when necessary** - use `typeof` and `Array.isArray()`
- **Be cautious with type coercion** - prefer explicit conversion
- **Remember `const` doesn't make objects immutable** - properties can change
- **Use template literals for string concatenation** - cleaner than `+` operator
- **Validate numeric operations** - check for `NaN` with `Number.isNaN()`

## 🧠 Summary

JavaScript variables can be declared with `const`, `let`, or `var`, each offering different scoping and hoisting behaviors. Modern JavaScript favors `const` for immutable bindings and `let` for reassignable values, while `var` should be avoided. The language supports 7 primitive types (String, Number, Boolean, Undefined, Null, Symbol, BigInt) and one reference type (Object). Understanding hoisting, scope, and JavaScript's unique Temporal Dead Zone is crucial for avoiding common pitfalls. Type conversion happens both explicitly through functions like `Number()` and implicitly through coercion, with truthy/falsy values playing a key role in conditional logic.

## 🔗 References

- [MDN: JavaScript Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#declarations) - Comprehensive variable guide
- [MDN: JavaScript Data Types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures) - Data types and structures
- [MDN: Type Coercion](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion) - Understanding coercion
- [JavaScript.info: Variables](https://javascript.info/variables) - Modern variable tutorial
- [JavaScript.info: Data Types](https://javascript.info/types) - Interactive data types guide
- [JavaScript.info: Type Conversions](https://javascript.info/type-conversions) - Conversion examples
- [ECMAScript Let and Const](https://262.ecma-international.org/6.0/#sec-let-and-const-declarations) - Official specification
- [You Don't Know JS: Types & Grammar](https://github.com/getify/You-Dont-Know-JS/tree/1st-ed/types%20%26%20grammar) - Deep dive into types

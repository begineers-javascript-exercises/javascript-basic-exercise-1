# Exercise 1 - File 1: Variables and Data Types

## 🎯 Interview Topics Covered
- Variable declarations (var, let, const)
- Data types and type checking
- Hoisting concept
- Scope (global, function, block)
- Temporal Dead Zone

---

## 📋 1. Variable Declarations - Interview Essential

### ❓ Common Interview Question: "What's the difference between var, let, and const?"

```javascript
// Example 1: User Registration System
// const - Values that never change
const APP_NAME = "UserHub";
const MAX_USERNAME_LENGTH = 20;
const API_BASE_URL = "https://api.userhub.com";

// let - Values that can change
let currentUser = null;
let isLoggedIn = false;
let loginAttempts = 0;

// var - Old way (has issues we'll discuss)
var sessionId = "abc123";

// Demonstrating the differences
console.log("=== Registration System ===");
console.log(`App: ${APP_NAME}`);
console.log(`Max username length: ${MAX_USERNAME_LENGTH}`);
console.log(`Currently logged in: ${isLoggedIn}`);
```

```javascript
// Example 2: Shopping Cart System
const STORE_NAME = "TechMart";
const TAX_RATE = 0.08;
const FREE_SHIPPING_THRESHOLD = 50;

let cartItems = [];
let cartTotal = 0;
let shippingCost = 5.99;
let customerEmail = "";

// Adding items to cart
function addToCart(item, price) {
    cartItems.push({name: item, price: price});
    cartTotal += price;
    
    // Free shipping logic
    if (cartTotal >= FREE_SHIPPING_THRESHOLD) {
        shippingCost = 0;
    }
    
    console.log(`Added ${item} - $${price}`);
    console.log(`Cart total: $${cartTotal.toFixed(2)}`);
    console.log(`Shipping: $${shippingCost}`);
}

addToCart("Wireless Mouse", 29.99);
addToCart("Keyboard", 79.99);
```

---

## 🔍 2. Data Types - Must Know for Interviews

### ❓ Interview Question: "What are the primitive data types in JavaScript?"

```javascript
// Example 1: Employee Management System
let employeeId = 12345;                    // Number
let employeeName = "Sarah Johnson";        // String
let isFullTime = true;                     // Boolean
let middleName = null;                     // Null (intentionally empty)
let socialSecurityNumber = undefined;      // Undefined
let uniqueEmployeeSymbol = Symbol("emp");  // Symbol (ES6)
let salaryInCents = 5000000n;             // BigInt (for large numbers)

// Type checking - Critical for interviews
console.log("=== Employee Data Types ===");
console.log(`ID type: ${typeof employeeId}`);
console.log(`Name type: ${typeof employeeName}`);
console.log(`Full-time type: ${typeof isFullTime}`);
console.log(`Middle name type: ${typeof middleName}`);
console.log(`SSN type: ${typeof socialSecurityNumber}`);
console.log(`Symbol type: ${typeof uniqueEmployeeSymbol}`);
console.log(`Salary type: ${typeof salaryInCents}`);
```

```javascript
// Example 2: Product Inventory System
// Complex data types
let productCategories = ["Electronics", "Books", "Clothing"];  // Array
let product = {                                                // Object
    id: 101,
    name: "Laptop",
    price: 999.99,
    inStock: true,
    specifications: {
        processor: "Intel i7",
        ram: "16GB",
        storage: "512GB SSD"
    },
    tags: ["computer", "portable", "work"]
};

// Advanced type checking
console.log("=== Product Data Types ===");
console.log(`Categories type: ${typeof productCategories}`);
console.log(`Is categories an array: ${Array.isArray(productCategories)}`);
console.log(`Product type: ${typeof product}`);
console.log(`Product constructor: ${product.constructor.name}`);

// Accessing nested data
console.log(`Product name: ${product.name}`);
console.log(`Processor: ${product.specifications.processor}`);
console.log(`First tag: ${product.tags[0]}`);
```

---

## 🔄 3. Scope and Hoisting - Interview Favorites

### ❓ Interview Question: "Explain variable hoisting"

```javascript
// Example 1: Understanding var hoisting
console.log("=== Hoisting Example ===");

// This works due to hoisting (but undefined)
console.log("userName before declaration:", userName);  // undefined
var userName = "John";
console.log("userName after declaration:", userName);   // "John"

// This is what actually happens (conceptually):
// var userName;  // hoisted to top
// console.log(userName);  // undefined
// userName = "John";
```

```javascript
// Example 2: let and const - Temporal Dead Zone
console.log("=== Temporal Dead Zone ===");

function demonstrateScope() {
    console.log("Function started");
    
    // This will throw ReferenceError
    // console.log(userAge);  // Cannot access before initialization
    
    let userAge = 25;
    const userCity = "New York";
    
    console.log(`User age: ${userAge}`);
    console.log(`User city: ${userCity}`);
    
    // Block scope demonstration
    if (true) {
        let blockVariable = "I'm in a block";
        const blockConstant = "Me too";
        var functionScoped = "I'm function scoped";
        
        console.log(`Inside block: ${blockVariable}`);
    }
    
    // console.log(blockVariable);  // ReferenceError - not accessible
    console.log(`Function scope: ${functionScoped}`);  // Works fine
}

demonstrateScope();
```

---

## 🎯 4. Practical Interview Challenges

### Challenge 1: Fix the Scope Issues

```javascript
// Problem: Fix this code to work correctly
console.log("=== Scope Challenge ===");

function createCounter() {
    // Problem: Using var in loop
    for (var i = 0; i < 3; i++) {
        setTimeout(function() {
            console.log("Counter with var:", i);  // Always prints 3
        }, 100);
    }
    
    // Solution: Using let
    for (let j = 0; j < 3; j++) {
        setTimeout(function() {
            console.log("Counter with let:", j);  // Prints 0, 1, 2
        }, 200);
    }
}

createCounter();
```

### Challenge 2: Variable Best Practices

```javascript
// Example: User Profile Manager
console.log("=== Best Practices ===");

// Good practices
const USER_ROLES = {
    ADMIN: 'admin',
    USER: 'user',
    MODERATOR: 'moderator'
};

let currentUserProfile = {
    id: 1,
    name: "Alice Smith",
    email: "alice@email.com",
    role: USER_ROLES.USER
};

// Function to update profile
function updateUserProfile(updates) {
    // Create new object instead of mutating
    currentUserProfile = {
        ...currentUserProfile,
        ...updates,
        updatedAt: new Date()
    };
    
    console.log("Profile updated:", currentUserProfile);
}

updateUserProfile({ name: "Alice Johnson" });
```

---

## 📝 Practice Exercises

### Exercise 1: Create a Library Management System
```javascript
// TODO: Create variables for:
// - Library name (constant)
// - Available books count (can change)
// - Library hours (constant object)
// - Current borrower (can be null)
// - Is library open (boolean)

// Your code here...
```

### Exercise 2: Build a Temperature Converter
```javascript
// TODO: Create variables for:
// - Temperature in Celsius (input)
// - Temperature in Fahrenheit (calculated)
// - Temperature in Kelvin (calculated)
// - Show proper data types for each

// Your code here...
```

---

## 🎯 Key Takeaways for Interviews

1. **Always use `const` by default**, `let` when you need to reassign
2. **Avoid `var`** in modern JavaScript
3. **Understand hoisting** - var is hoisted, let/const have temporal dead zone
4. **Know all primitive types**: string, number, boolean, null, undefined, symbol, bigint
5. **Use `typeof` and `Array.isArray()`** for type checking
6. **Understand scope**: global, function, and block scope

---

## 🔗 Next Files
- **File 2**: Functions and Arrow Functions
- **File 3**: Control Structures and Loops  
- **File 4**: Arrays and Objects Deep Dive
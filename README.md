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

# Exercise 1.1: Core Declarations & Primitive Data Types

**Objective:** Master the declaration of variables using modern best practices (`let`, `const`) and understand the fundamental "primitive" data types that form the building blocks of all JavaScript programs.

## Part 1: Declaring Variables

In JavaScript, a variable is a named container for a value. How you create this container is crucial.

### `const` (Constant)
Use `const` when the variable's value **will not be reassigned**. This should be your default choice as it prevents a common class of bugs.

*   **Example 1: Application Configuration**
    A setting like a server URL or a company name is fixed throughout the application's life.

    ```javascript
    const API_BASE_URL = 'https://api.my-app.com/v3';
    const COMPANY_NAME = 'Tech Solutions Inc.';
    console.log(`Connecting to ${COMPANY_NAME} server at ${API_BASE_URL}...`);
    // Trying to change it: API_BASE_URL = 'http://localhost'; // This will cause a TypeError.
    ```

*   **Example 2: Mathematical Constant**
    A value like the gravitational constant doesn't change.

    ```javascript
    const GRAVITATIONAL_CONSTANT = 9.8; // m/s^2
    console.log('The pull of gravity is:', GRAVITATIONAL_CONSTANT);
    ```

### `let` (Re-assignable)
Use `let` only when you know the variable's value **will need to change**.

*   **Example 1: A User's Shopping Cart**
    The contents and total of a shopping cart change as a user adds and removes items.

    ```javascript
    let cartItemCount = 0;
    console.log(`You have ${cartItemCount} items in your cart.`); // Output: 0

    cartItemCount = 2; // User adds two items.
    console.log(`You have ${cartItemCount} items in your cart.`); // Output: 2
    ```

*   **Example 2: Tracking Game State**
    The player's score and current level change throughout a game.
    ```javascript
    let playerLevel = 1;
    let playerScore = 0;

    playerLevel = 2;
    playerScore = 1500;
    console.log(`Player reached Level ${playerLevel} with a score of ${playerScore}.`);
    ```

## Part 2: Primitive Data Types

**1. String:** Textual data, enclosed in quotes. Backticks (`` `...` ``) are the most powerful as they allow for embedded variables (interpolation).

```javascript
const userName = "Brenda";
const orderStatus = 'Processing';
const confirmationMessage = `Hello ${userName}, your order status is: ${orderStatus}.`;
console.log(confirmationMessage);


### 2. Number: Represents all numbers, including integers and decimals.
> Try to create these variables.

```
const price = 19.99;
const quantity = 3;
const taxRate = 0.05; // 5%
const total = (price * quantity) * (1 + taxRate);
console.log('Total cost:', total);
```

### 3. Boolean: Represents true or false. Essential for making decisions in code.

```
const hasAdminRights = false;
const isUserLoggedIn = true;
if (isUserLoggedIn) {
  console.log('Welcome back!');
}
```

## Practice Exercise: Online Store Product Page
### Task

> You are coding the backend logic for a product page. You need to declare variables to hold product information and calculate the initial price.

- Declare a constant for the product's name ('Wireless Headphones').
- Declare a re-assignable variable for the quantity the user wants to buy, initialized to 1.
- Declare a constant for the price per unit (149.99).
- Declare a boolean constant isProductInStock and set it to true.
- Declare a constant for the product's unique ID ('abc-123').
- Calculate the totalPrice and store it in a constant.
- Log a descriptive message using a template string: "User wants to buy [quantity] of [productName] for a total of $[totalPrice].".
- Use the typeof operator to log the type of the product name, quantity, and in-stock status.

## Solution

```
// 1. Declare product ID
const productID = 'abc-123';

// 2. Declare product name
const productName = 'Wireless Headphones';

// 3. Declare a re-assignable quantity
let quantity = 1;

// 4. Declare price per unit
const pricePerUnit = 149.99;

// 5. Declare stock status
const isProductInStock = true;

// 6. Calculate total price
const totalPrice = quantity * pricePerUnit;

// 7. Log the descriptive message
console.log(`User wants to buy ${quantity} of ${productName} for a total of $${totalPrice}.`);
// Expected Output: User wants to buy 1 of Wireless Headphones for a total of $149.99.

// 8. Log the data types
console.log('Type of productName:', typeof productName);       // Expected Output: string
console.log('Type of quantity:', typeof quantity);             // Expected Output: number
console.log('Type of isProductInStock:', typeof isProductInStock); // Expected Output: boolean
```

### **File 1.2: Naming Conventions & Deep Dive on String/Number Methods**
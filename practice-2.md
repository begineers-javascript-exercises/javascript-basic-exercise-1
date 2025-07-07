# Exercise 1 - File 2: Functions and Arrow Functions

## 🎯 Interview Topics Covered
- Function declarations vs expressions
- Arrow functions and their differences
- Parameters and arguments
- Return statements
- Function hoisting
- Closures and scope
- Higher-order functions

---

## 📋 1. Function Declarations - Interview Essential

### ❓ Common Interview Question: "What's the difference between function declaration and function expression?"

```javascript
// Example 1: User Authentication System
console.log("=== Function Declarations ===");

// Function Declaration - Hoisted (can be called before declaration)
function authenticateUser(username, password) {
    console.log(`Authenticating user: ${username}`);
    
    // Simulate authentication logic
    if (username === "admin" && password === "secret123") {
        return {
            success: true,
            message: "Login successful",
            user: {
                id: 1,
                username: username,
                role: "admin"
            }
        };
    }
    
    return {
        success: false,
        message: "Invalid credentials"
    };
}

// Function can be called before declaration due to hoisting
let result = authenticateUser("admin", "secret123");
console.log("Auth result:", result);

// Function Expression - Not hoisted
const logUserActivity = function(userId, action) {
    const timestamp = new Date().toISOString();
    console.log(`[${timestamp}] User ${userId} performed: ${action}`);
};

logUserActivity(1, "login");
```

```javascript
// Example 2: E-commerce Order Processing
console.log("=== Order Processing Functions ===");

// Function with multiple parameters and validation
function processOrder(customerId, items, shippingAddress) {
    // Parameter validation
    if (!customerId || !items || !shippingAddress) {
        return {
            success: false,
            error: "Missing required parameters"
        };
    }
    
    // Calculate total
    let total = 0;
    for (let item of items) {
        total += item.price * item.quantity;
    }
    
    // Apply shipping cost
    const shippingCost = total > 100 ? 0 : 9.99;
    const finalTotal = total + shippingCost;
    
    return {
        success: true,
        orderId: `ORDER-${Date.now()}`,
        customerId: customerId,
        items: items,
        subtotal: total,
        shipping: shippingCost,
        total: finalTotal,
        estimatedDelivery: "3-5 business days"
    };
}

// Test the function
const orderResult = processOrder(
    "CUST-001",
    [
        { name: "Laptop", price: 999.99, quantity: 1 },
        { name: "Mouse", price: 29.99, quantity: 2 }
    ],
    {
        street: "123 Main St",
        city: "New York",
        zip: "10001"
    }
);

console.log("Order processed:", orderResult);
```

---

## 🏹 2. Arrow Functions - Modern JavaScript

### ❓ Interview Question: "When would you use arrow functions vs regular functions?"

```javascript
// Example 1: Data Processing with Arrow Functions
console.log("=== Arrow Functions ===");

// Traditional function
const calculateTax = function(amount, rate) {
    return amount * rate;
};

// Arrow function - concise
const calculateTaxArrow = (amount, rate) => amount * rate;

// Arrow function with block body
const generateInvoice = (order) => {
    const tax = calculateTaxArrow(order.total, 0.08);
    const grandTotal = order.total + tax;
    
    return {
        invoiceId: `INV-${Date.now()}`,
        orderId: order.orderId,
        subtotal: order.total,
        tax: tax,
        grandTotal: grandTotal,
        dueDate: new Date(Date.now() + 30 * 24 * 60 * 60 * 1000) // 30 days
    };
};

// Using the functions
const sampleOrder = { orderId: "ORD-001", total: 100 };
const invoice = generateInvoice(sampleOrder);
console.log("Generated invoice:", invoice);
```

```javascript
// Example 2: Array Processing with Arrow Functions
console.log("=== Array Processing ===");

const employees = [
    { id: 1, name: "John Doe", salary: 50000, department: "IT" },
    { id: 2, name: "Jane Smith", salary: 60000, department: "HR" },
    { id: 3, name: "Bob Johnson", salary: 55000, department: "IT" },
    { id: 4, name: "Alice Brown", salary: 70000, department: "Finance" }
];

// Arrow functions in array methods
const itEmployees = employees.filter(emp => emp.department === "IT");
const highSalaryEmployees = employees.filter(emp => emp.salary > 55000);
const employeeNames = employees.map(emp => emp.name);
const totalSalary = employees.reduce((sum, emp) => sum + emp.salary, 0);

console.log("IT Employees:", itEmployees);
console.log("High Salary Employees:", highSalaryEmployees);
console.log("Employee Names:", employeeNames);
console.log("Total Salary:", totalSalary);

// Complex arrow function with multiple operations
const getEmployeeReport = (department) => {
    const deptEmployees = employees.filter(emp => emp.department === department);
    const avgSalary = deptEmployees.reduce((sum, emp) => sum + emp.salary, 0) / deptEmployees.length;
    
    return {
        department: department,
        count: deptEmployees.length,
        employees: deptEmployees.map(emp => emp.name),
        averageSalary: avgSalary
    };
};

console.log("IT Department Report:", getEmployeeReport("IT"));
```

---

## 🔄 3. Advanced Function Concepts

### ❓ Interview Question: "Explain closures with a practical example"

```javascript
// Example 1: Counter with Closure
console.log("=== Closures ===");

function createCounter(initialValue = 0) {
    let count = initialValue;
    
    // These functions have access to 'count' even after createCounter returns
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count,
        reset: () => count = initialValue
    };
}

const counter1 = createCounter(5);
const counter2 = createCounter(10);

console.log("Counter 1 initial:", counter1.getValue());
console.log("Counter 1 increment:", counter1.increment());
console.log("Counter 1 increment:", counter1.increment());

console.log("Counter 2 initial:", counter2.getValue());
console.log("Counter 2 decrement:", counter2.decrement());

// Each counter maintains its own state
console.log("Counter 1 final:", counter1.getValue());
console.log("Counter 2 final:", counter2.getValue());
```

```javascript
// Example 2: Private Variables with Closures
console.log("=== Private Variables ===");

function createBankAccount(initialBalance = 0) {
    let balance = initialBalance;
    let transactionHistory = [];
    
    const addTransaction = (type, amount) => {
        transactionHistory.push({
            type: type,
            amount: amount,
            timestamp: new Date(),
            balanceAfter: balance
        });
    };
    
    return {
        deposit: (amount) => {
            if (amount > 0) {
                balance += amount;
                addTransaction("deposit", amount);
                return `Deposited $${amount}. New balance: $${balance}`;
            }
            return "Invalid deposit amount";
        },
        
        withdraw: (amount) => {
            if (amount > 0 && amount <= balance) {
                balance -= amount;
                addTransaction("withdrawal", amount);
                return `Withdrew $${amount}. New balance: $${balance}`;
            }
            return "Invalid withdrawal amount or insufficient funds";
        },
        
        getBalance: () => balance,
        
        getTransactionHistory: () => [...transactionHistory] // Return copy
    };
}

const account = createBankAccount(100);
console.log(account.deposit(50));
console.log(account.withdraw(30));
console.log("Current balance:", account.getBalance());
console.log("Transaction history:", account.getTransactionHistory());
```

---

## 🎯 4. Higher-Order Functions

### ❓ Interview Question: "What are higher-order functions? Give examples."

```javascript
// Example 1: Function that takes another function as parameter
console.log("=== Higher-Order Functions ===");

function processUserData(users, processor) {
    return users.map(processor);
}

const users = [
    { id: 1, firstName: "John", lastName: "Doe", age: 30 },
    { id: 2, firstName: "Jane", lastName: "Smith", age: 25 },
    { id: 3, firstName: "Bob", lastName: "Johnson", age: 35 }
];

// Different processors
const getFullName = (user) => `${user.firstName} ${user.lastName}`;
const getAgeCategory = (user) => user.age >= 30 ? "Senior" : "Junior";
const getUserSummary = (user) => ({
    id: user.id,
    fullName: getFullName(user),
    ageCategory: getAgeCategory(user)
});

// Using higher-order function
const fullNames = processUserData(users, getFullName);
const ageCategories = processUserData(users, getAgeCategory);
const summaries = processUserData(users, getUserSummary);

console.log("Full names:", fullNames);
console.log("Age categories:", ageCategories);
console.log("User summaries:", summaries);
```

```javascript
// Example 2: Function that returns another function
console.log("=== Function Factory ===");

function createValidator(rule) {
    return function(value) {
        switch(rule) {
            case "email":
                return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value);
            case "phone":
                return /^\d{10}$/.test(value.replace(/\D/g, ''));
            case "password":
                return value.length >= 8 && /[A-Z]/.test(value) && /[0-9]/.test(value);
            default:
                return true;
        }
    };
}

// Create specific validators
const validateEmail = createValidator("email");
const validatePhone = createValidator("phone");
const validatePassword = createValidator("password");

// Test validators
console.log("Email valid:", validateEmail("user@example.com"));
console.log("Phone valid:", validatePhone("123-456-7890"));
console.log("Password valid:", validatePassword("SecurePass123"));

// Form validation function
function validateForm(formData, validators) {
    const errors = {};
    
    for (let field in validators) {
        if (!validators[field](formData[field])) {
            errors[field] = `Invalid ${field}`;
        }
    }
    
    return {
        isValid: Object.keys(errors).length === 0,
        errors: errors
    };
}

const formData = {
    email: "user@example.com",
    phone: "1234567890",
    password: "weak"
};

const validationResult = validateForm(formData, {
    email: validateEmail,
    phone: validatePhone,
    password: validatePassword
});

console.log("Form validation:", validationResult);
```

---

## 📝 Practice Exercises

### Exercise 1: Build a Calculator
```javascript
// TODO: Create functions for:
// - Basic operations (add, subtract, multiply, divide)
// - Advanced operations (power, square root)
// - Memory functions (store, recall, clear)
// Use both regular and arrow functions

// Your code here...
```

### Exercise 2: User Management System
```javascript
// TODO: Create functions for:
// - Add user (with validation)
// - Remove user
// - Update user
// - Search users
// - Get user statistics
// Use closures to maintain private user data

// Your code here...
```

---

## 🎯 Key Takeaways for Interviews

1. **Function Declaration** - Hoisted, can be called before declaration
2. **Function Expression** - Not hoisted, assigned to variable
3. **Arrow Functions** - Concise syntax, no `this` binding
4. **Closures** - Functions remember their outer scope
5. **Higher-Order Functions** - Functions that take/return other functions
6. **Use arrow functions** for callbacks and short functions
7. **Use regular functions** when you need `this` binding

---

## 🔗 Navigation
- **[← File 1](exercise1_variables.md)**: Variables and Data Types
- **[File 3 →](exercise1_control.md)**: Control Structures and Loops
- **[File 4 →](exercise1_arrays_objects.md)**: Arrays and Objects Deep Dive

---

### **File 2: Naming Conventions & Deep Dive on String/Number Methods**

```markdown
# Exercise 1.2: Naming & Working with Strings and Numbers

**Objective:** Learn professional naming conventions and explore the powerful built-in methods for `String` and `Number` types, which are used daily in professional development.

## Part 1: Professional Naming Conventions

How you name your variables matters. Good names make code readable and maintainable.

*   **camelCase:** The standard for variables and functions in JavaScript. Start with a lowercase letter, and capitalize the first letter of each subsequent word.
    *   **Good:** `let userFirstName`, `const maxRetries`, `function calculateTotal()`
    *   **Bad:** `let user_first_name`, `const maxretries`, `function Calculatetotal()`

*   **PascalCase:** Used for class names and components. Capitalize the first letter of every word.
    *   **Good:** `class UserSession { ... }`, `class DatabaseManager { ... }`

*   **UPPER_SNAKE_CASE:** Used for "hard-coded" constant values that are treated as global configuration.
    *   **Good:** `const API_KEY = '...';`, `const SECONDS_IN_A_DAY = 86400;`

## Part 2: String Properties and Methods

Strings come with built-in tools (methods) to manipulate them.

*   **`.length` (Property)**: Returns the number of characters in the string.

    ```javascript
    const userComment = 'This is great!';
    console.log('Comment length:', userComment.length); // Output: 14
    ```

*   **`.toUpperCase()` & `.toLowerCase()`**: Return a new string in all upper or lower case.

    ```javascript
    const userInput = 'New York';
    const dbEntry = userInput.toUpperCase(); // Storing as 'NEW YORK' for consistency
    console.log(dbEntry); // Output: NEW YORK
    ```

*   **`.slice(startIndex, endIndex)`**: Extracts a section of a string and returns it as a new string. `endIndex` is optional.

    ```javascript
    const orderId = 'ORD-2025-4817-USER';
    const userPart = orderId.slice(15); // Extracts from index 15 to the end
    console.log('User part:', userPart); // Output: USER

    const yearPart = orderId.slice(4, 8); // Extracts from index 4 up to (but not including) 8
    console.log('Year part:', yearPart); // Output: 2025
    ```

*   **`.replace(searchValue, newValue)`**: Finds the first match of `searchValue` and replaces it.

    ```javascript
    let statusMessage = "Your order is pending.";
    let updatedMessage = statusMessage.replace('pending', 'shipped');
    console.log(updatedMessage); // Output: Your order is shipped.
    ```

## Part 3: Number Methods and the `Math` Object

Numbers also have useful methods.

*   **`.toFixed(decimalPlaces)`**: Formats a number to a specific number of decimal places and returns it as a **string**. Essential for displaying currency.

    ```javascript
    const price = 49.95678;
    const displayPrice = price.toFixed(2); // Rounds to 2 decimal places
    console.log('Price to display: $' + displayPrice); // Output: $49.96
    ```

*   **`parseInt(string)` & `parseFloat(string)`**: Global functions to convert a string into an integer or a floating-point number.

    ```javascript
    const cssWidth = '250.5px';
    const widthAsNumber = parseFloat(cssWidth); // Extracts the number 250.5
    console.log('Numeric width:', widthAsNumber); // Output: 250.5
    ```

*   **The `Math` Object**: A built-in object with properties and methods for mathematical operations.
    *   **`Math.round(n)`**: Standard rounding to the nearest integer.
    *   **`Math.ceil(n)`**: Rounds up to the nearest integer.
    *   **`Math.floor(n)`**: Rounds down to the nearest integer.
    *   **`Math.random()`**: Returns a random number between 0 (inclusive) and 1 (exclusive).

    ```javascript
    // Example: Calculate how many boxes are needed.
    const items = 21;
    const itemsPerBox = 5;
    const boxesNeeded = Math.ceil(items / itemsPerBox); // 21/5 is 4.2. ceil() rounds up to 5.
    console.log('Boxes needed:', boxesNeeded); // Output: 5

    // Example: Generate a random dice roll (1-6)
    const diceRoll = Math.floor(Math.random() * 6) + 1;
    console.log('You rolled a:', diceRoll);
    ```

## Practice Exercise: User Profile and Invoice Formatting

### Task
You need to process user data and format it for display.

1.  A user signs up with the name `  alex green  ` (with extra spaces). Create a variable for this.
2.  Clean up the name: remove leading/trailing spaces (`.trim()`) and format it to be "Alex Green" (capitalize first letters). *Hint: Slice the first letter, uppercase it, and concatenate it with the rest of the name.*
3.  You have a total bill of `120.345`. Store this in a variable. Format this for an invoice to always show two decimal places.
4.  You need to generate a 4-digit random PIN for account verification. Use `Math.random()` and `Math.floor()` to generate a random number between 1000 and 9999.
5.  Log the cleaned name, the formatted invoice total, and the random PIN.

### Solution

```javascript
// 1. User's raw input
const rawUserName = '  alex green  ';

// 2. Clean and format the name
const trimmedName = rawUserName.trim(); // "alex green"
const firstName = trimmedName.slice(0, 4); // "alex"
const lastName = trimmedName.slice(5);     // "green"

const formattedFirstName = firstName.charAt(0).toUpperCase() + firstName.slice(1); // "Alex"
const formattedLastName = lastName.charAt(0).toUpperCase() + lastName.slice(1);   // "Green"
const finalName = `${formattedFirstName} ${formattedLastName}`;

// 3. Format the bill
const totalBill = 120.345;
const formattedBill = totalBill.toFixed(2);

// 4. Generate a 4-digit PIN
// Math.random() gives 0 to 0.999...
// * 9000 gives 0 to 8999.999...
// + 1000 gives 1000 to 9999.999...
// Math.floor() drops the decimal.
const randomPin = Math.floor(Math.random() * 9000) + 1000;

// 5. Log the results
console.log('Formatted User Name:', finalName); // Expected: "Alex Green"
console.log('Invoice Total: $' + formattedBill);  // Expected: "$120.35"
console.log('Generated Security PIN:', randomPin); // Expected: A random number between 1000 and 9999
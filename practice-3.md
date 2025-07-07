# Exercise 1 - File 3: Control Structures and Loops

## 🎯 Interview Topics Covered
- Conditional statements (if/else, switch)
- Comparison and logical operators
- Ternary operator
- Loops (for, while, do-while)
- Loop control (break, continue)
- for...in and for...of loops
- Modern iteration methods

---

## 📋 1. Conditional Statements - Interview Essential

### ❓ Common Interview Question: "Explain different ways to handle conditions in JavaScript"

```javascript
// Example 1: User Role Authorization System
console.log("=== Authorization System ===");

function checkUserPermissions(user) {
    // Basic if/else structure
    if (!user) {
        return { access: false, message: "No user provided" };
    }
    
    if (user.role === "admin") {
        return { 
            access: true, 
            message: "Full access granted",
            permissions: ["read", "write", "delete", "manage"]
        };
    } else if (user.role === "moderator") {
        return { 
            access: true, 
            message: "Moderator access granted",
            permissions: ["read", "write", "moderate"]
        };
    } else if (user.role === "user") {
        return { 
            access: true, 
            message: "User access granted",
            permissions: ["read"]
        };
    } else {
        return { 
            access: false, 
            message: "Unknown role - access denied",
            permissions: []
        };
    }
}

// Test different user roles
const users = [
    { id: 1, name: "Alice", role: "admin" },
    { id: 2, name: "Bob", role: "moderator" },
    { id: 3, name: "Charlie", role: "user" },
    { id: 4, name: "David", role: "guest" }
];

users.forEach(user => {
    const result = checkUserPermissions(user);
    console.log(`${user.name} (${user.role}):`, result);
});
```

```javascript
// Example 2: E-commerce Pricing System
console.log("=== Pricing System ===");

function calculatePrice(product, customer) {
    let basePrice = product.price;
    let discount = 0;
    let finalPrice = basePrice;
    
    // Multiple conditions with logical operators
    if (customer.isPremium && customer.yearsActive >= 2) {
        discount = 0.15; // 15% discount for premium customers with 2+ years
    } else if (customer.isPremium || customer.yearsActive >= 5) {
        discount = 0.10; // 10% discount for premium OR long-term customers
    } else if (customer.totalOrders > 50) {
        discount = 0.05; // 5% discount for frequent buyers
    }
    
    finalPrice = basePrice * (1 - discount);
    
    // Additional conditions
    if (product.category === "electronics" && finalPrice > 1000) {
        finalPrice -= 50; // $50 off expensive electronics
    }
    
    // Free shipping condition
    const freeShipping = finalPrice > 100 || customer.isPremium;
    
    return {
        basePrice: basePrice,
        discount: discount,
        finalPrice: finalPrice.toFixed(2),
        freeShipping: freeShipping,
        savings: (basePrice - finalPrice).toFixed(2)
    };
}

// Test the pricing system
const product = { name: "Laptop", price: 1200, category: "electronics" };
const customers = [
    { name: "Premium Customer", isPremium: true, yearsActive: 3, totalOrders: 25 },
    { name: "Long-term Customer", isPremium: false, yearsActive: 6, totalOrders: 30 },
    { name: "Frequent Buyer", isPremium: false, yearsActive: 1, totalOrders: 75 },
    { name: "New Customer", isPremium: false, yearsActive: 0, totalOrders: 2 }
];

customers.forEach(customer => {
    const pricing = calculatePrice(product, customer);
    console.log(`${customer.name}:`, pricing);
});
```

---

## 🔄 2. Switch Statements and Ternary Operator

### ❓ Interview Question: "When would you use switch vs if/else?"

```javascript
// Example 1: Order Status Management
console.log("=== Order Status System ===");

function getOrderStatusInfo(status) {
    let statusInfo;
    
    // Switch statement for multiple discrete values
    switch (status) {
        case "pending":
            statusInfo = {
                message: "Order is being processed",
                color: "orange",
                allowCancel: true,
                estimatedTime: "1-2 hours"
            };
            break;
        case "confirmed":
            statusInfo = {
                message: "Order confirmed and being prepared",
                color: "blue",
                allowCancel: true,
                estimatedTime: "2-4 hours"
            };
            break;
        case "shipped":
            statusInfo = {
                message: "Order has been shipped",
                color: "purple",
                allowCancel: false,
                estimatedTime: "2-3 days"
            };
            break;
        case "delivered":
            statusInfo = {
                message: "Order delivered successfully",
                color: "green",
                allowCancel: false,
                estimatedTime: "Completed"
            };
            break;
        case "cancelled":
            statusInfo = {
                message: "Order has been cancelled",
                color: "red",
                allowCancel: false,
                estimatedTime: "N/A"
            };
            break;
        default:
            statusInfo = {
                message: "Unknown order status",
                color: "gray",
                allowCancel: false,
                estimatedTime: "Unknown"
            };
    }
    
    return statusInfo;
}

// Test different order statuses
const orderStatuses = ["pending", "confirmed", "shipped", "delivered", "cancelled"];
orderStatuses.forEach(status => {
    const info = getOrderStatusInfo(status);
    console.log(`Status: ${status}`, info);
});
```

```javascript
// Example 2: Ternary Operator Usage
console.log("=== Ternary Operator Examples ===");

// Simple ternary
const checkAge = (age) => age >= 18 ? "Adult" : "Minor";

// Nested ternary (use sparingly)
const getDiscountLevel = (points) => 
    points >= 1000 ? "Gold" :
    points >= 500 ? "Silver" :
    points >= 100 ? "Bronze" : "None";

// Ternary in function parameters
const formatCurrency = (amount, currency = "USD") => 
    currency === "USD" ? `$${amount}` : `${amount} ${currency}`;

// Ternary for conditional assignment
const processPayment = (amount, method) => {
    const fee = method === "credit" ? amount * 0.03 : 0;
    const total = amount + fee;
    
    return {
        amount: amount,
        fee: fee,
        total: total,
        message: total > 100 ? "High value transaction" : "Standard transaction"
    };
};

// Testing ternary operators
console.log("Age check:", checkAge(17), checkAge(25));
console.log("Discount levels:", getDiscountLevel(1200), getDiscountLevel(300), getDiscountLevel(50));
console.log("Currency format:", formatCurrency(100), formatCurrency(100, "EUR"));
console.log("Payment processing:", processPayment(150, "credit"));
```

---

## 🔁 3. Loops - Interview Essential

### ❓ Interview Question: "Explain different types of loops and when to use each"

```javascript
// Example 1: Data Processing with Different Loop Types
console.log("=== Loop Types ===");

const products = [
    { id: 1, name: "Laptop", price: 999, category: "electronics", stock: 5 },
    { id: 2, name: "Mouse", price: 29, category: "electronics", stock: 50 },
    { id: 3, name: "Keyboard", price: 79, category: "electronics", stock: 30 },
    { id: 4, name: "Monitor", price: 299, category: "electronics", stock: 0 },
    { id: 5, name: "Headphones", price: 199, category: "electronics", stock: 15 }
];

// 1. Traditional for loop - when you need index
console.log("=== Traditional For Loop ===


---

### **File 1.3: Tricky Primitives & Type Coercion**

```markdown
# Exercise 1.3: Tricky Primitives & Type Coercion

**Objective:** Understand the important differences between `null` and `undefined`, and grasp the concept of Type Coercion, a common source of bugs and a favorite topic in technical interviews.

## Part 1: `undefined` vs. `null`

These two types represent "emptiness" but have different semantic meanings.

### `undefined`
A variable has the type `undefined` when it has been **declared but not yet assigned a value**. It's JavaScript's way of saying "I know this variable exists, but it has no value."

*   **Example 1: Implicitly `undefined`**
    A variable is automatically `undefined` until you assign something to it.

    ```javascript
    let userShippingAddress;
    console.log(userShippingAddress); // Output: undefined
    console.log(typeof userShippingAddress); // Output: "undefined"
    ```

*   **Example 2: Function with no return**
    A function that doesn't explicitly `return` a value will implicitly return `undefined`.

    ```javascript
    function logMessage(message) {
      console.log(message);
      // No return statement here
    }
    const result = logMessage('Hello!'); // Logs "Hello!" to the console
    console.log('The function returned:', result); // Output: The function returned: undefined
    ```

### `null`
`null` is an **intentional assignment of "no value"**. As a programmer, you use `null` to explicitly state that a variable is empty.

*   **Example 1: Clearing a Selection**
    Imagine a user can select a product from a list. When they deselect it, you can set the variable to `null`.

    ```javascript
    let selectedProduct = 'T-Shirt Model X';
    console.log('Selected product is:', selectedProduct); // Output: T-Shirt Model X

    // User clicks a "clear selection" button
    selectedProduct = null;
    console.log('Selected product is now:', selectedProduct); // Output: null
    ```
*   **Interview Tip:** The `typeof null` is `'object'`. This is a famous, long-standing bug in JavaScript that can't be fixed due to backward compatibility. Be ready to explain this!

    ```javascript
    console.log(typeof null); // Output: "object" (This is the historical bug!)
    ```

## Part 2: Type Coercion (Implicit Conversion)

JavaScript often tries to be "helpful" by automatically converting data types when you use operators. This is called **Type Coercion**. It can be useful but also very dangerous.

### Coercion to String
When you use the `+` operator with a string, any other operand will be converted to a string.

```javascript
// Example 1: Number to String
const result1 = 'My favorite number is ' + 7;
console.log(result1); // Output: "My favorite number is 7"
console.log(typeof result1); // "string"

// Example 2: The classic trap
const result2 = '5' + 3; // '+' with a string means concatenation
console.log(result2); // Output: "53"
console.log(typeof result2); // "string"

## Coercion to Number

> Most other math operators (-, *, /, %) will try to convert operands to numbers.

```
// Example 1: The 'helpful' case
const result3 = '10' - '2'; // '-' coerces both strings to numbers
console.log(result3); // Output: 8
console.log(typeof result3); // "number"

// Example 2: What happens with non-numeric strings?
const result4 = 'hello' * 3;
console.log(result4); // Output: NaN (Not-a-Number)
console.log(typeof result4); // "number" - Yes, NaN is technically of type number!
```

> Best Practice: Always be explicit. Don't rely on coercion. If you need to add numbers, make sure they are both numbers first using parseInt() or Number(). Number('5') + 3 gives 8.


# Practice Exercise: A Simple Shopping Cart Calculator
## Task

> You're building a feature where a user can input a quantity into a form field on a webpage. Form inputs are always read as strings. Your task is to perform calculations correctly, avoiding coercion pitfalls.

- A variable inputQuantity is received from a form. It has the string value '2'.
- A variable priceString is received from another part of the UI. It has the value '25.50'.
- A shippingCost variable is a number, 9.99.
- The Wrong Way: Add priceString and shippingCost using the + operator. Log the result and its type to see the coercion bug in action.
- The Right Way: Convert inputQuantity and priceString to numbers.
- Calculate the subtotal by multiplying the numeric quantity and numeric price.
- Calculate the grandTotal by adding the subtotal and the shippingCost.
- Log the final grandTotal.

## Solution

```
// 1. & 2. & 3. Initial variables from the UI
const inputQuantity = '2';
const priceString = '25.50';
const shippingCost = 9.99;

// 4. The Wrong Way (demonstrating the bug)
const wrongTotal = priceString + shippingCost;
console.log('--- The Wrong Way ---');
console.log('Result of string + number:', wrongTotal); // Expected: "25.509.99"
console.log('Type of wrongTotal:', typeof wrongTotal); // Expected: "string"
console.log('-----------------------');

// 5. The Right Way (explicit conversion)
const numericQuantity = parseInt(inputQuantity); // Or Number(inputQuantity)
const numericPrice = parseFloat(priceString);   // Or Number(priceString)

// 6. Calculate subtotal
const subtotal = numericQuantity * numericPrice;

// 7. Calculate grand total
const grandTotal = subtotal + shippingCost;

// 8. Log the final, correct result
console.log('--- The Right Way ---');
console.log('Numeric Quantity:', numericQuantity);
console.log('Numeric Price:', numericPrice);
console.log('Subtotal:', subtotal.toFixed(2));
console.log('Grand Total:', grandTotal.toFixed(2)); // Expected: 60.99
```
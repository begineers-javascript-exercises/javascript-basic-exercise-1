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
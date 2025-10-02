# 🏗️ JavaScript Objects & Exception Handling

## 🎯 **Lesson Overview**

### **Objective:**
Learn about **objects**, **prototypal inheritance**, **reflection**, and **exception handling** in JavaScript - essential concepts for SAP UI5 development

---

## 📦 **JavaScript Objects**

### 🔧 **Object Creation Methods:**

| Method | Syntax | Use Case |
|--------|--------|----------|
| **Object Literal** | `const obj = { }` | Simple objects |
| **Constructor Function** | `function Obj() { }` + `new` | Reusable object templates |
| **Class Syntax (ES6)** | `class Obj { }` | Modern OOP approach |

---

## 🏷️ **1. Object Literal Syntax**

### 📝 **Basic Structure:**
```javascript
const objectName = {
    property1: value1,
    property2: value2,
    nestedObject: {
        nestedProperty: value
    }
};
```

### 🧪 **Practical Example - Candidate Object:**
```javascript
const candidate = {
    name: {
        first: "Isabela",
        middle: "Mendes",
        last: "Silva"
    },
    age: 18,
    hasDegree: true,
    position: "Developer"
};
```

### 🔍 **Accessing Object Properties:**

#### **Dot Notation:**
```javascript
console.log(candidate.age);              // 18
console.log(candidate.name.first);       // "Isabela"
```

#### **Bracket Notation:**
```javascript
console.log(candidate["age"]);           // 18
console.log(candidate["name"]["first"]); // "Isabela"
```

### ✏️ **Modifying Objects:**

#### **Updating Existing Properties:**
```javascript
candidate.age = 19;
console.log(candidate.age); // 19
```

#### **Adding New Properties:**
```javascript
candidate.approved = true;
console.log(candidate.approved); // true
```

#### **Dynamic Property Names:**
```javascript
const propertyName = "approved";
candidate[propertyName] = true;
```

---

## 🏭 **2. Constructor Functions**

### 📝 **Basic Structure:**
```javascript
function ObjectName(parameters) {
    this.property = value;
    this.method = function() {
        // method logic
    };
}
```

### 🧪 **Practical Example - Bank Account:**
```javascript
function Account(holder) {
    this.holder = holder;
    this.balance = 0;
    
    this.deposit = function(amount) {
        this.balance += amount;
    };
    
    this.withdraw = function(amount) {
        if (amount > this.balance) {
            throw new Error("Insufficient balance");
        }
        this.balance -= amount;
    };
    
    this.transfer = function(amount, destination) {
        this.withdraw(amount);
        destination.deposit(amount);
    };
}
```

### 🔧 **Creating Object Instances:**
```javascript
// Creating account instances
const acc1 = new Account("Nelson");
const acc2 = new Account("Mateus");

// Using methods
acc1.deposit(100);
acc2.deposit(50);
acc1.transfer(60, acc2);

console.log(`${acc1.holder}: $${acc1.balance}`); // "Nelson: $40"
console.log(`${acc2.holder}: $${acc2.balance}`); // "Mateus: $110"
```

---

## 🔄 **Prototypal Inheritance**

### 📝 **Understanding Prototypes:**
- Every JavaScript object has a **prototype**
- Objects inherit properties and methods from their prototype
- Changes to prototype affect all instances

### 🧪 **Modifying Prototype:**
```javascript
// Adding method to prototype
Account.prototype.toString = function() {
    return `Account Holder: ${this.holder}, Balance: $${this.balance}`;
};

// Using the new method
console.log(acc1.toString()); // "Account Holder: Nelson, Balance: $40"
console.log(acc2.toString()); // "Account Holder: Mateus, Balance: $110"
```

### 💡 **Prototype Chain:**
```javascript
// All instances share the same prototype method
console.log(acc1.toString === acc2.toString); // true
```

---

## 🔍 **Reflection with typeof**

### 📝 **Checking Types:**
```javascript
// Using typeof operator
console.log(typeof acc1.holder);    // "string"
console.log(typeof acc1);           // "object"
console.log(typeof acc1.balance);   // "number"
console.log(typeof acc1.deposit);   // "function"
```

### 🧪 **Practical Type Checking:**
```javascript
function processAccount(account) {
    if (typeof account !== 'object') {
        throw new Error("Expected an account object");
    }
    
    if (typeof account.balance !== 'number') {
        throw new Error("Account balance must be a number");
    }
    
    if (typeof account.deposit !== 'function') {
        throw new Error("Account must have deposit method");
    }
    
    return account.balance;
}
```

---

## 🚨 **Exception Handling with try/catch**

### 📝 **Basic Syntax:**
```javascript
try {
    // Code that might throw an error
    riskyOperation();
} catch (error) {
    // Handle the error
    console.log("Error occurred:", error.message);
}
```

### 🧪 **Practical Example - Bank Account Withdrawal:**
```javascript
// Enhanced withdraw method with exception
Account.prototype.withdraw = function(amount) {
    if (amount > this.balance) {
        throw new Error("Insufficient balance");
    }
    this.balance -= amount;
};

// Using try/catch for safe operations
try {
    const acc3 = new Account("Alex");
    acc3.deposit(10);
    console.log(`Balance: $${acc3.balance}`); // "Balance: $10"
    
    acc3.withdraw(500); // This will throw an error
} catch (error) {
    console.log("Transaction failed:", error.message);
    // "Transaction failed: Insufficient balance"
}
```

### 🔧 **Advanced Error Handling:**
```javascript
function safeTransaction(operation) {
    try {
        const result = operation();
        console.log("Transaction successful:", result);
        return result;
    } catch (error) {
        console.error("Transaction failed:", error.message);
        
        // Log error for debugging
        console.error("Error details:", {
            name: error.name,
            message: error.message,
            stack: error.stack
        });
        
        return null;
    } finally {
        console.log("Transaction attempt completed");
    }
}

// Usage
safeTransaction(() => {
    const account = new Account("John");
    account.deposit(100);
    account.withdraw(200); // This will fail but be handled gracefully
});
```

---

## 🏗️ **Complete Bank Account System**

### 🔧 **Enhanced Account Class:**
```javascript
function BankAccount(holder, initialBalance = 0) {
    // Validation
    if (typeof holder !== 'string') {
        throw new Error("Holder name must be a string");
    }
    
    if (typeof initialBalance !== 'number' || initialBalance < 0) {
        throw new Error("Initial balance must be a non-negative number");
    }
    
    // Properties
    this.holder = holder;
    this.balance = initialBalance;
    this.accountNumber = Math.random().toString(36).substr(2, 9);
    this.transactions = [];
    
    // Methods
    this.deposit = function(amount) {
        if (typeof amount !== 'number' || amount <= 0) {
            throw new Error("Deposit amount must be a positive number");
        }
        
        this.balance += amount;
        this.transactions.push({
            type: 'DEPOSIT',
            amount: amount,
            timestamp: new Date()
        });
        
        return this.balance;
    };
    
    this.withdraw = function(amount) {
        if (typeof amount !== 'number' || amount <= 0) {
            throw new Error("Withdrawal amount must be a positive number");
        }
        
        if (amount > this.balance) {
            throw new Error(`Insufficient balance. Available: $${this.balance}`);
        }
        
        this.balance -= amount;
        this.transactions.push({
            type: 'WITHDRAWAL',
            amount: amount,
            timestamp: new Date()
        });
        
        return this.balance;
    };
    
    this.transfer = function(amount, destination) {
        if (!(destination instanceof BankAccount)) {
            throw new Error("Destination must be a BankAccount instance");
        }
        
        this.withdraw(amount);
        destination.deposit(amount);
        
        this.transactions.push({
            type: 'TRANSFER_OUT',
            amount: amount,
            to: destination.holder,
            timestamp: new Date()
        });
        
        return this.balance;
    };
    
    this.getStatement = function() {
        return {
            holder: this.holder,
            accountNumber: this.accountNumber,
            balance: this.balance,
            transactions: this.transactions
        };
    };
}

// Add to prototype
BankAccount.prototype.toString = function() {
    return `Account ${this.accountNumber} - ${this.holder}: $${this.balance}`;
};

BankAccount.prototype.getTransactionHistory = function() {
    return this.transactions.map(transaction => 
        `${transaction.timestamp.toLocaleString()} - ${transaction.type}: $${transaction.amount}`
    );
};
```

### 🧪 **Using the Enhanced System:**
```javascript
try {
    // Create accounts
    const johnAccount = new BankAccount("John Doe", 1000);
    const janeAccount = new BankAccount("Jane Smith", 500);
    
    // Perform transactions
    johnAccount.deposit(200);
    johnAccount.transfer(300, janeAccount);
    janeAccount.withdraw(100);
    
    // Check results
    console.log(johnAccount.toString());
    console.log(janeAccount.toString());
    
    // Get statements
    console.log("John's Statement:", johnAccount.getStatement());
    console.log("Jane's Transactions:", janeAccount.getTransactionHistory());
    
} catch (error) {
    console.error("Banking error:", error.message);
}
```

---

## 💡 **Best Practices for SAP UI5 Development**

### ✅ **Object Design Patterns:**
```javascript
// Factory function for UI5 controls
function createButton(config) {
    return {
        id: config.id,
        text: config.text || "Button",
        type: config.type || "Default",
        press: config.handler || function() { },
        
        // Method to render button
        render: function() {
            return new sap.m.Button({
                text: this.text,
                type: this.type,
                press: this.press
            });
        }
    };
}

// Usage in UI5
const myButton = createButton({
    id: "btnSubmit",
    text: "Submit Form",
    type: "Emphasized",
    handler: function() {
        // Handle button press
        console.log("Button clicked!");
    }
});
```

### 🛡️ **Error Handling in UI5:**
```javascript
// Safe data binding in UI5 controllers
function safeDataBinding(model, path) {
    try {
        const data = model.getProperty(path);
        
        if (typeof data === 'undefined') {
            console.warn(`Data not found at path: ${path}`);
            return null;
        }
        
        return data;
    } catch (error) {
        console.error(`Data binding error for path ${path}:`, error.message);
        return null;
    }
}
```

---
*🎯 **Objects and exception handling mastered!** Next step: Exploring modern JavaScript features and modules!*
# JavaScript Promises Case Study

## Online Order Processing System

---

## 1. Case Study Overview

An e-commerce company needs an online order-processing application. When a customer places an order, the system must:

1. Validate the order.
2. Check product availability.
3. Process payment.
4. Create the order.
5. Send email and SMS notifications.
6. Display the final result.

These operations may take time and may fail. JavaScript Promises will be used to manage this asynchronous workflow.

---

## 2. Learning Objectives

After completing this case study, participants will understand:

- Synchronous and asynchronous execution
- Promise states: pending, fulfilled, and rejected
- The Promise constructor
- `resolve()` and `reject()`
- `.then()`, `.catch()`, and `.finally()`
- Promise chaining
- Returning Promises from `.then()`
- Error propagation
- `Promise.all()`
- `Promise.allSettled()`
- `Promise.race()`
- `Promise.any()`
- `async` and `await`

---

## 3. Business Workflow

```text
Customer submits order
        ↓
Validate order
        ↓
Check inventory
        ↓
Process payment
        ↓
Create order
        ↓
Send email and SMS
        ↓
Display confirmation
```

Possible failures:

- Product is out of stock.
- Payment is declined.
- Order service is unavailable.
- Email or SMS notification fails.

---

## 4. Project Structure

```text
promise-order-case-study/
│
├── index.html
├── style.css
└── app.js
```

---

## 5. Step 1: Create `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Promise Order Processing Demo</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <main class="container">
        <section class="card">

            <div class="header">
                <span class="label">JavaScript Promise Case Study</span>
                <h1>Online Order Processing</h1>
                <p>
                    Process an order and observe how JavaScript Promises
                    manage asynchronous operations.
                </p>
            </div>

            <form id="orderForm">

                <div class="form-group">
                    <label for="customerName">Customer Name</label>
                    <input
                        type="text"
                        id="customerName"
                        value="Abhinandan"
                        required
                    >
                </div>

                <div class="form-group">
                    <label for="productName">Product</label>
                    <select id="productName">
                        <option value="Laptop">Laptop</option>
                        <option value="Monitor">Monitor</option>
                        <option value="Keyboard">Keyboard</option>
                    </select>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="quantity">Quantity</label>
                        <input
                            type="number"
                            id="quantity"
                            value="1"
                            min="1"
                            required
                        >
                    </div>

                    <div class="form-group">
                        <label for="amount">Amount</label>
                        <input
                            type="number"
                            id="amount"
                            value="75000"
                            min="1"
                            required
                        >
                    </div>
                </div>

                <div class="form-group">
                    <label for="failureStage">Simulate Failure</label>
                    <select id="failureStage">
                        <option value="none">No Failure</option>
                        <option value="inventory">Inventory Failure</option>
                        <option value="payment">Payment Failure</option>
                        <option value="order">Order Creation Failure</option>
                        <option value="email">Email Failure</option>
                        <option value="sms">SMS Failure</option>
                    </select>
                </div>

                <button type="submit" id="processButton">
                    Process Order
                </button>

            </form>

            <section class="status-section">
                <h2>Execution Status</h2>

                <div id="currentStatus" class="current-status">
                    Waiting for an order.
                </div>

                <div id="executionLog" class="execution-log"></div>
            </section>

        </section>
    </main>

    <script src="app.js"></script>
</body>
</html>
```

### Explanation

The form collects customer, product, quantity, amount, and simulated failure information. The execution log displays the progress of every Promise operation.

---

## 6. Step 2: Create `style.css`

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    min-height: 100vh;
    padding: 30px;
    background: linear-gradient(135deg, #eff6ff, #f5f3ff);
    color: #111827;
    font-family: Arial, Helvetica, sans-serif;
}

.container {
    width: min(760px, 100%);
    margin: 0 auto;
}

.card {
    padding: 32px;
    background: white;
    border: 1px solid #e5e7eb;
    border-radius: 18px;
    box-shadow: 0 20px 45px rgba(15, 23, 42, 0.1);
}

.header {
    margin-bottom: 28px;
}

.label {
    display: block;
    margin-bottom: 5px;
    color: #2563eb;
    font-size: 12px;
    font-weight: bold;
    letter-spacing: 1px;
    text-transform: uppercase;
}

.header h1 {
    margin-bottom: 8px;
    font-size: 30px;
}

.header p {
    color: #6b7280;
    line-height: 1.6;
}

.form-group {
    margin-bottom: 18px;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
}

label {
    display: block;
    margin-bottom: 7px;
    color: #374151;
    font-size: 14px;
    font-weight: bold;
}

input,
select {
    width: 100%;
    height: 46px;
    padding: 0 13px;
    background: #f9fafb;
    border: 1px solid #d1d5db;
    border-radius: 8px;
    font-size: 14px;
    outline: none;
}

input:focus,
select:focus {
    background: white;
    border-color: #2563eb;
    box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.12);
}

button {
    width: 100%;
    height: 48px;
    background: #2563eb;
    color: white;
    border: none;
    border-radius: 8px;
    font-size: 15px;
    font-weight: bold;
    cursor: pointer;
}

button:hover {
    background: #1d4ed8;
}

button:disabled {
    background: #93c5fd;
    cursor: not-allowed;
}

.status-section {
    margin-top: 30px;
}

.status-section h2 {
    margin-bottom: 12px;
    font-size: 18px;
}

.current-status {
    margin-bottom: 15px;
    padding: 13px;
    background: #eff6ff;
    color: #1d4ed8;
    border-left: 4px solid #2563eb;
    border-radius: 6px;
    font-size: 14px;
    font-weight: bold;
}

.execution-log {
    min-height: 250px;
    max-height: 400px;
    padding: 18px;
    background: #111827;
    color: #f9fafb;
    border-radius: 10px;
    font-family: monospace;
    font-size: 13px;
    line-height: 1.8;
    overflow-y: auto;
}

.log-info {
    color: #93c5fd;
}

.log-success {
    color: #4ade80;
}

.log-error {
    color: #f87171;
}

.log-warning {
    color: #facc15;
}

@media (max-width: 600px) {
    body {
        padding: 15px;
    }

    .card {
        padding: 22px;
    }

    .form-row {
        grid-template-columns: 1fr;
        gap: 0;
    }

    .header h1 {
        font-size: 24px;
    }
}
```

---

## 7. Step 3: Understand a Basic Promise

```javascript
const promise = new Promise((resolve, reject) => {
    const operationSuccessful = true;

    if (operationSuccessful) {
        resolve("Operation completed");
    } else {
        reject("Operation failed");
    }
});
```

A Promise has three states:

```text
Pending   → Operation is still running
Fulfilled → Operation completed successfully
Rejected  → Operation failed
```

`resolve()` fulfills the Promise, while `reject()` rejects it.

---

## 8. Step 4: Read the HTML Elements

Add this code to `app.js`:

```javascript
"use strict";

const orderForm = document.getElementById("orderForm");
const customerNameInput = document.getElementById("customerName");
const productNameInput = document.getElementById("productName");
const quantityInput = document.getElementById("quantity");
const amountInput = document.getElementById("amount");
const failureStageInput = document.getElementById("failureStage");
const processButton = document.getElementById("processButton");
const currentStatus = document.getElementById("currentStatus");
const executionLog = document.getElementById("executionLog");
```

Each variable stores a reference to an HTML element.

---

## 9. Step 5: Create the Logging Function

```javascript
function addLog(message, type = "info") {
    const logEntry = document.createElement("div");

    logEntry.className = `log-${type}`;
    logEntry.textContent = message;

    executionLog.appendChild(logEntry);
    executionLog.scrollTop = executionLog.scrollHeight;
}
```

This function creates a new log entry and adds it to the browser page.

---

## 10. Step 6: Create a Delay Promise

```javascript
function delay(milliseconds) {
    return new Promise(resolve => {
        setTimeout(resolve, milliseconds);
    });
}
```

`setTimeout()` is asynchronous. When the timer completes, `resolve()` changes the Promise from pending to fulfilled.

---

## 11. Step 7: Collect Order Data

```javascript
function getOrderData() {
    return {
        customerName: customerNameInput.value.trim(),
        productName: productNameInput.value,
        quantity: Number(quantityInput.value),
        amount: Number(amountInput.value),
        failureStage: failureStageInput.value
    };
}
```

Example result:

```javascript
{
    customerName: "Abhinandan",
    productName: "Laptop",
    quantity: 1,
    amount: 75000,
    failureStage: "none"
}
```

---

## 12. Step 8: Validate the Order

```javascript
function validateOrder(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 1: Validating order details...", "info");

        setTimeout(() => {
            if (!order.customerName) {
                reject(new Error("Customer name is required."));
                return;
            }

            if (order.quantity <= 0) {
                reject(new Error("Quantity must be greater than zero."));
                return;
            }

            if (order.amount <= 0) {
                reject(new Error("Amount must be greater than zero."));
                return;
            }

            addLog("Order validation completed.", "success");
            resolve(order);
        }, 800);
    });
}
```

### Explanation

- The Promise starts in the pending state.
- Invalid data calls `reject()`.
- Valid data calls `resolve(order)`.
- The resolved order is passed to the next `.then()`.

---

## 13. Step 9: Check Inventory

```javascript
function checkInventory(order) {
    return new Promise((resolve, reject) => {
        addLog(
            `Step 2: Checking inventory for ${order.productName}...`,
            "info"
        );

        setTimeout(() => {
            if (order.failureStage === "inventory") {
                reject(
                    new Error(
                        `${order.productName} is currently out of stock.`
                    )
                );
                return;
            }

            const availableQuantity = 10;

            if (order.quantity > availableQuantity) {
                reject(
                    new Error(
                        `Only ${availableQuantity} units are available.`
                    )
                );
                return;
            }

            addLog(`${order.productName} is available.`, "success");

            resolve({
                ...order,
                inventoryConfirmed: true
            });
        }, 1200);
    });
}
```

The spread operator copies the existing order properties and adds `inventoryConfirmed`.

---

## 14. Step 10: Process Payment

```javascript
function processPayment(order) {
    return new Promise((resolve, reject) => {
        addLog(
            `Step 3: Processing payment of ₹${order.amount}...`,
            "info"
        );

        setTimeout(() => {
            if (order.failureStage === "payment") {
                reject(new Error("Payment was declined by the bank."));
                return;
            }

            const paymentId = `PAY-${Date.now()}`;

            addLog(
                `Payment successful. Payment ID: ${paymentId}`,
                "success"
            );

            resolve({
                ...order,
                paymentId,
                paymentStatus: "Paid"
            });
        }, 1500);
    });
}
```

The resolved object contains the original order and payment information.

---

## 15. Step 11: Create the Order

```javascript
function createOrder(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 4: Creating order...", "info");

        setTimeout(() => {
            if (order.failureStage === "order") {
                reject(new Error("The order service is unavailable."));
                return;
            }

            const orderId = `ORD-${Date.now()}`;

            const createdOrder = {
                ...order,
                orderId,
                orderStatus: "Confirmed",
                createdAt: new Date().toISOString()
            };

            addLog(
                `Order created successfully. Order ID: ${orderId}`,
                "success"
            );

            resolve(createdOrder);
        }, 1200);
    });
}
```

---

## 16. Step 12: Send Email

```javascript
function sendEmail(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 5A: Sending confirmation email...", "info");

        setTimeout(() => {
            if (order.failureStage === "email") {
                reject(new Error("Email notification failed."));
                return;
            }

            addLog("Confirmation email sent.", "success");

            resolve({
                service: "Email",
                status: "Sent"
            });
        }, 1000);
    });
}
```

---

## 17. Step 13: Send SMS

```javascript
function sendSms(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 5B: Sending confirmation SMS...", "info");

        setTimeout(() => {
            if (order.failureStage === "sms") {
                reject(new Error("SMS notification failed."));
                return;
            }

            addLog("Confirmation SMS sent.", "success");

            resolve({
                service: "SMS",
                status: "Sent"
            });
        }, 1300);
    });
}
```

Email and SMS can run in parallel because they do not depend on each other.

---

## 18. Step 14: Run Notifications in Parallel

```javascript
function sendNotifications(order) {
    addLog(
        "Step 5: Starting notifications in parallel...",
        "info"
    );

    return Promise.allSettled([
        sendEmail(order),
        sendSms(order)
    ]).then(notificationResults => {
        notificationResults.forEach(result => {
            if (result.status === "fulfilled") {
                addLog(
                    `${result.value.service} notification completed.`,
                    "success"
                );
            }

            if (result.status === "rejected") {
                addLog(result.reason.message, "warning");
            }
        });

        return {
            ...order,
            notificationResults
        };
    });
}
```

### Why use `Promise.allSettled()`?

It waits for all Promises and reports every result, even when one notification fails.

---

## 19. Step 15: Create the Promise Chain

```javascript
orderForm.addEventListener("submit", handleOrderSubmission);

function handleOrderSubmission(event) {
    event.preventDefault();

    executionLog.innerHTML = "";

    const order = getOrderData();

    processButton.disabled = true;
    processButton.textContent = "Processing Order...";
    currentStatus.textContent = "Order processing started.";

    addLog("Order processing started.", "info");

    validateOrder(order)
        .then(validatedOrder => {
            return checkInventory(validatedOrder);
        })
        .then(inventoryConfirmedOrder => {
            return processPayment(inventoryConfirmedOrder);
        })
        .then(paidOrder => {
            return createOrder(paidOrder);
        })
        .then(createdOrder => {
            return sendNotifications(createdOrder);
        })
        .then(finalOrder => {
            currentStatus.textContent =
                `Order ${finalOrder.orderId} completed successfully.`;

            addLog("Entire order workflow completed.", "success");
            console.log("Final order:", finalOrder);
        })
        .catch(error => {
            currentStatus.textContent = "Order processing failed.";
            addLog(`Error: ${error.message}`, "error");
            console.error("Order error:", error);
        })
        .finally(() => {
            processButton.disabled = false;
            processButton.textContent = "Process Order";
            addLog("Promise workflow finished.", "info");
        });
}
```

---

## 20. Complete `app.js`

```javascript
"use strict";

const orderForm = document.getElementById("orderForm");
const customerNameInput = document.getElementById("customerName");
const productNameInput = document.getElementById("productName");
const quantityInput = document.getElementById("quantity");
const amountInput = document.getElementById("amount");
const failureStageInput = document.getElementById("failureStage");
const processButton = document.getElementById("processButton");
const currentStatus = document.getElementById("currentStatus");
const executionLog = document.getElementById("executionLog");

function addLog(message, type = "info") {
    const logEntry = document.createElement("div");
    logEntry.className = `log-${type}`;
    logEntry.textContent = message;
    executionLog.appendChild(logEntry);
    executionLog.scrollTop = executionLog.scrollHeight;
}

function delay(milliseconds) {
    return new Promise(resolve => {
        setTimeout(resolve, milliseconds);
    });
}

function getOrderData() {
    return {
        customerName: customerNameInput.value.trim(),
        productName: productNameInput.value,
        quantity: Number(quantityInput.value),
        amount: Number(amountInput.value),
        failureStage: failureStageInput.value
    };
}

function validateOrder(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 1: Validating order details...", "info");

        setTimeout(() => {
            if (!order.customerName) {
                reject(new Error("Customer name is required."));
                return;
            }

            if (order.quantity <= 0) {
                reject(new Error("Quantity must be greater than zero."));
                return;
            }

            if (order.amount <= 0) {
                reject(new Error("Amount must be greater than zero."));
                return;
            }

            addLog("Order validation completed.", "success");
            resolve(order);
        }, 800);
    });
}

function checkInventory(order) {
    return new Promise((resolve, reject) => {
        addLog(
            `Step 2: Checking inventory for ${order.productName}...`,
            "info"
        );

        setTimeout(() => {
            if (order.failureStage === "inventory") {
                reject(
                    new Error(
                        `${order.productName} is currently out of stock.`
                    )
                );
                return;
            }

            const availableQuantity = 10;

            if (order.quantity > availableQuantity) {
                reject(
                    new Error(
                        `Only ${availableQuantity} units are available.`
                    )
                );
                return;
            }

            addLog(`${order.productName} is available.`, "success");

            resolve({
                ...order,
                inventoryConfirmed: true
            });
        }, 1200);
    });
}

function processPayment(order) {
    return new Promise((resolve, reject) => {
        addLog(
            `Step 3: Processing payment of ₹${order.amount}...`,
            "info"
        );

        setTimeout(() => {
            if (order.failureStage === "payment") {
                reject(new Error("Payment was declined by the bank."));
                return;
            }

            const paymentId = `PAY-${Date.now()}`;

            addLog(
                `Payment successful. Payment ID: ${paymentId}`,
                "success"
            );

            resolve({
                ...order,
                paymentId,
                paymentStatus: "Paid"
            });
        }, 1500);
    });
}

function createOrder(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 4: Creating order...", "info");

        setTimeout(() => {
            if (order.failureStage === "order") {
                reject(new Error("The order service is unavailable."));
                return;
            }

            const orderId = `ORD-${Date.now()}`;

            const createdOrder = {
                ...order,
                orderId,
                orderStatus: "Confirmed",
                createdAt: new Date().toISOString()
            };

            addLog(
                `Order created successfully. Order ID: ${orderId}`,
                "success"
            );

            resolve(createdOrder);
        }, 1200);
    });
}

function sendEmail(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 5A: Sending confirmation email...", "info");

        setTimeout(() => {
            if (order.failureStage === "email") {
                reject(new Error("Email notification failed."));
                return;
            }

            addLog("Confirmation email sent.", "success");

            resolve({
                service: "Email",
                status: "Sent"
            });
        }, 1000);
    });
}

function sendSms(order) {
    return new Promise((resolve, reject) => {
        addLog("Step 5B: Sending confirmation SMS...", "info");

        setTimeout(() => {
            if (order.failureStage === "sms") {
                reject(new Error("SMS notification failed."));
                return;
            }

            addLog("Confirmation SMS sent.", "success");

            resolve({
                service: "SMS",
                status: "Sent"
            });
        }, 1300);
    });
}

function sendNotifications(order) {
    addLog(
        "Step 5: Starting notifications in parallel...",
        "info"
    );

    return Promise.allSettled([
        sendEmail(order),
        sendSms(order)
    ]).then(notificationResults => {
        notificationResults.forEach(result => {
            if (result.status === "fulfilled") {
                addLog(
                    `${result.value.service} notification completed.`,
                    "success"
                );
            }

            if (result.status === "rejected") {
                addLog(result.reason.message, "warning");
            }
        });

        return {
            ...order,
            notificationResults
        };
    });
}

orderForm.addEventListener("submit", handleOrderSubmission);

function handleOrderSubmission(event) {
    event.preventDefault();

    executionLog.innerHTML = "";

    const order = getOrderData();

    processButton.disabled = true;
    processButton.textContent = "Processing Order...";
    currentStatus.textContent = "Order processing started.";

    addLog("Order processing started.", "info");

    validateOrder(order)
        .then(checkInventory)
        .then(processPayment)
        .then(createOrder)
        .then(sendNotifications)
        .then(finalOrder => {
            currentStatus.textContent =
                `Order ${finalOrder.orderId} completed successfully.`;

            addLog("Entire order workflow completed.", "success");
            console.log("Final order:", finalOrder);
        })
        .catch(error => {
            currentStatus.textContent = "Order processing failed.";
            addLog(`Error: ${error.message}`, "error");
            console.error("Order error:", error);
        })
        .finally(() => {
            processButton.disabled = false;
            processButton.textContent = "Process Order";
            addLog("Promise workflow finished.", "info");
        });
}
```

---

## 21. Understanding `.then()`

`.then()` handles a fulfilled Promise.

```javascript
validateOrder(order)
    .then(result => {
        console.log(result);
    });
```

The value passed to `resolve()` becomes the parameter received by `.then()`.

---

## 22. Understanding `.catch()`

`.catch()` handles rejected Promises.

```javascript
.catch(error => {
    console.error(error.message);
});
```

If payment fails, order creation and notifications are skipped.

```text
Validation       → Successful
Inventory        → Successful
Payment          → Failed
Order creation   → Skipped
Notifications    → Skipped
catch()          → Executed
finally()        → Executed
```

---

## 23. Understanding `.finally()`

`.finally()` executes whether the Promise succeeds or fails.

```javascript
.finally(() => {
    processButton.disabled = false;
});
```

Common uses:

- Hide loading indicators
- Enable buttons
- Release resources
- Perform cleanup

---

## 24. Error Propagation

```javascript
validateOrder(order)
    .then(checkInventory)
    .then(processPayment)
    .then(createOrder)
    .catch(handleError);
```

If `checkInventory()` rejects, the error moves down the chain until `.catch()` handles it.

---

## 25. Convert the Workflow to `async` and `await`

```javascript
async function handleOrderSubmission(event) {
    event.preventDefault();

    executionLog.innerHTML = "";

    const order = getOrderData();

    processButton.disabled = true;
    processButton.textContent = "Processing Order...";
    currentStatus.textContent = "Order processing started.";

    addLog("Order processing started.", "info");

    try {
        const validatedOrder =
            await validateOrder(order);

        const inventoryConfirmedOrder =
            await checkInventory(validatedOrder);

        const paidOrder =
            await processPayment(inventoryConfirmedOrder);

        const createdOrder =
            await createOrder(paidOrder);

        const finalOrder =
            await sendNotifications(createdOrder);

        currentStatus.textContent =
            `Order ${finalOrder.orderId} completed successfully.`;

        addLog("Entire order workflow completed.", "success");
        console.log("Final order:", finalOrder);
    } catch (error) {
        currentStatus.textContent = "Order processing failed.";
        addLog(`Error: ${error.message}`, "error");
        console.error("Order error:", error);
    } finally {
        processButton.disabled = false;
        processButton.textContent = "Process Order";
        addLog("Promise workflow finished.", "info");
    }
}
```

`async/await` does not replace Promises. It provides cleaner syntax for consuming them.

---

## 26. `Promise.all()` Demo

Use it when all operations must succeed.

```javascript
Promise.all([
    sendEmail(order),
    sendSms(order)
])
    .then(results => {
        console.log(results);
    })
    .catch(error => {
        console.error(error);
    });
```

If one Promise rejects, `Promise.all()` rejects.

---

## 27. `Promise.allSettled()` Demo

Use it when every result must be collected, even if some operations fail.

```javascript
Promise.allSettled([
    sendEmail(order),
    sendSms(order)
])
    .then(results => {
        console.log(results);
    });
```

---

## 28. `Promise.race()` Demo

`Promise.race()` settles with the first Promise that settles.

```javascript
const serverOne = new Promise(resolve => {
    setTimeout(() => {
        resolve("Server One responded");
    }, 1000);
});

const serverTwo = new Promise(resolve => {
    setTimeout(() => {
        resolve("Server Two responded");
    }, 1500);
});

Promise.race([
    serverOne,
    serverTwo
])
    .then(result => {
        console.log(result);
    });
```

---

## 29. `Promise.any()` Demo

`Promise.any()` returns the first fulfilled Promise.

```javascript
const firstServer =
    Promise.reject("First server failed");

const secondServer = new Promise(resolve => {
    setTimeout(() => {
        resolve("Second server succeeded");
    }, 1000);
});

Promise.any([
    firstServer,
    secondServer
])
    .then(result => {
        console.log(result);
    });
```

---

## 30. Testing Scenarios

### Successful order

```text
No Failure
```

Expected:

```text
Validation completed
Inventory available
Payment successful
Order created
Email sent
SMS sent
Workflow completed
```

### Inventory failure

```text
Validation completed
Inventory failed
Payment skipped
Order creation skipped
Notifications skipped
catch() executed
finally() executed
```

### Payment failure

```text
Validation completed
Inventory available
Payment failed
Order creation skipped
Notifications skipped
catch() executed
finally() executed
```

### Email failure

```text
Order created
Email failed
SMS succeeded
Overall workflow completed
```

The final scenario succeeds because notifications use `Promise.allSettled()`.

---

## 31. Important Promise Rules

### Rule 1: A Promise settles only once

```javascript
new Promise((resolve, reject) => {
    resolve("Success");
    reject("Failure");
});
```

The first call wins.

### Rule 2: Return dependent Promises

Correct:

```javascript
.then(order => {
    return processPayment(order);
})
```

Incorrect:

```javascript
.then(order => {
    processPayment(order);
})
```

### Rule 3: Throw errors to reject a chain

```javascript
.then(result => {
    if (!result) {
        throw new Error("Result was not found");
    }

    return result;
})
```

### Rule 4: Use `.finally()` for cleanup

```javascript
.finally(() => {
    loading = false;
});
```

### Rule 5: `fetch()` returns a Promise

```javascript
fetch("http://localhost:3000/orders")
    .then(response => {
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        return response.json();
    })
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error(error);
    });
```

---

## 32. Assignment Extensions

1. Add customer email and mobile number.
2. Add product-price calculation.
3. Add tax calculation using a Promise.
4. Add discount validation.
5. Add delivery-service allocation.
6. Add delivery-date calculation.
7. Save the final order to JSON Server.
8. Fetch products from JSON Server.
9. Add a loading spinner.
10. Add cancellation and refund Promises.
11. Use `Promise.race()` to implement payment timeout.
12. Compare Promise chaining with `async/await`.

---

## 33. Review Questions

1. What is a JavaScript Promise?
2. What are the three Promise states?
3. What is the role of `resolve()`?
4. What is the role of `reject()`?
5. Why should dependent Promises be returned from `.then()`?
6. What is Promise chaining?
7. What is error propagation?
8. When does `.finally()` execute?
9. What is the difference between `Promise.all()` and `Promise.allSettled()`?
10. What is the difference between `Promise.race()` and `Promise.any()`?
11. What does an `async` function return?
12. What happens when an awaited Promise rejects?
13. How does `fetch()` use Promises?
14. Can a Promise be fulfilled more than once?
15. When should Promises run in parallel?

---

## 34. Final Summary

Successful workflow:

```text
validateOrder()
        ↓
checkInventory()
        ↓
processPayment()
        ↓
createOrder()
        ↓
Promise.allSettled([
    sendEmail(),
    sendSms()
])
        ↓
Final order result
```

Error workflow:

```text
An important step rejects
        ↓
Dependent steps are skipped
        ↓
catch() handles the error
        ↓
finally() performs cleanup
```

This case study demonstrates how JavaScript Promises organize asynchronous operations into a readable, controlled, and maintainable workflow.

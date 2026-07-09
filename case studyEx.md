# Case Study: Ecommerce Order Management System

## 1. Case Study Objective

Build an ecommerce order management module where a customer can place an order, view order details, and track expected delivery.

The main purpose of this case study is to understand:

* Java package organization
* Layered architecture
* DTO class usage
* Explicit constructor usage
* LocalDate usage in real business scenarios

---

## 2. Business Scenario

An ecommerce company wants to create a backend module for handling customer orders.

When a customer places an order, the system should:

1. Accept customer and product details.
2. Calculate order information.
3. Store order details.
4. Generate an expected delivery date.
5. Return a clean response to the client using DTOs.

---

## 3. Main Functional Requirements

| Requirement ID | Requirement                                                                    |
| -------------- | ------------------------------------------------------------------------------ |
| FR-01          | Customer should be able to place an order                                      |
| FR-02          | System should store order details                                              |
| FR-03          | System should capture order date using LocalDate                               |
| FR-04          | System should calculate expected delivery date                                 |
| FR-05          | System should return order response using DTO                                  |
| FR-06          | System should separate controller, service, repository, entity, and DTO layers |

---

## 4. Suggested Package Structure

The application should be organized using proper packages.

```text
com.ecommerce
│
├── controller
│   └── OrderController
│
├── service
│   ├── OrderService
│   └── OrderServiceImpl
│
├── repository
│   └── OrderRepository
│
├── entity
│   ├── Order
│   ├── Customer
│   └── Product
│
├── dto
│   ├── OrderRequestDTO
│   └── OrderResponseDTO
│
├── exception
│   ├── OrderNotFoundException
│   └── GlobalExceptionHandler
│
└── util
    └── DeliveryDateCalculator
```

---

## 5. Why Packages Are Used

Packages help to organize classes based on their responsibility.

| Package    | Purpose                                   |
| ---------- | ----------------------------------------- |
| controller | Handles incoming API requests             |
| service    | Contains business logic                   |
| repository | Handles database communication            |
| entity     | Represents database tables                |
| dto        | Transfers data between client and backend |
| exception  | Handles application errors                |
| util       | Contains reusable helper logic            |

---

## 6. Layered Architecture Explanation

The ecommerce order module should follow layered architecture.

```text
Client / UI
   ↓
Controller Layer
   ↓
Service Layer
   ↓
Repository Layer
   ↓
Database
```

---

## 7. Responsibility of Each Layer

### 7.1 Controller Layer

The controller layer receives requests from the client.

Example responsibility:

* Accept order placement request
* Call service layer
* Return response DTO to client

The controller should not contain business logic.

---

### 7.2 Service Layer

The service layer contains the actual business logic.

Example responsibility:

* Validate customer details
* Validate product availability
* Calculate order date
* Calculate expected delivery date
* Prepare order entity
* Convert entity to response DTO

---

### 7.3 Repository Layer

The repository layer communicates with the database.

Example responsibility:

* Save order details
* Find order by ID
* Fetch customer orders

---

### 7.4 Entity Layer

The entity layer represents database tables.

Example entities:

| Entity   | Purpose                     |
| -------- | --------------------------- |
| Customer | Stores customer information |
| Product  | Stores product information  |
| Order    | Stores order information    |

---

### 7.5 DTO Layer

DTO means **Data Transfer Object**.

DTOs are used to transfer data between client and server without exposing internal entity structure.

---

## 8. Why DTO Is Needed

In a real ecommerce system, entity classes may contain sensitive or unnecessary data.

For example, the Order entity may contain:

* Internal database ID
* Customer internal reference
* Product cost price
* Audit fields
* Database-related fields

The client does not need all this information.

So, DTOs are used to expose only required data.

---

## 9. DTO Classes in This Case Study

### 9.1 OrderRequestDTO

This DTO is used when the customer places an order.

Suggested fields:

| Field           | Purpose                                 |
| --------------- | --------------------------------------- |
| customerId      | Identifies the customer                 |
| productId       | Identifies the product                  |
| quantity        | Number of items ordered                 |
| deliveryAddress | Address where order should be delivered |

---

### 9.2 OrderResponseDTO

This DTO is returned after successful order placement.

Suggested fields:

| Field                | Purpose                        |
| -------------------- | ------------------------------ |
| orderId              | Generated order ID             |
| customerName         | Name of customer               |
| productName          | Ordered product name           |
| quantity             | Ordered quantity               |
| orderDate            | Date on which order was placed |
| expectedDeliveryDate | Expected delivery date         |
| orderStatus          | Current order status           |
| totalAmount          | Total order amount             |

---

## 10. Explicit Constructor Usage

In this case study, explicit constructors should be used instead of relying only on default constructors or Lombok.

### Why explicit constructors are useful

Explicit constructors help to:

* Initialize object values clearly
* Avoid incomplete object creation
* Improve readability
* Make DTO creation controlled
* Help beginners understand object creation properly

---

## 11. Where Explicit Constructors Should Be Used

| Class            | Constructor Usage                          |
| ---------------- | ------------------------------------------ |
| OrderRequestDTO  | Constructor to initialize request data     |
| OrderResponseDTO | Constructor to initialize response data    |
| Order Entity     | Constructor to initialize order details    |
| Customer Entity  | Constructor to initialize customer details |
| Product Entity   | Constructor to initialize product details  |

---

## 12. Example Constructor Design Without Code

### OrderRequestDTO Constructor

The constructor should accept:

* customerId
* productId
* quantity
* deliveryAddress

Purpose:

To create an order request object with all required input values.

---

### OrderResponseDTO Constructor

The constructor should accept:

* orderId
* customerName
* productName
* quantity
* orderDate
* expectedDeliveryDate
* orderStatus
* totalAmount

Purpose:

To return a clean response after order placement.

---

### Order Entity Constructor

The constructor should accept:

* customer
* product
* quantity
* orderDate
* expectedDeliveryDate
* orderStatus
* totalAmount

Purpose:

To create a valid order object before saving it into the database.

---

## 13. LocalDate Usage in This Case Study

LocalDate should be used to handle date-only values.

In ecommerce, many business dates do not need time.

Examples:

| Field                | Data Type | Purpose                               |
| -------------------- | --------- | ------------------------------------- |
| orderDate            | LocalDate | Date when order is placed             |
| expectedDeliveryDate | LocalDate | Date when order is expected to arrive |
| returnWindowEndDate  | LocalDate | Last date to return the product       |
| invoiceDate          | LocalDate | Date when invoice is generated        |

---

## 14. Why LocalDate Is Better Here

LocalDate is suitable because:

* Order date does not always require time
* Delivery date is usually shown as a date only
* Return policy is calculated using days
* It avoids unnecessary time-zone complexity

Example business logic:

```text
orderDate = current date
expectedDeliveryDate = orderDate + 5 days
returnWindowEndDate = deliveryDate + 7 days
```

No source code is required for this logic during design explanation.

---

## 15. Ecommerce Order Placement Flow

### Step 1: Customer Sends Order Request

The customer provides:

* Customer ID
* Product ID
* Quantity
* Delivery address

This request is captured using `OrderRequestDTO`.

---

### Step 2: Controller Receives Request

The controller receives the request and forwards it to the service layer.

The controller should not calculate price or delivery date.

---

### Step 3: Service Validates Customer

The service checks whether the customer exists.

If the customer does not exist, the service should throw a customer-related exception.

---

### Step 4: Service Validates Product

The service checks whether the product exists and whether stock is available.

If the product is not available, the service should return a meaningful error.

---

### Step 5: Service Calculates Total Amount

The service calculates the total amount using:

```text
totalAmount = product price × quantity
```

---

### Step 6: Service Uses LocalDate for Order Date

The service captures the current date as the order date.

Example:

```text
orderDate = today’s date
```

This should be stored using LocalDate.

---

### Step 7: Service Calculates Expected Delivery Date

The service calculates expected delivery date based on business rules.

Example:

```text
expectedDeliveryDate = orderDate + 5 days
```

For premium delivery:

```text
expectedDeliveryDate = orderDate + 2 days
```

For standard delivery:

```text
expectedDeliveryDate = orderDate + 5 days
```

---

### Step 8: Service Creates Order Entity

The service creates an Order entity using an explicit constructor.

The Order entity should contain:

* Customer reference
* Product reference
* Quantity
* Order date
* Expected delivery date
* Total amount
* Order status

---

### Step 9: Repository Saves Order

The repository saves the Order entity into the database.

The saved order receives a generated order ID.

---

### Step 10: Service Creates Response DTO

After saving the order, the service creates `OrderResponseDTO`.

The response DTO should contain only the data required by the client.

---

### Step 11: Controller Returns Response

The controller returns the response DTO to the client.

The client receives details such as:

* Order ID
* Product name
* Order date
* Expected delivery date
* Total amount
* Order status

---

## 16. Sample Order Request Data

```text
customerId: 101
productId: 501
quantity: 2
deliveryAddress: Pune, Maharashtra
```

---

## 17. Sample Order Response Data

```text
orderId: 9001
customerName: Abhi
productName: Wireless Mouse
quantity: 2
orderDate: 2026-07-09
expectedDeliveryDate: 2026-07-14
orderStatus: PLACED
totalAmount: 1600
```

---

## 18. Database Table Design

### Customer Table

| Column        | Purpose                |
| ------------- | ---------------------- |
| customer_id   | Unique customer ID     |
| customer_name | Name of customer       |
| email         | Customer email         |
| mobile        | Customer mobile number |

---

### Product Table

| Column         | Purpose           |
| -------------- | ----------------- |
| product_id     | Unique product ID |
| product_name   | Product name      |
| price          | Product price     |
| stock_quantity | Available stock   |

---

### Order Table

| Column                 | Purpose                |
| ---------------------- | ---------------------- |
| order_id               | Unique order ID        |
| customer_id            | Customer reference     |
| product_id             | Product reference      |
| quantity               | Ordered quantity       |
| order_date             | Date of order          |
| expected_delivery_date | Expected delivery date |
| order_status           | Current order status   |
| total_amount           | Total order amount     |

---

## 19. Step-by-Step Implementation Plan

### Step 1: Create Main Project

Create a Java ecommerce backend project.

Project name example:

```text
ecommerce-order-management
```

---

### Step 2: Create Base Package

Create the base package:

```text
com.ecommerce
```

All other packages should be created inside this base package.

---

### Step 3: Create Layer-Based Packages

Create the following packages:

```text
controller
service
repository
entity
dto
exception
util
```

Each package should contain only related classes.

---

### Step 4: Create Entity Classes

Create entity classes for:

* Customer
* Product
* Order

These classes represent database tables.

Use explicit constructors to initialize important fields.

---

### Step 5: Create DTO Classes

Create DTO classes for:

* OrderRequestDTO
* OrderResponseDTO

The request DTO should receive data from the client.

The response DTO should return data to the client.

---

### Step 6: Add Explicit Constructors

Add explicit constructors in DTO and entity classes.

Avoid depending only on no-argument constructors.

The constructor should clearly show what data is required to create the object.

---

### Step 7: Add LocalDate Fields

Use LocalDate for:

* orderDate
* expectedDeliveryDate
* returnWindowEndDate, if return feature is added later

---

### Step 8: Create Repository Layer

Create repositories for:

* Customer
* Product
* Order

The repository layer should perform database operations.

---

### Step 9: Create Service Interface

Create an order service interface.

It should define business operations such as:

* placeOrder
* getOrderById
* getOrdersByCustomerId

---

### Step 10: Create Service Implementation

Create service implementation class.

This class should contain the actual order processing logic.

Important logic:

* Validate customer
* Validate product
* Check stock
* Calculate total amount
* Set order date using LocalDate
* Calculate expected delivery date
* Save order
* Prepare response DTO

---

### Step 11: Create Controller

Create an order controller.

The controller should expose APIs such as:

| API Action          | Purpose                      |
| ------------------- | ---------------------------- |
| Place Order         | Customer places new order    |
| Get Order by ID     | Customer views order details |
| Get Customer Orders | Customer views order history |

---

### Step 12: Add Exception Handling

Create custom exceptions for:

* Customer not found
* Product not found
* Order not found
* Insufficient stock

Use a global exception handler to return clean error responses.

---

### Step 13: Test Order Placement Flow

Test the order placement flow with sample data.

Verify:

* Order is saved
* Order date is generated correctly
* Expected delivery date is calculated correctly
* Response DTO contains correct data

---

### Step 14: Test Error Scenarios

Test the following cases:

| Scenario                    | Expected Result          |
| --------------------------- | ------------------------ |
| Invalid customer ID         | Customer not found error |
| Invalid product ID          | Product not found error  |
| Quantity greater than stock | Insufficient stock error |
| Invalid order ID            | Order not found error    |

---

## 20. Final Flow Summary

```text
OrderRequestDTO
      ↓
OrderController
      ↓
OrderService
      ↓
Business Logic
      ↓
Order Entity
      ↓
OrderRepository
      ↓
Database
      ↓
OrderResponseDTO
      ↓
Client
```

---

## 21. Key Learning Outcomes

After completing this case study, learners should understand:

* How to organize Java classes using packages
* Why layered architecture is important
* How controller, service, repository, entity, and DTO layers work together
* Why DTOs are used instead of exposing entities directly
* How explicit constructors help in object creation
* Where LocalDate is useful in ecommerce applications
* How to design a clean order placement flow without mixing responsibilities

---


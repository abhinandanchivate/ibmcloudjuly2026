# Product Catalog and Inventory Management REST API

## 1. Case Study Overview

Design and develop a RESTful backend application for a Product Catalog and Inventory Management System using:

- Node.js
- Express.js
- MongoDB
- Mongoose
- REST API principles
- Postman

The system should allow administrators and inventory teams to manage products, categories, pricing, stock, availability, supplier information, discounts, and inventory status.

The backend should expose REST APIs that can later be consumed by a web frontend, mobile application, or e-commerce system.

No frontend implementation is required as part of this case study.

---

# 2. Business Scenario

An e-commerce organization manages hundreds of products across multiple categories.

Currently, product details are maintained using spreadsheets and separate inventory files.

This creates several problems:

- Product information is duplicated.
- Pricing is inconsistent.
- Stock levels are difficult to monitor.
- Inactive products still appear in catalogs.
- Discounts are sometimes applied incorrectly.
- Product codes are duplicated.
- Products are created without mandatory information.
- Expired products remain active.
- Selling prices are sometimes lower than procurement cost.
- Inventory teams cannot easily identify low-stock products.
- Invalid stock values are sometimes entered.
- Error responses from existing systems are inconsistent.

The organization wants to build a centralized Product Catalog and Inventory REST API.

The application should provide complete CRUD operations while enforcing complex business rules and standardized custom error handling.

---

# 3. Project Objectives

The backend application should support:

- Create product
- Retrieve all products
- Retrieve product by ID
- Update complete product
- Partially update product
- Delete product
- Search products
- Filter products
- Sort products
- Paginate product results
- Manage stock
- Manage pricing
- Manage discounts
- Track product status
- Detect low-stock products
- Detect expired products
- Validate business rules
- Handle custom application errors
- Return standardized API responses

---

# 4. Technology Stack

## Backend

- Node.js
- Express.js
- JavaScript

## Database

- MongoDB

## ODM

- Mongoose

## API Testing

- Postman

## Development Tools

- Visual Studio Code
- MongoDB Compass
- npm

---

# 5. High-Level Architecture

The application should follow layered architecture.

```text
Client
   |
   v
REST API
   |
   v
Router
   |
   v
Controller
   |
   v
Service
   |
   v
Model / Repository
   |
   v
MongoDB
```

Recommended request flow:

```text
HTTP Request
     |
     v
Express Router
     |
     v
Product Controller
     |
     v
Product Service
     |
     v
Product Model
     |
     v
MongoDB
     |
     v
HTTP Response
```

---

# 6. Recommended Project Structure

```text
product-management-api/
│
├── config/
│   └── database configuration
│
├── controllers/
│   └── product controller
│
├── services/
│   └── product service
│
├── models/
│   └── product model
│
├── routes/
│   └── product routes
│
├── errors/
│   ├── base application error
│   └── custom product errors
│
├── middleware/
│   ├── validation middleware
│   ├── route-not-found middleware
│   └── global error middleware
│
├── utils/
│   └── utility functions
│
├── app.js
├── server.js
├── .env
├── .gitignore
└── package.json
```

---

# 7. Product Entity Requirements

Each product should contain:

| Field | Description |
|---|---|
| id | Unique MongoDB identifier |
| productCode | Unique business product code |
| name | Product name |
| description | Product description |
| category | Product category |
| brand | Product brand |
| supplierName | Supplier name |
| costPrice | Procurement cost |
| sellingPrice | Selling price |
| discountPercent | Discount percentage |
| stockQuantity | Current available stock |
| reorderLevel | Minimum safe stock level |
| unit | Unit of measurement |
| status | Product status |
| manufacturedDate | Manufacturing date |
| expiryDate | Expiry date when applicable |
| createdAt | Product creation timestamp |
| updatedAt | Last modification timestamp |

---

# 8. Supported Product Categories

The application should support:

- Electronics
- Grocery
- Fashion
- Home Appliances
- Books
- Personal Care
- Sports
- Office Supplies
- Other

---

# 9. Product Status Values

Supported statuses:

- Active
- Inactive
- Discontinued
- Out of Stock

---

# 10. Units of Measurement

Supported units may include:

- Piece
- Box
- Pack
- Kg
- Gram
- Liter
- Milliliter

---

# 11. REST API Base URL

```text
http://localhost:3000/api/products
```

---

# 12. REST API Operations

| Operation | HTTP Method | Endpoint |
|---|---|---|
| Create product | POST | `/api/products` |
| Get all products | GET | `/api/products` |
| Get product by ID | GET | `/api/products/{id}` |
| Replace product | PUT | `/api/products/{id}` |
| Partial update | PATCH | `/api/products/{id}` |
| Delete product | DELETE | `/api/products/{id}` |

---

# 13. Create Product

## Endpoint

```text
POST /api/products
```

The request should contain:

- Product code
- Product name
- Description
- Category
- Brand
- Supplier name
- Cost price
- Selling price
- Discount percentage
- Stock quantity
- Reorder level
- Unit
- Status
- Manufacturing date
- Expiry date when applicable

The application should:

1. Receive product data.
2. Validate mandatory fields.
3. Validate field formats.
4. Validate product code uniqueness.
5. Validate pricing rules.
6. Validate discount rules.
7. Validate stock.
8. Validate dates.
9. Apply category-specific validations.
10. Store the product in MongoDB.
11. Return the created product.

Expected status:

```text
201 Created
```

---

# 14. Get All Products

## Endpoint

```text
GET /api/products
```

The API should support:

- Search
- Filtering
- Sorting
- Pagination

Expected status:

```text
200 OK
```

If no products are available, return an empty collection instead of an error.

---

# 15. Get Product By ID

## Endpoint

```text
GET /api/products/{productId}
```

The application should:

1. Validate the MongoDB ID.
2. Search for the product.
3. Return the product when found.
4. Return a custom not-found error when the product does not exist.

---

# 16. Update Complete Product

## Endpoint

```text
PUT /api/products/{productId}
```

The request should replace all editable product information.

All creation-related validations should be re-applied where relevant.

---

# 17. Partial Product Update

## Endpoint

```text
PATCH /api/products/{productId}
```

The application should allow selected fields to be updated.

Examples:

- Selling price
- Discount
- Stock
- Status
- Supplier
- Reorder level
- Expiry date

Business validations should also run for PATCH requests.

---

# 18. Delete Product

## Endpoint

```text
DELETE /api/products/{productId}
```

The API should:

1. Validate product ID.
2. Check whether the product exists.
3. Apply deletion business rules.
4. Delete or reject the operation.
5. Return an appropriate response.

---

# 19. Search Product

Example:

```text
GET /api/products?search=laptop
```

Search should work on:

- Product name
- Product code
- Brand
- Category
- Supplier

---

# 20. Filter By Category

```text
GET /api/products?category=Electronics
```

---

# 21. Filter By Status

```text
GET /api/products?status=Active
```

---

# 22. Filter By Brand

```text
GET /api/products?brand=Samsung
```

---

# 23. Filter By Price Range

```text
GET /api/products?minPrice=1000&maxPrice=50000
```

The API should return products whose selling price falls within the requested range.

---

# 24. Filter By Stock Status

Supported stock statuses:

```text
inStock
lowStock
outOfStock
```

Example:

```text
GET /api/products?stockStatus=lowStock
```

A product should be considered low stock when:

```text
stockQuantity <= reorderLevel
```

---

# 25. Combined Filtering

Example:

```text
GET /api/products?category=Electronics&status=Active&brand=Samsung
```

Example:

```text
GET /api/products?stockStatus=lowStock&category=Grocery
```

---

# 26. Sorting Requirements

Support sorting by:

- Product name
- Selling price
- Cost price
- Stock quantity
- Created date
- Expiry date

Examples:

- Lowest price first
- Highest price first
- Newly created products first
- Lowest stock first
- Products expiring soon first

---

# 27. Pagination

Supported query parameters:

```text
page
limit
```

Example:

```text
GET /api/products?page=1&limit=10
```

The response should contain:

- Current page
- Page size
- Total records
- Total pages
- Product list

---

# 28. Product Code Validation

Rules:

- Mandatory
- Unique
- Minimum 4 characters
- No spaces
- May contain letters, numbers, hyphens, and underscores

Valid examples:

```text
PROD-1001
LAPTOP_101
ELEC5001
```

---

# 29. Product Name Validation

Rules:

- Mandatory
- Minimum 3 characters
- Cannot contain only numbers
- Cannot contain only special characters

---

# 30. Description Validation

Rules:

- Mandatory
- Minimum 10 characters
- Should contain meaningful product information

---

# 31. Category Validation

Rules:

- Mandatory
- Must match a supported category

Unsupported values should generate a custom validation error.

---

# 32. Brand Validation

Rules:

- Mandatory
- Minimum 2 characters
- Cannot contain only numbers

---

# 33. Supplier Validation

Rules:

- Mandatory
- Minimum 3 characters
- Cannot contain only spaces

---

# 34. Cost Price Validation

Rules:

- Mandatory
- Numeric
- Greater than zero

Invalid examples:

```text
0
-100
abc
```

---

# 35. Selling Price Validation

Rules:

- Mandatory
- Numeric
- Greater than zero
- Normally cannot be below cost price

Invalid example:

```text
Cost Price    : 1000
Selling Price : 900
```

Expected:

Request should be rejected.

---

# 36. Discount Validation

Rules:

```text
0 <= discountPercent <= 70
```

The value should:

- Be numeric
- Not be negative
- Not exceed 70%

---

# 37. Effective Price Validation

The final price after discount must not be lower than cost price.

Conceptually:

```text
Effective Price =
Selling Price - Discount Amount
```

Example:

```text
Cost Price      : ₹800
Selling Price   : ₹1000
Discount        : 30%
Effective Price : ₹700
```

Expected:

Rejected because the final selling price is below cost.

---

# 38. Stock Quantity Validation

Rules:

- Mandatory
- Whole number
- Cannot be negative

Invalid:

```text
stockQuantity = -5
```

---

# 39. Reorder Level Validation

Rules:

- Mandatory
- Whole number
- Zero or positive

---

# 40. Automatic Out-of-Stock Rule

If:

```text
stockQuantity = 0
```

the product should normally have status:

```text
Out of Stock
```

An Active product should not have zero stock unless backorders are explicitly supported.

---

# 41. Low Stock Rule

A product is low stock when:

```text
stockQuantity <= reorderLevel
```

Example:

```text
Stock Quantity : 8
Reorder Level  : 10
```

Expected:

Low-stock condition.

---

# 42. Manufacturing Date Validation

Rules:

- Must be a valid date
- Cannot be in the future

---

# 43. Expiry Date Validation

If expiry applies:

- Expiry date must be provided.
- Expiry date must be after manufacturing date.

Invalid:

```text
Manufactured Date : 10-Aug-2026
Expiry Date       : 05-Aug-2026
```

Expected:

Rejected.

---

# 44. Expired Product Rule

If:

```text
expiryDate < currentDate
```

the product:

- Should not remain Active
- Should not be available for sale
- Should not be reactivated without valid business handling

---

# 45. Category-Specific Expiry Validation

For categories such as:

- Grocery
- Personal Care

expiry information may be mandatory.

For categories such as:

- Books
- Office Supplies

expiry may be optional.

This logic should be implemented in the service layer.

---

# 46. Discontinued Product Rule

When a product is Discontinued:

- New stock should not be added.
- It should not directly return to Active status.
- Future procurement should normally be prohibited.

---

# 47. Delete Business Rule

A product should not be deleted automatically when inventory still exists.

Example restriction:

```text
stockQuantity > 0
```

The product may first need to:

- Reach zero stock
- Become Inactive
- Become Discontinued

---

# 48. Duplicate Product Code Rule

Two products must never use the same:

```text
productCode
```

This validation must apply during:

- POST
- PUT
- PATCH where productCode can change

A product update should not conflict with its own current code.

---

# 49. MongoDB Requirements

Database:

```text
product_management_db
```

Collection:

```text
products
```

Conceptually:

```text
product_management_db
    |
    └── products
```

MongoDB should generate the `_id`.

---

# 50. Environment Configuration

The application should store environment settings outside source code.

Expected values:

```text
PORT
MONGODB_URI
NODE_ENV
```

Sensitive information should not be committed to a public repository.

---

# 51. Router Responsibilities

The Router should define:

```text
POST    /api/products
GET     /api/products
GET     /api/products/:id
PUT     /api/products/:id
PATCH   /api/products/:id
DELETE  /api/products/:id
```

The router should delegate processing to controllers.

---

# 52. Controller Responsibilities

Controllers should:

- Receive requests
- Read request body
- Read path parameters
- Read query parameters
- Call service methods
- Set HTTP status codes
- Return responses
- Forward errors

Controllers should not contain detailed MongoDB or business logic.

---

# 53. Service Layer Responsibilities

The service layer should handle:

- Product code uniqueness
- Pricing validation
- Discount validation
- Effective-price validation
- Stock validation
- Reorder validation
- Expiry validation
- Status transitions
- Delete restrictions
- Search
- Filtering
- Sorting
- Pagination
- Low-stock calculation

---

# 54. Model Layer Responsibilities

The Mongoose model should define:

- Fields
- Data types
- Required fields
- Allowed values
- Defaults
- Uniqueness where appropriate
- Date fields
- Timestamps

---

# 55. Middleware Requirements

Middleware should be used for:

- JSON request parsing
- Validation
- Logging
- Invalid route handling
- Global error handling

Authentication may be added in future versions.

---

# 56. Custom Error Handling Requirement

The application must implement custom application errors.

Participants should not rely only on generic JavaScript `Error`.

Custom errors should distinguish:

- Invalid requests
- Missing resources
- Business rule failures
- Conflict situations
- Infrastructure failures

---

# 57. Base Application Error

Create a common conceptual application error that can act as the parent of custom errors.

It should contain information such as:

| Property | Purpose |
|---|---|
| message | Human-readable description |
| statusCode | Corresponding HTTP status |
| errorCode | Stable application-specific code |
| details | Additional information |
| operational | Whether the error is expected |

---

# 58. Product Not Found Error

Suggested custom error:

```text
ProductNotFoundError
```

Trigger when:

- A valid product ID does not exist.
- A deleted product is requested.
- Update targets a missing product.

Suggested status:

```text
404 Not Found
```

Suggested error code:

```text
PRODUCT_NOT_FOUND
```

---

# 59. Invalid Product ID Error

Suggested:

```text
InvalidProductIdError
```

Example:

```text
GET /api/products/abc
```

Suggested status:

```text
400 Bad Request
```

Suggested error code:

```text
INVALID_PRODUCT_ID
```

A malformed ID and a missing product should be treated differently.

---

# 60. Duplicate Product Code Error

Suggested:

```text
DuplicateProductCodeError
```

Trigger when another product already uses the requested product code.

Suggested status:

```text
409 Conflict
```

Suggested error code:

```text
DUPLICATE_PRODUCT_CODE
```

---

# 61. Product Validation Error

Suggested:

```text
ProductValidationError
```

Trigger for multiple field-level problems such as:

- Missing product name
- Missing supplier
- Invalid category
- Invalid unit
- Missing required fields

Suggested status:

```text
422 Unprocessable Entity
```

Suggested code:

```text
PRODUCT_VALIDATION_FAILED
```

---

# 62. Invalid Pricing Error

Suggested:

```text
InvalidPricingError
```

Trigger when:

- Cost price is zero or negative
- Selling price is zero or negative
- Selling price is lower than cost
- Effective discounted price falls below cost

Suggested status:

```text
422 Unprocessable Entity
```

Suggested code:

```text
INVALID_PRODUCT_PRICING
```

---

# 63. Invalid Discount Error

Suggested:

```text
InvalidDiscountError
```

Trigger when:

- Discount is negative
- Discount exceeds 70%
- Discount is non-numeric
- Discount produces an invalid effective price

Suggested code:

```text
INVALID_DISCOUNT
```

Suggested status:

```text
422 Unprocessable Entity
```

---

# 64. Invalid Stock Error

Suggested:

```text
InvalidStockError
```

Trigger when:

- Stock is negative
- Stock has decimal values where whole numbers are required
- Reorder level is negative

Suggested code:

```text
INVALID_STOCK
```

Suggested status:

```text
422 Unprocessable Entity
```

---

# 65. Product Out Of Stock Error

Suggested:

```text
ProductOutOfStockError
```

Trigger when a future business operation requires available inventory but:

```text
stockQuantity = 0
```

Suggested status:

```text
409 Conflict
```

Suggested code:

```text
PRODUCT_OUT_OF_STOCK
```

---

# 66. Insufficient Stock Error

Suggested:

```text
InsufficientStockError
```

Useful when a requested quantity is greater than available inventory.

Suggested response details:

- Product ID
- Product code
- Requested quantity
- Available quantity

Suggested status:

```text
409 Conflict
```

Suggested code:

```text
INSUFFICIENT_STOCK
```

---

# 67. Invalid Product Date Error

Suggested:

```text
InvalidProductDateError
```

Trigger when:

- Manufacturing date is in the future
- Expiry date is before manufacturing date
- Expiry date is required but missing
- Date format is invalid

Suggested status:

```text
422 Unprocessable Entity
```

Suggested code:

```text
INVALID_PRODUCT_DATE
```

---

# 68. Product Expired Error

Suggested:

```text
ProductExpiredError
```

Trigger when trying to:

- Activate expired product
- Sell expired product
- Mark expired product as available

Suggested status:

```text
409 Conflict
```

Suggested code:

```text
PRODUCT_EXPIRED
```

---

# 69. Product Discontinued Error

Suggested:

```text
ProductDiscontinuedError
```

Trigger when attempting prohibited operations such as:

- Adding stock
- Activating directly
- Creating new procurement

Suggested status:

```text
409 Conflict
```

Suggested code:

```text
PRODUCT_DISCONTINUED
```

---

# 70. Product Deletion Not Allowed Error

Suggested:

```text
ProductDeletionNotAllowedError
```

Example condition:

```text
stockQuantity > 0
```

Suggested status:

```text
409 Conflict
```

Suggested code:

```text
PRODUCT_DELETE_NOT_ALLOWED
```

Details may include:

```text
productId
productCode
stockQuantity
```

---

# 71. Invalid Product Status Transition Error

Suggested:

```text
InvalidProductStatusTransitionError
```

Examples:

```text
Discontinued -> Active
```

or:

```text
Out of Stock -> Active
```

when stock is still zero.

Suggested status:

```text
409 Conflict
```

Suggested code:

```text
INVALID_PRODUCT_STATUS_TRANSITION
```

Error details should include:

- Current status
- Requested status
- Reason

---

# 72. Invalid Category Error

Suggested:

```text
InvalidCategoryError
```

Trigger when an unsupported category is submitted.

Suggested status:

```text
422 Unprocessable Entity
```

Suggested code:

```text
INVALID_PRODUCT_CATEGORY
```

---

# 73. Database Operation Error

Suggested:

```text
DatabaseOperationError
```

Possible scenarios:

- Database connection failure
- Query failure
- Insert failure
- Update failure
- Database timeout

Suggested status:

```text
500 Internal Server Error
```

Suggested code:

```text
DATABASE_OPERATION_FAILED
```

Raw MongoDB details should not be exposed to clients.

---

# 74. Route Not Found Error

Suggested:

```text
RouteNotFoundError
```

Example:

```text
GET /api/productss
```

Suggested status:

```text
404 Not Found
```

Suggested code:

```text
ROUTE_NOT_FOUND
```

---

# 75. Method Not Allowed Error

For advanced implementations, distinguish an unsupported HTTP method from an unknown URL.

Suggested status:

```text
405 Method Not Allowed
```

Suggested code:

```text
METHOD_NOT_ALLOWED
```

---

# 76. Recommended Error Hierarchy

```text
ApplicationError
│
├── ProductNotFoundError
├── InvalidProductIdError
├── DuplicateProductCodeError
├── ProductValidationError
├── InvalidPricingError
├── InvalidDiscountError
├── InvalidStockError
├── ProductOutOfStockError
├── InsufficientStockError
├── InvalidProductDateError
├── ProductExpiredError
├── ProductDiscontinuedError
├── ProductDeletionNotAllowedError
├── InvalidProductStatusTransitionError
├── InvalidCategoryError
├── DatabaseOperationError
└── RouteNotFoundError
```

---

# 77. Standard Error Response

Every application error should follow a consistent format.

Suggested fields:

```text
success
timestamp
status
error
errorCode
message
details
path
```

Example conceptual response:

```text
success    : false
timestamp  : 2026-08-07T13:30:00
status     : 409
error      : Conflict
errorCode  : DUPLICATE_PRODUCT_CODE
message    : Product code PROD-1001 already exists.
path       : /api/products
```

---

# 78. Multiple Validation Error Response

If multiple fields fail validation, the application should ideally return all relevant errors together.

Example invalid input:

```text
name            : ""
costPrice       : -500
sellingPrice    : 0
stockQuantity   : -10
discountPercent : 90
```

Expected details:

```text
name
    Product name is required.

costPrice
    Cost price must be greater than zero.

sellingPrice
    Selling price must be greater than zero.

stockQuantity
    Stock quantity cannot be negative.

discountPercent
    Discount cannot exceed 70%.
```

Suggested code:

```text
PRODUCT_VALIDATION_FAILED
```

---

# 79. Standard Error Codes

| Scenario | Error Code | HTTP Status |
|---|---|---:|
| Product not found | PRODUCT_NOT_FOUND | 404 |
| Invalid MongoDB ID | INVALID_PRODUCT_ID | 400 |
| Duplicate product code | DUPLICATE_PRODUCT_CODE | 409 |
| Validation failure | PRODUCT_VALIDATION_FAILED | 422 |
| Invalid pricing | INVALID_PRODUCT_PRICING | 422 |
| Invalid discount | INVALID_DISCOUNT | 422 |
| Invalid stock | INVALID_STOCK | 422 |
| Out of stock | PRODUCT_OUT_OF_STOCK | 409 |
| Insufficient stock | INSUFFICIENT_STOCK | 409 |
| Invalid date | INVALID_PRODUCT_DATE | 422 |
| Product expired | PRODUCT_EXPIRED | 409 |
| Product discontinued | PRODUCT_DISCONTINUED | 409 |
| Delete prohibited | PRODUCT_DELETE_NOT_ALLOWED | 409 |
| Invalid status transition | INVALID_PRODUCT_STATUS_TRANSITION | 409 |
| Invalid category | INVALID_PRODUCT_CATEGORY | 422 |
| Route not found | ROUTE_NOT_FOUND | 404 |
| Database failure | DATABASE_OPERATION_FAILED | 500 |
| Internal server error | INTERNAL_SERVER_ERROR | 500 |

---

# 80. Global Error Middleware Responsibilities

The global error middleware should:

1. Receive forwarded errors.
2. Identify known custom errors.
3. Determine HTTP status.
4. Determine application error code.
5. Create a standardized response.
6. Log diagnostic information.
7. Hide sensitive infrastructure details.
8. Handle unknown errors safely.

Controllers should not construct independent error-response formats.

---

# 81. Development vs Production Error Handling

During development, additional debugging information may be available:

```text
stack trace
internal cause
diagnostic information
```

Production responses should not expose:

- Stack traces
- MongoDB server information
- Connection strings
- Credentials
- Internal file paths

---

# 82. Error Handling Flow

```text
HTTP Request
      |
      v
Router
      |
      v
Controller
      |
      v
Service
      |
      | Business validation fails
      v
Custom Application Error
      |
      v
Global Error Middleware
      |
      v
Standard Error Response
      |
      v
Client
```

---

# 83. HTTP Status Codes

| Scenario | Status |
|---|---:|
| Successful request | 200 |
| Resource created | 201 |
| Invalid request | 400 |
| Unauthorized | 401 |
| Forbidden | 403 |
| Resource not found | 404 |
| Method not allowed | 405 |
| Business conflict | 409 |
| Validation failure | 422 |
| Internal server failure | 500 |

---

# 84. Postman Testing Requirements

Create Postman requests for:

```text
POST    /api/products
GET     /api/products
GET     /api/products/{id}
PUT     /api/products/{id}
PATCH   /api/products/{id}
DELETE  /api/products/{id}
```

Also test query APIs such as:

```text
GET /api/products?search=laptop

GET /api/products?category=Electronics

GET /api/products?status=Active

GET /api/products?brand=Samsung

GET /api/products?stockStatus=lowStock

GET /api/products?minPrice=1000&maxPrice=50000

GET /api/products?page=1&limit=10
```

---

# 85. Required Positive Test Scenarios

Participants should test:

- Valid product creation
- Retrieve all products
- Retrieve valid product ID
- Valid PUT update
- Valid PATCH update
- Valid delete
- Product search
- Category filtering
- Status filtering
- Brand filtering
- Price filtering
- Low-stock filtering
- Sorting
- Pagination

---

# 86. Required Negative Test Scenarios

Test at minimum:

### Invalid ID

Expected:

```text
400
INVALID_PRODUCT_ID
```

### Product Not Found

Expected:

```text
404
PRODUCT_NOT_FOUND
```

### Duplicate Product Code

Expected:

```text
409
DUPLICATE_PRODUCT_CODE
```

### Missing Required Fields

Expected:

```text
422
PRODUCT_VALIDATION_FAILED
```

### Selling Price Below Cost

Expected:

```text
422
INVALID_PRODUCT_PRICING
```

### Discount Above Limit

Expected:

```text
422
INVALID_DISCOUNT
```

### Discount Below Cost Price

Expected:

```text
422
INVALID_DISCOUNT
```

### Negative Stock

Expected:

```text
422
INVALID_STOCK
```

### Expiry Before Manufacturing Date

Expected:

```text
422
INVALID_PRODUCT_DATE
```

### Activate Expired Product

Expected:

```text
409
PRODUCT_EXPIRED
```

### Add Stock To Discontinued Product

Expected:

```text
409
PRODUCT_DISCONTINUED
```

### Delete Product With Stock

Expected:

```text
409
PRODUCT_DELETE_NOT_ALLOWED
```

### Invalid Status Transition

Expected:

```text
409
INVALID_PRODUCT_STATUS_TRANSITION
```

### Unsupported Category

Expected:

```text
422
INVALID_PRODUCT_CATEGORY
```

### Invalid URL

Expected:

```text
404
ROUTE_NOT_FOUND
```

### Database Failure

Expected:

```text
500
DATABASE_OPERATION_FAILED
```

---

# 87. Development Steps

## Step 1

Create the Product Management Node.js project.

## Step 2

Initialize the project using npm.

## Step 3

Add required backend dependencies.

Required dependency categories:

- Express framework
- MongoDB ODM
- Environment configuration
- Development reload utility if required

## Step 4

Create layered folder structure.

## Step 5

Configure MongoDB.

Possible options:

- Local MongoDB
- MongoDB using Docker
- MongoDB Atlas

## Step 6

Create environment configuration.

## Step 7

Configure MongoDB connectivity.

## Step 8

Create Product model.

## Step 9

Define schema-level validation.

## Step 10

Create custom application error structure.

## Step 11

Create Product-specific custom error definitions.

## Step 12

Create Product service.

## Step 13

Implement complex business validations in the service layer.

## Step 14

Create Product controller.

## Step 15

Create Product router.

## Step 16

Register routes in Express.

## Step 17

Configure JSON request parsing.

## Step 18

Configure invalid-route handling.

## Step 19

Configure global error middleware.

## Step 20

Implement Product creation.

## Step 21

Implement Get All Products.

## Step 22

Implement Get Product By ID.

## Step 23

Implement PUT update.

## Step 24

Implement PATCH update.

## Step 25

Implement Delete.

## Step 26

Implement search functionality.

## Step 27

Implement filtering.

## Step 28

Implement price-range filtering.

## Step 29

Implement stock-status filtering.

## Step 30

Implement sorting.

## Step 31

Implement pagination.

## Step 32

Create Postman collection.

## Step 33

Test all positive scenarios.

## Step 34

Test all custom error scenarios.

---

# 88. Pricing Test Scenarios

Valid:

```text
Cost Price    : 1000
Selling Price : 1200
```

Invalid:

```text
Cost Price    : 1000
Selling Price : 900
```

Expected:

```text
INVALID_PRODUCT_PRICING
```

---

# 89. Discount Test Scenarios

Valid:

```text
Cost Price      : 800
Selling Price   : 1000
Discount        : 10%
Effective Price : 900
```

Invalid:

```text
Cost Price      : 800
Selling Price   : 1000
Discount        : 30%
Effective Price : 700
```

Expected:

```text
INVALID_DISCOUNT
```

---

# 90. Stock Test Scenarios

Normal:

```text
Stock Quantity : 20
Reorder Level  : 10
```

Low stock:

```text
Stock Quantity : 8
Reorder Level  : 10
```

Out of stock:

```text
Stock Quantity : 0
```

Invalid:

```text
Stock Quantity : -10
```

Expected:

```text
INVALID_STOCK
```

---

# 91. Date Test Scenarios

Test:

- Valid manufacturing date
- Valid expiry date
- Manufacturing date in future
- Expiry before manufacturing date
- Already expired product
- Missing mandatory expiry date
- Category where expiry is optional

---

# 92. Update Test Scenarios

Test:

- Update selling price
- Update stock
- Update status
- Update discount
- Set stock to zero
- Activate expired product
- Add stock to discontinued product
- Change product code to duplicate value

---

# 93. Delete Test Scenarios

Test:

- Delete product with zero stock
- Delete product having stock
- Delete missing product
- Delete using malformed MongoDB ID

---

# 94. Functional Flow

```text
Client
  |
  | POST /api/products
  v
Express Router
  |
  v
Product Controller
  |
  v
Product Service
  |
  | Business Validation
  |
  | Custom Error if needed
  v
Product Model
  |
  v
MongoDB
  |
  v
HTTP Response
```

---

# 95. CRUD Mapping

| CRUD | REST Method | MongoDB Concept |
|---|---|---|
| Create | POST | Insert document |
| Read All | GET | Find documents |
| Read One | GET | Find by ID |
| Update | PUT | Replace/update document |
| Partial Update | PATCH | Update selected fields |
| Delete | DELETE | Delete document |

---

# 96. Optional Advanced Requirements

The project can later be extended with:

- Product images
- Multiple suppliers
- Category management
- Supplier management
- Inventory transactions
- Purchase orders
- Product ratings
- Reviews
- Barcode support
- SKU management
- Product variants
- Warehouse management
- Product audit history
- Soft delete
- JWT authentication
- Role-based access
- Swagger/OpenAPI documentation
- Docker
- Automated API testing
- MongoDB aggregation reports

---

# 97. Advanced Business Rules

Future enhancements can include:

1. Only administrators can delete products.
2. Inventory users can update stock but cannot modify pricing.
3. Sales users can view only Active products.
4. Expired products cannot be sold.
5. Discontinued products cannot receive new stock.
6. Selling price cannot fall below cost price.
7. Effective discounted price cannot fall below cost.
8. Products with zero stock automatically become Out of Stock.
9. Products below reorder level should be identified as Low Stock.
10. Duplicate product codes must never be accepted.
11. Product code cannot change after confirmed sales exist.
12. Products with inventory transactions should use soft delete.
13. Critical business errors should always use stable error codes.

---

# 98. Expected Learning Outcomes

Participants should understand:

- Node.js backend development
- Express.js
- REST API design
- MongoDB
- Mongoose
- CRUD operations
- Layered architecture
- Controller responsibilities
- Service-layer business logic
- Model validation
- Custom error classes
- Global error middleware
- HTTP status codes
- Stable application error codes
- Query parameters
- Search
- Filtering
- Sorting
- Pagination
- Inventory validation
- Pricing validation
- Discount validation
- Date validation
- Environment configuration
- Postman testing

---

# 99. Final Deliverables

Participants should submit:

1. Product Management Node.js project.
2. Product model.
3. Product controller.
4. Product service.
5. Product router.
6. MongoDB configuration.
7. Environment configuration.
8. Product CRUD APIs.
9. Search functionality.
10. Filtering.
11. Sorting.
12. Pagination.
13. Complex business validations.
14. Base application error.
15. Custom product errors.
16. Invalid-ID handling.
17. Duplicate-product handling.
18. Pricing error handling.
19. Discount error handling.
20. Stock error handling.
21. Expiry-related error handling.
22. Product-status transition handling.
23. Delete-restriction handling.
24. Route-not-found handling.
25. Database-error handling.
26. Global Express error middleware.
27. Standardized error-response format.
28. Stable error codes.
29. Postman collection.
30. Positive API test cases.
31. Negative API test cases.
32. Sample MongoDB data.
33. README documentation.

---

# 100. Final Expected API Set

```text
POST    /api/products

GET     /api/products

GET     /api/products/:id

PUT     /api/products/:id

PATCH   /api/products/:id

DELETE  /api/products/:id
```

Additional queries:

```text
GET /api/products?search=laptop

GET /api/products?category=Electronics

GET /api/products?brand=Samsung

GET /api/products?status=Active

GET /api/products?stockStatus=lowStock

GET /api/products?minPrice=1000&maxPrice=50000

GET /api/products?page=1&limit=10
```

The final outcome should be a complete **Product Catalog and Inventory Management REST API using Node.js, Express.js, MongoDB, and Mongoose**, demonstrating CRUD operations, search, filtering, sorting, pagination, complex business validation, layered architecture, and production-style custom error handling.
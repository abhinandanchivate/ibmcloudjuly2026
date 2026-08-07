# Task Management REST API Using Node.js, Express.js, and MongoDB

## 1. Case Study Overview

Design and develop a RESTful backend application for a Task Management System using:

- Node.js
- Express.js
- MongoDB
- Mongoose
- REST API principles
- Postman

The backend will provide APIs for creating, retrieving, updating, deleting, searching, and filtering tasks.

The frontend can later consume these APIs using JavaScript Fetch API, React, Angular, Vue, mobile applications, or any other REST client.

---

# 2. Business Scenario

An organization requires a centralized Task Management System for managing day-to-day work across multiple teams.

Currently, users maintain their tasks manually using spreadsheets, messages, or personal notes. This creates several problems:

- Tasks are not centrally available.
- Task status is difficult to track.
- Due dates can easily be missed.
- Team members do not have a common view of work.
- Task ownership is unclear.
- Managers cannot easily identify pending or delayed tasks.
- Searching and filtering tasks becomes difficult.

The organization wants to build a backend REST API where task information can be permanently stored in MongoDB.

The REST API should support complete CRUD operations and should follow proper backend architecture.

---

# 3. Project Objective

The objective is to build a REST API that allows clients to:

- Create tasks
- View all tasks
- View an individual task
- Update tasks
- Partially update tasks
- Delete tasks
- Search tasks
- Filter tasks
- Track task status
- Track task priority
- Manage due dates
- Validate incoming requests
- Handle application errors properly

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
- Node Package Manager
- MongoDB Compass

---

# 5. High-Level Architecture

The application should follow a layered architecture.

```text
Client
   |
   v
REST API
   |
   v
Controller Layer
   |
   v
Service Layer
   |
   v
Repository / Model Layer
   |
   v
MongoDB
```

Recommended flow:

```text
HTTP Request
     |
     v
Express Router
     |
     v
Controller
     |
     v
Service
     |
     v
Mongoose Model
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
task-management-api/
│
├── config/
│   └── database configuration
│
├── controllers/
│   └── task controller
│
├── services/
│   └── task service
│
├── models/
│   └── task model
│
├── routes/
│   └── task routes
│
├── middleware/
│   ├── error handling middleware
│   └── validation middleware
│
├── utils/
│   └── utility functions
│
├── app.js
│
├── server.js
│
├── .env
│
├── .gitignore
│
└── package.json
```

---

# 7. Task Entity Requirements

Each task should contain the following fields.

| Field | Description |
|---|---|
| id | Unique task identifier |
| title | Task title |
| description | Detailed description |
| assignedTo | Person responsible for the task |
| category | Task category |
| priority | Task priority |
| status | Current task status |
| startDate | Task starting date |
| dueDate | Expected completion date |
| createdAt | Task creation timestamp |
| updatedAt | Last modification timestamp |

---

# 8. Task Categories

The application should support categories such as:

- Development
- Testing
- Documentation
- Training
- Meeting
- Support
- Research
- Other

---

# 9. Task Priorities

Supported task priority values:

- Low
- Medium
- High
- Critical

Priority should be mandatory.

---

# 10. Task Status

Supported task statuses:

- Pending
- In Progress
- Completed
- Cancelled

A newly created task may have `Pending` as its default status.

---

# 11. REST API Base URL

Suggested development base URL:

```text
http://localhost:3000/api/tasks
```

---

# 12. REST API Requirements

## 12.1 Create Task

### HTTP Method

POST

### Endpoint

```text
/api/tasks
```

### Purpose

Create a new task.

### Input Information

The API should accept:

- Title
- Description
- Assigned person
- Category
- Priority
- Status
- Start date
- Due date

### Expected Behaviour

The application should:

1. Receive the request.
2. Validate request data.
3. Check mandatory fields.
4. Validate start and due dates.
5. Create the task.
6. Store the task in MongoDB.
7. Return the created task.

### Expected HTTP Status

```text
201 Created
```

---

# 13. Get All Tasks

### HTTP Method

GET

### Endpoint

```text
/api/tasks
```

### Purpose

Retrieve all tasks stored in MongoDB.

### Expected Behaviour

The application should:

1. Receive the GET request.
2. Read tasks from MongoDB.
3. Return task records.
4. Return an empty list if no tasks exist.

### Expected HTTP Status

```text
200 OK
```

---

# 14. Get Task By ID

### HTTP Method

GET

### Endpoint

```text
/api/tasks/{taskId}
```

Example:

```text
/api/tasks/67ab1234567890
```

### Expected Behaviour

The API should:

1. Receive the task ID.
2. Validate the MongoDB ID.
3. Search the database.
4. Return the matching task.

If the task does not exist, return an appropriate error.

### Success Status

```text
200 OK
```

### Not Found Status

```text
404 Not Found
```

---

# 15. Update Complete Task

### HTTP Method

PUT

### Endpoint

```text
/api/tasks/{taskId}
```

### Purpose

Replace the complete task information.

### Expected Behaviour

The API should:

1. Validate task ID.
2. Validate request body.
3. Check whether the task exists.
4. Replace task information.
5. Save the changes.
6. Return the updated task.

### Expected Status

```text
200 OK
```

---

# 16. Partially Update Task

### HTTP Method

PATCH

### Endpoint

```text
/api/tasks/{taskId}
```

### Purpose

Update only selected task fields.

Example scenarios:

- Change task status.
- Change priority.
- Change assigned employee.
- Extend due date.
- Update description.

The client should not be required to send the complete task.

---

# 17. Delete Task

### HTTP Method

DELETE

### Endpoint

```text
/api/tasks/{taskId}
```

### Expected Behaviour

The application should:

1. Validate the task ID.
2. Check whether the task exists.
3. Delete the task from MongoDB.
4. Return a successful response.

### Suggested Status

```text
200 OK
```

or

```text
204 No Content
```

---

# 18. Search Tasks

The API should support searching tasks.

Example:

```text
GET /api/tasks?search=login
```

Search may be performed on:

- Task title
- Description
- Assigned person
- Category

Example use case:

A user searches for:

```text
login
```

The system should return tasks containing the term `login`.

---

# 19. Filter By Status

Example:

```text
GET /api/tasks?status=Pending
```

Possible values:

- Pending
- In Progress
- Completed
- Cancelled

---

# 20. Filter By Priority

Example:

```text
GET /api/tasks?priority=High
```

Possible values:

- Low
- Medium
- High
- Critical

---

# 21. Combined Filters

The application should allow multiple filters.

Example:

```text
GET /api/tasks?status=In Progress&priority=High
```

The API should return only High-priority tasks currently in progress.

---

# 22. Filter By Assigned Employee

Example:

```text
GET /api/tasks?assignedTo=Amit
```

This can be used to retrieve tasks assigned to a particular team member.

---

# 23. Filter By Category

Example:

```text
GET /api/tasks?category=Development
```

The API should return Development-related tasks.

---

# 24. Sorting Requirements

The REST API should support sorting.

Possible sorting fields:

- Title
- Priority
- Due date
- Created date
- Updated date

Examples of expected behaviour:

- Sort tasks by due date ascending.
- Sort newly created tasks first.
- Sort by priority.

---

# 25. Pagination Requirement

For a larger task database, the API should support pagination.

Suggested request parameters:

```text
page
limit
```

Example:

```text
GET /api/tasks?page=1&limit=10
```

The response should provide useful pagination information such as:

- Current page
- Number of tasks
- Page size
- Total number of records
- Total number of pages

---

# 26. Task Validation Requirements

## Title

Rules:

- Mandatory
- Minimum 3 characters
- Maximum reasonable length

---

## Description

Rules:

- Mandatory
- Minimum 10 characters

---

## Assigned To

Rules:

- Mandatory
- Cannot contain only whitespace

---

## Category

Rules:

- Mandatory
- Must contain a supported category

---

## Priority

Rules:

- Mandatory
- Must be:

```text
Low
Medium
High
Critical
```

---

## Status

Must contain one of:

```text
Pending
In Progress
Completed
Cancelled
```

---

# 27. Date Validation

The application should validate:

- Start date must be provided.
- Due date must be provided.
- Due date cannot be earlier than start date.

Example invalid scenario:

```text
Start Date : 15-Aug-2026
Due Date   : 10-Aug-2026
```

The API should reject this request.

---

# 28. MongoDB Database Requirements

Recommended database:

```text
task_management_db
```

Recommended collection:

```text
tasks
```

Conceptual structure:

```text
task_management_db
    |
    └── tasks
```

Each task should be represented as a MongoDB document.

MongoDB should automatically generate a unique `_id` for every task.

---

# 29. Database Configuration

The application should keep database configuration outside application logic.

Environment configuration should include values such as:

```text
PORT
MONGODB_URI
```

Do not hard-code database credentials directly inside source files.

---

# 30. Environment Configuration

Create environment-specific configuration using a `.env` file.

The `.env` file may store:

- Application port
- MongoDB connection URL
- Environment type
- Other sensitive configuration

The `.env` file should not normally be committed to a public repository.

---

# 31. Express Application Configuration

The Express application should perform the following responsibilities:

1. Create an Express application.
2. Enable JSON request parsing.
3. Configure middleware.
4. Configure task routes.
5. Configure invalid-route handling.
6. Configure global error handling.

---

# 32. Router Responsibility

The Router layer should define REST endpoints.

Examples:

```text
POST    /api/tasks
GET     /api/tasks
GET     /api/tasks/:id
PUT     /api/tasks/:id
PATCH   /api/tasks/:id
DELETE  /api/tasks/:id
```

The router should delegate the request to the appropriate controller.

---

# 33. Controller Responsibility

The controller should handle HTTP-level responsibilities.

Responsibilities include:

- Read URL parameters.
- Read query parameters.
- Read request body.
- Call the service layer.
- Build HTTP responses.
- Set HTTP status codes.
- Forward errors.

Controllers should avoid containing database-specific logic.

---

# 34. Service Layer Responsibility

The Service layer contains business logic.

Examples:

- Validate due date.
- Check business rules.
- Process filters.
- Decide whether an operation is valid.
- Call the model or repository layer.
- Handle task-related business operations.

This keeps controllers lightweight.

---

# 35. Model Layer Responsibility

The Task Model should define the MongoDB task structure using Mongoose.

The model should define:

- Fields
- Data types
- Required fields
- Default values
- Allowed values
- Date fields
- Timestamps

The Model layer interacts with MongoDB.

---

# 36. Middleware Requirement

Middleware should be considered for:

- JSON request parsing
- Validation
- Logging
- Invalid routes
- Error handling
- Authentication in future versions

---

# 37. Global Error Handling

The backend should have centralized error handling.

Possible error scenarios include:

- Invalid task ID
- Task not found
- Validation error
- Database connection failure
- MongoDB operation failure
- Invalid request body
- Duplicate information if relevant
- Unsupported URL
- Internal server error

---

# 38. Standard Error Response

The application should maintain a consistent error response format.

Conceptually, an error response should contain:

```text
timestamp
status
error
message
path
```

This makes errors easier for frontend applications to handle.

---

# 39. HTTP Status Codes

The application should use appropriate HTTP status codes.

| Scenario | Status |
|---|---:|
| Request successful | 200 |
| Resource created | 201 |
| Invalid request | 400 |
| Unauthorized | 401 |
| Forbidden | 403 |
| Task not found | 404 |
| Conflict | 409 |
| Validation failure | 400 / 422 |
| Server failure | 500 |

---

# 40. API Testing Using Postman

Create a Postman collection containing:

### Request 1

Create Task

```text
POST /api/tasks
```

### Request 2

Get All Tasks

```text
GET /api/tasks
```

### Request 3

Get Task By ID

```text
GET /api/tasks/{id}
```

### Request 4

Update Complete Task

```text
PUT /api/tasks/{id}
```

### Request 5

Update Task Status

```text
PATCH /api/tasks/{id}
```

### Request 6

Delete Task

```text
DELETE /api/tasks/{id}
```

### Request 7

Search Tasks

```text
GET /api/tasks?search=keyword
```

### Request 8

Filter By Status

```text
GET /api/tasks?status=Pending
```

### Request 9

Filter By Priority

```text
GET /api/tasks?priority=High
```

---

# 41. Development Steps

## Step 1

Create the project directory.

---

## Step 2

Initialize the Node.js project.

---

## Step 3

Install the required backend dependencies.

Required categories of dependencies:

- Express
- MongoDB ODM
- Environment configuration library
- Development server reload utility if required

---

## Step 4

Create the recommended folder structure.

---

## Step 5

Configure MongoDB.

Decide whether the application will use:

- Local MongoDB
- MongoDB running through Docker
- MongoDB Atlas

---

## Step 6

Configure environment variables.

Store:

- Server port
- MongoDB URI

---

## Step 7

Create the MongoDB connection configuration.

The application should establish the database connection when the server starts.

---

## Step 8

Create the Task model.

Define all task fields and validation rules.

---

## Step 9

Create the service layer.

Implement task-related business operations.

---

## Step 10

Create the controller layer.

Map HTTP requests to business operations.

---

## Step 11

Create the task router.

Configure all REST API URLs.

---

## Step 12

Register task routes inside the Express application.

Recommended root path:

```text
/api/tasks
```

---

## Step 13

Configure request parsing.

The backend should accept JSON request bodies.

---

## Step 14

Create application-level error handling.

All unexpected errors should be forwarded to one centralized error handler.

---

## Step 15

Implement the Create Task operation.

Test using Postman.

---

## Step 16

Implement Get All Tasks.

Verify data is retrieved from MongoDB.

---

## Step 17

Implement Get Task By ID.

Test valid and invalid IDs.

---

## Step 18

Implement Update Task using PUT.

Verify the complete resource is updated.

---

## Step 19

Implement partial updates using PATCH.

Use cases include:

- Change status
- Change priority
- Change due date

---

## Step 20

Implement Delete Task.

Verify the MongoDB document is actually removed.

---

## Step 21

Implement search functionality.

---

## Step 22

Implement filtering.

Filters should include:

- Status
- Priority
- Category
- Assigned person

---

## Step 23

Implement sorting.

---

## Step 24

Implement pagination.

---

## Step 25

Create a complete Postman collection.

---

## Step 26

Test successful and failure scenarios.

---

# 42. Important Test Scenarios

## Create Task

Test:

- Valid task
- Missing title
- Missing description
- Missing assigned person
- Invalid category
- Invalid priority
- Invalid status
- Invalid due date

---

## Get Task

Test:

- Existing ID
- Non-existing ID
- Invalid MongoDB ID

---

## Update Task

Test:

- Valid update
- Non-existing task
- Invalid priority
- Invalid status
- Due date before start date

---

## Delete Task

Test:

- Existing task
- Already deleted task
- Invalid ID

---

# 43. Functional Flow

```text
User / Frontend
       |
       | POST /api/tasks
       v
Express Router
       |
       v
Task Controller
       |
       v
Task Service
       |
       v
Task Model
       |
       v
MongoDB
       |
       v
Task Created
       |
       v
201 Response
```

---

# 44. CRUD Mapping

| CRUD Operation | REST Method | MongoDB Operation |
|---|---|---|
| Create | POST | Insert document |
| Read all | GET | Find documents |
| Read one | GET | Find document by ID |
| Update | PUT | Update document |
| Partial Update | PATCH | Update selected fields |
| Delete | DELETE | Delete document |

---

# 45. Integration With Existing Task Frontend

The HTML/CSS/JavaScript Task Management application created earlier can consume this backend.

Instead of:

```text
http://localhost:3000/tasks
```

the frontend would use:

```text
http://localhost:3000/api/tasks
```

The frontend should use Fetch API for:

```text
GET
POST
PUT
PATCH
DELETE
```

This converts the earlier JSON Server application into a real backend-based application.

---

# 46. Optional Advanced Requirements

After completing the basic CRUD application, participants can extend it with:

- User registration
- User login
- JWT authentication
- Role-based access
- Manager and Employee roles
- Task comments
- Task attachments
- Task history
- Audit logs
- Email notifications
- Overdue task notifications
- Dashboard reporting
- Task analytics
- MongoDB aggregation
- Soft delete
- Docker
- Swagger / OpenAPI
- Automated testing

---

# 47. Advanced Business Rules

Possible business rules for the next phase:

1. Completed tasks cannot return to Pending without manager approval.
2. Critical tasks must have an assigned employee.
3. Due date cannot be before the start date.
4. Cancelled tasks cannot be marked Completed.
5. Tasks crossing the due date should be identified as overdue.
6. Only authorized users should delete tasks.
7. Managers should see all tasks.
8. Employees should see only tasks assigned to them.

---

# 48. Expected Learning Outcomes

After completing the case study, participants should understand:

- Node.js application structure
- Express.js routing
- REST API design
- MongoDB integration
- Mongoose
- Layered architecture
- Controllers
- Services
- Models
- Middleware
- CRUD operations
- Request validation
- Global exception handling
- HTTP status codes
- Search and filtering
- Pagination
- API testing using Postman
- Environment configuration
- Frontend-to-backend integration

---

# 49. Final Deliverables

Participants should submit:

1. Node.js REST API project.
2. Express Router implementation.
3. Task controller.
4. Task service.
5. Task model.
6. MongoDB configuration.
7. Environment configuration.
8. CRUD REST APIs.
9. Search and filtering functionality.
10. Global error handling.
11. Postman collection.
12. Sample MongoDB task data.
13. README documentation.
14. API testing evidence.

---

# 50. Final Expected API

```text
POST    /api/tasks
GET     /api/tasks
GET     /api/tasks/:id
PUT     /api/tasks/:id
PATCH   /api/tasks/:id
DELETE  /api/tasks/:id
```

Additional query APIs should support:

```text
GET /api/tasks?status=Pending

GET /api/tasks?priority=High

GET /api/tasks?category=Development

GET /api/tasks?assignedTo=Amit

GET /api/tasks?search=login

GET /api/tasks?page=1&limit=10
```

The final result should be a properly layered **Node.js + Express.js + MongoDB REST API** capable of serving the Task Management frontend application.
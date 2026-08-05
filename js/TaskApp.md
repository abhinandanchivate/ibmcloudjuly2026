
## 1. Task Management Case Study

# Task Management System Using JavaScript and JSON Server

## 1. Project Overview

Develop a web-based Task Management System using HTML, CSS, JavaScript, Fetch API, and JSON Server.

The application allows users to create, view, update, search, filter, and delete tasks. JSON Server will act as a lightweight REST API and store task information inside a `db.json` file.

The application should provide a responsive dashboard that displays task statistics, a task form, search and filtering options, and a task listing table.

---

## 2. Business Scenario

An organization needs a simple task-tracking application to manage day-to-day work.

Employees and team members should be able to record tasks, assign priorities, specify due dates, update task progress, and remove completed or unnecessary tasks.

The organization does not currently require a full backend application. Therefore, JSON Server will be used as a mock REST API for development and training purposes.

---

## 3. Technology Stack

* HTML5
* CSS3
* JavaScript
* Fetch API
* JSON Server
* REST API
* JSON
* Visual Studio Code
* Live Server
* Postman

---

## 4. Task Details

Each task should contain the following information:

| Field       | Description                                   |
| ----------- | --------------------------------------------- |
| ID          | Unique task identifier                        |
| Title       | Short title of the task                       |
| Description | Detailed task description                     |
| Assigned To | Person responsible for the task               |
| Category    | Task category                                 |
| Priority    | Low, Medium, High, or Critical                |
| Status      | Pending, In Progress, Completed, or Cancelled |
| Start Date  | Date on which work begins                     |
| Due Date    | Expected completion date                      |
| Created At  | Date and time when the task was created       |

---

## 5. Functional Requirements

### 5.1 Create Task

The user should be able to enter task details and submit the form.

The application should send a POST request to:

```text
http://localhost:3000/tasks
```

After successful creation:

* Display a success message.
* Clear the form.
* Refresh the task list.
* Update dashboard statistics.

---

### 5.2 View All Tasks

The application should retrieve all tasks using a GET request:

```text
GET http://localhost:3000/tasks
```

The task list should display:

* Task title
* Assigned person
* Category
* Priority
* Start date
* Due date
* Status
* Edit action
* Delete action

---

### 5.3 View Task by ID

A single task should be retrievable using:

```text
GET http://localhost:3000/tasks/{id}
```

Example:

```text
GET http://localhost:3000/tasks/1
```

---

### 5.4 Update Task

When the user clicks the Edit button:

* Populate the form with the existing task details.
* Change the form heading to “Update Task.”
* Change the submit button text to “Update Task.”
* Display a Cancel Update button.

The application should send a PUT request:

```text
PUT http://localhost:3000/tasks/{id}
```

After successful update:

* Display a success message.
* Reset the form.
* Refresh the task list.
* Update statistics.

---

### 5.5 Delete Task

When the user clicks the Delete button:

* Display a confirmation modal.
* Show the selected task title.
* Allow the user to cancel or confirm deletion.

The application should send a DELETE request:

```text
DELETE http://localhost:3000/tasks/{id}
```

After successful deletion:

* Close the confirmation modal.
* Display a success message.
* Refresh the task list.
* Update dashboard statistics.

---

### 5.6 Search Tasks

The user should be able to search tasks using:

* Task title
* Description
* Assigned person
* Category
* Priority
* Status

Search results should update dynamically while the user types.

---

### 5.7 Filter Tasks

The user should be able to filter tasks based on:

* All statuses
* Pending
* In Progress
* Completed
* Cancelled

The user should also be able to filter tasks based on priority.

---

## 6. Dashboard Requirements

The application dashboard should display:

* Total Tasks
* Pending Tasks
* In Progress Tasks
* Completed Tasks

The statistics should update whenever a task is created, updated, or deleted.

---

## 7. Form Validation Requirements

The application should validate the following fields:

### Task Title

* Required
* Minimum three characters

### Description

* Required
* Minimum ten characters

### Assigned To

* Required
* Minimum three characters

### Category

* Required

### Priority

* Required

### Status

* Required

### Start Date

* Required

### Due Date

* Required
* Must not be earlier than the start date

Validation messages should appear below the corresponding fields.

---

## 8. Task Categories

The form should provide the following categories:

* Development
* Testing
* Documentation
* Training
* Meeting
* Support
* Research
* Other

---

## 9. Task Priorities

The supported priorities are:

* Low
* Medium
* High
* Critical

Each priority should use a different visual badge.

---

## 10. Task Statuses

The supported task statuses are:

* Pending
* In Progress
* Completed
* Cancelled

Each status should use a different visual badge.

---

## 11. REST API Operations

| Operation             | HTTP Method | Endpoint      |
| --------------------- | ----------- | ------------- |
| Get all tasks         | GET         | `/tasks`      |
| Get task by ID        | GET         | `/tasks/{id}` |
| Create task           | POST        | `/tasks`      |
| Replace task          | PUT         | `/tasks/{id}` |
| Partially update task | PATCH       | `/tasks/{id}` |
| Delete task           | DELETE      | `/tasks/{id}` |

Base URL:

```text
http://localhost:3000
```

---

## 12. Suggested Project Structure

```text
task-management-app/
│
├── index.html
├── db.json
├── package.json
│
├── css/
│   └── style.css
│
└── js/
    └── app.js
```

---

## 13. Sample JSON Structure

```json
{
  "tasks": [
    {
      "id": "1",
      "title": "Develop Login Page",
      "description": "Create a responsive login page with client-side validation.",
      "assignedTo": "Amit Sharma",
      "category": "Development",
      "priority": "High",
      "status": "In Progress",
      "startDate": "2026-08-01",
      "dueDate": "2026-08-10",
      "createdAt": "2026-08-01T10:30:00"
    }
  ]
}
```

---

## 14. Acceptance Criteria

The application will be considered complete when:

1. Users can create a valid task.
2. All tasks are retrieved from JSON Server.
3. Tasks are displayed in a responsive table.
4. Users can edit an existing task.
5. Users can delete a task after confirmation.
6. Search works without reloading the page.
7. Status and priority filtering work correctly.
8. Dashboard statistics are updated dynamically.
9. Validation messages are displayed correctly.
10. The application works on desktop, tablet, and mobile screens.
11. API failures display meaningful error messages.
12. The application is executed using Live Server and JSON Server.

---

## 15. Expected Learning Outcomes

After completing this project, participants should be able to:

* Build responsive user interfaces using HTML and CSS.
* Work with JavaScript events and DOM manipulation.
* Use the Fetch API.
* Perform CRUD operations.
* Work with REST endpoints.
* Use async and await.
* Handle API errors.
* Validate HTML forms.
* Search and filter JavaScript arrays.
* Use JSON Server as a mock backend.

---

# 2. Project structure

```text
task-management-app/
│
├── index.html
├── db.json
├── package.json
│
├── css/
│   └── style.css
└── js/
    └── app.js
```

---

# 3. `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0"
    >

    <meta
        name="description"
        content="Task Management System using JavaScript and JSON Server"
    >

    <title>Task Management System</title>

    <link
        rel="preconnect"
        href="https://fonts.googleapis.com"
    >

    <link
        rel="preconnect"
        href="https://fonts.gstatic.com"
        crossorigin
    >

    <link
        href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap"
        rel="stylesheet"
    >

    <link
        rel="stylesheet"
        href="css/style.css"
    >
</head>

<body>

    <!-- Header -->
    <header class="main-header">
        <div class="container header-content">

            <div class="brand">

                <div class="brand-logo">
                    TM
                </div>

                <div>
                    <h1>Task Management</h1>
                    <p>Plan, organize and complete your work</p>
                </div>

            </div>

            <div class="header-badge">
                JavaScript + JSON Server
            </div>

        </div>
    </header>


    <main class="container main-content">

        <!-- Dashboard Statistics -->
        <section class="stats-grid">

            <article class="stat-card">

                <div class="stat-icon stat-icon-blue">
                    📋
                </div>

                <div>
                    <p class="stat-label">Total Tasks</p>
                    <h2 id="totalTasks">0</h2>
                </div>

            </article>


            <article class="stat-card">

                <div class="stat-icon stat-icon-orange">
                    ⏳
                </div>

                <div>
                    <p class="stat-label">Pending Tasks</p>
                    <h2 id="pendingTasks">0</h2>
                </div>

            </article>


            <article class="stat-card">

                <div class="stat-icon stat-icon-purple">
                    ⚙️
                </div>

                <div>
                    <p class="stat-label">In Progress</p>
                    <h2 id="inProgressTasks">0</h2>
                </div>

            </article>


            <article class="stat-card">

                <div class="stat-icon stat-icon-green">
                    ✅
                </div>

                <div>
                    <p class="stat-label">Completed Tasks</p>
                    <h2 id="completedTasks">0</h2>
                </div>

            </article>

        </section>


        <section class="content-grid">

            <!-- Task Form -->
            <article class="card form-card">

                <div class="card-header">
                    <span class="section-label">
                        Task Form
                    </span>

                    <h2 id="formTitle">
                        Add New Task
                    </h2>

                    <p>
                        Enter the details of the task below.
                    </p>
                </div>


                <form id="taskForm" novalidate>

                    <input
                        type="hidden"
                        id="taskId"
                    >


                    <div class="form-group">

                        <label for="taskTitle">
                            Task Title
                            <span class="required">*</span>
                        </label>

                        <input
                            type="text"
                            id="taskTitle"
                            name="taskTitle"
                            placeholder="Enter task title"
                            required
                        >

                        <small
                            id="taskTitleError"
                            class="error-message"
                        ></small>

                    </div>


                    <div class="form-group">

                        <label for="taskDescription">
                            Description
                            <span class="required">*</span>
                        </label>

                        <textarea
                            id="taskDescription"
                            name="taskDescription"
                            rows="4"
                            placeholder="Enter detailed task description"
                            required
                        ></textarea>

                        <small
                            id="taskDescriptionError"
                            class="error-message"
                        ></small>

                    </div>


                    <div class="form-group">

                        <label for="assignedTo">
                            Assigned To
                            <span class="required">*</span>
                        </label>

                        <input
                            type="text"
                            id="assignedTo"
                            name="assignedTo"
                            placeholder="Enter assignee name"
                            required
                        >

                        <small
                            id="assignedToError"
                            class="error-message"
                        ></small>

                    </div>


                    <div class="form-row">

                        <div class="form-group">

                            <label for="taskCategory">
                                Category
                                <span class="required">*</span>
                            </label>

                            <select
                                id="taskCategory"
                                name="taskCategory"
                                required
                            >
                                <option value="">
                                    Select category
                                </option>

                                <option value="Development">
                                    Development
                                </option>

                                <option value="Testing">
                                    Testing
                                </option>

                                <option value="Documentation">
                                    Documentation
                                </option>

                                <option value="Training">
                                    Training
                                </option>

                                <option value="Meeting">
                                    Meeting
                                </option>

                                <option value="Support">
                                    Support
                                </option>

                                <option value="Research">
                                    Research
                                </option>

                                <option value="Other">
                                    Other
                                </option>
                            </select>

                            <small
                                id="taskCategoryError"
                                class="error-message"
                            ></small>

                        </div>


                        <div class="form-group">

                            <label for="taskPriority">
                                Priority
                                <span class="required">*</span>
                            </label>

                            <select
                                id="taskPriority"
                                name="taskPriority"
                                required
                            >
                                <option value="">
                                    Select priority
                                </option>

                                <option value="Low">
                                    Low
                                </option>

                                <option value="Medium">
                                    Medium
                                </option>

                                <option value="High">
                                    High
                                </option>

                                <option value="Critical">
                                    Critical
                                </option>
                            </select>

                            <small
                                id="taskPriorityError"
                                class="error-message"
                            ></small>

                        </div>

                    </div>


                    <div class="form-group">

                        <label for="taskStatus">
                            Task Status
                            <span class="required">*</span>
                        </label>

                        <select
                            id="taskStatus"
                            name="taskStatus"
                            required
                        >
                            <option value="Pending">
                                Pending
                            </option>

                            <option value="In Progress">
                                In Progress
                            </option>

                            <option value="Completed">
                                Completed
                            </option>

                            <option value="Cancelled">
                                Cancelled
                            </option>
                        </select>

                        <small
                            id="taskStatusError"
                            class="error-message"
                        ></small>

                    </div>


                    <div class="form-row">

                        <div class="form-group">

                            <label for="taskStartDate">
                                Start Date
                                <span class="required">*</span>
                            </label>

                            <input
                                type="date"
                                id="taskStartDate"
                                name="taskStartDate"
                                required
                            >

                            <small
                                id="taskStartDateError"
                                class="error-message"
                            ></small>

                        </div>


                        <div class="form-group">

                            <label for="taskDueDate">
                                Due Date
                                <span class="required">*</span>
                            </label>

                            <input
                                type="date"
                                id="taskDueDate"
                                name="taskDueDate"
                                required
                            >

                            <small
                                id="taskDueDateError"
                                class="error-message"
                            ></small>

                        </div>

                    </div>


                    <div class="form-actions">

                        <button
                            type="submit"
                            id="submitButton"
                            class="btn btn-primary"
                        >
                            <span id="submitButtonText">
                                Add Task
                            </span>
                        </button>


                        <button
                            type="button"
                            id="cancelButton"
                            class="btn btn-secondary hidden"
                        >
                            Cancel Update
                        </button>


                        <button
                            type="reset"
                            id="resetButton"
                            class="btn btn-light"
                        >
                            Reset
                        </button>

                    </div>

                </form>

            </article>


            <!-- Task List -->
            <article class="card task-list-card">

                <div class="list-header">

                    <div>
                        <span class="section-label">
                            Task Directory
                        </span>

                        <h2>Task List</h2>
                    </div>


                    <div class="list-controls">

                        <div class="search-wrapper">

                            <span class="search-icon">
                                ⌕
                            </span>

                            <input
                                type="search"
                                id="searchInput"
                                placeholder="Search tasks..."
                                aria-label="Search tasks"
                            >

                        </div>


                        <select
                            id="statusFilter"
                            class="filter-select"
                            aria-label="Filter tasks by status"
                        >
                            <option value="All">
                                All Statuses
                            </option>

                            <option value="Pending">
                                Pending
                            </option>

                            <option value="In Progress">
                                In Progress
                            </option>

                            <option value="Completed">
                                Completed
                            </option>

                            <option value="Cancelled">
                                Cancelled
                            </option>
                        </select>


                        <select
                            id="priorityFilter"
                            class="filter-select"
                            aria-label="Filter tasks by priority"
                        >
                            <option value="All">
                                All Priorities
                            </option>

                            <option value="Low">
                                Low
                            </option>

                            <option value="Medium">
                                Medium
                            </option>

                            <option value="High">
                                High
                            </option>

                            <option value="Critical">
                                Critical
                            </option>
                        </select>

                    </div>

                </div>


                <div
                    id="notification"
                    class="notification hidden"
                    role="alert"
                ></div>


                <div
                    id="loadingIndicator"
                    class="loading-container hidden"
                >
                    <div class="spinner"></div>

                    <p>Loading tasks...</p>
                </div>


                <div class="table-responsive">

                    <table class="task-table">

                        <thead>
                            <tr>
                                <th>Task</th>
                                <th>Assigned To</th>
                                <th>Category</th>
                                <th>Priority</th>
                                <th>Start Date</th>
                                <th>Due Date</th>
                                <th>Status</th>
                                <th class="action-column">
                                    Actions
                                </th>
                            </tr>
                        </thead>

                        <tbody id="taskTableBody">

                            <!-- Task rows will be inserted here -->

                        </tbody>

                    </table>

                </div>


                <div
                    id="emptyState"
                    class="empty-state hidden"
                >

                    <div class="empty-icon">
                        📝
                    </div>

                    <h3>No tasks found</h3>

                    <p>
                        Add your first task using the task form.
                    </p>

                </div>


                <div class="table-footer">

                    <p>
                        Showing
                        <strong id="displayedTaskCount">
                            0
                        </strong>
                        task(s)
                    </p>

                </div>

            </article>

        </section>

    </main>


    <!-- Delete Confirmation Modal -->
    <div
        id="deleteModal"
        class="modal-overlay hidden"
    >

        <div
            class="modal"
            role="dialog"
            aria-modal="true"
            aria-labelledby="deleteModalTitle"
        >

            <div class="modal-icon">
                ⚠️
            </div>

            <h2 id="deleteModalTitle">
                Delete Task?
            </h2>

            <p>
                Are you sure you want to delete
                <strong id="deleteTaskTitle">
                    this task
                </strong>?
                This action cannot be undone.
            </p>

            <div class="modal-actions">

                <button
                    type="button"
                    id="cancelDeleteButton"
                    class="btn btn-secondary"
                >
                    Cancel
                </button>

                <button
                    type="button"
                    id="confirmDeleteButton"
                    class="btn btn-danger"
                >
                    Delete Task
                </button>

            </div>

        </div>

    </div>


    <footer class="main-footer">

        <div class="container">

            <p>
                Task Management System using JavaScript and JSON Server
            </p>

        </div>

    </footer>


    <script src="js/app.js"></script>

</body>
</html>
```

---

# 4. `css/style.css`

```css
/* =====================================================
   Global Variables
===================================================== */

:root {
    --primary-color: #2563eb;
    --primary-dark: #1d4ed8;
    --primary-light: #eff6ff;

    --success-color: #16a34a;
    --success-light: #dcfce7;

    --warning-color: #d97706;
    --warning-light: #fef3c7;

    --danger-color: #dc2626;
    --danger-dark: #b91c1c;
    --danger-light: #fee2e2;

    --purple-color: #7c3aed;
    --purple-light: #ede9fe;

    --orange-color: #ea580c;
    --orange-light: #ffedd5;

    --cyan-color: #0891b2;
    --cyan-light: #cffafe;

    --text-primary: #111827;
    --text-secondary: #6b7280;
    --text-muted: #9ca3af;

    --border-color: #e5e7eb;
    --background-color: #f4f7fc;
    --white-color: #ffffff;

    --shadow-sm:
        0 1px 3px rgba(15, 23, 42, 0.06);

    --shadow-md:
        0 10px 30px rgba(15, 23, 42, 0.09);

    --shadow-lg:
        0 20px 45px rgba(15, 23, 42, 0.18);

    --border-radius-sm: 8px;
    --border-radius-md: 14px;
    --border-radius-lg: 20px;

    --transition: 0.25s ease;
}


/* =====================================================
   Reset and Base Styles
===================================================== */

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    scroll-behavior: smooth;
}

body {
    min-height: 100vh;

    background:
        radial-gradient(
            circle at top left,
            rgba(37, 99, 235, 0.09),
            transparent 30%
        ),
        radial-gradient(
            circle at bottom right,
            rgba(124, 58, 237, 0.07),
            transparent 28%
        ),
        var(--background-color);

    color: var(--text-primary);
    font-family: "Inter", Arial, sans-serif;
    line-height: 1.6;
}

button,
input,
select,
textarea {
    font: inherit;
}

button {
    border: none;
    cursor: pointer;
}

textarea {
    resize: vertical;
}

.container {
    width: min(1500px, calc(100% - 40px));
    margin-inline: auto;
}

.hidden {
    display: none !important;
}


/* =====================================================
   Header
===================================================== */

.main-header {
    position: sticky;
    top: 0;
    z-index: 100;

    padding: 21px 0;

    background: rgba(255, 255, 255, 0.93);
    border-bottom: 1px solid var(--border-color);
    box-shadow: var(--shadow-sm);

    backdrop-filter: blur(12px);
}

.header-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
}

.brand {
    display: flex;
    align-items: center;
    gap: 14px;
}

.brand-logo {
    width: 52px;
    height: 52px;

    display: grid;
    place-items: center;

    background: linear-gradient(
        135deg,
        var(--primary-color),
        var(--purple-color)
    );

    color: var(--white-color);
    border-radius: 15px;

    font-size: 17px;
    font-weight: 700;

    box-shadow:
        0 9px 20px rgba(37, 99, 235, 0.25);
}

.brand h1 {
    font-size: 21px;
    line-height: 1.3;
}

.brand p {
    color: var(--text-secondary);
    font-size: 13px;
}

.header-badge {
    padding: 9px 14px;

    background: var(--primary-light);
    color: var(--primary-dark);

    border: 1px solid #bfdbfe;
    border-radius: 999px;

    font-size: 12px;
    font-weight: 600;
}


/* =====================================================
   Main Content
===================================================== */

.main-content {
    padding-top: 32px;
    padding-bottom: 50px;
}


/* =====================================================
   Statistics
===================================================== */

.stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);

    gap: 20px;
    margin-bottom: 25px;
}

.stat-card {
    display: flex;
    align-items: center;
    gap: 17px;

    padding: 21px;

    background: var(--white-color);
    border: 1px solid var(--border-color);
    border-radius: var(--border-radius-md);

    box-shadow: var(--shadow-sm);

    transition:
        transform var(--transition),
        box-shadow var(--transition);
}

.stat-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-md);
}

.stat-icon {
    width: 52px;
    height: 52px;

    display: grid;
    place-items: center;
    flex-shrink: 0;

    border-radius: 14px;
    font-size: 24px;
}

.stat-icon-blue {
    background: var(--primary-light);
}

.stat-icon-orange {
    background: var(--orange-light);
}

.stat-icon-purple {
    background: var(--purple-light);
}

.stat-icon-green {
    background: var(--success-light);
}

.stat-label {
    margin-bottom: 3px;

    color: var(--text-secondary);
    font-size: 13px;
    font-weight: 500;
}

.stat-card h2 {
    font-size: 27px;
    line-height: 1.2;
}


/* =====================================================
   Main Layout
===================================================== */

.content-grid {
    display: grid;
    grid-template-columns: 400px minmax(0, 1fr);

    gap: 24px;
    align-items: start;
}

.card {
    background: var(--white-color);
    border: 1px solid var(--border-color);
    border-radius: var(--border-radius-md);

    box-shadow: var(--shadow-sm);
}

.form-card {
    position: sticky;
    top: 117px;

    padding: 25px;
}

.task-list-card {
    min-width: 0;
    overflow: hidden;
}

.card-header {
    margin-bottom: 22px;
}

.card-header h2,
.list-header h2 {
    font-size: 21px;
}

.card-header p {
    margin-top: 4px;

    color: var(--text-secondary);
    font-size: 12px;
}

.section-label {
    display: block;

    margin-bottom: 3px;

    color: var(--primary-color);

    font-size: 11px;
    font-weight: 700;
    letter-spacing: 1.1px;

    text-transform: uppercase;
}


/* =====================================================
   Form Styles
===================================================== */

.form-group {
    margin-bottom: 18px;
}

.form-row {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
}

label {
    display: block;

    margin-bottom: 7px;

    color: #374151;
    font-size: 13px;
    font-weight: 600;
}

.required {
    color: var(--danger-color);
}

input,
select,
textarea {
    width: 100%;

    padding: 0 13px;

    background: #fafafa;
    color: var(--text-primary);

    border: 1px solid #d1d5db;
    border-radius: var(--border-radius-sm);

    outline: none;

    transition:
        border-color var(--transition),
        box-shadow var(--transition),
        background-color var(--transition);
}

input,
select {
    height: 45px;
}

textarea {
    min-height: 105px;
    padding-top: 11px;
    padding-bottom: 11px;
}

input::placeholder,
textarea::placeholder {
    color: var(--text-muted);
}

input:hover,
select:hover,
textarea:hover {
    border-color: #9ca3af;
}

input:focus,
select:focus,
textarea:focus {
    background: var(--white-color);

    border-color: var(--primary-color);

    box-shadow:
        0 0 0 4px rgba(37, 99, 235, 0.11);
}

input.input-error,
select.input-error,
textarea.input-error {
    border-color: var(--danger-color);

    box-shadow:
        0 0 0 3px rgba(220, 38, 38, 0.1);
}

.error-message {
    display: block;

    min-height: 17px;
    margin-top: 4px;

    color: var(--danger-color);
    font-size: 11px;
}

.form-actions {
    display: flex;
    flex-wrap: wrap;

    gap: 10px;
    margin-top: 6px;
}


/* =====================================================
   Buttons
===================================================== */

.btn {
    min-height: 42px;
    padding: 10px 17px;

    border-radius: var(--border-radius-sm);

    font-size: 13px;
    font-weight: 600;

    transition:
        transform var(--transition),
        background-color var(--transition),
        box-shadow var(--transition);
}

.btn:hover {
    transform: translateY(-1px);
}

.btn:active {
    transform: translateY(0);
}

.btn:disabled {
    cursor: not-allowed;
    opacity: 0.65;
    transform: none;
}

.btn-primary {
    background: var(--primary-color);
    color: var(--white-color);

    box-shadow:
        0 5px 13px rgba(37, 99, 235, 0.24);
}

.btn-primary:hover {
    background: var(--primary-dark);
}

.btn-secondary {
    background: #e5e7eb;
    color: #374151;
}

.btn-secondary:hover {
    background: #d1d5db;
}

.btn-light {
    background: var(--white-color);
    color: var(--text-secondary);

    border: 1px solid var(--border-color);
}

.btn-light:hover {
    background: #f9fafb;
}

.btn-danger {
    background: var(--danger-color);
    color: var(--white-color);
}

.btn-danger:hover {
    background: var(--danger-dark);
}


/* =====================================================
   Task List Header and Controls
===================================================== */

.list-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;

    gap: 20px;
    padding: 22px 24px;

    border-bottom: 1px solid var(--border-color);
}

.list-controls {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    flex-wrap: wrap;

    gap: 10px;
}

.search-wrapper {
    width: 250px;
    position: relative;
}

.search-wrapper input {
    height: 42px;
    padding-left: 39px;

    background: var(--white-color);
}

.search-icon {
    position: absolute;
    top: 50%;
    left: 14px;

    color: var(--text-secondary);
    font-size: 22px;
    line-height: 1;

    transform: translateY(-53%);
    pointer-events: none;
}

.filter-select {
    width: auto;
    min-width: 145px;
    height: 42px;

    background: var(--white-color);
}


/* =====================================================
   Notifications
===================================================== */

.notification {
    margin: 17px 24px 0;
    padding: 12px 15px;

    border: 1px solid transparent;
    border-radius: var(--border-radius-sm);

    font-size: 13px;
    font-weight: 500;
}

.notification-success {
    background: var(--success-light);
    color: #166534;
    border-color: #86efac;
}

.notification-error {
    background: var(--danger-light);
    color: #991b1b;
    border-color: #fca5a5;
}

.notification-warning {
    background: var(--warning-light);
    color: #92400e;
    border-color: #fcd34d;
}


/* =====================================================
   Task Table
===================================================== */

.table-responsive {
    width: 100%;
    overflow-x: auto;
}

.task-table {
    width: 100%;

    border-collapse: collapse;
    white-space: nowrap;
}

.task-table th {
    padding: 14px 16px;

    background: #f9fafb;
    color: var(--text-secondary);

    border-bottom: 1px solid var(--border-color);

    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.4px;

    text-align: left;
    text-transform: uppercase;
}

.task-table td {
    padding: 16px;

    border-bottom: 1px solid #f0f1f4;

    color: #374151;
    font-size: 13px;
    vertical-align: middle;
}

.task-table tbody tr {
    transition: background-color var(--transition);
}

.task-table tbody tr:hover {
    background: #fafcff;
}

.task-table tbody tr:last-child td {
    border-bottom: none;
}


/* =====================================================
   Task Display
===================================================== */

.task-info {
    display: flex;
    align-items: center;
    gap: 11px;
}

.task-icon {
    width: 40px;
    height: 40px;

    display: grid;
    place-items: center;
    flex-shrink: 0;

    background: linear-gradient(
        135deg,
        var(--primary-color),
        var(--purple-color)
    );

    color: var(--white-color);
    border-radius: 11px;

    font-size: 17px;
}

.task-details {
    max-width: 260px;
}

.task-details h4 {
    margin-bottom: 2px;

    color: var(--text-primary);

    font-size: 13px;
    font-weight: 600;

    overflow: hidden;
    text-overflow: ellipsis;
}

.task-details p {
    max-width: 250px;

    color: var(--text-secondary);
    font-size: 11px;

    overflow: hidden;
    text-overflow: ellipsis;
}


/* =====================================================
   Status Badges
===================================================== */

.status-badge,
.priority-badge,
.category-badge {
    display: inline-flex;
    align-items: center;

    padding: 5px 10px;
    border-radius: 999px;

    font-size: 11px;
    font-weight: 600;
}

.status-pending {
    background: var(--warning-light);
    color: #92400e;
}

.status-in-progress {
    background: var(--primary-light);
    color: var(--primary-dark);
}

.status-completed {
    background: var(--success-light);
    color: #166534;
}

.status-cancelled {
    background: #f3f4f6;
    color: #4b5563;
}


/* =====================================================
   Priority Badges
===================================================== */

.priority-low {
    background: var(--success-light);
    color: #166534;
}

.priority-medium {
    background: var(--cyan-light);
    color: #155e75;
}

.priority-high {
    background: var(--orange-light);
    color: #9a3412;
}

.priority-critical {
    background: var(--danger-light);
    color: #991b1b;
}


/* =====================================================
   Category Badge
===================================================== */

.category-badge {
    background: var(--purple-light);
    color: #5b21b6;
}


/* =====================================================
   Action Buttons
===================================================== */

.action-column {
    text-align: center !important;
}

.action-buttons {
    display: flex;
    align-items: center;
    justify-content: center;

    gap: 7px;
}

.action-btn {
    width: 34px;
    height: 34px;

    display: grid;
    place-items: center;

    background: transparent;
    border-radius: 7px;

    font-size: 15px;

    transition:
        background-color var(--transition),
        transform var(--transition);
}

.action-btn:hover {
    transform: translateY(-1px);
}

.edit-btn {
    color: var(--primary-color);
    background: var(--primary-light);
}

.edit-btn:hover {
    background: #dbeafe;
}

.delete-btn {
    color: var(--danger-color);
    background: var(--danger-light);
}

.delete-btn:hover {
    background: #fecaca;
}


/* =====================================================
   Empty State
===================================================== */

.empty-state {
    padding: 55px 20px;
    text-align: center;
}

.empty-icon {
    width: 70px;
    height: 70px;

    display: grid;
    place-items: center;

    margin: 0 auto 16px;

    background: var(--primary-light);
    border-radius: 50%;

    font-size: 30px;
}

.empty-state h3 {
    margin-bottom: 5px;
    font-size: 17px;
}

.empty-state p {
    color: var(--text-secondary);
    font-size: 13px;
}

.table-footer {
    padding: 14px 20px;

    background: #fafafa;
    border-top: 1px solid var(--border-color);
}

.table-footer p {
    color: var(--text-secondary);
    font-size: 12px;
}


/* =====================================================
   Loading Spinner
===================================================== */

.loading-container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    gap: 12px;
    padding: 50px 20px;

    color: var(--text-secondary);
    font-size: 13px;
}

.spinner {
    width: 38px;
    height: 38px;

    border: 4px solid #e5e7eb;
    border-top-color: var(--primary-color);
    border-radius: 50%;

    animation: spin 0.8s linear infinite;
}

@keyframes spin {
    to {
        transform: rotate(360deg);
    }
}


/* =====================================================
   Delete Modal
===================================================== */

.modal-overlay {
    position: fixed;
    inset: 0;
    z-index: 1000;

    display: grid;
    place-items: center;

    padding: 20px;

    background: rgba(15, 23, 42, 0.58);

    backdrop-filter: blur(4px);
}

.modal {
    width: min(430px, 100%);

    padding: 30px;

    background: var(--white-color);
    border-radius: var(--border-radius-lg);

    box-shadow: var(--shadow-lg);
    text-align: center;

    animation: modalOpen 0.2s ease;
}

@keyframes modalOpen {
    from {
        opacity: 0;
        transform: scale(0.94);
    }

    to {
        opacity: 1;
        transform: scale(1);
    }
}

.modal-icon {
    width: 65px;
    height: 65px;

    display: grid;
    place-items: center;

    margin: 0 auto 17px;

    background: var(--danger-light);
    border-radius: 50%;

    font-size: 29px;
}

.modal h2 {
    margin-bottom: 9px;
    font-size: 21px;
}

.modal p {
    color: var(--text-secondary);
    font-size: 13px;
}

.modal-actions {
    display: flex;
    justify-content: center;

    gap: 10px;
    margin-top: 25px;
}


/* =====================================================
   Footer
===================================================== */

.main-footer {
    padding: 20px 0;

    background: var(--white-color);
    border-top: 1px solid var(--border-color);

    text-align: center;
}

.main-footer p {
    color: var(--text-secondary);
    font-size: 12px;
}


/* =====================================================
   Responsive Design
===================================================== */

@media (max-width: 1250px) {

    .content-grid {
        grid-template-columns: 1fr;
    }

    .form-card {
        position: static;
    }
}


@media (max-width: 1000px) {

    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .list-header {
        flex-direction: column;
    }

    .list-controls {
        width: 100%;
        justify-content: flex-start;
    }
}


@media (max-width: 750px) {

    .container {
        width: min(100% - 24px, 1500px);
    }

    .list-controls {
        display: grid;
        grid-template-columns: 1fr;
    }

    .search-wrapper,
    .filter-select {
        width: 100%;
    }

    .header-badge {
        display: none;
    }
}


@media (max-width: 600px) {

    .main-header {
        padding: 15px 0;
    }

    .brand-logo {
        width: 45px;
        height: 45px;

        border-radius: 12px;
    }

    .brand h1 {
        font-size: 17px;
    }

    .brand p {
        display: none;
    }

    .main-content {
        padding-top: 20px;
    }

    .stats-grid {
        grid-template-columns: 1fr;
    }

    .form-card {
        padding: 20px;
    }

    .form-row {
        grid-template-columns: 1fr;
        gap: 0;
    }

    .form-actions {
        flex-direction: column;
    }

    .form-actions .btn {
        width: 100%;
    }

    .list-header {
        padding: 20px;
    }

    .modal-actions {
        flex-direction: column-reverse;
    }

    .modal-actions .btn {
        width: 100%;
    }
}
```

The corresponding JSON Server endpoint will be:

```text
http://localhost:3000/tasks
```

Initial `db.json` structure:

```json
{
  "tasks": []
}
```

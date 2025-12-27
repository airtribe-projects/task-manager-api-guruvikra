# Task Manager API

## Overview
This is a RESTful API built with Node.js and Express for managing tasks. It provides endpoints to create, read, update, and delete tasks. Additionally, it supports features like filtering tasks by completion status, sorting by creation date, and categorizing tasks by priority levels.

## Setup Instructions

### Prerequisites
- Node.js (version 18.0.0 or higher)
- npm (Node Package Manager)

### Installation
1. Clone the repository or navigate to the project directory.
2. Install the dependencies:
   ```bash
   npm install
   ```

### Running the Server
To start the API server:
```bash
node src/server.js
```
The server will start on port 3000 (default) or the port specified in the `PORT` environment variable.

## API Documentation

### Base URL
`http://localhost:3000`

### Endpoints

#### 1. Get All Tasks
Retrieve a list of all tasks.
- **URL:** `/tasks`
- **Method:** `GET`
- **Query Parameters:**
  - `completed` (optional): Filter by completion status (`true` or `false`).
  - `sort` (optional): Sort by field. Use `createdAt` to sort by creation date.
- **Example:** 
  - `GET /tasks?completed=false`
  - `GET /tasks?sort=createdAt`

#### 2. Create a Task
Create a new task.
- **URL:** `/tasks`
- **Method:** `POST`
- **Body:**
  ```json
  {
    "title": "Task Title",
    "description": "Task Description",
    "completed": false, // Optional, default: false
    "priority": "medium" // Optional, default: "low". Values: "low", "medium", "high"
  }
  ```
- **Response:** 201 Created

#### 3. Get Task by Priority
Retrieve tasks filtered by a specific priority level.
- **URL:** `/tasks/priority/:level`
- **Method:** `GET`
- **URL Params:**
  - `level`: Priority level (`low`, `medium`, `high`).
- **Example:** `GET /tasks/priority/high`

#### 4. Get Task by ID
Retrieve a single task by its unique ID.
- **URL:** `/tasks/:id`
- **Method:** `GET`
- **URL Params:**
  - `id`: The numeric ID of the task.
- **Response:** 200 OK or 404 Not Found

#### 5. Update a Task
Update an existing task.
- **URL:** `/tasks/:id`
- **Method:** `PUT`
- **Body:** (Any combination of fields)
  ```json
  {
    "title": "Updated Title",
    "completed": true,
    "priority": "high"
  }
  ```
- **Response:** 200 OK or 404 Not Found

#### 6. Delete a Task
Delete a task by its ID.
- **URL:** `/tasks/:id`
- **Method:** `DELETE`
- **Response:** 200 OK or 404 Not Found

## Testing

### Automated Tests
This project includes a test suite using `tap`. To run the automated tests:
```bash
npm test
```

### Manual Testing
You can test the API using tools like Postman, Insomnia, or `curl`.

**Example using curl:**
```bash
# Create a task
curl -X POST http://localhost:3000/tasks \
     -H "Content-Type: application/json" \
     -d '{"title": "Buy groceries", "description": "Milk and eggs", "priority": "high"}'

# Get all tasks
curl http://localhost:3000/tasks
```

# Act1-ToDoList - Backend Documentation

## Overview
A simple task management API built with NestJS and TypeORM. Allows users to create, read, update, and delete tasks.

## Architecture

### Technology Stack
- **Framework**: NestJS
- **Database**: MySQL with TypeORM
- **Language**: TypeScript

### Project Structure
```
backend/src/
├── main.ts                 # Application entry point
├── app.module.ts          # Root module configuration
├── app.controller.ts      # Root controller (health check)
├── app.service.ts         # Root service
└── tasks/                 # Tasks feature module
    ├── tasks.module.ts    # Tasks module configuration
    ├── tasks.controller.ts # HTTP request handlers
    ├── tasks.service.ts   # Business logic
    ├── entities/
    │   └── task.entity.ts # Task database entity
    └── dto/               # Data Transfer Objects
        ├── create-task.dto.ts
        └── update-task.dto.ts
```

## File-by-File Breakdown

### 1. `main.ts`
**Purpose**: Application bootstrap and server configuration

**Process**:
1. Creates NestJS application instance
2. Enables CORS for frontend communication (allows requests from `http://localhost:5173`)
3. Starts HTTP server on port 3000 (or from `process.env.PORT`)

**Key Features**:
- CORS enabled for frontend integration
- Configurable port via environment variable

### 2. `app.module.ts`
**Purpose**: Root application module - configures all dependencies

**Process**:
1. Imports `ConfigModule` for environment variable access (global)
2. Configures TypeORM database connection asynchronously:
   - Reads database credentials from `.env` file via `ConfigService`
   - Connects to MySQL database
   - Auto-loads all entity files matching `*.entity.ts` pattern
3. Imports `TasksModule` to enable task management functionality

**Key Features**:
- Environment-based configuration
- Automatic entity discovery
- Async database connection setup

### 3. `tasks.module.ts`
**Purpose**: Tasks feature module configuration

**Process**:
1. Imports `TypeOrmModule.forFeature([Task])` to register Task entity repository
2. Registers `TasksController` and `TasksService` as providers
3. Exports `TasksService` for use in other modules (if needed)

### 4. `task.entity.ts`
**Purpose**: Defines the Task database table structure

**Properties**:
- `id`: Primary key (auto-increment)
- `title`: Task title (string)
- `completed`: Completion status (boolean, default: false)
- `created_at`: Creation timestamp (auto-generated)

**Process**:
- TypeORM decorators define table columns
- Entity is used by repository for database operations

### 5. `tasks.controller.ts`
**Purpose**: Handles HTTP requests and routes them to service methods

**Endpoints**:
- `GET /tasks` → `findAll()` - Get all tasks
- `GET /tasks/:id` → `findOne(id)` - Get single task
- `POST /tasks` → `create(title)` - Create new task
- `PATCH /tasks/:id` → `update(id, update)` - Update task
- `DELETE /tasks/:id` → `remove(id)` - Delete task

**Process Flow**:
1. Receives HTTP request
2. Extracts parameters/body from request
3. Calls corresponding service method
4. Returns service response to client

### 6. `tasks.service.ts`
**Purpose**: Contains all business logic for task operations

**Methods**:

#### `findAll()`
- **Process**: Queries database for all tasks using TypeORM repository
- **Returns**: Array of all tasks

#### `findOne(id)`
- **Process**: 
  1. Searches for task by ID
  2. Throws `NotFoundException` if not found
  3. Returns task if found
- **Returns**: Single task object

#### `create(title)`
- **Process**:
  1. Creates new Task entity with provided title
  2. Sets `completed` to `false` by default
  3. Saves to database
  4. Returns created task
- **Returns**: Newly created task

#### `update(id, update)`
- **Process**:
  1. Updates task fields with provided data
  2. Saves changes to database
  3. Retrieves and returns updated task
- **Returns**: Updated task object

#### `remove(id)`
- **Process**:
  1. Attempts to delete task by ID
  2. Checks if any rows were affected
  3. Throws `NotFoundException` if task doesn't exist
- **Returns**: Promise that resolves when deleted

## Data Flow

### Creating a Task
```
Client Request (POST /tasks)
    ↓
TasksController.create()
    ↓
TasksService.create()
    ↓
Task Repository.save()
    ↓
MySQL Database
    ↓
Response (Task object)
```

### Reading Tasks
```
Client Request (GET /tasks)
    ↓
TasksController.findAll()
    ↓
TasksService.findAll()
    ↓
Task Repository.find()
    ↓
MySQL Database
    ↓
Response (Array of tasks)
```

## Database Schema

### Tasks Table
```sql
CREATE TABLE task (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    completed BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Environment Variables

Required in `.env` file:
```env
DATABASE_HOST=localhost
DATABASE_PORT=3306
DATABASE_USER=root
DATABASE_PASSWORD=
DATABASE_NAME=activity
```

## Error Handling

- **404 Not Found**: When task ID doesn't exist (in `findOne` and `remove`)
- **500 Internal Server Error**: Database connection issues or other server errors

## Security Considerations

- No authentication required (simple CRUD API)
- Input validation should be added for production
- SQL injection protection via TypeORM parameterized queries

## Testing Recommendations

1. Test all CRUD operations
2. Test error cases (non-existent IDs)
3. Test with empty database
4. Test with large datasets
5. Verify CORS is working correctly



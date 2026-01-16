# Act1 - ToDo List Application

A full-stack ToDo List application built with NestJS backend and React frontend.

## 🚀 Tech Stack

### Backend
- **NestJS** - Progressive Node.js framework
- **TypeScript** - Type-safe JavaScript
- **RESTful API** - Standard HTTP methods

### Frontend
- **React** - UI library
- **Vite** - Fast build tool
- **CSS** - Styling

## 📁 Project Structure

```
Act1-ToDoList/
├── backend/          # NestJS REST API
│   ├── src/
│   │   ├── tasks/    # Tasks module (controller, service, DTOs)
│   │   └── main.ts   # Entry point
│   └── package.json
└── frontend/         # React application
    ├── src/
    │   ├── App.jsx   # Main component
    │   └── main.jsx  # Entry point
    └── package.json
```

## 🛠️ Setup Instructions

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Backend Setup

1. Navigate to backend directory:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Configure environment variables:
   - Copy `.env.example` to `.env` (if exists)
   - Update the `.env` file with your configuration

4. Start the development server:
   ```bash
   npm run start:dev
   ```

The backend will run on `http://localhost:3000` (default)

### Frontend Setup

1. Navigate to frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

The frontend will run on `http://localhost:5173` (default for Vite)

## 🎯 Features

- ✅ Create new tasks
- ✅ View all tasks
- ✅ Update task details
- ✅ Delete tasks
- ✅ Mark tasks as complete/incomplete

## 📝 API Endpoints

- `GET /tasks` - Get all tasks
- `GET /tasks/:id` - Get task by ID
- `POST /tasks` - Create new task
- `PATCH /tasks/:id` - Update task
- `DELETE /tasks/:id` - Delete task

## 🧪 Testing

### Backend Tests
```bash
cd backend
npm run test
```

### End-to-End Tests
```bash
cd backend
npm run test:e2e
```

## 📚 Documentation

- Backend API documentation: [backend/BACKEND_DOCUMENTATION.md](backend/BACKEND_DOCUMENTATION.md)
- Backend README: [backend/README.md](backend/README.md)
- Frontend README: [frontend/README.md](frontend/README.md)

## 👨‍💻 Development

### Backend Development
The backend uses NestJS with the following structure:
- **Controllers** - Handle HTTP requests
- **Services** - Business logic
- **DTOs** - Data transfer objects for validation
- **Entities** - Data models

### Frontend Development
The frontend is built with React and uses:
- Functional components with hooks
- CSS for styling
- Fetch API for backend communication

## 🚢 Deployment

Refer to individual README files in backend and frontend directories for deployment instructions.

## 📄 License

This project is part of Laboratory Activities coursework.

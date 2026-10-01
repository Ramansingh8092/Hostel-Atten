# 🏨 Hostel-Attn — Hostel Attendance Management System

Hostel-Attn is a full-stack web application for managing hostel students and recording their daily attendance digitally. It provides student management, room-wise attendance entry, attendance analysis, user authentication, and admin-level user management through a React frontend and an Express/MongoDB backend.

## ✨ Features

### 👨‍🎓 Student Management
- Add new students with hostel and contact information.
- View student details including name, address, category/stream, city, contacts, room, block, image, and current status.
- Edit student information.
- Update a student's status between `Hostel`, `Outside`, and `Home`.
- Delete student records.
- Search students by name.
- Paginate student records.
- View students in either grid or table format.
- Filter students by room number for attendance entry.

### 📝 Attendance Management
- Select a hostel room and load the students assigned to that room.
- Record attendance for each student.
- Attendance values supported by the application include `Hostel`, `Home`, and `outside`.
- Update attendance records for a day across multiple rooms.
- View attendance for a selected date.
- Delete attendance records older than a specified number of days.
- Export attendance analysis as a CSV file.

### 🔐 Authentication & Authorization
- User registration and login.
- JWT-based authentication.
- Password hashing using bcrypt.
- Protected application routes and API endpoints.
- Admin role support.
- Admin users can view, edit, and delete application users.
- Users can view and update their own profile.

## 🛠️ Technology Stack

### Frontend
- React 17
- React Router
- Redux
- Redux Thunk
- React Bootstrap
- Axios
- React Datepicker
- React CSV

### Backend
- Node.js
- Express.js
- MongoDB
- Mongoose
- JWT (JSON Web Token)
- bcryptjs
- dotenv
- Express Async Handler
- Morgan
- Multer

### Development Tools
- Nodemon
- Concurrently
- npm
- Git & GitHub

## 🏗️ Application Architecture

```text
┌───────────────────────────┐
│       React Frontend      │
│ React + Redux + Bootstrap │
└─────────────┬─────────────┘
              │ HTTP / Axios
              ▼
┌───────────────────────────┐
│      Express Backend      │
│   REST API + Middleware   │
└─────────────┬─────────────┘
              │ Mongoose
              ▼
┌───────────────────────────┐
│          MongoDB          │
│ Users / Students /        │
│ Attendance                │
└───────────────────────────┘
```

## 📂 Project Structure

```text
Hostel-Atten/
└── Hostel-Management-master/
    ├── frontend/
    │   ├── public/
    │   └── src/
    │       ├── actions/
    │       ├── components/
    │       ├── constants/
    │       ├── css/
    │       ├── reducers/
    │       ├── screens/
    │       │   └── Authentication Screens/
    │       ├── App.js
    │       ├── index.js
    │       └── store.jsx
    │
    ├── server/
    │   ├── config/
    │   ├── controllers/
    │   ├── data/
    │   ├── middleware/
    │   ├── models/
    │   ├── routes/
    │   ├── utils/
    │   └── index.js
    │
    ├── package.json
    ├── package-lock.json
    └── Procfile
```

## 🗃️ Main Data Models

### User
Stores:
- Name
- Email
- Password
- Admin status

### Student
Stores:
- Name
- Address
- Category/stream
- City
- Contact number
- Father's contact number
- Image
- Room number
- Block number
- Current status

### Attendance
Stores:
- Room numbers
- Attendance date
- Attendance data
- Student attendance details
- Creation/update timestamps

## 🔌 Main API Routes

### Users

| Method | Endpoint | Purpose | Access |
|---|---|---|---|
| POST | `/users` | Register user | Public |
| POST | `/users/login` | Login | Public |
| GET | `/users/profile` | Get logged-in user profile | Authenticated |
| PUT | `/users/profile` | Update own profile | Authenticated |
| GET | `/users` | List users | Admin |
| GET | `/users/:id` | Get user by ID | Admin |
| PUT | `/users/:id` | Update user | Admin |
| DELETE | `/users/:id` | Delete user | Admin |

### Students

| Method | Endpoint | Purpose | Access |
|---|---|---|---|
| GET | `/student/all` | List/search students with pagination | Authenticated |
| POST | `/student/addStudent` | Add a student | Admin |
| GET | `/student/:id` | Get student details | Authenticated |
| PUT | `/student/:id` | Update student | Admin |
| DELETE | `/student/:id` | Delete student | Admin |
| GET | `/student/room/:roomId` | Get students for a room | Application route |

### Attendance

| Method | Endpoint | Purpose | Access |
|---|---|---|---|
| GET | `/attendance/:roomId` | Get attendance for a room | Authenticated |
| POST | `/attendance/` | Enter/update attendance | Admin |
| POST | `/attendance/getAnalysis` | Get attendance analysis by date | Authenticated |
| DELETE | `/attendance/:days` | Delete attendance older than a number of days | Admin |

## ⚙️ Prerequisites

Make sure the following are installed:

- [Node.js](https://nodejs.org/)
- npm
- MongoDB / MongoDB Atlas
- Git

The project declares Node.js `15.6.0` and npm `7.4.0` in its package configuration.

## 🚀 Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/Ramansingh8092/Hostel-Atten.git
cd Hostel-Atten/Hostel-Management-master
```

### 2. Install backend dependencies

From the project root:

```bash
npm install
```

### 3. Install frontend dependencies

```bash
cd frontend
npm install
cd ..
```

### 4. Configure environment variables

Create a `.env` file inside the `server` directory:

```env
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```

Do not commit real database credentials, JWT secrets, or other sensitive values to GitHub.

### 5. Start the application

From the project root:

```bash
npm run dev
```

This runs the Express backend and React frontend concurrently.

The frontend is configured to proxy API requests to:

```text
http://127.0.0.1:5000
```

### Other available commands

Start only the backend:

```bash
npm run server
```

Start only the frontend:

```bash
npm run client
```

Start the backend normally:

```bash
npm start
```

Build the React frontend:

```bash
cd frontend
npm run build
```

## 🔄 How It Works

1. A user registers or logs in.
2. The backend authenticates the user and returns a JWT.
3. The frontend stores the authenticated user information and sends the JWT with protected API requests.
4. Authorized users can view and search student records.
5. Admin users can add, update, and remove students.
6. For attendance, a room number is entered to retrieve the students assigned to that room.
7. Attendance is recorded for each student and stored in MongoDB.
8. Attendance can later be viewed by date and exported as a CSV file.
9. Admin users can remove older attendance records when required.

## 📊 Attendance Analysis

The analysis section allows users to:

- Select an attendance date.
- View student name, contact number, room number, and attendance status.
- Download the displayed attendance information as a CSV file.
- Remove attendance records older than a specified number of days when authorized as an admin.

## 🔒 Security

The application implements:

- JWT authentication for protected API requests.
- Password hashing using bcryptjs.
- Role-based authorization for admin operations.
- Environment variables for MongoDB and JWT configuration.

> **Deployment note:** Keep `.env` files out of version control and use environment variables provided by your deployment platform.

## 🖼️ Screenshots

You can add screenshots of the following application screens here:

- Login / Registration
- Student dashboard
- Student details
- Add/Edit student
- Room-wise attendance
- Attendance analysis
- User management

Example:

```markdown
![Student Dashboard](screenshots/student-dashboard.png)
![Attendance](screenshots/attendance.png)
![Attendance Analysis](screenshots/analysis.png)
```

## 🚀 Future Improvements

Potential improvements for future versions include:

- More detailed attendance statistics and visual charts.
- Role-specific dashboards.
- Improved validation for student and attendance data.
- More advanced attendance filtering and reporting.
- Improved responsive/mobile experience.
- Automated notifications or reminders.
- Expanded test coverage.

## 👨‍💻 Repository

GitHub: https://github.com/Ramansingh8092/Hostel-Atten

## 📄 License

This project currently uses the license configuration specified in its `package.json`.

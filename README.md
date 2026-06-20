# TaskFlow — Mini Project Management Portal

A full-stack web application for managing project tasks. Built with **React.js** (Frontend) and **Node.js + Express + MySQL** (Backend) with JWT authentication.

##  Features

- **User Authentication** — Register & Login with JWT tokens
- **Task CRUD** — Create, Read, Update, Delete tasks
- **Mark Complete / Reopen** tasks
- **Filter by Status** — All / Pending / In Progress / Completed
- **Search Tasks** — Real-time search by title or description
- **Sort Tasks** — By date, title, or status
- **Pagination** — Navigate through task pages
- **Dashboard Statistics** — Total, Pending, In Progress, Completed
- **Progress Bar** — Visual completion percentage
- **Dark Mode Toggle** — Persistent light/dark theme
- **Priority Levels** — Low, Medium, High with color badges
- **Responsive Design** — Desktop, tablet, and mobile
- **Toast Notifications** — Success/error feedback
- **Form Validation** — Client + server side

## 🛠 Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | React.js, Vite, Axios, React Router |
| Backend   | Node.js, Express.js                 |
| Database  | **MySQL** with Sequelize ORM        |
| Auth      | JWT, bcryptjs                       |
| Styling   | Vanilla CSS (Custom Design System)  |

## 📁 Folder Structure

```
task-management-portal/
├── backend/
│   ├── config/db.js            ← MySQL/Sequelize connection
│   ├── controllers/            ← authController, taskController
│   ├── middleware/auth.js      ← JWT verification
│   ├── models/Task.js          ← Task table schema
│   ├── models/User.js          ← User table schema
│   ├── routes/                 ← authRoutes, taskRoutes
│   ├── server.js               ← Express entry point
│   └── .env                    ← DB credentials
├── frontend/
│   ├── src/components/         ← Navbar, TaskCard, TaskStats
│   ├── src/pages/              ← Dashboard, AddTask, Login, Register
│   ├── src/services/api.js     ← Axios API layer
│   └── src/context/            ← AuthContext, ThemeContext
└── README.md
```

## ⚙️ Setup Instructions

### Prerequisites
- **Node.js** (v18+): https://nodejs.org/
- **MySQL** (v8+): Already installed (user: root, password: 1234)

### 1. Clone the repository
```bash
git clone https://github.com/Koushik Nimbalkar/task-management-portal.git
cd task-management-portal
```

### 2. Setup Backend
```bash
cd backend
npm install
npm run dev
```
The server will **auto-create** the `task_portal` database and all tables on first run.

**MySQL Config** (in `backend/.env`):
```
DB_HOST=localhost
DB_PORT=3306
DB_NAME=task_portal
DB_USER=root
DB_PASSWORD=1234
```

### 3. Setup Frontend (new terminal)
```bash
cd frontend
npm install
npm run dev
```

### 4. Open Browser
Go to `http://localhost:5173` → Register → Start managing tasks!

## 📡 API Documentation

### Authentication
| Method | Endpoint             | Description        |
|--------|----------------------|--------------------|
| POST   | `/api/auth/register` | Register new user  |
| POST   | `/api/auth/login`    | Login user         |
| GET    | `/api/auth/me`       | Get profile        |

### Tasks (Requires JWT)
| Method | Endpoint           | Description                     |
|--------|--------------------|---------------------------------|
| GET    | `/api/tasks`       | Get tasks (filter/search/page)  |
| POST   | `/api/tasks`       | Create task                     |
| PUT    | `/api/tasks/:id`   | Update task                     |
| DELETE | `/api/tasks/:id`   | Delete task                     |

**Query Params**: `status`, `search`, `sort` (newest/oldest/title/status), `page`, `limit`

**Sample Create Request:**
```json
POST /api/tasks
{ "title": "Build Login Page", "description": "Create a responsive login page with validation", "status": "Pending", "priority": "High" }
```

## 🗄 Database Schema (MySQL)

### `users` Table
| Field      | Type         | Constraints              |
|------------|--------------|--------------------------|
| id         | INT          | PK, Auto Increment       |
| name       | VARCHAR(50)  | NOT NULL                 |
| email      | VARCHAR(100) | NOT NULL, UNIQUE         |
| password   | VARCHAR(255) | NOT NULL (bcrypt hashed) |
| created_at | TIMESTAMP    | Auto-generated           |
| updated_at | TIMESTAMP    | Auto-generated           |

### `tasks` Table
| Field       | Type         | Constraints                     |
|-------------|--------------|----------------------------------|
| id          | INT          | PK, Auto Increment              |
| title       | VARCHAR(100) | NOT NULL                        |
| description | TEXT         | NOT NULL, min 20 chars          |
| status      | VARCHAR(20)  | Pending/In Progress/Completed   |
| priority    | VARCHAR(10)  | Low/Medium/High                 |
| user_id     | INT          | FK → users.id                   |
| created_at  | TIMESTAMP    | Auto-generated                  |
| updated_at  | TIMESTAMP    | Auto-generated                  |

##  Assumptions
1. MySQL is running locally with user `root` and password `1234`.
2. Database and tables are auto-created by Sequelize on server start.
3. Each user manages their own tasks (multi-tenant isolation).
4. JWT tokens expire after 7 days.



##  Git Commits
```
git commit -m "Initial project setup"
git commit -m "Implemented task APIs with Express and MySQL"
git commit -m "Added JWT authentication"
git commit -m "Created React Dashboard with task cards"
git commit -m "Added task creation form with validation"
git commit -m "Integrated frontend with backend APIs"
git commit -m "Added dark mode, search, and pagination"
git commit -m "Updated README with documentation"
```

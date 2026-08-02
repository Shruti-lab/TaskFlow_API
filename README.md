# 🧭 TaskFlow API – RESTful Task Management System

### 📘 Overview

**TaskFlow API** is a modern, API-first **Task Management System** built using **Flask** and **SQLAlchemy**. It allows users to **create, update, track, and organize tasks** through a clean and RESTful interface.
The system emphasizes **robust design principles**, **input validation**, and **scalability**, making it suitable for integration with web, mobile, or automation clients.

---
https://github.com/user-attachments/assets/78d4eed2-8edf-43ed-8b78-b70b9fb48a65

### 🎯 Objectives

- Develop a **fully RESTful API** with standardized endpoints and HTTP status codes.
- Design robust **data models** for `User` and `Task` using SQLAlchemy ORM.
- Enforce **validation and structured error responses** via Pydantic.
- Support **filtering, pagination, and query parameters** for flexible task retrieval.
- Implement a **CLI tool (Click)** for admin operations and automation.
- Use **Flask-Migrate** for database versioning and schema management.
- Build a **production-ready structure** compatible with future microservice extensions.

---

### 🧩 Tech Stack

| Category                       | Tools & Technologies                          |
| ------------------------------ | --------------------------------------------- |
| **Backend Framework**          | Flask, Flask-RESTful, Flask-SQLAlchemy        |
| **Validation & Serialization** | Pydantic                                      |
| **Database**                   | SQLite (Development), PostgreSQL (Production) |
| **CLI**                        | Click                                         |
| **Database Migrations**        | Flask-Migrate                                 |
| **Environment Management**     | python-dotenv                                 |
| **Testing & API Tools**        | pytest, Postman                               |

---

### 🏗️ Project Structure

```
taskflow_api/
│
├── app/                                 # Main application package
│   ├── __init__.py                      # App factory initialization (creates Flask app, registers blueprints)
│   │
|   |-- cli
|   |   |-- cli.py                       # Custom Click commands for admin/automation tasks
|   | 
│   ├── models/                          # Database models (SQLAlchemy ORM)
│   │   ├── __init__.py
│   │   ├── user.py                      # User model (fields, relationships, password hashing)
│   │   └── task.py                      # Task model (title, description, status, due date, user_id)
│   │
│   ├── routes/                          # API endpoints organized by resource
│   │   ├── __init__.py
│   │   ├── auth_routes.py               # Handles register, login, logout, user profile & update operations
│   │   └── task_routes.py               # CRUD operations for tasks + filters/pagination
│   │
│   ├── schemas/                         # Marshmallow / Pydantic schemas for validation & serialization
│   │   ├── __init__.py
│   │   ├── user_schema.py               # User input/output validation
│   │   └── task_schema.py               # Task input/output validation
│   │
│   ├── utils/                           # Helper utilities & CLI commands
│   │   ├── __init__.py
│   │   ├── jwtUtil.py                   # JWT generation, decoding, token validation helpers
│   │   └── response.py                  # Success, error responses formatted properly
│   │
│   └── config.py                        # App configuration (DB URL, secret keys, environment settings)
│
├── migrations/                          # Flask-Migrate auto-generated DB migration files
│
|-- tests                                # Includes tests
├── .env                                 # Environment variables (DB connection, secrets)
├── requirements.txt                     # Python dependencies list
├── run.py                               # Entry point to start the Flask server
└── README.md                            # Project documentation

```

---

### ⚙️ Setup Instructions

#### 1. Clone the repository

```bash
git clone https://github.com/Shruti-lab/Group_1_Revature_Project_1.git
cd .\Group_1_Revature_Project_1\
```

#### 2. Create and activate virtual environment

```bash
python -m venv venv
source venv/bin/activate    # macOS/Linux
venv\Scripts\activate       # Windows
```

#### 3. Install dependencies

```bash
pip install -r requirements.txt
```

#### 4. Setup environment variables

Create a `.env` file based on `.env.example` and configure:

```
FLASK_APP=run.py
FLASK_ENV=development
DATABASE_URL=sqlite:///instance/taskflow.db
JWT_SECRET_KEY=your_secret_key
```

#### 5. Initialize database

```bash
flask db init
flask db migrate -m "Initial migration"
flask db upgrade
```

#### 6. Run the application

```bash
python run.py
```

API will be available at:
📍 `http://127.0.0.1:5000/`

---

### 🚀 API Endpoints

#### 🧑‍💻 User Routes

#### Base URL : `/auth`

| Method | Endpoint  | Description                          |
| ------ | --------- | ------------------------------------ |
| POST   | `/signup` | Register new user                    |
| POST   | `/login`  | Authenticate and get JWT token       |
| GET    | `/user`   | Get current user profile (Protected) |
| PUT    | `/user`   | Update name or password (Protected)  |

#### 📝 Task Routes

#### Base URL : `/user/tasks`

| Method | Endpoint | Description                                              |
| ------ | -------- | -------------------------------------------------------- |
| POST   | `/`      | Create a new task (Protected)                            |
| GET    | `/`      | Get all tasks (supports filters, pagination) (Protected) |
| GET    | `/<id>`  | Retrieve a single task (Protected)                       |
| PUT    | `/<id>`  | Update a task (Protected)                                |
| DELETE | `/<id>`  | Delete a task (Protected)                                |

**Filtering Example:**

```
GET /tasks?status=COMPLETED
GET /tasks?priority=LOW
GET /tasks?status=PENDING&priority=HIGH
```

---

## 🧰 CLI Utilities (Click)

### 🔐 Authentication Commands

#### 1. **Sign Up**

Register a new user.

```bash
python app/cli/cli.py signup --name <NAME> --email <EMAIL> --password <PASSWORD>
```

#### 2. **Log In**

Logs in a user and stores the JWT token in `token.txt`.

```bash
python app/cli/cli.py login --email <EMAIL> --password <PASSWORD>
```

### 📝 Task Commands

#### 1. **Create Task**

Create a new task.

```bash
python app/cli/cli.py create --title <NEW_TITLE> --status <STATUS> --priority <PRIORITY> --description <TEXT> --due_date <DATE>
```

#### 2. **Update Task**

Update an existing task by its ID.

```bash
python app/cli/cli.py update <task_id> --title <NEW_TITLE> --status <STATUS> --priority <PRIORITY> --description <TEXT> --due_date <DATE>

```

#### 3. **Delete Task**

Delete a specific task by its ID.

```bash
python app/cli/cli.py delete <task_id>

```

#### 4. **Bulk Delete Task**

Delete multiple tasks at once.

```bash
python app/cli/cli.py bulk-delete --ids <ID1> <ID2> <ID3>

```

#### 4. **Get Specific Task**

Retrieve details of a specific task.

```bash
python app/cli/cli.py get-task <task_id>

```

---

---

### 🧱 Design Highlights

- Modular folder structure for **scalability**
- Follows **REST conventions** and **HTTP status standards**
- Centralized **error handling** and **response formatting**
- **Environment-independent DB setup** (SQLite → PostgreSQL)
- **Extensible CLI commands** for backend automation

---

### 🏁 Outcome

Delivered a **production-structured, testable, and maintainable REST API** with:

- Full CRUD functionality
- JWT-based authentication
- Input validation
- CLI utilities
- Database migrations
- Ready integration with frontend or mobile clients

This project demonstrates **intermediate-to-advanced Flask proficiency**, focusing on **real-world backend design and engineering principles**.

---

### 📜 License

This project is open-sourced under the **MIT License**.

---

# FastAPI Mini Project 🚀

This is a simple FastAPI-based backend project that includes multiple endpoints. The application supports arithmetic operations, palindrome checking, and task management via in-memory storage.

---

## 📂 Project Structure
FastApi_APP/
```
├── app/                            # Application package
│   ├── __init__.py
│   ├── main.py                     # FastAPI app instance and app startup
│   ├── database.py                 # database configuration
│   ├── create_tables.py            # building database
│   ├── init_db.py                  # initialize the database
│   ├── models/                     # Pydantic models
│   │   ├── __init__.py
│   │   └── task.py
│   └── routers/                    # API endpoint routers
│   │   ├── __init__.py
│   │   ├── tasks.py
│   │   └── util.py
│   └── auth/                       # API authentication
│       ├── __init__.py
│       └── auth.py
├── pyproject.toml                  # Poetry configuration
├── poetry.lock                     # Dependency lock file
├── README.md                       # Project info and usage (You're looking at it! 📘)
├── LICENSE                         # Project license
├── .gitignore                      # Git ignored files and folders
├── .env                            # env variables for authentication
└── tasks.db                        # Database file for tasks

```

---

## 📦 Requirements

- Python 3.10+
- [Poetry](https://python-poetry.org/docs/#installation)
- [FastAPI](https://fastapi.tiangolo.com/)
- [Uvicorn](https://www.uvicorn.org/) (for running the app)
- [Pydantic](https://docs.pydantic.dev/)

---

## 📦 Installation

Install all dependencies using:

```bash
poetry install
```

Or manually with:

```bash
pip install fastapi uvicorn pydantic
```


---

## 🚀 How to Run

Start the server with:

```bash
poetry run uvicorn main:app --reload
```

Then open your browser at:

```
http://127.0.0.1:8000/docs
```

> This will launch the Swagger UI — an interactive documentation for testing the API endpoints.

---

## 🧪 Endpoints

### 🔹 Root Endpoint

- **GET** `/`  
Returns a simple welcome message.

---

### 🔹 Add Two Numbers

- **GET** `/add/{a}/{b}`  
Returns the sum of two numeric values.

**Example:**  
`/add/3/5` → `a = 3, b = 5, a + b = 8`

---

### 🔹 Palindrome Checker

- **GET** `/pal/{word}`  
Checks whether a given word is a palindrome.

**Example:**  
`/pal/radar` → `"The word is a palindrome"`  
`/pal/hello` → `"The word is not a palindrome"`

---

### 🔹 POST `/tasks/` — Create a Task

**Requires Authentication**

**Request Body:**

```json
{
  "title": "Buy groceries",
  "description": "Milk, eggs, and bread"
}
```

**Response:**

```json
{
  "message": "Task stored",
  "task": {
    "id": 1,
    "title": "Buy groceries",
    "description": "Milk, eggs, and bread"
  }
}
```

---

### 🔹 GET `/tasks/` — Get All Tasks

**Response:**

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "Buy groceries",
      "description": "Milk, eggs, and bread"
    },
    {
      "id": 2,
      "title": "Clean room",
      "description": "Start with the desk"
    }
  ]
}
```

---

### 🔹 GET `/tasks/{task_id}` — Get Task by ID

**Example:** `GET /tasks/1`

**Response:**

```json
{
  "task": {
    "id": 1,
    "title": "Buy groceries",
    "description": "Milk, eggs, and bread"
  }
}
```

---

### 🔹 PUT `/tasks/{task_id}` — Replace a Task

**Requires Authentication**

**Request Body (full update required):**

```json
{
  "title": "Buy tools",
  "description": "Hammer and nails"
}
```

**Response:**

```json
{
  "message": "Task updated",
  "task": {
    "id": 1,
    "title": "Buy tools",
    "description": "Hammer and nails"
  }
}
```

---

### 🔹 PATCH `/tasks/{task_id}` — Partially Update a Task

**Requires Authentication**

**Update just the title or description (or both).**

**Example 1: Update only description**

```json
{
  "description": "Updated details"
}
```

**Example 2: Update both title and description**

```json
{
  "title": "Updated Title",
  "description": "Updated Description"
}
```

**Response:**

```json
{
  "message": "Task updated",
  "task": {
    "id": 1,
    "title": "Updated Title",
    "description": "Updated Description"
  }
}
```

⚠️ Title cannot be empty if provided, and must be unique.

---

### 🔹 DELETE `/tasks/{task_id}` — Delete a Task

**Requires Authentication**

**Example:** `DELETE /tasks/1`

**Response:**

```json
{
  "message": "Task deleted"
}
```

---

✅ All routes that modify data (POST, PUT, PATCH, DELETE) require Basic Authentication using a username and password.

---

## ⚠️ Notes

- Error handling is included for invalid numeric input and missing tasks.

---

## 📄 License

This project is licensed under the MIT License.  
See the [LICENSE](LICENSE) file for details.

---

# FastAPI Installation & Configuration Guide

A simple guide to setting up and running a FastAPI project with Python.

## 1. Requirements

Make sure you have:

* Python 3.10+
* pip
* VS Code or another code editor

Check Python:

```bash
python --version
```

Check pip:

```bash
pip --version
```

---

## 2. Create a Project

```bash
mkdir fastapi-project
cd fastapi-project
```

---

## 3. Create a Virtual Environment

Create the environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Activate it on Linux/macOS:

```bash
source venv/bin/activate
```

After activation, you should see:

```text
(venv)
```

in your terminal.

---

## 4. Install FastAPI

Install FastAPI and Uvicorn:

```bash
pip install fastapi uvicorn
```

Check installed packages:

```bash
pip list
```

---

## 5. Create the Application

Create:

```text
main.py
```

Add:

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def root():
    return {"message": "Hello FastAPI"}
```

---

## 6. Run the Server

Run:

```bash
uvicorn main:app --reload
```

Explanation:

```text
uvicorn     → ASGI server
main        → main.py
app         → FastAPI object
--reload    → Automatically restart when code changes
```

The application will normally run at:

```text
http://127.0.0.1:8000
```

---

## 7. Test the API

Open:

```text
http://127.0.0.1:8000
```

Response:

```json
{
  "message": "Hello FastAPI"
}
```

---

## 8. Automatic API Documentation

FastAPI automatically provides Swagger UI.

Open:

```text
http://127.0.0.1:8000/docs
```

It also provides ReDoc:

```text
http://127.0.0.1:8000/redoc
```

---

## 9. Create a GET Endpoint

```python
@app.get("/users")
def get_users():
    return {
        "users": [
            {"id": 1, "name": "Minidu"},
            {"id": 2, "name": "John"}
        ]
    }
```

Test:

```text
GET /users
```

---

## 10. Create a POST Endpoint

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class User(BaseModel):
    name: str
    age: int


@app.post("/users")
def create_user(user: User):
    return {
        "message": "User created",
        "user": user
    }
```

Example request:

```json
{
  "name": "Minidu",
  "age": 23
}
```

FastAPI automatically validates the request data using Pydantic.

---

## 11. Project Structure

A small project can start like this:

```text
fastapi-project/
│
├── venv/
│
├── main.py
│
└── requirements.txt
```

For a larger application:

```text
fastapi-project/
│
├── app/
│   ├── main.py
│   ├── routes/
│   ├── models/
│   ├── schemas/
│   ├── services/
│   └── database/
│
├── venv/
│
├── .env
├── .gitignore
└── requirements.txt
```

---

## 12. Save Dependencies

Create `requirements.txt`:

```bash
pip freeze > requirements.txt
```

Example:

```text
fastapi
uvicorn
pydantic
```

Install dependencies later with:

```bash
pip install -r requirements.txt
```

---

## 13. Environment Variables

Install `python-dotenv`:

```bash
pip install python-dotenv
```

Create:

```text
.env
```

Example:

```env
APP_NAME=My FastAPI App
DATABASE_URL=postgresql://user:password@localhost/mydb
```

Load environment variables:

```python
import os
from dotenv import load_dotenv

load_dotenv()

app_name = os.getenv("APP_NAME")
```

---

## 14. .gitignore

Create `.gitignore`:

```gitignore
venv/
__pycache__/
.env
*.pyc
```

Never commit passwords, API keys, or database credentials.

---

## 15. Development vs Production

For development:

```bash
uvicorn main:app --reload
```

For production, avoid `--reload`:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

---

## 16. Useful Commands

Create virtual environment:

```bash
python -m venv venv
```

Activate:

```bash
venv\Scripts\activate
```

Install FastAPI:

```bash
pip install fastapi uvicorn
```

Run server:

```bash
uvicorn main:app --reload
```

Save dependencies:

```bash
pip freeze > requirements.txt
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Deactivate environment:

```bash
deactivate
```

---

## 17. Basic FastAPI Flow

```text
Client
  ↓
HTTP Request
  ↓
FastAPI
  ↓
Route
  ↓
Validation
  ↓
Business Logic
  ↓
Database
  ↓
Response
  ↓
Client
```

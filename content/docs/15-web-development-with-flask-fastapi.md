---
title: "Ch 15: Web Development with Flask & FastAPI"
weight: 15
---

# Web Development with Flask & FastAPI

## Learning Objectives

After reading this chapter, you will be able to:
- Build REST APIs with Flask and FastAPI
- Handle routes, request data, and responses
- Work with databases in web applications
- Implement authentication and middleware
- Write async endpoints with FastAPI
- Deploy applications to production

---

## 15.1 Flask Basics

```python
# app.py
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, World!"

@app.route("/health")
def health():
    return jsonify({"status": "healthy", "version": "1.0.0"})

# Run: flask run
# Or: python app.py
if __name__ == "__main__":
    app.run(debug=True, port=5000)
```

### Routes and Methods

```python
from flask import Flask, jsonify, request

app = Flask(__name__)

# Route with methods
@app.route("/items", methods=["GET", "POST"])
def handle_items():
    if request.method == "GET":
        return jsonify(items)
    elif request.method == "POST":
        data = request.json
        items.append(data)
        return jsonify(data), 201

# Dynamic URL parameters
@app.route("/items/<int:item_id>")
def get_item(item_id):
    return jsonify({"id": item_id, "name": "Sample"})

# Query parameters
@app.route("/search")
def search():
    query = request.args.get("q", "")
    page = request.args.get("page", 1, type=int)
    return jsonify({"query": query, "page": page})
```

### Request and Response

```python
from flask import request, jsonify, make_response

@app.route("/submit", methods=["POST"])
def submit():
    # JSON body
    data = request.get_json()
    
    # Form data
    name = request.form.get("name")
    
    # Headers
    auth = request.headers.get("Authorization")
    
    # File uploads
    file = request.files.get("document")
    if file:
        file.save(f"uploads/{file.filename}")
    
    # Custom response
    response = make_response(jsonify({"message": "Success"}), 201)
    response.headers["X-Custom-Header"] = "value"
    return response
```

### Flask with SQLAlchemy

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///app.db"
db = SQLAlchemy(app)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

with app.app_context():
    db.create_all()

@app.route("/users")
def get_users():
    users = User.query.all()
    return [{"id": u.id, "username": u.username} for u in users]

@app.route("/users", methods=["POST"])
def create_user():
    data = request.json
    user = User(username=data["username"], email=data["email"])
    db.session.add(user)
    db.session.commit()
    return jsonify({"id": user.id}), 201
```

---

## 15.2 FastAPI Basics

```python
# main.py
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI(title="My API", version="1.0.0")

class Item(BaseModel):
    name: str
    price: float
    description: str | None = None

# Run: uvicorn main:app --reload
# Docs: http://localhost:8000/docs

@app.get("/")
async def root():
    return {"message": "Hello World"}

@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str | None = None):
    return {"item_id": item_id, "q": q}

@app.post("/items", status_code=201)
async def create_item(item: Item):
    return {"message": "Item created", "item": item}
```

### Request Validation with Pydantic

```python
from pydantic import BaseModel, Field, EmailStr
from typing import Literal
from datetime import datetime

class UserCreate(BaseModel):
    username: str = Field(..., min_length=3, max_length=50)
    email: EmailStr
    age: int = Field(ge=0, le=150)
    role: Literal["admin", "user", "moderator"] = "user"
    tags: list[str] = []
    created_at: datetime | None = None

@app.post("/users")
async def create_user(user: UserCreate):
    return {
        "username": user.username,
        "email": user.email,
        "is_adult": user.age >= 18
    }
```

### Dependency Injection

```python
from fastapi import Depends, HTTPException, Header

# Database dependency
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# Authentication dependency
def verify_token(authorization: str = Header(...)):
    if not authorization.startswith("Bearer "):
        raise HTTPException(status_code=401)
    token = authorization.split("Bearer ")[1]
    return verify_jwt(token)

@app.get("/users/me")
async def get_current_user(
    token: dict = Depends(verify_token),
    db: Session = Depends(get_db)
):
    user = db.query(User).filter(User.id == token["user_id"]).first()
    return user
```

### Async Database with SQLAlchemy

```python
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession
from sqlalchemy.orm import sessionmaker
from fastapi import Depends

# Async engine for FastAPI
DATABASE_URL = "postgresql+asyncpg://user:pass@localhost/db"
engine = create_async_engine(DATABASE_URL)
AsyncSessionLocal = sessionmaker(engine, class_=AsyncSession)

async def get_db():
    async with AsyncSessionLocal() as session:
        yield session

@app.get("/users")
async def get_users(db: AsyncSession = Depends(get_db)):
    result = await db.execute(select(User))
    return result.scalars().all()
```

---

## 15.3 Authentication & Security

### JWT Authentication (FastAPI)

```python
from datetime import datetime, timedelta
from jose import JWTError, jwt
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"])
SECRET_KEY = "your-secret-key"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

def create_access_token(data: dict):
    to_encode = data.copy()
    expire = datetime.utcnow() + timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    to_encode.update({"exp": expire})
    return jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)

async def get_current_user(token: str = Depends(oauth2_scheme)):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise credentials_exception
    except JWTError:
        raise credentials_exception
    return username
```

---

## 15.4 Middleware

```python
# FastAPI middleware
from fastapi.middleware.cors import CORSMiddleware
import time

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Custom middleware
@app.middleware("http")
async def add_process_time_header(request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response
```

---

## 15.5 Background Tasks

```python
from fastapi import BackgroundTasks

def write_log(message: str):
    with open("log.txt", "a") as f:
        f.write(f"{message}\n")

@app.post("/send-email")
async def send_email(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, f"Email sent to {email}")
    return {"message": "Email queued"}
```

---

## Key Takeaways

- **Flask** is lightweight and flexible — great for simple APIs and microservices
- **FastAPI** is modern, async-first with automatic OpenAPI docs
- Use **Pydantic** models for request/response validation in FastAPI
- **Dependency injection** in FastAPI provides clean code organization
- Use JWT tokens for stateless authentication
- Add CORS middleware for frontend integration
- Background tasks handle non-blocking operations
- FastAPI automatically generates interactive API docs at `/docs`

---

## Exercises

1. **REST API**: Build a CRUD API for a todo list with Flask or FastAPI
2. **User auth**: Implement registration, login, and JWT token refresh
3. **File upload**: Create an API that accepts and processes file uploads
4. **Database integration**: Connect your API to PostgreSQL using SQLAlchemy
5. **Async endpoint**: Write an async endpoint that calls an external API
6. **Deployment**: Containerize your FastAPI app with Docker

---

## Next Steps

→ Continue to [Chapter 16: Data Science & Visualization]({{< relref "16-data-science-and-visualization" >}})

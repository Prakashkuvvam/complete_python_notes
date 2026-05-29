---
title: "Ch 13: Database & SQL Integration"
weight: 13
---

# Database & SQL Integration

## Learning Objectives

After reading this chapter, you will be able to:
- Connect to SQLite, PostgreSQL, and MySQL databases from Python
- Execute SQL queries and retrieve results
- Use ORMs like SQLAlchemy for object-relational mapping
- Manage database migrations
- Work with NoSQL databases like MongoDB
- Implement connection pooling and transaction management

---

## 13.1 SQLite with `sqlite3`

SQLite is a lightweight, serverless database built into Python:

```python
import sqlite3

# Connect (creates file if not exists)
conn = sqlite3.connect("database.db")

# Create cursor
cursor = conn.cursor()

# Create table
cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    age INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
""")

# Insert data
cursor.execute(
    "INSERT INTO users (name, email, age) VALUES (?, ?, ?)",
    ("Alice", "alice@example.com", 30)
)

# Insert multiple
users = [
    ("Bob", "bob@example.com", 25),
    ("Charlie", "charlie@example.com", 35),
]
cursor.executemany(
    "INSERT INTO users (name, email, age) VALUES (?, ?, ?)",
    users
)

# Commit
conn.commit()

# Query data
cursor.execute("SELECT * FROM users WHERE age > ?", (25,))
results = cursor.fetchall()
for row in results:
    print(row)  # Tuple: (id, name, email, age, created_at)

# Single row
cursor.execute("SELECT * FROM users WHERE id = ?", (1,))
user = cursor.fetchone()

# Named placeholders
cursor.execute(
    "SELECT * FROM users WHERE name = :name",
    {"name": "Alice"}
)

# Update
cursor.execute(
    "UPDATE users SET age = ? WHERE name = ?",
    (31, "Alice")
)

# Delete
cursor.execute("DELETE FROM users WHERE id = ?", (3,))

# Close connection
conn.close()
```

### Row Factory — Named Column Access

```python
conn = sqlite3.connect("database.db")
conn.row_factory = sqlite3.Row  # Access by column name
cursor = conn.cursor()

cursor.execute("SELECT * FROM users LIMIT 1")
row = cursor.fetchone()
print(row["name"])  # Alice (instead of row[1])
print(dict(row))     # {'id': 1, 'name': 'Alice', ...}
```

### Context Manager

```python
with sqlite3.connect("database.db") as conn:
    cursor = conn.cursor()
    cursor.execute("SELECT COUNT(*) FROM users")
    count = cursor.fetchone()[0]
    print(f"Total users: {count}")
```

---

## 13.2 PostgreSQL with `psycopg2`

```python
import psycopg2
from psycopg2.extras import RealDictCursor

# Connect
conn = psycopg2.connect(
    host="localhost",
    port=5432,
    database="mydb",
    user="postgres",
    password="secret"
)

# RealDictCursor for dictionary access
dict_cursor = conn.cursor(cursor_factory=RealDictCursor)

# Connection string format
# conn = psycopg2.connect("postgresql://user:password@localhost:5432/mydb")

# Parameterized queries (always use %s placeholders!)
with conn:
    with conn.cursor() as cur:
        cur.execute(
            "INSERT INTO products (name, price) VALUES (%s, %s) RETURNING id",
            ("Laptop", 999.99)
        )
        new_id = cur.fetchone()[0]

# Query
with conn.cursor(cursor_factory=RealDictCursor) as cur:
    cur.execute("SELECT * FROM products WHERE price > %s", (500,))
    products = cur.fetchall()
    for p in products:
        print(p["name"], p["price"])
```

---

## 13.3 SQLAlchemy ORM

```python
# pip install sqlalchemy

from sqlalchemy import create_engine, Column, Integer, String, Float, ForeignKey
from sqlalchemy.orm import declarative_base, relationship, Session

Base = declarative_base()

# Define models
class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True)
    name = Column(String(100), nullable=False)
    email = Column(String(100), unique=True, nullable=False)
    age = Column(Integer)
    
    # Relationships
    orders = relationship("Order", back_populates="user")
    
    def __repr__(self):
        return f"<User(id={self.id}, name='{self.name}')"

class Order(Base):
    __tablename__ = "orders"
    
    id = Column(Integer, primary_key=True)
    product = Column(String(200), nullable=False)
    amount = Column(Float, nullable=False)
    user_id = Column(Integer, ForeignKey("users.id"))
    
    user = relationship("User", back_populates="orders")

# Create engine
engine = create_engine("sqlite:///mydb.sqlite", echo=True)
# PostgreSQL: create_engine("postgresql://user:pass@localhost/mydb")

# Create all tables
Base.metadata.create_all(engine)

# Session for CRUD operations
with Session(engine) as session:
    # Create
    user = User(name="Alice", email="alice@example.com", age=30)
    session.add(user)
    session.commit()
    print(f"Created user with id: {user.id}")
    
    # Read
    user = session.get(User, 1)
    users = session.query(User).filter(User.age > 25).all()
    user = session.query(User).filter_by(name="Alice").first()
    
    # Update
    user.age = 31
    session.commit()
    
    # Delete
    session.delete(user)
    session.commit()

# Relationships
with Session(engine) as session:
    user = session.get(User, 1)
    order = Order(product="Laptop", amount=999.99, user=user)
    session.add(order)
    session.commit()
    
    # Access related objects
    print(user.orders)  # [<Order...>, ...]
    print(order.user.name)  # Alice
```

### SQLAlchemy Querying

```python
from sqlalchemy import and_, or_, func

with Session(engine) as session:
    # Filtering
    active_users = session.query(User).filter(
        and_(User.age >= 18, User.age <= 65)
    ).all()
    
    # Ordering
    sorted_users = session.query(User).order_by(
        User.age.desc(), User.name.asc()
    ).all()
    
    # Limiting
    top_3 = session.query(User).limit(3).offset(0).all()
    
    # Aggregation
    avg_age = session.query(func.avg(User.age)).scalar()
    user_count = session.query(func.count(User.id)).scalar()
    
    # Joins
    orders = session.query(Order).join(User).filter(
        User.name == "Alice"
    ).all()
    
    # Lazy loading vs eager loading
    from sqlalchemy.orm import joinedload
    users = session.query(User).options(
        joinedload(User.orders)
    ).all()  # Single query with JOIN
```

---

## 13.4 Database Migrations with Alembic

```bash
# Install Alembic
pip install alembic

# Initialize
# alembic init alembic

# Create migration
# alembic revision --autogenerate -m "add age column"

# Apply migrations
# alembic upgrade head

# Rollback
# alembic downgrade -1
```

```python
# alembic/versions/xxxx_add_age_column.py
"""add age column"""

from alembic import op
import sqlalchemy as sa

revision = "xxxx"
down_revision = "yyyy"

def upgrade():
    op.add_column("users", sa.Column("age", sa.Integer(), nullable=True))

def downgrade():
    op.drop_column("users", "age")
```

---

## 13.5 NoSQL with MongoDB (PyMongo)

```python
from pymongo import MongoClient

# Connect
client = MongoClient("mongodb://localhost:27017")
db = client["mydatabase"]
collection = db["users"]

# Insert
user = {"name": "Alice", "email": "alice@example.com", "age": 30}
result = collection.insert_one(user)
print(result.inserted_id)  # ObjectId

# Insert multiple
users = [
    {"name": "Bob", "email": "bob@example.com"},
    {"name": "Charlie", "email": "charlie@example.com"}
]
result = collection.insert_many(users)

# Find
user = collection.find_one({"name": "Alice"})
users = collection.find({"age": {"$gte": 25}})
for user in users:
    print(user)

# Update
collection.update_one(
    {"name": "Alice"},
    {"$set": {"age": 31}}
)

# Delete
collection.delete_one({"name": "Charlie"})

# Aggregation pipeline
pipeline = [
    {"$group": {"_id": "$city", "count": {"$sum": 1}}},
    {"$sort": {"count": -1}},
    {"$limit": 5}
]
results = collection.aggregate(pipeline)
```

---

## 13.6 Connection Pooling

```python
from sqlalchemy import create_engine

# Connection pool
engine = create_engine(
    "postgresql://user:pass@localhost/mydb",
    pool_size=10,           # Max connections in pool
    max_overflow=20,         # Additional connections when pool is full
    pool_timeout=30,         # Timeout waiting for connection
    pool_recycle=3600,       # Recycle connections after 1 hour
    echo=False
)

# Verify connection
def get_db():
    """FastAPI dependency injection pattern."""
    db = Session(engine)
    try:
        yield db
    finally:
        db.close()
```

---

## Key Takeaways

- Python has built-in `sqlite3` for lightweight databases
- Use parameterized queries (never string formatting!) to prevent SQL injection
- **SQLAlchemy** is the most popular Python ORM — supports SQLite, PostgreSQL, MySQL
- **Alembic** manages database schema migrations
- **PyMongo** is the standard MongoDB client
- Always close connections or use context managers
- Connection pooling is essential for production database access
﻿

---

## Exercises

1. **SQLite CRUD**: Create a task manager with SQLite (add, list, complete, delete tasks)
2. **SQLAlchemy models**: Define User, Post, and Comment models with relationships
3. **MongoDB document**: Store and query blog posts in MongoDB
4. **Migrations**: Add a `status` column to an existing table using Alembic
5. **SQL injection**: Try to inject SQL into an unsafe query and see what happens
6. **Aggregation**: Use SQLAlchemy to generate monthly sales reports

---

## Next Steps

→ Continue to [Chapter 14: Concurrency, Async & Multiprocessing]({{< relref "14-concurrency-async-multiprocessing" >}})

---
title: "📝 Practice Test 5: APIs, Databases & Web"
weight: 23
bookToc: false
---

# Practice Test 5: APIs, Databases & Web

<div class="exam-container">
  <div class="exam-header">
    <div class="exam-meta">
      <span><strong>📍 Topic:</strong> APIs, Databases & Web</span>
      <span><strong>⏱️ Time:</strong> 40 minutes</span>
      <span><strong>📝 Questions:</strong> 25</span>
    </div>
    <div class="exam-timer" id="exam-timer-5">⏱️ <span id="time-5">40:00</span></div>
  </div>

  <div class="exam-section">
    <h3>Section 1: Multiple Choice (Questions 1-10)</h3>

    <div class="question"><strong>1.</strong> What does HTTP status code 201 indicate?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q1" value="A"> A) OK</label></div>
      <div class="option"><label><input type="radio" name="q1" value="B"> B) Created</label></div>
      <div class="option"><label><input type="radio" name="q1" value="C"> C) No Content</label></div>
      <div class="option"><label><input type="radio" name="q1" value="D"> D) Found</label></div>
    </div>
    <div class="answer" id="a1">✅ <strong>Answer:</strong> B) 201 Created — returned after successfully creating a resource.</div>

    <div class="question"><strong>2.</strong> Which SQLAlchemy method is used to define a database model class?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q2" value="A"> A) <code>db.Model</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="B"> B) <code>db.Table</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="C"> C) <code>Base.metadata</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="D"> D) Both A and C (depending on the style)</label></div>
    </div>
    <div class="answer" id="a2">✅ <strong>Answer:</strong> D) Both <code>db.Model</code> (Flask-SQLAlchemy) and <code>declarative_base()</code> (plain SQLAlchemy) can define models.</div>

    <div class="question"><strong>3.</strong> In FastAPI, what does Pydantic provide?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q3" value="A"> A) Database connection pooling</label></div>
      <div class="option"><label><input type="radio" name="q3" value="B"> B) Request and response validation using Python type hints</label></div>
      <div class="option"><label><input type="radio" name="q3" value="C"> C) Template rendering</label></div>
      <div class="option"><label><input type="radio" name="q3" value="D"> D) Authentication middleware</label></div>
    </div>
    <div class="answer" id="a3">✅ <strong>Answer:</strong> B) Pydantic validates request/response data models using Python type annotations.</div>

    <div class="question"><strong>4.</strong> What is the correct way to prevent SQL injection in Python?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q4" value="A"> A) Sanitize input with regex</label></div>
      <div class="option"><label><input type="radio" name="q4" value="B"> B) Use parameterized queries with placeholders</label></div>
      <div class="option"><label><input type="radio" name="q4" value="C"> C) Escape single quotes</label></div>
      <div class="option"><label><input type="radio" name="q4" value="D"> D) Use uppercase SQL keywords</label></div>
    </div>
    <div class="answer" id="a4">✅ <strong>Answer:</strong> B) Always use parameterized queries (e.g., <code>?</code> in sqlite3, <code>%s</code> in psycopg2).</div>

    <div class="question"><strong>5.</strong> What is the purpose of <code>response.raise_for_status()</code> in the <code>requests</code> library?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q5" value="A"> A) It retries the request</label></div>
      <div class="option"><label><input type="radio" name="q5" value="B"> B) It raises an HTTPError for 4xx/5xx status codes</label></div>
      <div class="option"><label><input type="radio" name="q5" value="C"> C) It returns the status code</label></div>
      <div class="option"><label><input type="radio" name="q5" value="D"> D) It converts the response to JSON</label></div>
    </div>
    <div class="answer" id="a5">✅ <strong>Answer:</strong> B) <code>raise_for_status()</code> throws an exception if the HTTP response indicates an error.</div>

    <div class="question"><strong>6.</strong> Which Python library is best for web scraping static HTML content?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q6" value="A"> A) Selenium</label></div>
      <div class="option"><label><input type="radio" name="q6" value="B"> B) BeautifulSoup</label></div>
      <div class="option"><label><input type="radio" name="q6" value="C"> C) Playwright</label></div>
      <div class="option"><label><input type="radio" name="q6" value="D"> D) Pyppeteer</label></div>
    </div>
    <div class="answer" id="a6">✅ <strong>Answer:</strong> B) BeautifulSoup is the standard for parsing static HTML. Selenium/Playwright are for dynamic JavaScript pages.</div>

    <div class="question"><strong>7.</strong> What is the role of Alembic in a Python project?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q7" value="A"> A) Web framework</label></div>
      <div class="option"><label><input type="radio" name="q7" value="B"> B) Database migration tool</label></div>
      <div class="option"><label><input type="radio" name="q7" value="C"> C) Testing library</label></div>
      <div class="option"><label><input type="radio" name="q7" value="D"> D) Task queue</label></div>
    </div>
    <div class="answer" id="a7">✅ <strong>Answer:</strong> B) Alembic is a lightweight database migration tool, often used with SQLAlchemy.</div>

    <div class="question"><strong>8.</strong> How do you define a dependency in FastAPI?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q8" value="A"> A) Using <code>@app.dependency</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="B"> B) Using <code>Depends()</code> in the function signature</label></div>
      <div class="option"><label><input type="radio" name="q8" value="C"> C) Using <code>require()</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="D"> D) Using <code>inject()</code></label></div>
    </div>
    <div class="answer" id="a8">✅ <strong>Answer:</strong> B) FastAPI uses <code>Depends()</code> for dependency injection in route handlers.</div>

    <div class="question"><strong>9.</strong> What does <code>requests.Session()</code> provide?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q9" value="A"> A) A way to make multiple requests with persistent settings and connection pooling</label></div>
      <div class="option"><label><input type="radio" name="q9" value="B"> B) An async HTTP client</label></div>
      <div class="option"><label><input type="radio" name="q9" value="C"> C) A mock HTTP server</label></div>
      <div class="option"><label><input type="radio" name="q9" value="D"> D) Automatic retry logic</label></div>
    </div>
    <div class="answer" id="a9">✅ <strong>Answer:</strong> A) <code>Session</code> persists cookies, headers, and reuses TCP connections for efficiency.</div>

    <div class="question"><strong>10.</strong> Which of the following is NOT a NoSQL database?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q10" value="A"> A) MongoDB</label></div>
      <div class="option"><label><input type="radio" name="q10" value="B"> B) PostgreSQL</label></div>
      <div class="option"><label><input type="radio" name="q10" value="C"> C) Redis</label></div>
      <div class="option"><label><input type="radio" name="q10" value="D"> D) Cassandra</label></div>
    </div>
    <div class="answer" id="a10">✅ <strong>Answer:</strong> B) PostgreSQL is a relational (SQL) database; the others are NoSQL databases.</div>
  </div>

  <div class="exam-section">
    <h3>Section 2: True/False (Questions 11-15)</h3>

    <div class="question"><strong>11.</strong> Flask is an async-native web framework.</div>
    <div class="options"><div class="option">True / False</div></div>
    <div class="answer">✅ <strong>Answer:</strong> False — Flask is WSGI-based (synchronous). FastAPI is async-native.</div>

    <div class="question"><strong>12.</strong> SQLite is a serverless database — no separate server process needed.</div>
    <div class="options"><div class="option">True / False</div></div>
    <div class="answer">✅ <strong>Answer:</strong> True — SQLite reads/writes directly to a file.</div>

    <div class="question"><strong>13.</strong> The <code>pip freeze > requirements.txt</code> command saves currently installed packages with versions.</div>
    <div class="options"><div class="option">True / False</div></div>
    <div class="answer">✅ <strong>Answer:</strong> True — This is the standard way to document dependencies.</div>

    <div class="question"><strong>14.</strong> FastAPI automatically generates interactive API documentation.</div>
    <div class="options"><div class="option">True / False</div></div>
    <div class="answer">✅ <strong>Answer:</strong> True — Swagger UI at <code>/docs</code> and ReDoc at <code>/redoc</code>.</div>

    <div class="question"><strong>15.</strong> A <code>GET</code> request should never have a request body.</div>
    <div class="options"><div class="option">True / False</div></div>
    <div class="answer">✅ <strong>Answer:</strong> True — By HTTP specification, GET requests should not have a body (though some clients send them).</div>
  </div>

  <div class="exam-section">
    <h3>Section 3: Coding Exercises (Questions 16-20)</h3>

    <div class="question"><strong>16.</strong> Write a function that connects to SQLite, creates a table, and inserts data.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import sqlite3

def init_db():
    with sqlite3.connect("app.db") as conn:
        cur = conn.cursor()
        cur.execute("""CREATE TABLE IF NOT EXISTS tasks (
            id INTEGER PRIMARY KEY,
            title TEXT NOT NULL,
            done BOOLEAN DEFAULT 0
        )""")
        cur.execute("INSERT INTO tasks (title) VALUES (?)", ("Learn Python",))
        conn.commit()

init_db()</code></pre></div>

    <div class="question"><strong>17.</strong> Write a function that fetches data from a REST API and returns JSON.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import requests

def get_user_repos(username):
    url = f"https://api.github.com/users/{username}/repos"
    response = requests.get(url, headers={"Accept": "application/vnd.github.v3+json"})
    response.raise_for_status()
    return [{"name": r["name"], "stars": r["stargazers_count"]} for r in response.json()]</code></pre></div>

    <div class="question"><strong>18.</strong> Write a FastAPI endpoint that accepts a POST request with a JSON body.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    quantity: int = 1

@app.post("/items/")
async def create_item(item: Item):
    return {"message": f"Created {item.name}", "total": item.price * item.quantity}</code></pre></div>

    <div class="question"><strong>19.</strong> Write a SQLAlchemy model for a blog post with a foreign key to a User.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from sqlalchemy import create_engine, Column, Integer, String, Text, ForeignKey, DateTime
from sqlalchemy.orm import declarative_base, relationship
from datetime import datetime

Base = declarative_base()

class Post(Base):
    __tablename__ = "posts"
    id = Column(Integer, primary_key=True)
    title = Column(String(200), nullable=False)
    content = Column(Text)
    created_at = Column(DateTime, default=datetime.utcnow)
    user_id = Column(Integer, ForeignKey("users.id"))
    author = relationship("User", back_populates="posts")</code></pre></div>

    <div class="question"><strong>20.</strong> Write a simple web scraper that extracts all links from a webpage.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def get_all_links(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    links = []
    for a in soup.find_all("a", href=True):
        absolute_url = urljoin(url, a["href"])
        links.append({"text": a.text.strip(), "url": absolute_url})
    return links</code></pre></div>
  </div>

  <div class="exam-section">
    <h3>Section 4: Scenario Questions (Questions 21-25)</h3>

    <div class="question"><strong>21.</strong> How would you handle rate limiting when calling an external API?</div>
    <div class="answer">✅ <strong>Answer:</strong> Implement exponential backoff with jitter, check <code>Retry-After</code> headers, use a queue to throttle requests, and track remaining API calls from response headers.</div>

    <div class="question"><strong>22.</strong> How would you structure a Flask/FastAPI project for a large application?</div>
    <div class="answer">✅ <strong>Answer:</strong> Use a modular structure: separate routers/blueprints for each resource, separate models, schemas (Pydantic), services (business logic), and database configuration. Use dependency injection for shared resources.</div>

    <div class="question"><strong>23.</strong> When would you use MongoDB instead of PostgreSQL?</div>
    <div class="answer">✅ <strong>Answer:</strong> MongoDB is good for: flexible/unstructured schemas, rapid prototyping, hierarchical data, horizontal scaling. PostgreSQL is good for: complex relationships, ACID transactions, structured data, joins.</div>

    <div class="question"><strong>24.</strong> How would you debug a slow database query in a Python web app?</div>
    <div class="answer">✅ <strong>Answer:</strong> Enable SQLAlchemy echo logging (<code>echo=True</code>), use <code>EXPLAIN ANALYZE</code>, check for missing indexes, use a profiling tool like <code>slowquery</code> logger, and add database-level query logging.</div>

    <div class="question"><strong>25.</strong> How would you secure an API endpoint that requires authentication?</div>
    <div class="answer">✅ <strong>Answer:</strong> Use JWT tokens (issued at login, verified on each request), implement a dependency that decodes and verifies the token, store passwords with bcrypt hashing, use HTTPS, set token expiration, and implement refresh tokens.</div>
  </div>
</div>

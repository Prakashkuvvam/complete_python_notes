---
title: "Ch 18: Real-World Scenarios & Coding Problems"
weight: 18
---

# Real-World Scenarios & Coding Problems

## Learning Objectives

After reading this chapter, you will be able to:
- Apply Python to real-world problems
- Design solutions for common business scenarios
- Write production-quality code with best practices
- Handle edge cases and error conditions gracefully

---

## 18.1 Log Analyzer

Parse server logs, extract errors, and generate a summary report.

```python
import re
from collections import Counter, defaultdict
from datetime import datetime

def analyze_logs(log_file):
    """
    Parse a server log file and return error statistics.
    
    Log format: [2025-01-15 10:30:45] ERROR: User 123 - Connection timeout
    """
    pattern = r'\[(\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2})\] (\w+): (.+)'
    levels = Counter()
    errors_by_type = Counter()
    hourly_traffic = Counter()
    
    with open(log_file, 'r') as f:
        for line in f:
            match = re.match(pattern, line)
            if not match:
                continue
            
            timestamp, level, message = match.groups()
            levels[level] += 1
            
            # Extract error type from message
            if level == "ERROR":
                error_type = message.split(" -")[0] if " -" in message else message[:50]
                errors_by_type[error_type] += 1
            
            # Hourly traffic
            hour = timestamp[:13]  # 2025-01-15 10
            hourly_traffic[hour] += 1
    
    return {
        "total_lines": sum(levels.values()),
        "levels": dict(levels),
        "top_errors": dict(errors_by_type.most_common(10)),
        "busiest_hours": dict(hourly_traffic.most_common(5)),
        "error_rate": f"{levels.get('ERROR', 0) / sum(levels.values()) * 100:.1f}%"
    }

# Usage
report = analyze_logs("server.log")
print(f"Error rate: {report['error_rate']}")
print(f"Top errors: {report['top_errors']}")
```

---

## 18.2 ETL Pipeline

Extract data from an API, transform it, and load it into a database.

```python
import requests
import pandas as pd
from sqlalchemy import create_engine
from typing import Generator, Dict, Any

def extract_users(page: int = 1) -> list[Dict[str, Any]]:
    """Extract users from an API."""
    response = requests.get(
        f"https://api.example.com/users",
        params={"page": page, "per_page": 100}
    )
    response.raise_for_status()
    return response.json()["data"]

def transform_user(user: Dict[str, Any]) -> Dict[str, Any]:
    """Clean and transform a user record."""
    return {
        "id": user["id"],
        "full_name": f"{user['first_name']} {user['last_name']}",
        "email": user["email"].lower(),
        "is_active": user.get("status") == "active",
        "created_at": pd.to_datetime(user["created_at"]),
        "age": calculate_age(user["birth_date"]) if user.get("birth_date") else None
    }

def load_users(users: list[Dict[str, Any]], db_url: str):
    """Load transformed users into database."""
    engine = create_engine(db_url)
    df = pd.DataFrame(users)
    df.to_sql("users", engine, if_exists="append", index=False)

# Full pipeline
def run_etl(db_url: str):
    all_users = []
    for page in range(1, 6):
        raw_users = extract_users(page)
        transformed = [transform_user(u) for u in raw_users]
        all_users.extend(transformed)
    
    load_users(all_users, db_url)
    print(f"Loaded {len(all_users)} users")
```

---

## 18.3 Web Scraper with Rate Limiting

Scrape product data from an e-commerce site with rate limiting.

```python
import time
import random
import requests
from bs4 import BeautifulSoup
from dataclasses import dataclass

@dataclass
class Product:
    name: str
    price: float
    rating: float
    url: str

class Scraper:
    def __init__(self, base_url, delay=1.0):
        self.base_url = base_url
        self.delay = delay
        self.session = requests.Session()
        self.session.headers.update({
            "User-Agent": "Mozilla/5.0 (compatible; Scraper/1.0)"
        })
    
    def _wait(self):
        """Rate limiting with jitter."""
        time.sleep(self.delay + random.uniform(0, 0.5))
    
    def scrape_product(self, url):
        self._wait()
        response = self.session.get(url)
        soup = BeautifulSoup(response.text, "html.parser")
        
        return Product(
            name=soup.select_one("h1.product-title").text.strip(),
            price=float(soup.select_one(".price").text.replace("$", "")),
            rating=float(soup.select_one(".rating")["data-rating"]),
            url=url
        )
    
    def scrape_category(self, category_url, max_pages=5):
        products = []
        for page in range(1, max_pages + 1):
            url = f"{category_url}?page={page}"
            self._wait()
            response = self.session.get(url)
            soup = BeautifulSoup(response.text, "html.parser")
            
            for link in soup.select(".product-card a"):
                product_url = link["href"]
                products.append(self.scrape_product(product_url))
        
        return products
```

---

## 18.4 REST API Client with Caching

```python
import json
from datetime import datetime, timedelta
from pathlib import Path

class CachedAPIClient:
    def __init__(self, cache_dir=".cache", ttl_minutes=30):
        self.cache_dir = Path(cache_dir)
        self.cache_dir.mkdir(exist_ok=True)
        self.ttl = timedelta(minutes=ttl_minutes)
    
    def _cache_path(self, key):
        # Create a safe filename from the cache key
        safe_key = str(hash(key))
        return self.cache_dir / f"{safe_key}.json"
    
    def _is_fresh(self, cache_path):
        if not cache_path.exists():
            return False
        modified = datetime.fromtimestamp(cache_path.stat().st_mtime)
        return datetime.now() - modified < self.ttl
    
    def get(self, url, **params):
        key = f"{url}:{json.dumps(params, sort_keys=True)}"
        cache_path = self._cache_path(key)
        
        if self._is_fresh(cache_path):
            return json.loads(cache_path.read_text())
        
        response = requests.get(url, params=params)
        response.raise_for_status()
        data = response.json()
        
        cache_path.write_text(json.dumps(data))
        return data
```

---

## 18.5 Task Queue / Job Scheduler

```python
from queue import PriorityQueue
import time
import threading
from dataclasses import dataclass, field
from typing import Any

@dataclass(order=True)
class Job:
    priority: int
    run_at: float = field(compare=False)
    task_id: str = field(compare=False)
    func: callable = field(compare=False)
    args: tuple = field(compare=False, default=())
    kwargs: dict = field(compare=False, default_factory=dict)

class Scheduler:
    def __init__(self):
        self.queue = PriorityQueue()
        self.running = False
        self.thread = None
    
    def schedule(self, delay, func, *args, priority=0, **kwargs):
        run_at = time.time() + delay
        job = Job(priority, run_at, f"job_{id(func)}", func, args, kwargs)
        self.queue.put(job)
    
    def _process(self):
        while self.running:
            job = self.queue.get()
            now = time.time()
            if job.run_at > now:
                time.sleep(job.run_at - now)
            try:
                job.func(*job.args, **job.kwargs)
            except Exception as e:
                print(f"Job {job.task_id} failed: {e}")
            self.queue.task_done()
    
    def start(self):
        self.running = True
        self.thread = threading.Thread(target=self._process, daemon=True)
        self.thread.start()
    
    def stop(self):
        self.running = False

# Usage
scheduler = Scheduler()
scheduler.start()
scheduler.schedule(5, lambda: print("Task after 5s"))
scheduler.schedule(10, lambda: print("Task after 10s"))
time.sleep(12)
scheduler.stop()
```

---

## 18.6 File Watcher / Event Monitor

```python
import time
from pathlib import Path
from hashlib import md5

class FileWatcher:
    def __init__(self, path, callback, interval=1.0):
        self.path = Path(path)
        self.callback = callback
        self.interval = interval
        self.file_hashes = {}
    
    def _get_file_hash(self, filepath):
        return md5(filepath.read_bytes()).hexdigest()
    
    def _scan(self):
        current_files = set()
        changes = []
        
        for filepath in self.path.rglob("*"):
            if not filepath.is_file():
                continue
            current_files.add(filepath)
            
            new_hash = self._get_file_hash(filepath)
            old_hash = self.file_hashes.get(filepath)
            
            if old_hash is None:
                changes.append(("created", filepath))
            elif old_hash != new_hash:
                changes.append(("modified", filepath))
            
            self.file_hashes[filepath] = new_hash
        
        # Detect deletions
        for filepath in set(self.file_hashes) - current_files:
            changes.append(("deleted", filepath))
            del self.file_hashes[filepath]
        
        return changes
    
    def watch(self):
        print(f"Watching {self.path}...")
        self._scan()  # Initialize
        while True:
            time.sleep(self.interval)
            changes = self._scan()
            for event, filepath in changes:
                self.callback(event, filepath)

# Usage
def handle_change(event, path):
    print(f"[{event}] {path}")

watcher = FileWatcher("./", handle_change)
watcher.watch()
```

---

## Key Takeaways

- Real-world code needs **error handling**, **logging**, and **monitoring**
- Use **dataclasses** for clean data containers
- Implement **rate limiting** and **caching** for production API clients
- Design for **testability** — dependency injection, interfaces
- **Composition** over inheritance for flexible, maintainable code
- Always handle **edge cases** (missing data, network failures, timeouts)

---

## Next Steps

→ Continue to [Chapter 19: Practice Test 1]({{< relref "19-exam-practice-test-1" >}})

---
title: "Ch 14: Concurrency, Async & Multiprocessing"
weight: 14
---

# Concurrency, Async & Multiprocessing

## Learning Objectives

After reading this chapter, you will be able to:
- Understand the difference between concurrency and parallelism
- Write threaded programs with `threading` and `concurrent.futures`
- Write async programs with `asyncio`
- Use multiprocessing for CPU-bound tasks
- Choose the right concurrency model for different scenarios
- Handle shared state with locks and queues

---

## 14.1 Concurrency vs Parallelism

```
Concurrency: Multiple tasks making progress (interleaved execution)
Parallelism: Multiple tasks running simultaneously (multi-core)

I/O-bound tasks: Waiting for network, disk, database → Threads or Async
CPU-bound tasks: Computation-heavy → Multiprocessing
```

| Model | Best For | Example |
|-------|----------|---------|
| **Threading** | I/O-bound (network, file) | Web scraping, API calls |
| **Async/await** | I/O-bound (many connections) | Web servers, chat apps |
| **Multiprocessing** | CPU-bound (compute) | Image processing, ML |

---

## 14.2 Threading

```python
import threading
import time

def worker(name, delay):
    """Simulate a task."""
    for i in range(3):
        time.sleep(delay)
        print(f"Worker {name}: iteration {i}")
    print(f"Worker {name} done")

# Create threads
threads = []
for i in range(3):
    t = threading.Thread(target=worker, args=(f"T{i}", 1))
    threads.append(t)
    t.start()

# Wait for all threads
for t in threads:
    t.join()

print("All threads complete")
```

### Thread Pools with `concurrent.futures`

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
import requests

def fetch_url(url):
    response = requests.get(url, timeout=10)
    return url, len(response.content), response.status_code

urls = [
    "https://python.org",
    "https://github.com",
    "https://stackoverflow.com",
]

with ThreadPoolExecutor(max_workers=5) as executor:
    # Submit and collect futures
    future_to_url = {executor.submit(fetch_url, url): url for url in urls}
    
    for future in as_completed(future_to_url):
        url, size, status = future.result()
        print(f"{url}: {size} bytes, status={status}")
    
    # Or use map (simpler)
    results = list(executor.map(fetch_url, urls))
```

### Thread Safety — Locks

```python
import threading

counter = 0
lock = threading.Lock()

def increment():
    global counter
    for _ in range(100000):
        with lock:  # Acquire and release automatically
            counter += 1

threads = [threading.Thread(target=increment) for _ in range(5)]
for t in threads:
    t.start()
for t in threads:
    t.join()

print(f"Counter: {counter}")  # Always 500000
```

### Thread Communication — Queue

```python
from queue import Queue
import threading

# Producer-consumer pattern
def producer(queue, items):
    for item in items:
        queue.put(item)
        print(f"Produced: {item}")
    queue.put(None)  # Sentinel

def consumer(queue):
    while True:
        item = queue.get()
        if item is None:
            break
        print(f"Consumed: {item}")
        queue.task_done()

q = Queue()
threads = [
    threading.Thread(target=producer, args=(q, range(5))),
    threading.Thread(target=consumer, args=(q,))
]

for t in threads:
    t.start()
for t in threads:
    t.join()
```

---

## 14.3 Async Programming with `asyncio`

### Basic Async/Await

```python
import asyncio

async def say_after(delay, message):
    await asyncio.sleep(delay)
    print(message)

async def main():
    print("Start")
    
    # Sequential execution
    await say_after(1, "First")
    await say_after(2, "Second")
    
    print("Done")

asyncio.run(main())
```

### Concurrent Execution

```python
async def main():
    # Run concurrently using gather
    await asyncio.gather(
        say_after(1, "Hello"),
        say_after(2, "World"),
        say_after(3, "Python")
    )
    # Total time: ~3s (not 6s!)

# Task creation
async def main():
    task1 = asyncio.create_task(say_after(2, "Task 1"))
    task2 = asyncio.create_task(say_after(1, "Task 2"))
    
    print("Tasks created")
    await task1
    print("Task 1 done")
    await task2
    print("Task 2 done")
```

### Async HTTP Client

```python
import asyncio
import httpx

async def fetch_url(client, url):
    response = await client.get(url)
    return url, response.status_code

async def fetch_all(urls):
    async with httpx.AsyncClient() as client:
        tasks = [fetch_url(client, url) for url in urls]
        results = await asyncio.gather(*tasks)
        return results

urls = ["https://python.org", "https://github.com", "https://google.com"]
results = asyncio.run(fetch_all(urls))
for url, status in results:
    print(f"{url}: {status}")
```

### Async Iterator

```python
import asyncio

class AsyncRange:
    def __init__(self, start, end, delay=0.5):
        self.start = start
        self.end = end
        self.delay = delay
    
    def __aiter__(self):
        return self
    
    async def __anext__(self):
        if self.start >= self.end:
            raise StopAsyncIteration
        await asyncio.sleep(self.delay)
        value = self.start
        self.start += 1
        return value

async def main():
    async for num in AsyncRange(1, 5):
        print(num)  # 1, 2, 3, 4 (with 0.5s delay each)

asyncio.run(main())
```

### Async Context Manager

```python
import asyncio

class AsyncFile:
    async def __aenter__(self):
        print("Opening file...")
        await asyncio.sleep(0.1)
        return self
    
    async def __aexit__(self, *args):
        print("Closing file...")
        await asyncio.sleep(0.1)
    
    async def read(self):
        return "file content"

async def main():
    async with AsyncFile() as f:
        content = await f.read()
        print(content)

asyncio.run(main())
```

### Practical Async Web Scraper

```python
import asyncio
import httpx
from bs4 import BeautifulSoup

async def scrape_page(client, url):
    try:
        response = await client.get(url, timeout=10)
        soup = BeautifulSoup(response.text, "html.parser")
        title = soup.title.text if soup.title else "No title"
        return url, title, len(response.text)
    except Exception as e:
        return url, f"Error: {e}", 0

async def scrape_sites(urls):
    async with httpx.AsyncClient() as client:
        tasks = [scrape_page(client, url) for url in urls]
        results = await asyncio.gather(*tasks, return_exceptions=True)
        return results

urls = [
    "https://python.org",
    "https://github.com",
    "https://stackoverflow.com",
    "https://reddit.com"
]

results = asyncio.run(scrape_sites(urls))
for url, title, size in results:
    print(f"{url}: {title[:50]}... ({size} bytes)")
```

---

## 14.4 Multiprocessing

### Basic Multiprocessing

```python
import multiprocessing
import time

def square(n):
    """CPU-intensive task."""
    return sum(i * i for i in range(n * 1000000))

if __name__ == "__main__":
    numbers = [1, 2, 3, 4]
    
    # Sequential
    start = time.time()
    results_seq = [square(n) for n in numbers]
    print(f"Sequential: {time.time() - start:.2f}s")
    
    # Parallel
    start = time.time()
    with multiprocessing.Pool(processes=4) as pool:
        results_par = pool.map(square, numbers)
    print(f"Parallel: {time.time() - start:.2f}s")
    
    print(results_par)
```

### ProcessPoolExecutor

```python
from concurrent.futures import ProcessPoolExecutor

def cpu_intensive(n):
    return sum(i ** 2 for i in range(n * 10_000_000))

if __name__ == "__main__":
    with ProcessPoolExecutor(max_workers=4) as executor:
        results = list(executor.map(cpu_intensive, [1, 2, 3, 4]))
    print(results)
```

### Multiprocessing Pitfalls

```python
# Process memory isolation — processes don't share memory!
# Use multiprocessing.Queue, Value, Array for sharing

from multiprocessing import Process, Value, Array

def increment(counter):
    for _ in range(100):
        with counter.get_lock():
            counter.value += 1

if __name__ == "__main__":
    counter = Value("i", 0)  # Shared integer
    processes = [Process(target=increment, args=(counter,)) for _ in range(10)]
    
    for p in processes:
        p.start()
    for p in processes:
        p.join()
    
    print(f"Counter: {counter.value}")  # 1000
```

---

## 14.5 GIL — Global Interpreter Lock

```python
"""
The GIL allows only one thread to execute Python bytecode at a time.

Effects:
- Threads DON'T speed up CPU-bound tasks
- Threads DO speed up I/O-bound tasks (releases GIL during I/O)
- Multiprocessing bypasses the GIL (separate processes)
- C extensions (NumPy, Cython) can release the GIL

Python 3.13+: Free-threading mode (experimental, compile with --disable-gil)
"""
```

---

## 14.6 Choosing the Right Model

```python
def choose_model(task_type):
    """
    I/O-bound (network, disk, database):
        - Few connections (< 50): ThreadPoolExecutor
        - Many connections (1000+): asyncio
    
    CPU-bound (calculations, processing):
        - ProcessPoolExecutor or multiprocessing
    
    Mixed workload:
        - Async for I/O + ProcessPoolExecutor for CPU tasks
    """
    pass
```

---

## Key Takeaways

- **Threads**: Good for I/O-bound tasks, limited by GIL for CPU work
- **Async**: Great for many concurrent I/O operations (servers, scrapers)
- **Multiprocessing**: True parallelism for CPU-bound tasks
- Use `concurrent.futures` for high-level thread/process management
- Use `asyncio` for modern async programming
- Shared state needs synchronization (Lock, Queue)
- The GIL limits threading for CPU-bound work — use multiprocessing instead

---

## Exercises

1. **Concurrent downloader**: Download multiple files in parallel using threads
2. **Async web server**: Build a simple async HTTP server
3. **Parallel image processing**: Resize multiple images using multiprocessing
4. **Rate limiter**: Implement an async rate limiter for API calls
5. **Producer-consumer**: Use a Queue to coordinate multiple producers and consumers
6. **Benchmark**: Compare threading vs async vs multiprocessing for a mixed workload

---

## Next Steps

→ Continue to [Chapter 15: Web Development with Flask/FastAPI]({{< relref "15-web-development-with-flask-fastapi" >}})

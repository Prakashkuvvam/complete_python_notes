---
title: "📝 Practice Test 4: Advanced Python"
weight: 22
bookToc: false
---

# Practice Test 4: Advanced Python

<div class="exam-container">
  <div class="exam-header">
    <div class="exam-meta">
      <span><strong>📍 Topic:</strong> Advanced Python</span>
      <span><strong>⏱️ Time:</strong> 40 minutes</span>
      <span><strong>📝 Questions:</strong> 25</span>
    </div>
    <div class="exam-timer" id="exam-timer-4">⏱️ <span id="time-4">40:00</span></div>
  </div>

  <div class="exam-section">
    <h3>Section 1: Multiple Choice (Questions 1-10)</h3>

    <div class="question"><strong>1.</strong> What is the purpose of the <code>@functools.wraps</code> decorator?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q1" value="A"> A) It prevents the decorated function from being called</label></div>
      <div class="option"><label><input type="radio" name="q1" value="B"> B) It copies the metadata (name, docstring) from the original function to the wrapper</label></div>
      <div class="option"><label><input type="radio" name="q1" value="C"> C) It makes the function run faster</label></div>
      <div class="option"><label><input type="radio" name="q1" value="D"> D) It converts a function into a class</label></div>
    </div>
    <div class="answer" id="a1">✅ <strong>Answer:</strong> B) <code>@functools.wraps</code> preserves the original function's <code>__name__</code>, <code>__doc__</code>, and other metadata.</div>

    <div class="question"><strong>2.</strong> What does the following code return? <code>sum(x * x for x in range(4))</code></div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q2" value="A"> A) 14</label></div>
      <div class="option"><label><input type="radio" name="q2" value="B"> B) [0, 1, 4, 9]</label></div>
      <div class="option"><label><input type="radio" name="q2" value="C"> C) 30</label></div>
      <div class="option"><label><input type="radio" name="q2" value="D"> D) (0, 1, 4, 9)</label></div>
    </div>
    <div class="answer" id="a2">✅ <strong>Answer:</strong> A) 14 — sum(0² + 1² + 2² + 3²) = sum(0, 1, 4, 9) = 14</div>

    <div class="question"><strong>3.</strong> Which of the following is NOT true about the <code>asyncio</code> module?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q3" value="A"> A) It enables concurrent execution using a single thread</label></div>
      <div class="option"><label><input type="radio" name="q3" value="B"> B) It is best for CPU-bound tasks</label></div>
      <div class="option"><label><input type="radio" name="q3" value="C"> C) It uses the <code>async</code>/<code>await</code> syntax</label></div>
      <div class="option"><label><input type="radio" name="q3" value="D"> D) It uses an event loop to manage tasks</label></div>
    </div>
    <div class="answer" id="a3">✅ <strong>Answer:</strong> B) asyncio is NOT best for CPU-bound tasks — it's designed for I/O-bound tasks.</div>

    <div class="question"><strong>4.</strong> What does <code>itertools.chain([1, 2], [3, 4])</code> produce?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q4" value="A"> A) [[1, 2], [3, 4]]</label></div>
      <div class="option"><label><input type="radio" name="q4" value="B"> B) [1, 2, 3, 4]</label></div>
      <div class="option"><label><input type="radio" name="q4" value="C"> C) An iterator yielding 1, 2, 3, 4</label></div>
      <div class="option"><label><input type="radio" name="q4" value="D"> D) [(1, 2), (3, 4)]</label></div>
    </div>
    <div class="answer" id="a4">✅ <strong>Answer:</strong> C) <code>chain</code> returns an iterator that yields elements from each iterable sequentially.</div>

    <div class="question"><strong>5.</strong> What is the GIL (Global Interpreter Lock)?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q5" value="A"> A) A mutex that prevents multiple threads from executing Python bytecode simultaneously</label></div>
      <div class="option"><label><input type="radio" name="q5" value="B"> B) A security feature that restricts imports</label></div>
      <div class="option"><label><input type="radio" name="q5" value="C"> C) A memory management system</label></div>
      <div class="option"><label><input type="radio" name="q5" value="D"> D) A file locking mechanism</label></div>
    </div>
    <div class="answer" id="a5">✅ <strong>Answer:</strong> A) The GIL allows only one thread to execute Python bytecode at a time.</div>

    <div class="question"><strong>6.</strong> What is the primary advantage of generators over lists?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q6" value="A"> A) Generators are faster for random access</label></div>
      <div class="option"><label><input type="radio" name="q6" value="B"> B) Generators use less memory for large sequences</label></div>
      <div class="option"><label><input type="radio" name="q6" value="C"> C) Generators can be indexed</label></div>
      <div class="option"><label><input type="radio" name="q6" value="D"> D) Generators support slicing</label></div>
    </div>
    <div class="answer" id="a6">✅ <strong>Answer:</strong> B) Generators produce items lazily, using memory proportional to the number of items in flight, not the total sequence size.</div>

    <div class="question"><strong>7.</strong> What is the correct way to run multiple coroutines concurrently?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q7" value="A"> A) <code>asyncio.run(coro1, coro2)</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="B"> B) <code>asyncio.gather(coro1(), coro2())</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="C"> C) <code>await coro1(), await coro2()</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="D"> D) <code>coro1.start(); coro2.start()</code></label></div>
    </div>
    <div class="answer" id="a7">✅ <strong>Answer:</strong> B) <code>asyncio.gather</code> runs multiple coroutines concurrently.</div>

    <div class="question"><strong>8.</strong> What does <code>functools.lru_cache</code> do?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q8" value="A"> A) It caches the return values of a function based on its arguments</label></div>
      <div class="option"><label><input type="radio" name="q8" value="B"> B) It caches the function's source code</label></div>
      <div class="option"><label><input type="radio" name="q8" value="C"> C) It limits how often a function can be called</label></div>
      <div class="option"><label><input type="radio" name="q8" value="D"> D) It logs function calls and returns</label></div>
    </div>
    <div class="answer" id="a8">✅ <strong>Answer:</strong> A) <code>lru_cache</code> memoizes a function, caching recent return values.</div>

    <div class="question"><strong>9.</strong> Which multiprocessing tool provides a map-style parallel execution?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q9" value="A"> A) <code>threading.Thread</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="B"> B) <code>asyncio.gather</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="C"> C) <code>multiprocessing.Pool</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="D"> D) <code>collections.Counter</code></label></div>
    </div>
    <div class="answer" id="a9">✅ <strong>Answer:</strong> C) <code>multiprocessing.Pool</code> provides <code>map()</code>, <code>apply()</code>, etc. for parallel execution.</div>

    <div class="question"><strong>10.</strong> Which of the following is true about the <code>yield</code> keyword in Python?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q10" value="A"> A) It terminates a function</label></div>
      <div class="option"><label><input type="radio" name="q10" value="B"> B) It returns a value and pauses the function's execution</label></div>
      <div class="option"><label><input type="radio" name="q10" value="C"> C) It imports a module</label></div>
      <div class="option"><label><input type="radio" name="q10" value="D"> D) It creates a new thread</label></div>
    </div>
    <div class="answer" id="a10">✅ <strong>Answer:</strong> B) <code>yield</code> returns a value and saves the function's state for later resumption.</div>
  </div>

  <div class="exam-section">
    <h3>Section 2: Short Code Output (Questions 11-15)</h3>

    <div class="question"><strong>11.</strong> <code>print(list(zip([1, 2], ['a', 'b', 'c'])))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[(1, 'a'), (2, 'b')]</code> — <code>zip</code> stops at the shortest.</div>

    <div class="question"><strong>12.</strong> <code>g = (x**2 for x in range(3)); print(list(g)); print(list(g))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[0, 1, 4]</code> then <code>[]</code> — Generators can only be iterated once.</div>

    <div class="question"><strong>13.</strong> <code>print([x for x in [1,2,3] if x%2]</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1, 3]</code> — 1%2=1 (truthy), 2%2=0 (falsy), 3%2=1 (truthy).</div>

    <div class="question"><strong>14.</strong> <code>print(list(map(lambda x: x**2, filter(lambda x: x%2, [1,2,3,4,5]))))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1, 9, 25]</code> — Squares of odd numbers.</div>

    <div class="question"><strong>15.</strong> <code>from functools import reduce; print(reduce(lambda a,b: a if a>b else b, [3,1,4,1,5,9]))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> 9 — This is a manual <code>max()</code> using reduce.</div>
  </div>

  <div class="exam-section">
    <h3>Section 3: Coding Exercises (Questions 16-20)</h3>

    <div class="question"><strong>16.</strong> Write a decorator that counts how many times a function is called.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from functools import wraps

def count_calls(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        wrapper.count += 1
        print(f"Call {wrapper.count} of {func.__name__}")
        return func(*args, **kwargs)
    wrapper.count = 0
    return wrapper

@count_calls
def hello():
    print("Hello!")

hello()  # Call 1 of hello
hello()  # Call 2 of hello
print(hello.count)  # 2</code></pre></div>

    <div class="question"><strong>17.</strong> Write a generator that yields all Fibonacci numbers up to a limit.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def fibonacci(limit):
    a, b = 0, 1
    while a <= limit:
        yield a
        a, b = b, a + b</code></pre></div>

    <div class="question"><strong>18.</strong> Write an async function that fetches multiple URLs concurrently.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import asyncio
import httpx

async def fetch_urls(urls):
    async with httpx.AsyncClient() as client:
        tasks = [client.get(url) for url in urls]
        responses = await asyncio.gather(*tasks)
        return [r.status_code for r in responses]</code></pre></div>

    <div class="question"><strong>19.</strong> Write a function that caches results using a decorator.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from functools import wraps

def memoize(func):
    cache = {}
    @wraps(func)
    def wrapper(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return wrapper

@memoize
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)</code></pre></div>

    <div class="question"><strong>20.</strong> Write a function that uses <code>itertools.groupby</code> to group words by their first letter.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from itertools import groupby

def group_by_first_letter(words):
    sorted_words = sorted(words)
    return {
        key: list(group)
        for key, group in groupby(sorted_words, key=lambda w: w[0].upper())
    }</code></pre></div>
  </div>

  <div class="exam-section">
    <h3>Section 4: Conceptual Questions (Questions 21-25)</h3>

    <div class="question"><strong>21.</strong> Compare <code>threading</code> vs <code>asyncio</code> — when would you use each?</div>
    <div class="answer">✅ <strong>Answer:</strong> Use <code>threading</code> when you have blocking I/O calls that may not have async equivalents. Use <code>asyncio</code> when you need many concurrent I/O operations with async libraries (e.g., web servers, API clients).</div>

    <div class="question"><strong>22.</strong> What is the difference between a decorator and a context manager?</div>
    <div class="answer">✅ <strong>Answer:</strong> A decorator wraps a function to modify its behavior permanently (used with <code>@</code> syntax). A context manager wraps a block of code for setup/teardown (used with <code>with</code> syntax).</div>

    <div class="question"><strong>23.</strong> How does <code>yield from</code> differ from <code>yield</code> in a generator?</div>
    <div class="answer">✅ <strong>Answer:</strong> <code>yield from</code> delegates to a sub-generator, yielding all values from it. It also handles sending values and exceptions to the sub-generator.</div>

    <div class="question"><strong>24.</strong> What is the difference between <code>@classmethod</code> and <code>@staticmethod</code>?</div>
    <div class="answer">✅ <strong>Answer:</strong> <code>@classmethod</code> receives the class (<code>cls</code>) as the first argument and can modify class state. <code>@staticmethod</code> receives no special first argument and behaves like a regular function.</div>

    <div class="question"><strong>25.</strong> When would you use <code>multiprocessing</code> instead of <code>threading</code>?</div>
    <div class="answer">✅ <strong>Answer:</strong> Use <code>multiprocessing</code> for CPU-bound tasks (computations) because it bypasses the GIL by running separate processes. Use <code>threading</code> for I/O-bound tasks (network, disk).</div>
  </div>
</div>

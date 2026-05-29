---
title: "📝 Practice Test 3: OOP & Exception Handling"
weight: 21
bookToc: false
---

# Practice Test 3: OOP & Exception Handling

<div class="exam-container">
  <div class="exam-header">
    <div class="exam-meta">
      <span><strong>📍 Topic:</strong> OOP & Exception Handling</span>
      <span><strong>⏱️ Time:</strong> 35 minutes</span>
      <span><strong>📝 Questions:</strong> 25</span>
    </div>
    <div class="exam-timer" id="exam-timer-3">⏱️ <span id="time-3">35:00</span></div>
  </div>

  <div class="exam-section">
    <h3>Section 1: Multiple Choice (Questions 1-10)</h3>

    <div class="question"><strong>1.</strong> What is the purpose of <code>__init__</code> method in a Python class?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q1" value="A"> A) Create the object in memory</label></div>
      <div class="option"><label><input type="radio" name="q1" value="B"> B) Initialize the object's attributes after creation</label></div>
      <div class="option"><label><input type="radio" name="q1" value="C"> C) Destroy the object</label></div>
      <div class="option"><label><input type="radio" name="q1" value="D"> D) Define the class interface</label></div>
    </div>
    <div class="answer" id="a1">✅ <strong>Answer:</strong> B) Initialize the object's attributes after creation. (<code>__new__</code> creates the object.)</div>

    <div class="question"><strong>2.</strong> Which keyword is used to refer to the parent class in Python?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q2" value="A"> A) <code>parent</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="B"> B) <code>super</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="C"> C) <code>super()</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="D"> D) <code>base</code></label></div>
    </div>
    <div class="answer" id="a2">✅ <strong>Answer:</strong> C) <code>super()</code> returns a proxy object to the parent class.</div>

    <div class="question"><strong>3.</strong> What does the <code>@staticmethod</code> decorator do?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q3" value="A"> A) Makes a method callable without creating an instance</label></div>
      <div class="option"><label><input type="radio" name="q3" value="B"> B) Makes a method receive the class as the first argument</label></div>
      <div class="option"><label><input type="radio" name="q3" value="C"> C) Prevents a method from being overridden</label></div>
      <div class="option"><label><input type="radio" name="q3" value="D"> D) Makes the method private</label></div>
    </div>
    <div class="answer" id="a3">✅ <strong>Answer:</strong> A) Static methods can be called on the class without an instance, and they don't receive self or cls.</div>

    <div class="question"><strong>4.</strong> What is the MRO (Method Resolution Order)?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q4" value="A"> A) The order in which methods are stored in memory</label></div>
      <div class="option"><label><input type="radio" name="q4" value="B"> B) The order Python searches for methods in inheritance hierarchy</label></div>
      <div class="option"><label><input type="radio" name="q4" value="C"> C) The order methods are called in runtime</label></div>
      <div class="option"><label><input type="radio" name="q4" value="D"> D) A list of all methods in a class</label></div>
    </div>
    <div class="answer" id="a4">✅ <strong>Answer:</strong> B) MRO determines the order Python searches for methods in the inheritance hierarchy (C3 linearization).</div>

    <div class="question"><strong>5.</strong> Which of the following is NOT a built-in exception in Python?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q5" value="A"> A) <code>ValueError</code></label></div>
      <div class="option"><label><input type="radio" name="q5" value="B"> B) <code>TypeError</code></label></div>
      <div class="option"><label><input type="radio" name="q5" value="C"> C) <code>NumberError</code></label></div>
      <div class="option"><label><input type="radio" name="q5" value="D"> D) <code>KeyError</code></label></div>
    </div>
    <div class="answer" id="a5">✅ <strong>Answer:</strong> C) <code>NumberError</code> is not a built-in exception.</div>

    <div class="question"><strong>6.</strong> What is the output? <code>try: print(1/0); except: print("error"); finally: print("done")</code></div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q6" value="A"> A) error</label></div>
      <div class="option"><label><input type="radio" name="q6" value="B"> B) error  done</label></div>
      <div class="option"><label><input type="radio" name="q6" value="C"> C) done</label></div>
      <div class="option"><label><input type="radio" name="q6" value="D"> D) error done</label></div>
    </div>
    <div class="answer" id="a6">✅ <strong>Answer:</strong> B) "error" and "done" on separate lines — <code>finally</code> always executes.</div>

    <div class="question"><strong>7.</strong> How do you create an abstract base class in Python?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q7" value="A"> A) Inherit from <code>ABC</code> and use <code>@abstractmethod</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="B"> B) Use the <code>@abstract</code> decorator</label></div>
      <div class="option"><label><input type="radio" name="q7" value="C"> C) Define a class with <code>abstract</code> keyword</label></div>
      <div class="option"><label><input type="radio" name="q7" value="D"> D) Create a class and raise NotImplementedError</label></div>
    </div>
    <div class="answer" id="a7">✅ <strong>Answer:</strong> A) Inherit from <code>ABC</code> (from <code>abc</code> module) and use <code>@abstractmethod</code>.</div>

    <div class="question"><strong>8.</strong> What does the <code>__str__</code> method return?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q8" value="A"> A) The memory address of the object</label></div>
      <div class="option"><label><input type="radio" name="q8" value="B"> B) A developer-friendly representation for debugging</label></div>
      <div class="option"><label><input type="radio" name="q8" value="C"> C) A user-friendly string representation</label></div>
      <div class="option"><label><input type="radio" name="q8" value="D"> D) The class name</label></div>
    </div>
    <div class="answer" id="a8">✅ <strong>Answer:</strong> C) <code>__str__</code> returns a user-friendly string representation (used by <code>print()</code>). <code>__repr__</code> is for debugging.</div>

    <div class="question"><strong>9.</strong> In a <code>try-except</code> block, the <code>else</code> clause executes when:</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q9" value="A"> A) An exception occurs</label></div>
      <div class="option"><label><input type="radio" name="q9" value="B"> B) No exception occurs</label></div>
      <div class="option"><label><input type="radio" name="q9" value="C"> C) Always</label></div>
      <div class="option"><label><input type="radio" name="q9" value="D"> D) When the exception is caught</label></div>
    </div>
    <div class="answer" id="a9">✅ <strong>Answer:</strong> B) <code>else</code> executes only when no exception was raised in the <code>try</code> block.</div>

    <div class="question"><strong>10.</strong> What is encapsulation in OOP?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q10" value="A"> A) Hiding internal state and requiring all interaction through methods</label></div>
      <div class="option"><label><input type="radio" name="q10" value="B"> B) Inheriting properties from a parent class</label></div>
      <div class="option"><label><input type="radio" name="q10" value="C"> C) Defining multiple methods with the same name</label></div>
      <div class="option"><label><input type="radio" name="q10" value="D"> D) Creating a class from an object</label></div>
    </div>
    <div class="answer" id="a10">✅ <strong>Answer:</strong> A) Encapsulation bundles data and methods, hiding internal state.</div>
  </div>

  <div class="exam-section">
    <h3>Section 2: True/False (Questions 11-15)</h3>

    <div class="question"><strong>11.</strong> Python supports multiple inheritance.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q11" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q11" value="B"> False</label></div>
    </div>
    <div class="answer" id="a11">✅ <strong>Answer:</strong> True — A class can inherit from multiple parent classes.</div>

    <div class="question"><strong>12.</strong> The <code>finally</code> block is optional in a try-except statement.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q12" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q12" value="B"> False</label></div>
    </div>
    <div class="answer" id="a12">✅ <strong>Answer:</strong> True — <code>finally</code> is optional but useful for cleanup.</div>

    <div class="question"><strong>13.</strong> A private attribute in Python (e.g., <code>__secret</code>) is completely inaccessible outside the class.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q13" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q13" value="B"> False</label></div>
    </div>
    <div class="answer" id="a13">✅ <strong>Answer:</strong> False — Name mangling only renames it to <code>_ClassName__secret</code>, which can still be accessed.</div>

    <div class="question"><strong>14.</strong> A class can have both a <code>__str__</code> and <code>__repr__</code> method.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q14" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q14" value="B"> False</label></div>
    </div>
    <div class="answer" id="a14">✅ <strong>Answer:</strong> True — Both can coexist; <code>__str__</code> is for users, <code>__repr__</code> for developers.</div>

    <div class="question"><strong>15.</strong> The <code>__init__</code> method is called before <code>__new__</code>.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q15" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q15" value="B"> False</label></div>
    </div>
    <div class="answer" id="a15">✅ <strong>Answer:</strong> False — <code>__new__</code> is called first (creates the object), then <code>__init__</code> initializes it.</div>
  </div>

  <div class="exam-section">
    <h3>Section 3: Coding Exercises (Questions 16-20)</h3>

    <div class="question"><strong>16.</strong> Create a <code>BankAccount</code> class with deposit, withdraw, and balance methods.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self._balance = balance
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")
        self._balance += amount
        return self._balance
    
    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")
        if amount > self._balance:
            raise ValueError("Insufficient funds")
        self._balance -= amount
        return self._balance
    
    @property
    def balance(self):
        return self._balance</code></pre></div>

    <div class="question"><strong>17.</strong> Create a custom exception and use it.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>class InsufficientFundsError(Exception):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"Need {amount}, have {balance}")

def withdraw(balance, amount):
    if amount > balance:
        raise InsufficientFundsError(balance, amount)
    return balance - amount</code></pre></div>

    <div class="question"><strong>18.</strong> Write a class that implements <code>__len__</code>, <code>__getitem__</code>, and <code>__iter__</code>.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>class Playlist:
    def __init__(self, songs):
        self.songs = songs
    def __len__(self):
        return len(self.songs)
    def __getitem__(self, index):
        return self.songs[index]
    def __iter__(self):
        return iter(self.songs)</code></pre></div>

    <div class="question"><strong>19.</strong> Create a context manager that measures execution time.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import time
from contextlib import contextmanager

@contextmanager
def timer(label=""):
    start = time.perf_counter()
    try:
        yield
    finally:
        end = time.perf_counter()
        print(f"{label}: {end - start:.4f}s")

# Usage:
# with timer("sleep"):
#     time.sleep(1)</code></pre></div>

    <div class="question"><strong>20.</strong> Create a <code>@property</code> that validates input.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>class Person:
    def __init__(self, name, age):
        self.name = name
        self._age = 0
        self.age = age  # Use setter
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if not isinstance(value, (int, float)):
            raise TypeError("Age must be a number")
        if value < 0 or value > 150:
            raise ValueError("Age must be between 0 and 150")
        self._age = value</code></pre></div>
  </div>

  <div class="exam-section">
    <h3>Section 4: Output Prediction (Questions 21-25)</h3>

    <div class="question"><strong>21.</strong> <code>class A: pass; a = A(); print(type(a))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>&lt;class '__main__.A'&gt;</code></div>

    <div class="question"><strong>22.</strong> <code>class A: x = 1; class B(A): pass; print(B.x)</code></div>
    <div class="answer">✅ <strong>Answer:</strong> 1 (inherited from A)</div>

    <div class="question"><strong>23.</strong> <code>class A: pass; print(hasattr(A(), 'missing'))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> False</div>

    <div class="question"><strong>24.</strong> <code>print(issubclass(bool, int))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> True — <code>bool</code> is a subclass of <code>int</code> in Python.</div>

    <div class="question"><strong>25.</strong> <code>try: pass; except: pass; else: print("else"); finally: print("finally")</code></div>
    <div class="answer">✅ <strong>Answer:</strong> "else" then "finally" — The <code>else</code> block runs because no exception occurred.</div>
  </div>
</div>

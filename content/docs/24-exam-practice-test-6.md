---
title: "📝 Practice Test 6: Mock Interview — Full Assessment"
weight: 24
bookToc: false
---

# Practice Test 6: Mock Interview — Full Assessment

<div class="exam-container">
  <div class="exam-header">
    <div class="exam-meta">
      <span><strong>📍 Topic:</strong> Full Python Assessment</span>
      <span><strong>⏱️ Time:</strong> 60 minutes</span>
      <span><strong>📝 Questions:</strong> 30</span>
    </div>
    <div class="exam-timer" id="exam-timer-6">⏱️ <span id="time-6">60:00</span></div>
  </div>

  <div class="exam-section">
    <h3>Section 1: Multiple Choice (Questions 1-10)</h3>

    <div class="question"><strong>1.</strong> What will be the output of <code>print(0.1 + 0.2 == 0.3)</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q1" value="A"> A) True</label></div>
      <div class="option"><label><input type="radio" name="q1" value="B"> B) False</label></div>
      <div class="option"><label><input type="radio" name="q1" value="C"> C) Error</label></div>
      <div class="option"><label><input type="radio" name="q1" value="D"> D) None</label></div>
    </div>
    <div class="answer" id="a1">✅ <strong>Answer:</strong> B) False — Floating-point precision: 0.1 + 0.2 = 0.30000000000000004 ≠ 0.3.</div>

    <div class="question"><strong>2.</strong> What is the purpose of the <code>__slots__</code> attribute in a class?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q2" value="A"> A) Prevents attribute creation at runtime</label></div>
      <div class="option"><label><input type="radio" name="q2" value="B"> B) Reduces memory usage by preventing __dict__ creation</label></div>
      <div class="option"><label><input type="radio" name="q2" value="C"> C) Speeds up attribute access</label></div>
      <div class="option"><label><input type="radio" name="q2" value="D"> D) All of the above</label></div>
    </div>
    <div class="answer" id="a2">✅ <strong>Answer:</strong> D) <code>__slots__</code> prevents adding new attributes, reduces memory, and speeds up access.</div>

    <div class="question"><strong>3.</strong> Which of the following sorting algorithms is Python's built-in <code>sorted()</code> based on?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q3" value="A"> A) QuickSort</label></div>
      <div class="option"><label><input type="radio" name="q3" value="B"> B) MergeSort</label></div>
      <div class="option"><label><input type="radio" name="q3" value="C"> C) TimSort</label></div>
      <div class="option"><label><input type="radio" name="q3" value="D"> D) BubbleSort</label></div>
    </div>
    <div class="answer" id="a3">✅ <strong>Answer:</strong> C) TimSort — a hybrid sorting algorithm derived from MergeSort and InsertionSort.</div>

    <div class="question"><strong>4.</strong> What is the output of <code>print(*[1, 2, 3])</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q4" value="A"> A) <code>[1, 2, 3]</code></label></div>
      <div class="option"><label><input type="radio" name="q4" value="B"> B) <code>1 2 3</code></label></div>
      <div class="option"><label><input type="radio" name="q4" value="C"> C) <code>1, 2, 3</code></label></div>
      <div class="option"><label><input type="radio" name="q4" value="D"> D) Error</label></div>
    </div>
    <div class="answer" id="a4">✅ <strong>Answer:</strong> B) <code>1 2 3</code> — The <code>*</code> unpacking operator unpacks the list as separate arguments to print.</div>

    <div class="question"><strong>5.</strong> How do you define a type alias in Python 3.12+?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q5" value="A"> A) <code>type Vector = list[float]</code></label></div>
      <div class="option"><label><input type="radio" name="q5" value="B"> B) <code>Vector = list[float]</code></label></div>
      <div class="option"><label><input type="radio" name="q5" value="C"> C) <code>type Vector = List[float]</code></label></div>
      <div class="option"><label><input type="radio" name="q5" value="D"> D) <code>alias Vector = list[float]</code></label></div>
    </div>
    <div class="answer" id="a5">✅ <strong>Answer:</strong> A) Python 3.12 introduced the <code>type</code> keyword for type aliases. Before that, B was used.</div>

    <div class="question"><strong>6.</strong> What is the result of <code>isinstance(True, int)</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q6" value="A"> A) True</label></div>
      <div class="option"><label><input type="radio" name="q6" value="B"> B) False</label></div>
      <div class="option"><label><input type="radio" name="q6" value="C"> C) TypeError</label></div>
      <div class="option"><label><input type="radio" name="q6" value="D"> D) None</label></div>
    </div>
    <div class="answer" id="a6">✅ <strong>Answer:</strong> A) True — <code>bool</code> is a subclass of <code>int</code> in Python (<code>True == 1</code>, <code>False == 0</code>).</div>

    <div class="question"><strong>7.</strong> What is the correct way to handle multiple exceptions with a single block?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q7" value="A"> A) <code>except (ValueError, TypeError) as e:</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="B"> B) <code>except ValueError, TypeError:</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="C"> C) <code>except [ValueError, TypeError]:</code></label></div>
      <div class="option"><label><input type="radio" name="q7" value="D"> D) <code>except ValueError & TypeError:</code></label></div>
    </div>
    <div class="answer" id="a7">✅ <strong>Answer:</strong> A) Use a tuple of exception types in parentheses.</div>

    <div class="question"><strong>8.</strong> What is the output of <code>print({i: i**2 for i in range(3)})</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q8" value="A"> A) <code>{0: 0, 1: 1, 2: 4}</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="B"> B) <code>{0: 0, 1: 1, 2: 4, 3: 9}</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="C"> C) <code>[0, 1, 4]</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="D"> D) <code>{0, 1, 4}</code></label></div>
    </div>
    <div class="answer" id="a8">✅ <strong>Answer:</strong> A) Dict comprehension with range(3) = {0, 1, 2}.</div>

    <div class="question"><strong>9.</strong> Which module provides <code>Path</code> for filesystem paths?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q9" value="A"> A) <code>os.path</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="B"> B) <code>pathlib</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="C"> C) <code>filepath</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="D"> D) <code>filesystem</code></label></div>
    </div>
    <div class="answer" id="a9">✅ <strong>Answer:</strong> B) <code>pathlib.Path</code> is the modern, object-oriented way to handle file paths.</div>

    <div class="question"><strong>10.</strong> How do you specify a path for Python to look for modules?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q10" value="A"> A) <code>PYTHONPATH</code> environment variable</label></div>
      <div class="option"><label><input type="radio" name="q10" value="B"> B) <code>sys.path.append()</code></label></div>
      <div class="option"><label><input type="radio" name="q10" value="C"> C) Both A and B</label></div>
      <div class="option"><label><input type="radio" name="q10" value="D"> D) <code>os.add_module_path()</code></label></div>
    </div>
    <div class="answer" id="a10">✅ <strong>Answer:</strong> C) Both setting <code>PYTHONPATH</code> and modifying <code>sys.path</code> work.</div>
  </div>

  <div class="exam-section">
    <h3>Section 2: Coding Challenge (Questions 11-18)</h3>

    <div class="question"><strong>11.</strong> Write a function that checks if a string is a palindrome (ignoring case, spaces, and punctuation).</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import re

def is_palindrome(s):
    cleaned = re.sub(r'[^a-zA-Z0-9]', '', s).lower()
    return cleaned == cleaned[::-1]

# Tests
print(is_palindrome("A man, a plan, a canal: Panama"))  # True
print(is_palindrome("race a car"))  # False</code></pre></div>

    <div class="question"><strong>12.</strong> Implement a function that finds the missing number in an array of 1 to n.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def find_missing(nums):
    n = len(nums) + 1
    expected_sum = n * (n + 1) // 2
    actual_sum = sum(nums)
    return expected_sum - actual_sum

print(find_missing([1, 2, 4, 5, 6]))  # 3</code></pre></div>

    <div class="question"><strong>13.</strong> Implement a function to compress a string (e.g., "aabcccccaaa" → "a2b1c5a3").</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def compress_string(s):
    if not s:
        return ""
    result = []
    count = 1
    for i in range(1, len(s)):
        if s[i] == s[i-1]:
            count += 1
        else:
            result.append(f"{s[i-1]}{count}")
            count = 1
    result.append(f"{s[-1]}{count}")
    compressed = "".join(result)
    return compressed if len(compressed) < len(s) else s

print(compress_string("aabcccccaaa"))  # a2b1c5a3</code></pre></div>

    <div class="question"><strong>14.</strong> Write a function that merges two sorted linked lists.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def merge_two_lists(l1, l2):
    dummy = ListNode()
    current = dummy
    
    while l1 and l2:
        if l1.val <= l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    
    current.next = l1 or l2
    return dummy.next</code></pre></div>

    <div class="question"><strong>15.</strong> Implement a Queue using two stacks.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>class QueueWithStacks:
    def __init__(self):
        self.stack_in = []
        self.stack_out = []
    
    def enqueue(self, value):
        self.stack_in.append(value)
    
    def dequeue(self):
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
        return self.stack_out.pop()
    
    def peek(self):
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
        return self.stack_out[-1]
    
    def empty(self):
        return len(self.stack_in) == 0 and len(self.stack_out) == 0</code></pre></div>

    <div class="question"><strong>16.</strong> Find the longest common prefix among a list of strings.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def longest_common_prefix(strs):
    if not strs:
        return ""
    prefix = strs[0]
    for s in strs[1:]:
        while s[:len(prefix)] != prefix and prefix:
            prefix = prefix[:-1]
    return prefix

print(longest_common_prefix(["flower", "flow", "flight"]))  # "fl"</code></pre></div>

    <div class="question"><strong>17.</strong> Write a decorator that retries a function up to 3 times with exponential backoff.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>import time
from functools import wraps

def retry(max_attempts=3, base_delay=1):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, max_attempts + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts:
                        raise
                    delay = base_delay * (2 ** (attempt - 1))
                    print(f"Attempt {attempt} failed, retrying in {delay}s...")
                    time.sleep(delay)
        return wrapper
    return decorator</code></pre></div>

    <div class="question"><strong>18.</strong> Implement a function that performs a deep merge of two dictionaries.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def deep_merge(dict1, dict2):
    result = dict1.copy()
    for key, value in dict2.items():
        if key in result and isinstance(result[key], dict) and isinstance(value, dict):
            result[key] = deep_merge(result[key], value)
        else:
            result[key] = value
    return result

a = {"a": 1, "b": {"c": 2, "d": 3}}
b = {"b": {"d": 4, "e": 5}, "f": 6}
print(deep_merge(a, b))
# {'a': 1, 'b': {'c': 2, 'd': 4, 'e': 5}, 'f': 6}</code></pre></div>
  </div>

  <div class="exam-section">
    <h3>Section 3: Conceptual Questions (Questions 19-25)</h3>

    <div class="question"><strong>19.</strong> Explain the difference between <code>__str__</code> and <code>__repr__</code> in Python.</div>
    <div class="answer">✅ <strong>Answer:</strong> <code>__str__</code> is for end-users (readable, informal), used by <code>print()</code>. <code>__repr__</code> is for developers (unambiguous, detailed), used by <code>repr()</code> and the REPL. If <code>__str__</code> is not defined, <code>__repr__</code> is used as fallback.</div>

    <div class="question"><strong>20.</strong> How does Python's garbage collection work?</div>
    <div class="answer">✅ <strong>Answer:</strong> Python uses reference counting (primary) and a generational garbage collector (secondary). Reference counting immediately frees objects when their count reaches zero. The GC handles circular references by periodically detecting and collecting unreachable cycles. The GC has three generations — younger generations are collected more frequently.</div>

    <div class="question"><strong>21.</strong> What is the difference between <code>deepcopy</code> and <code>shallow copy</code>?</div>
    <div class="answer">✅ <strong>Answer:</strong> A shallow copy creates a new object but inserts references to the original's nested objects. A deep copy recursively copies all nested objects, creating fully independent copies. Use <code>copy.copy()</code> for shallow and <code>copy.deepcopy()</code> for deep copies.</div>

    <div class="question"><strong>22.</strong> Explain the walrus operator (<code>:=</code>) and give an example.</div>
    <div class="answer">✅ <strong>Answer:</strong> The walrus operator (<code>:=</code>) assigns a value to a variable within an expression. Useful in while loops and comprehensions:
<pre><code># Without walrus
line = f.readline()
while line:
    print(line)
    line = f.readline()

# With walrus
while line := f.readline():
    print(line)</code></pre></div>

    <div class="question"><strong>23.</strong> How do you handle circular imports in Python?</div>
    <div class="answer">✅ <strong>Answer:</strong> Solutions: 1) Restructure code — move shared code to a common module. 2) Import inside functions (lazy import) instead of at module level. 3) Use <code>import module</code> instead of <code>from module import name</code>. 4) Combine the two modules. 5) Use a third module for shared dependencies.</div>

    <div class="question"><strong>24.</strong> Explain Python's method resolution order (MRO) with an example.</div>
    <div class="answer">✅ <strong>Answer:</strong> MRO determines the order Python searches for methods in inheritance hierarchies. It uses C3 linearization. For <code>class D(B, C)</code> where B and C inherit from A: <code>D -> B -> C -> A -> object</code>. Check <code>D.__mro__</code> to see the order. Python uses this to resolve which method to call when using <code>super()</code>.</div>

    <div class="question"><strong>25.</strong> What are Python's <code>__getattr__</code> and <code>__getattribute__</code> methods?</div>
    <div class="answer">✅ <strong>Answer:</strong> <code>__getattribute__</code> is called unconditionally for every attribute access. <code>__getattr__</code> is only called when the attribute is not found through normal lookup. Overriding <code>__getattr__</code> is common for dynamic attributes or proxy classes. Be careful with <code>__getattribute__</code> — infinite recursion is easy to trigger.</div>
  </div>

  <div class="exam-section">
    <h3>Section 4: Output Prediction (Questions 26-30)</h3>

    <div class="question"><strong>26.</strong> <code>def f(a, L=[]): L.append(a); return L; print(f(1, [])); print(f(2)); print(f(3))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1]</code>, <code>[2]</code>, <code>[2, 3]</code> — First call uses a new list; subsequent calls use the default list which persists.</div>

    <div class="question"><strong>27.</strong> <code>print(sorted([3, 1, 2], key=lambda x: -x))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[3, 2, 1]</code> — Sorted in descending order using negative key.</div>

    <div class="question"><strong>28.</strong> <code>import this; print("".join([this.d.get(c, c) for c in "pbatenghyngvbaf"]))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>"congratulations"</code> — This uses the "rot13" cipher from the Zen of Python.</div>

    <div class="question"><strong>29.</strong> <code>print([x for x in range(1, 11) if all(x % y != 0 for y in range(2, int(x**0.5) + 1))])</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1, 2, 3, 5, 7]</code> — Prime numbers up to 10 (1 is included because the inner generator is empty for x=1, and all([]) is True).</div>

    <div class="question"><strong>30.</strong> <code>class A: pass; class B(A): pass; class C(A): pass; class D(B, C): pass; print(D.__mro__[1])</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>&lt;class '__main__.B'&gt;</code> — MRO is D → B → C → A → object, so index 1 is B.</div>
  </div>

  <div class="exam-section">
    <div class="exam-summary">
      <h3>🏆 Congratulations!</h3>
      <p>You've completed the full mock interview assessment. Review any incorrect answers and revisit the relevant chapters for deeper understanding.</p>
      <p>Topics covered: Python fundamentals, data structures, OOP, advanced topics, web development, databases, and algorithms.</p>
    </div>
  </div>
</div>

---
title: "📝 Practice Test 1: Python Fundamentals"
weight: 19
bookToc: false
---

# Practice Test 1: Python Fundamentals

<div class="exam-container">
  <div class="exam-header">
    <div class="exam-meta">
      <span><strong>📍 Topic:</strong> Python Fundamentals</span>
      <span><strong>⏱️ Time:</strong> 30 minutes</span>
      <span><strong>📝 Questions:</strong> 25</span>
    </div>
    <div class="exam-timer" id="exam-timer-1">⏱️ <span id="time-1">30:00</span></div>
  </div>

  <div class="exam-section">
    <h3>Section 1: Multiple Choice (Questions 1-10)</h3>

    <div class="question"><strong>1.</strong> What is the output of <code>print(type(10/2))</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q1" value="A"> A) <code>&lt;class 'int'&gt;</code></label></div>
      <div class="option"><label><input type="radio" name="q1" value="B"> B) <code>&lt;class 'float'&gt;</code></label></div>
      <div class="option"><label><input type="radio" name="q1" value="C"> C) <code>&lt;class 'number'&gt;</code></label></div>
      <div class="option"><label><input type="radio" name="q1" value="D"> D) TypeError</label></div>
    </div>
    <div class="answer" id="a1">✅ <strong>Answer:</strong> B) <code>&lt;class 'float'&gt;</code> — In Python 3, <code>/</code> always returns a float.</div>

    <div class="question"><strong>2.</strong> Which of the following is NOT a valid Python variable name?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q2" value="A"> A) <code>my_var</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="B"> B) <code>_private</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="C"> C) <code>2nd_place</code></label></div>
      <div class="option"><label><input type="radio" name="q2" value="D"> D) <code>VAR_NAME</code></label></div>
    </div>
    <div class="answer" id="a2">✅ <strong>Answer:</strong> C) <code>2nd_place</code> — Variable names cannot start with a digit.</div>

    <div class="question"><strong>3.</strong> What is the result of <code>print("Hello" + 5)</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q3" value="A"> A) <code>Hello5</code></label></div>
      <div class="option"><label><input type="radio" name="q3" value="B"> B) <code>TypeError</code></label></div>
      <div class="option"><label><input type="radio" name="q3" value="C"> C) <code>Hello 5</code></label></div>
      <div class="option"><label><input type="radio" name="q3" value="D"> D) <code>"Hello5"</code></label></div>
    </div>
    <div class="answer" id="a3">✅ <strong>Answer:</strong> B) TypeError — You cannot concatenate str and int directly.</div>

    <div class="question"><strong>4.</strong> What does <code>len("Python")</code> return?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q4" value="A"> A) 5</label></div>
      <div class="option"><label><input type="radio" name="q4" value="B"> B) 6</label></div>
      <div class="option"><label><input type="radio" name="q4" value="C"> C) 7</label></div>
      <div class="option"><label><input type="radio" name="q4" value="D"> D) Error</label></div>
    </div>
    <div class="answer" id="a4">✅ <strong>Answer:</strong> B) 6 — "Python" has 6 characters.</div>

    <div class="question"><strong>5.</strong> Which of these is a mutable data type?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q5" value="A"> A) Tuple</label></div>
      <div class="option"><label><input type="radio" name="q5" value="B"> B) String</label></div>
      <div class="option"><label><input type="radio" name="q5" value="C"> C) List</label></div>
      <div class="option"><label><input type="radio" name="q5" value="D"> D) Frozenset</label></div>
    </div>
    <div class="answer" id="a5">✅ <strong>Answer:</strong> C) List — Lists are mutable; tuples, strings, and frozensets are immutable.</div>

    <div class="question"><strong>6.</strong> What is the output of <code>print(3 * 'ab')</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q6" value="A"> A) <code>ababab</code></label></div>
      <div class="option"><label><input type="radio" name="q6" value="B"> B) <code>3ab</code></label></div>
      <div class="option"><label><input type="radio" name="q6" value="C"> C) <code>ab3</code></label></div>
      <div class="option"><label><input type="radio" name="q6" value="D"> D) Error</label></div>
    </div>
    <div class="answer" id="a6">✅ <strong>Answer:</strong> A) <code>ababab</code> — The * operator repeats strings.</div>

    <div class="question"><strong>7.</strong> What is the difference between <code>==</code> and <code>is</code> in Python?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q7" value="A"> A) They are the same</label></div>
      <div class="option"><label><input type="radio" name="q7" value="B"> B) <code>==</code> compares values, <code>is</code> compares identity</label></div>
      <div class="option"><label><input type="radio" name="q7" value="C"> C) <code>==</code> compares identity, <code>is</code> compares values</label></div>
      <div class="option"><label><input type="radio" name="q7" value="D"> D) <code>==</code> is for numbers only</label></div>
    </div>
    <div class="answer" id="a7">✅ <strong>Answer:</strong> B) <code>==</code> compares values, <code>is</code> compares identity (memory address).</div>

    <div class="question"><strong>8.</strong> What is the output of <code>print(not True and False or True)</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q8" value="A"> A) True</label></div>
      <div class="option"><label><input type="radio" name="q8" value="B"> B) False</label></div>
      <div class="option"><label><input type="radio" name="q8" value="C"> C) None</label></div>
      <div class="option"><label><input type="radio" name="q8" value="D"> D) Error</label></div>
    </div>
    <div class="answer" id="a8">✅ <strong>Answer:</strong> A) True — Order: not → and → or, so (not True and False) or True → (False and False) or True → False or True → True.</div>

    <div class="question"><strong>9.</strong> Which of the following creates an empty set?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q9" value="A"> A) <code>{}</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="B"> B) <code>set()</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="C"> C) <code>[]</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="D"> D) <code>()</code></label></div>
    </div>
    <div class="answer" id="a9">✅ <strong>Answer:</strong> B) <code>set()</code> — <code>{}</code> creates an empty dict, not an empty set.</div>

    <div class="question"><strong>10.</strong> What does <code>range(5)</code> generate?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q10" value="A"> A) [1, 2, 3, 4, 5]</label></div>
      <div class="option"><label><input type="radio" name="q10" value="B"> B) [0, 1, 2, 3, 4]</label></div>
      <div class="option"><label><input type="radio" name="q10" value="C"> C) [0, 1, 2, 3, 4, 5]</label></div>
      <div class="option"><label><input type="radio" name="q10" value="D"> D) (0, 1, 2, 3, 4)</label></div>
    </div>
    <div class="answer" id="a10">✅ <strong>Answer:</strong> B) [0, 1, 2, 3, 4] — range starts from 0 by default and excludes the stop value.</div>
  </div>

  <div class="exam-section">
    <h3>Section 2: True/False (Questions 11-15)</h3>

    <div class="question"><strong>11.</strong> Python is a statically-typed language.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q11" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q11" value="B"> False</label></div>
    </div>
    <div class="answer" id="a11">✅ <strong>Answer:</strong> False — Python is dynamically-typed.</div>

    <div class="question"><strong>12.</strong> Tuples can be used as dictionary keys.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q12" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q12" value="B"> False</label></div>
    </div>
    <div class="answer" id="a12">✅ <strong>Answer:</strong> True — Tuples are hashable (immutable) so they can be dict keys.</div>

    <div class="question"><strong>13.</strong> The <code>global</code> keyword allows modifying a variable in an enclosing (non-global) scope.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q13" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q13" value="B"> False</label></div>
    </div>
    <div class="answer" id="a13">✅ <strong>Answer:</strong> False — <code>global</code> modifies the global scope; <code>nonlocal</code> modifies an enclosing scope.</div>

    <div class="question"><strong>14.</strong> The <code>break</code> statement can be used inside a list comprehension.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q14" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q14" value="B"> False</label></div>
    </div>
    <div class="answer" id="a14">✅ <strong>Answer:</strong> False — <code>break</code> cannot be used inside comprehensions; they are expressions, not statements.</div>

    <div class="question"><strong>15.</strong> Python's <code>with</code> statement automatically closes files even if an exception occurs.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q15" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q15" value="B"> False</label></div>
    </div>
    <div class="answer" id="a15">✅ <strong>Answer:</strong> True — Context managers guarantee cleanup even when exceptions occur.</div>
  </div>

  <div class="exam-section">
    <h3>Section 3: Coding Exercises (Questions 16-20)</h3>

    <div class="question"><strong>16.</strong> Write a function that checks if a number is even.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def is_even(n):
    return n % 2 == 0</code></pre></div>

    <div class="question"><strong>17.</strong> Write a function that returns the factorial of n (iterative).</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result</code></pre></div>

    <div class="question"><strong>18.</strong> Write a function that reverses a string.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def reverse_string(s):
    return s[::-1]</code></pre></div>

    <div class="question"><strong>19.</strong> Write a function that counts the vowels in a string.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def count_vowels(s):
    vowels = "aeiouAEIOU"
    return sum(1 for char in s if char in vowels)</code></pre></div>

    <div class="question"><strong>20.</strong> Write a function that finds the maximum element in a list without using <code>max()</code>.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def find_max(lst):
    if not lst:
        return None
    max_val = lst[0]
    for item in lst[1:]:
        if item > max_val:
            max_val = item
    return max_val</code></pre></div>
  </div>

  <div class="exam-section">
    <h3>Section 4: Output Prediction (Questions 21-25)</h3>

    <div class="question"><strong>21.</strong> What is the output? <code>print(list(range(0, 10, 2)))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[0, 2, 4, 6, 8]</code></div>

    <div class="question"><strong>22.</strong> What is the output? <code>print(2 ** 3 ** 2)</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>512</code> — <code>**</code> is right-associative: 2 ** (3 ** 2) = 2 ** 9 = 512.</div>

    <div class="question"><strong>23.</strong> What is the output? <code>print([x*2 for x in [1,2,3] if x > 1])</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[4, 6]</code></div>

    <div class="question"><strong>24.</strong> What is the output? <code>x = [1, 2, 3]; y = x; y.append(4); print(x)</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1, 2, 3, 4]</code> — Lists are mutable and y is a reference to the same object.</div>

    <div class="question"><strong>25.</strong> What is the output? <code>print(bool([]), bool([0]), bool(""))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>False True False</code> — Empty list is falsy, non-empty list is truthy, empty string is falsy.</div>
  </div>
</div>

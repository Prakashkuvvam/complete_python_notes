---
title: "📝 Practice Test 2: Data Structures & Functions"
weight: 20
bookToc: false
---

# Practice Test 2: Data Structures & Functions

<div class="exam-container">
  <div class="exam-header">
    <div class="exam-meta">
      <span><strong>📍 Topic:</strong> Data Structures & Functions</span>
      <span><strong>⏱️ Time:</strong> 35 minutes</span>
      <span><strong>📝 Questions:</strong> 25</span>
    </div>
    <div class="exam-timer" id="exam-timer-2">⏱️ <span id="time-2">35:00</span></div>
  </div>

  <div class="exam-section">
    <h3>Section 1: Multiple Choice (Questions 1-10)</h3>

    <div class="question"><strong>1.</strong> What is the time complexity of checking if an item exists in a Python set?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q1" value="A"> A) O(n)</label></div>
      <div class="option"><label><input type="radio" name="q1" value="B"> B) O(log n)</label></div>
      <div class="option"><label><input type="radio" name="q1" value="C"> C) O(1) average</label></div>
      <div class="option"><label><input type="radio" name="q1" value="D"> D) O(n²)</label></div>
    </div>
    <div class="answer" id="a1">✅ <strong>Answer:</strong> C) O(1) average — Python sets are hash tables, providing average O(1) lookup.</div>

    <div class="question"><strong>2.</strong> What does <code>*args</code> represent in a function definition?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q2" value="A"> A) All keyword arguments as a dict</label></div>
      <div class="option"><label><input type="radio" name="q2" value="B"> B) All positional arguments as a list</label></div>
      <div class="option"><label><input type="radio" name="q2" value="C"> C) All positional arguments as a tuple</label></div>
      <div class="option"><label><input type="radio" name="q2" value="D"> D) All arguments as a set</label></div>
    </div>
    <div class="answer" id="a2">✅ <strong>Answer:</strong> C) All positional arguments as a tuple.</div>

    <div class="question"><strong>3.</strong> What is the output? <code>d = {1: 'a', 2: 'b'}; print(d.get(3, 'default'))</code></div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q3" value="A"> A) KeyError</label></div>
      <div class="option"><label><input type="radio" name="q3" value="B"> B) None</label></div>
      <div class="option"><label><input type="radio" name="q3" value="C"> C) 'default'</label></div>
      <div class="option"><label><input type="radio" name="q3" value="D"> D) d[3]</label></div>
    </div>
    <div class="answer" id="a3">✅ <strong>Answer:</strong> C) 'default' — <code>.get()</code> returns the default if key is missing.</div>

    <div class="question"><strong>4.</strong> Which of the following creates a list with elements 1, 4, 9, 16?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q4" value="A"> A) <code>[x**2 for x in range(4)]</code></label></div>
      <div class="option"><label><input type="radio" name="q4" value="B"> B) <code>[x**2 for x in range(1, 5)]</code></label></div>
      <div class="option"><label><input type="radio" name="q4" value="C"> C) <code>[x*x for x in (1,2,3,4)]</code></label></div>
      <div class="option"><label><input type="radio" name="q4" value="D"> D) Both B and C</label></div>
    </div>
    <div class="answer" id="a4">✅ <strong>Answer:</strong> D) Both B and C produce [1, 4, 9, 16].</div>

    <div class="question"><strong>5.</strong> What is the output of <code>print({1, 2, 3} & {2, 3, 4})</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q5" value="A"> A) {1, 2, 3}</label></div>
      <div class="option"><label><input type="radio" name="q5" value="B"> B) {2, 3, 4}</label></div>
      <div class="option"><label><input type="radio" name="q5" value="C"> C) {2, 3}</label></div>
      <div class="option"><label><input type="radio" name="q5" value="D"> D) {1, 2, 3, 4}</label></div>
    </div>
    <div class="answer" id="a5">✅ <strong>Answer:</strong> C) {2, 3} — & is set intersection.</div>

    <div class="question"><strong>6.</strong> What is the purpose of the <code>return</code> statement in a Python generator using <code>yield</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q6" value="A"> A) Returns a value and continues</label></div>
      <div class="option"><label><input type="radio" name="q6" value="B"> B) Stops iteration with a return value in StopIteration</label></div>
      <div class="option"><label><input type="radio" name="q6" value="C"> C) Same as yield</label></div>
      <div class="option"><label><input type="radio" name="q6" value="D"> D) Cannot use return in a generator</label></div>
    </div>
    <div class="answer" id="a6">✅ <strong>Answer:</strong> B) <code>return</code> in a generator signals the <code>StopIteration</code> exception; the value is stored in <code>StopIteration.value</code>.</div>

    <div class="question"><strong>7.</strong> What is the output of <code>f = lambda x: x**2; print(f(5))</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q7" value="A"> A) 25</label></div>
      <div class="option"><label><input type="radio" name="q7" value="B"> B) 5</label></div>
      <div class="option"><label><input type="radio" name="q7" value="C"> C) None</label></div>
      <div class="option"><label><input type="radio" name="q7" value="D"> D) Error</label></div>
    </div>
    <div class="answer" id="a7">✅ <strong>Answer:</strong> A) 25 — Lambda function squares the input.</div>

    <div class="question"><strong>8.</strong> How do you access the last element of a list <code>lst</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q8" value="A"> A) <code>lst[len(lst)]</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="B"> B) <code>lst[-1]</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="C"> C) <code>lst.last()</code></label></div>
      <div class="option"><label><input type="radio" name="q8" value="D"> D) <code>lst[last]</code></label></div>
    </div>
    <div class="answer" id="a8">✅ <strong>Answer:</strong> B) <code>lst[-1]</code> — Python supports negative indexing.</div>

    <div class="question"><strong>9.</strong> What is the result of <code>"a" + "b" * 3</code>?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q9" value="A"> A) <code>abbb</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="B"> B) <code>ab3</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="C"> C) <code>aaab</code></label></div>
      <div class="option"><label><input type="radio" name="q9" value="D"> D) <code>aaa</code></label></div>
    </div>
    <div class="answer" id="a9">✅ <strong>Answer:</strong> A) <code>abbb</code> — <code>*</code> has higher precedence than <code>+</code>: <code>"a" + ("b" * 3)</code>.</div>

    <div class="question"><strong>10.</strong> What does <code>from collections import Counter</code> provide?</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q10" value="A"> A) A thread-safe counter</label></div>
      <div class="option"><label><input type="radio" name="q10" value="B"> B) A dict subclass for counting hashable objects</label></div>
      <div class="option"><label><input type="radio" name="q10" value="C"> C) An atomic increment operation</label></div>
      <div class="option"><label><input type="radio" name="q10" value="D"> D) A performance timer</label></div>
    </div>
    <div class="answer" id="a10">✅ <strong>Answer:</strong> B) A dict subclass for counting hashable objects.</div>
  </div>

  <div class="exam-section">
    <h3>Section 2: True/False (Questions 11-15)</h3>

    <div class="question"><strong>11.</strong> Python dictionaries maintain insertion order as of Python 3.7.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q11" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q11" value="B"> False</label></div>
    </div>
    <div class="answer" id="a11">✅ <strong>Answer:</strong> True — Dictionary ordering is an official language feature since Python 3.7.</div>

    <div class="question"><strong>12.</strong> A lambda function can contain multiple statements.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q12" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q12" value="B"> False</label></div>
    </div>
    <div class="answer" id="a12">✅ <strong>Answer:</strong> False — Lambda functions can only contain a single expression, not statements.</div>

    <div class="question"><strong>13.</strong> The <code>defaultdict</code> from <code>collections</code> raises a KeyError for missing keys.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q13" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q13" value="B"> False</label></div>
    </div>
    <div class="answer" id="a13">✅ <strong>Answer:</strong> False — <code>defaultdict</code> returns a default value instead of raising KeyError.</div>

    <div class="question"><strong>14.</strong> The <code>zip()</code> function stops at the shortest input iterable.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q14" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q14" value="B"> False</label></div>
    </div>
    <div class="answer" id="a14">✅ <strong>Answer:</strong> True — <code>zip()</code> stops when the shortest iterable is exhausted.</div>

    <div class="question"><strong>15.</strong> A function without a <code>return</code> statement returns <code>None</code>.</div>
    <div class="options">
      <div class="option"><label><input type="radio" name="q15" value="A"> True</label></div>
      <div class="option"><label><input type="radio" name="q15" value="B"> False</label></div>
    </div>
    <div class="answer" id="a15">✅ <strong>Answer:</strong> True — Every function returns a value; <code>None</code> is returned by default.</div>
  </div>

  <div class="exam-section">
    <h3>Section 3: Coding Exercises (Questions 16-20)</h3>

    <div class="question"><strong>16.</strong> Write a function that removes duplicates from a list while preserving order.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def remove_duplicates(lst):
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result</code></pre></div>

    <div class="question"><strong>17.</strong> Write a function that counts word frequency in a string.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from collections import Counter
def word_frequency(text):
    return Counter(text.lower().split())</code></pre></div>

    <div class="question"><strong>18.</strong> Write a function that merges two sorted lists into one sorted list.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def merge_sorted(list1, list2):
    result = []
    i = j = 0
    while i < len(list1) and j < len(list2):
        if list1[i] < list2[j]:
            result.append(list1[i])
            i += 1
        else:
            result.append(list2[j])
            j += 1
    result.extend(list1[i:])
    result.extend(list2[j:])
    return result</code></pre></div>

    <div class="question"><strong>19.</strong> Write a function that flattens a nested list (one level).</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>def flatten(nested):
    return [item for sublist in nested for item in sublist]</code></pre></div>

    <div class="question"><strong>20.</strong> Write a function that groups a list of dictionaries by a key.</div>
    <div class="answer">✅ <strong>Solution:</strong>
<pre><code>from collections import defaultdict
def group_by(lst, key):
    groups = defaultdict(list)
    for item in lst:
        groups[item[key]].append(item)
    return dict(groups)</code></pre></div>
  </div>

  <div class="exam-section">
    <h3>Section 4: Output Prediction (Questions 21-25)</h3>

    <div class="question"><strong>21.</strong> <code>print([1, 2] + [3, 4])</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1, 2, 3, 4]</code></div>

    <div class="question"><strong>22.</strong> <code>print(list(set([1, 2, 2, 3, 3, 3])))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1, 2, 3]</code> (order may vary)</div>

    <div class="question"><strong>23.</strong> <code>d = {'a': 1, 'b': 2}; print({v: k for k, v in d.items()})</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>{1: 'a', 2: 'b'}</code></div>

    <div class="question"><strong>24.</strong> <code>print({1, 2, 3} - {2, 3, 4})</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>{1}</code></div>

    <div class="question"><strong>25.</strong> <code>def f(a, b=[]): b.append(a); return b; print(f(1)); print(f(2))</code></div>
    <div class="answer">✅ <strong>Answer:</strong> <code>[1]</code> then <code>[1, 2]</code> — Default mutable arguments are shared across calls! (Beware of this pitfall.)</div>
  </div>
</div>

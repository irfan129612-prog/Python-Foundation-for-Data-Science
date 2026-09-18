# Lab 3: Looping Through Data

## Overview

This lab focuses on **loops in Python**, which are used to repeat tasks and process multiple values efficiently.

The lab covers:

* `for` loops
* `while` loops
* `break`
* `continue`
* List iteration
* Running totals
* User input inside loops
* Countdown timers
* Input validation
* Nested loops
* Basic loop testing and debugging

Several practical programs were developed, including a **sum calculator**, **countdown timer**, **data validation system**, and **multiplication table generator**.

---

## Objectives

By completing this lab, I learned how to:

* Iterate through lists using `for` loops
* Repeat tasks using `while` loops
* Calculate totals using loops
* Stop a loop using `break`
* Skip iterations using `continue`
* Validate repeated user input
* Build countdown timers
* Work with nested loops
* Avoid infinite loops
* Process collections efficiently

---

# 1. Basic `for` Loop

A `for` loop processes items one by one.

```python
numbers = [1, 2, 3, 4, 5]

for number in numbers:
    print(number)
```

### Flow

```text
List
 ↓
1
 ↓
2
 ↓
3
 ↓
4
 ↓
5
```

The loop automatically moves through every item in the list.

---

# 2. Sum Numbers Using a `for` Loop

```python
numbers = [10, 25, 30, 45, 50]

total_sum = 0

for number in numbers:
    total_sum = total_sum + number

print(f"Final sum: {total_sum}")
```

### How It Works

Initially:

```text
total_sum = 0
```

Then:

```text
0 + 10  = 10
10 + 25 = 35
35 + 30 = 65
65 + 45 = 110
110 + 50 = 160
```

Final result:

```text
160
```

---

# 3. Shortcut Assignment Operator

Instead of:

```python
total_sum = total_sum + number
```

Python allows:

```python
total_sum += number
```

Both perform the same operation.

---

# 4. Interactive Sum Calculator

A more practical version accepts numbers from the user.

```python
numbers = []

while True:

    user_input = input("Enter a number or 'done': ")

    if user_input.lower() == "done":
        break

    try:
        number = float(user_input)
        numbers.append(number)

    except ValueError:
        print("Please enter a valid number.")
```

### Workflow

```text
User enters number
       ↓
Convert to float
       ↓
Add to list
       ↓
Ask again
       ↓
User types "done"
       ↓
Stop loop
```

---

# 5. `.append()`

The `append()` method adds a new item to a list.

```python
numbers = []

numbers.append(10)
numbers.append(20)
```

Result:

```python
[10, 20]
```

This is useful when collecting data dynamically from users.

---

# 6. Basic `while` Loop

A `while` loop repeats code while a condition remains true.

```python
count = 5

while count > 0:

    print(count)

    count -= 1

print("Done!")
```

Output:

```text
5
4
3
2
1
Done!
```

### Important

```python
count -= 1
```

decreases the value after every iteration.

Without it, the loop could run forever.

---

# 7. `for` vs `while`

| Loop    | Best Used When              |
| ------- | --------------------------- |
| `for`   | Number of items is known    |
| `while` | Loop depends on a condition |

Example:

```python
for number in numbers:
```

Processes all values in a list.

While:

```python
while count > 0:
```

Runs until `count > 0` becomes false.

---

# 8. Countdown Timer

A practical countdown timer was created using a `while` loop.

```python
import time

seconds = 5

while seconds > 0:

    print(seconds)

    time.sleep(1)

    seconds -= 1

print("Time's up!")
```

### `time.sleep(1)`

```python
time.sleep(1)
```

pauses the program for **1 second**.

This allows the countdown to behave like a real timer.

---

# 9. Minutes and Seconds Conversion

The enhanced timer converts total seconds into minutes and seconds.

```python
minutes = seconds // 60

secs = seconds % 60
```

Example:

```text
125 seconds
```

Becomes:

```text
2 minutes
5 seconds
```

Because:

```text
125 // 60 = 2

125 % 60 = 5
```

---

# 10. Formatted Timer Output

```python
print(f"{minutes:02d}:{secs:02d}")
```

`:02d` displays numbers using two digits.

Example:

```text
2 minutes, 5 seconds
```

Displays as:

```text
02:05
```

---

# 11. `break`

The `break` statement immediately stops a loop.

```python
numbers = [1, 3, 7, 12, 8, 15]

target = 12

for number in numbers:

    if number == target:

        print("Target found!")

        break
```

### Flow

```text
1 → check
3 → check
7 → check
12 → FOUND
      ↓
    BREAK
      ↓
Loop stops
```

Real-world uses:

* Searching data
* Exit commands
* Login attempt limits
* Menu systems

---

# 12. `continue`

The `continue` statement skips the current iteration and moves to the next one.

```python
numbers = [1, 2, 3, 4, 5, 6]

for number in numbers:

    if number % 2 != 0:
        continue

    print(number)
```

Output:

```text
2
4
6
```

Odd numbers are skipped.

---

# 13. Even Number Detection

```python
number % 2
```

checks the remainder after division by 2.

For even numbers:

```python
number % 2 == 0
```

For odd numbers:

```python
number % 2 != 0
```

Example:

```text
6 % 2 = 0 → Even

7 % 2 = 1 → Odd
```

---

# 14. Difference Between `break` and `continue`

### `break`

Stops the complete loop.

```text
Loop
 ↓
Condition
 ↓
break
 ↓
STOP
```

### `continue`

Only skips the current iteration.

```text
Loop
 ↓
Condition
 ↓
continue
 ↓
Next iteration
```

---

# 15. Data Validation System

A practical validation system combines:

* `while`
* `break`
* `continue`
* `try-except`
* Lists
* Statistics

Example:

```python
valid_numbers = []

while True:

    user_input = input("Enter number or 'quit': ")

    if user_input.lower() == "quit":
        break

    try:

        number = float(user_input)

        if number < 1 or number > 100:
            print("Number outside range.")
            continue

        valid_numbers.append(number)

    except ValueError:

        print("Invalid input.")
```

### Program Logic

```text
Input
 ↓
quit?
 ↓
No
 ↓
Convert to number
 ↓
Valid range?
 ↓
Yes
 ↓
Add to list
```

---

# 16. List Statistics

The validation program calculates useful statistics.

### Count

```python
len(valid_numbers)
```

### Sum

```python
sum(valid_numbers)
```

### Average

```python
sum(valid_numbers) / len(valid_numbers)
```

### Minimum

```python
min(valid_numbers)
```

### Maximum

```python
max(valid_numbers)
```

These functions are commonly used when working with numerical datasets.

---

# 17. Nested Loops

A nested loop means one loop inside another.

```python
for table in range(1, 6):

    for multiplier in range(1, 11):

        result = table * multiplier

        print(f"{table} × {multiplier} = {result}")
```

### Concept

```text
Table 1
   ↓
1 × 1
1 × 2
1 × 3
...

Table 2
   ↓
2 × 1
2 × 2
2 × 3
...
```

Nested loops are useful for:

* Multiplication tables
* Matrix processing
* Grid-based data
* Comparing datasets

---

# 18. `range()`

`range()` generates a sequence of numbers.

```python
range(1, 6)
```

Produces:

```text
1, 2, 3, 4, 5
```

The ending value `6` is not included.

Example:

```python
for number in range(1, 6):
    print(number)
```

---

# 19. Testing Loop Logic

The lab also tests whether loops produce expected results.

Example:

```python
numbers = [5, 10, 15, 20, 25]

total = 0

for number in numbers:
    total += number

expected = 75

if total == expected:
    print("Test PASSED")
else:
    print("Test FAILED")
```

This introduces the idea of checking whether program logic produces the expected output.

---

# 20. `enumerate()`

The testing section also uses:

```python
for i, num in enumerate(numbers):
```

`enumerate()` provides both:

```text
Index
+
Value
```

Example:

```python
numbers = [10, 20, 30]

for i, number in enumerate(numbers):
    print(i, number)
```

Output:

```text
0 10
1 20
2 30
```

---

# 21. Infinite Loops

An infinite loop happens when the loop condition never becomes false.

Wrong:

```python
count = 5

while count > 0:
    print(count)
```

`count` never changes.

Correct:

```python
count = 5

while count > 0:

    print(count)

    count -= 1
```

Now:

```text
5 → 4 → 3 → 2 → 1 → 0
```

At `0`, the condition becomes false and the loop stops.

---

# 22. Safe List Iteration

Risky approach:

```python
numbers = [1, 2, 3]

for i in range(10):
    print(numbers[i])
```

This can cause an `IndexError`.

Safer approach:

```python
for number in numbers:
    print(number)
```

This automatically processes only existing list elements.

---

# Main Lab Flow

```text
Data Collection
      ↓
Lists
      ↓
For Loop
      ↓
While Loop
      ↓
Break / Continue
      ↓
Validation
      ↓
Nested Loops
      ↓
Data Processing
      ↓
Final Results
```

---

# Practical Applications Built

During this lab, I worked on:

### Sum Calculator

Calculates the total and average of user-entered numbers.

### Countdown Timer

Uses a `while` loop and time delays to create a functional timer.

### Number Search

Uses `break` to stop searching once the required value is found.

### Even Number Processor

Uses `continue` to ignore unwanted values.

### Data Validation System

Validates user input and calculates basic statistics.

### Multiplication Table Generator

Uses nested loops to generate multiple multiplication tables.

---

# Real-World Applications of Loops

Loops are commonly used in:

* Data analysis
* File processing
* Automation
* Web scraping
* Database records
* Machine learning datasets
* User input systems
* Report generation
* Search algorithms
* Repetitive administrative tasks

---

# Key Concepts Learned

```text
for
    → Process items one by one

while
    → Repeat while condition is true

break
    → Stop loop completely

continue
    → Skip current iteration

range()
    → Generate number sequences

append()
    → Add item to list

len()
    → Count items

sum()
    → Calculate total

min()
    → Find smallest value

max()
    → Find largest value
```

---

# Technologies Used

* Python 3
* PyCharm
* Python Standard Library
* `time` module

---

# Learning Outcome

After completing this lab, I gained a practical understanding of how loops can automate repetitive operations and process collections of data efficiently.

The overall workflow practiced in this lab was:

```text
Collect Data
     ↓
Loop Through Data
     ↓
Check Conditions
     ↓
Process Values
     ↓
Skip / Stop When Required
     ↓
Calculate Results
     ↓
Display Output
```

These concepts are especially important for future work in **Python automation, data analysis, data science, and software development**.

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

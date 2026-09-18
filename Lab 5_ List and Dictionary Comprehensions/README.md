# Lab 5: List and Dictionary Comprehensions

## Overview

This lab focuses on **List and Dictionary Comprehensions in Python**.

Comprehensions provide a shorter and cleaner way to create, filter, and transform lists and dictionaries compared with traditional loops.

The main goal of this lab was to understand how repetitive data-processing tasks can be written in a concise and readable form.

---

## Objectives

By completing this lab, I learned how to:

* Create lists using list comprehensions
* Filter data using conditions
* Transform values while creating new lists
* Combine filtering and transformation
* Create dictionaries using dictionary comprehensions
* Combine multiple lists using `zip()`
* Use `enumerate()` to work with indexes
* Apply `if`, `and`, and `or` inside comprehensions
* Work with nested dictionaries
* Use comprehensions for practical data-processing tasks

---

# 1. Traditional Loop vs List Comprehension

A traditional loop may look like this:

```python
numbers = [1, 2, 3, 4, 5]

squares = []

for number in numbers:
    squares.append(number ** 2)

print(squares)
```

The same result can be achieved using list comprehension:

```python
numbers = [1, 2, 3, 4, 5]

squares = [number ** 2 for number in numbers]

print(squares)
```

Output:

```text
[1, 4, 9, 16, 25]
```

List comprehensions make simple loops shorter and easier to read.

---

# 2. Basic List Comprehension

Basic syntax:

```python
[new_value for item in collection]
```

Example:

```python
numbers = [1, 2, 3, 4]

doubled = [x * 2 for x in numbers]

print(doubled)
```

Output:

```text
[2, 4, 6, 8]
```

---

# 3. Filtering Data

Conditions can be added to a comprehension.

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [
    number
    for number in numbers
    if number % 2 == 0
]

print(even_numbers)
```

Output:

```text
[2, 4, 6]
```

The condition:

```python
number % 2 == 0
```

selects only even numbers.

---

# 4. Filter and Transform Together

Filtering and transformation can be combined.

```python
numbers = [1, 2, 3, 4, 5, 6]

result = [
    number ** 2
    for number in numbers
    if number % 2 == 0
]

print(result)
```

Output:

```text
[4, 16, 36]
```

Here the program:

```text
Filters even numbers
        ↓
Squares the selected values
        ↓
Creates a new list
```

---

# 5. Conditional Expressions

An `if-else` expression can also be used inside a comprehension.

```python
numbers = [1, 2, 3, 4]

types = [
    "Even" if number % 2 == 0 else "Odd"
    for number in numbers
]

print(types)
```

Output:

```text
['Odd', 'Even', 'Odd', 'Even']
```

Unlike filtering, this keeps every item but assigns a different result based on a condition.

---

# 6. Multiple Conditions

More than one condition can be applied.

```python
numbers = range(1, 30)

result = [
    number
    for number in numbers
    if number % 2 == 0 and number > 10
]
```

This returns numbers that are:

```text
Even
AND
Greater than 10
```

---

# 7. Dictionary Comprehension

Dictionary comprehensions create dictionaries using concise syntax.

Basic structure:

```python
{key: value for item in collection}
```

Example:

```python
numbers = [1, 2, 3, 4]

squared_dict = {
    number: number ** 2
    for number in numbers
}

print(squared_dict)
```

Output:

```python
{
    1: 1,
    2: 4,
    3: 9,
    4: 16
}
```

---

# 8. Creating Dictionaries from Two Lists

The `zip()` function combines values from two lists.

```python
names = ["Ali", "Sara", "Ahmed"]

ages = [20, 22, 25]

people = {
    name: age
    for name, age in zip(names, ages)
}

print(people)
```

Output:

```python
{
    "Ali": 20,
    "Sara": 22,
    "Ahmed": 25
}
```

The lab uses this technique to build dictionaries from separate data sources.

---

# 9. Filtering Dictionary Data

Conditions can also be used with dictionary comprehensions.

```python
scores = {
    "Ali": 80,
    "Sara": 45,
    "Ahmed": 90
}

passed_students = {
    name: score
    for name, score in scores.items()
    if score >= 60
}
```

Result:

```python
{
    "Ali": 80,
    "Ahmed": 90
}
```

---

# 10. Using `.items()`

The `.items()` method provides both dictionary keys and values.

```python
student = {
    "name": "Ali",
    "age": 20
}

for key, value in student.items():
    print(key, value)
```

Output:

```text
name Ali
age 20
```

This is useful when processing dictionary data.

---

# 11. Using `enumerate()`

`enumerate()` provides both:

```text
Index
+
Value
```

Example:

```python
fruits = ["apple", "banana", "mango"]

fruit_positions = {
    fruit: index
    for index, fruit in enumerate(fruits)
}
```

Result:

```python
{
    "apple": 0,
    "banana": 1,
    "mango": 2
}
```

The lab also uses `enumerate()` to create indexed dictionary structures.

---

# 12. Nested Dictionaries

Comprehensions can also be used to create nested data structures.

```python
students = ["Ali", "Sara"]

student_data = {
    student: {
        "Math": 80,
        "English": 75
    }
    for student in students
}
```

This produces:

```python
{
    "Ali": {
        "Math": 80,
        "English": 75
    },
    "Sara": {
        "Math": 80,
        "English": 75
    }
}
```

Nested structures are common in real-world datasets.

---

# 13. Data Cleaning Example

Comprehensions are useful for cleaning data.

```python
names = [
    " Ali ",
    " Sara ",
    " Ahmed "
]

clean_names = [
    name.strip()
    for name in names
]

print(clean_names)
```

Output:

```text
['Ali', 'Sara', 'Ahmed']
```

---

# 14. Data Filtering Example

```python
ages = [15, 18, 22, 14, 35, 40]

adults = [
    age
    for age in ages
    if age >= 18
]
```

Result:

```text
[18, 22, 35, 40]
```

This type of filtering is common in data analysis.

---

# 15. Transformation Example

```python
prices = [100, 200, 300]

updated_prices = [
    price * 1.10
    for price in prices
]
```

This can be used to apply calculations to every value in a dataset.

---

# Main Comprehension Patterns

## Simple Transformation

```python
[x * 2 for x in numbers]
```

Meaning:

```text
Process every item
```

---

## Filtering

```python
[x for x in numbers if x > 10]
```

Meaning:

```text
Keep only matching items
```

---

## Filter + Transform

```python
[x ** 2 for x in numbers if x % 2 == 0]
```

Meaning:

```text
Filter
  ↓
Transform
```

---

## Conditional Expression

```python
["Even" if x % 2 == 0 else "Odd" for x in numbers]
```

Meaning:

```text
Keep every item
but classify it
```

---

## Dictionary Comprehension

```python
{x: x ** 2 for x in numbers}
```

Meaning:

```text
Create key-value pairs
```

---

# Traditional Loop vs Comprehension

Traditional approach:

```python
result = []

for x in numbers:

    if x > 10:
        result.append(x * 2)
```

Comprehension:

```python
result = [
    x * 2
    for x in numbers
    if x > 10
]
```

Both perform the same task.

The comprehension version is shorter and often easier to use for simple data-processing operations.

---

# Practical Applications

List and dictionary comprehensions can be used for:

* Data filtering
* Data cleaning
* Data transformation
* Extracting values from datasets
* Creating lookup dictionaries
* Processing student records
* Sales data analysis
* Inventory filtering
* Preparing data for analysis
* Automation scripts

---

# Main Concepts Learned

```text
List Comprehension
        ↓
Create lists quickly

Filtering
        ↓
Select required data

Transformation
        ↓
Modify every value

Conditional Expression
        ↓
Classify values

Dictionary Comprehension
        ↓
Create key-value structures

zip()
        ↓
Combine multiple lists

enumerate()
        ↓
Get index + value

.items()
        ↓
Get dictionary key + value
```

---

# Technologies Used

* Python 3
* PyCharm
* Python Lists
* Python Dictionaries
* Built-in Python functions

---

# Learning Outcome

After completing this lab, I learned how to write cleaner and more concise Python code for filtering and transforming data.

The main workflow practiced was:

```text
Original Data
      ↓
Loop Through Data
      ↓
Apply Condition
      ↓
Transform Values
      ↓
Create New List / Dictionary
```

These concepts are especially useful for future work in:

* Data Analysis
* Data Science
* Automation
* Data Cleaning
* API Data Processing

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

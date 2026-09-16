# Python Syntax and Data Types Lab

## Overview

This lab introduces the fundamental concepts of Python programming, including variables, data types, user input, type conversion, arithmetic operations, string operations, conditional statements, and basic error handling.

The lab also includes practical programs such as an interactive calculator and a student grade calculator to demonstrate how these concepts are applied in real-world applications.

---

## Objectives

By completing this lab, I learned how to:

* Create and use Python variables
* Work with basic Python data types
* Identify variable types using `type()`
* Collect user input using `input()`
* Convert data between different types
* Perform arithmetic operations
* Perform basic string operations
* Format output using f-strings
* Use conditional statements for decision-making
* Create a weighted student grade calculator
* Handle invalid user input using `try-except`

---

## Python Data Types Covered

| Data Type | Description     | Example         |
| --------- | --------------- | --------------- |
| `int`     | Whole numbers   | `25`            |
| `float`   | Decimal numbers | `3.75`          |
| `str`     | Text data       | `"Python"`      |
| `bool`    | Logical values  | `True`, `False` |

---

## Lab Files

### `variables_demo.py`

Demonstrates:

* Variables
* Integer values
* Float values
* Strings
* Boolean values
* `type()` function

Example:

```python
student_age = 20
student_gpa = 3.75
student_name = "Alice Johnson"
is_enrolled = True

print(type(student_age))
print(type(student_gpa))
print(type(student_name))
print(type(is_enrolled))
```

---

### `variable_naming.py`

Explores Python variable naming conventions and assignment techniques.

Topics include:

* Valid variable names
* Snake case naming
* Multiple assignment
* Assigning the same value to multiple variables

Example:

```python
first_name = "John"
age_in_years = 25

x, y, z = 10, 20.5, "Hello"

a = b = c = 100
```

---

### `user_input_demo.py`

Demonstrates how Python collects information from users using the `input()` function.

```python
user_name = input("Please enter your name: ")

print("Hello,", user_name)
```

An important concept demonstrated in this exercise is that `input()` returns data as a string.

---

### `advanced_input.py`

Implements a simple student registration-style program.

The program collects:

* Student name
* Student ID
* Email address
* Course selection
* Semester
* Full-time status

This demonstrates how interactive applications collect multiple pieces of information from users.

---

### `type_conversion.py`

Demonstrates converting values between Python data types.

Examples:

```python
age = int("25")

price = float("19.99")

score = str(95)

gpa = int(3.87)
```

Conversions covered:

```text
str → int
str → float
int → str
float → int
bool → int
number → bool
```

---

### `interactive_calculator.py`

A simple interactive calculator that collects two numbers from the user and performs mathematical operations.

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

addition = num1 + num2
subtraction = num1 - num2
multiplication = num1 * num2
division = num1 / num2
```

This program demonstrates an important programming workflow:

```text
User Input
    ↓
Type Conversion
    ↓
Processing
    ↓
Output
```

---

### `operations_demo.py`

Demonstrates Python arithmetic and string operations.

Arithmetic operators covered:

```text
+   Addition
-   Subtraction
*   Multiplication
/   Division
//  Floor Division
%   Modulus
**  Exponentiation
```

String operations include:

* Concatenation
* Repetition
* String length using `len()`

---

### `grade_calculator.py`

A practical student grade calculator that combines multiple concepts from the lab.

The program:

1. Collects student information
2. Accepts assessment scores
3. Converts input into numeric values
4. Calculates quiz averages
5. Calculates a weighted final score
6. Assigns a letter grade
7. Determines pass/fail status
8. Displays a formatted grade report

Example weighted calculation:

```python
quiz_average = (quiz1 + quiz2) / 2

weighted_score = (
    quiz_average * 0.20
    + midterm * 0.25
    + final * 0.35
    + project * 0.20
)
```

Grade decision:

```python
if weighted_score >= 90:
    letter_grade = "A"
elif weighted_score >= 80:
    letter_grade = "B"
elif weighted_score >= 70:
    letter_grade = "C"
elif weighted_score >= 60:
    letter_grade = "D"
else:
    letter_grade = "F"
```

---

### `error_examples.py`

Introduces basic Python error handling using `try-except`.

Example:

```python
user_input = input("Enter a number: ")

try:
    number = int(user_input)
    print("Conversion successful")

except ValueError:
    print("Please enter a valid whole number.")
```

This prevents the application from immediately crashing when invalid data is entered.

---

## Key Concepts Learned

### Variables

Variables store information that can be used throughout a program.

```python
student_name = "Irfan"
```

### Type Checking

```python
type(student_name)
```

### User Input

```python
name = input("Enter your name: ")
```

### Type Conversion

```python
age = int(input("Enter your age: "))
```

### Formatted Output

```python
print(f"Student Name: {student_name}")
```

### Conditional Logic

```python
if score >= 60:
    print("Pass")
else:
    print("Fail")
```

### Error Handling

```python
try:
    number = int(user_input)
except ValueError:
    print("Invalid input")
```

---

## Real-World Applications

The concepts practiced in this lab are fundamental to building applications such as:

* Student management systems
* Registration systems
* Interactive calculators
* Data entry applications
* E-commerce systems
* Automation scripts
* Data analysis programs
* Web applications

---

## Technologies Used

* Python 3
* PyCharm
* Python Standard Library

---

## Learning Outcome

After completing this lab, I gained a strong understanding of how Python receives, stores, converts, processes, and validates data.

The overall programming workflow demonstrated in this lab is:

```text
Input
  ↓
Store
  ↓
Convert
  ↓
Process
  ↓
Decision
  ↓
Output
```

These concepts provide the foundation for more advanced Python topics including data structures, functions, file handling, automation, and data science.

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

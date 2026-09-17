# Lab 2: Control Flow in Python

## Overview

This lab focuses on **Control Flow in Python**, which allows programs to make decisions based on different conditions.

In this lab, I practiced:

* `if`
* `if-else`
* `if-elif-else`
* Comparison operators
* Logical operators
* Nested conditions
* Input validation
* Error handling
* Debugging common control flow mistakes

A practical **Temperature Categorization Program** was also developed to apply these concepts in a real-world scenario.

---

## Objectives

By completing this lab, I learned how to:

* Use conditional statements in Python
* Compare values using comparison operators
* Combine multiple conditions using logical operators
* Build multi-level decision systems
* Use nested `if` statements
* Validate user input
* Handle invalid inputs
* Debug common conditional logic errors
* Build a practical weather categorization program

---

# 1. Simple `if` Statement

The `if` statement executes code only when a condition is true.

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("You are an adult!")

print("Program finished.")
```

### Concept

```text
Condition True
     ↓
Execute Code
```

---

# 2. `if-else` Statement

`if-else` handles both true and false conditions.

```python
score = int(input("Enter your test score: "))

if score >= 60:
    print("Congratulations! You passed.")
else:
    print("Sorry, you did not pass.")
```

### Logic

```text
Score >= 60?
      |
   ┌──┴──┐
 True   False
  |       |
Pass     Fail
```

---

# 3. `if-elif-else`

Used when a program has multiple possible conditions.

```python
score = int(input("Enter your test score: "))

if score >= 90:
    grade = "A"

elif score >= 80:
    grade = "B"

elif score >= 70:
    grade = "C"

elif score >= 60:
    grade = "D"

else:
    grade = "F"

print(f"Grade: {grade}")
```

This type of logic is commonly used in:

* Grading systems
* Performance evaluation
* Pricing systems
* User access levels

---

# 4. Comparison Operators

Comparison operators are used to compare values.

| Operator | Meaning                  |
| -------- | ------------------------ |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |
| `==`     | Equal to                 |
| `!=`     | Not equal to             |

Example:

```python
age >= 18
```

---

# 5. Logical Operator — `and`

The `and` operator requires **all conditions to be true**.

```python
username = input("Enter username: ")
password = input("Enter password: ")
age = int(input("Enter your age: "))

if username == "student" and password == "python123" and age >= 13:
    print("Access granted!")
else:
    print("Access denied!")
```

### Logic

```text
Username Correct
       AND
Password Correct
       AND
Age >= 13
       ↓
Access Granted
```

---

# 6. Logical Operator — `or`

The `or` operator requires **at least one condition to be true**.

```python
day = input("What day is it? ").lower()

if day == "saturday" or day == "sunday":
    print("It's the weekend!")
else:
    print("It's a weekday.")
```

Real-world uses include:

* Weekend detection
* Multiple access conditions
* Range validation

---

# 7. Logical Operator — `not`

The `not` operator reverses a condition.

```python
is_raining = input("Is it raining? (yes/no): ").lower()

if not is_raining == "yes":
    print("You can go outside.")
else:
    print("Take an umbrella.")
```

A simpler equivalent:

```python
if is_raining != "yes":
    print("You can go outside.")
```

---

# 8. Using `.lower()`

The `.lower()` method converts text into lowercase.

```python
day = input("Enter day: ").lower()
```

Example:

```text
SUNDAY
Sunday
sunday
```

All become:

```text
sunday
```

This makes user input easier to compare.

---

# 9. Temperature Categorization Program

A practical temperature classification program was created.

```python
temperature = float(input("Enter temperature in Fahrenheit: "))

if temperature >= 80:
    category = "hot"

elif temperature <= 50:
    category = "cold"

else:
    category = "mild"

print(f"Temperature category: {category.upper()}")
```

### Classification Logic

```text
80°F or above
      ↓
     HOT

50°F or below
      ↓
     COLD

Between 50°F and 80°F
      ↓
     MILD
```

---

# 10. Nested `if` Statements

Nested conditions mean placing an `if` statement inside another `if`.

```python
if temperature >= 80:

    print("Hot weather")

    if humidity > 70:
        print("High humidity makes it feel hotter.")
```

This allows more detailed decision-making.

### Example

```text
Temperature is Hot?
        ↓
       Yes
        ↓
Humidity > 70?
        ↓
       Yes
        ↓
Very Uncomfortable
```

---

# 11. Combining Multiple Conditions

Multiple conditions can be combined using logical operators.

```python
if is_sunny == "yes" and temperature > 90:
    print("Stay hydrated!")
```

Another example:

```python
if temperature > 85 and humidity > 70:
    print("Stay indoors and drink water.")
```

---

# 12. Input Validation

Input validation prevents incorrect user input from crashing the program.

```python
def get_valid_temperature():

    while True:

        try:
            temp = float(input("Enter temperature: "))
            return temp

        except ValueError:
            print("Please enter a valid number.")
```

### Workflow

```text
User Input
   ↓
Try Conversion
   ↓
Valid?
 ┌───────┐
Yes      No
 |        |
Return   Error Message
          |
       Try Again
```

---

# 13. `while True`

```python
while True:
```

Creates a loop that keeps running until valid input is received or the loop is stopped manually.

It is useful for:

* Input validation
* Login systems
* Menu-driven programs
* Repeated user interaction

---

# 14. `continue`

The `continue` statement skips the current loop iteration and starts again.

```python
if temp < -100 or temp > 150:
    print("Enter a realistic temperature.")
    continue
```

If the user enters an invalid value, the program asks again.

---

# 15. `return`

`return` sends a value back from a function.

```python
return temp
```

Example:

```python
temperature = get_valid_temperature()
```

The validated temperature is returned and stored in `temperature`.

---

# 16. Yes/No Input Validation

```python
def get_yes_no_input(prompt):

    while True:

        response = input(prompt).lower().strip()

        if response in ['yes', 'y', 'no', 'n']:
            return response in ['yes', 'y']

        print("Please enter 'yes' or 'no'")
```

Concepts used:

* `.lower()`
* `.strip()`
* `in`
* `while`
* `return`

---

# 17. Using `in`

The `in` operator checks whether a value exists inside a collection.

```python
response in ['yes', 'y', 'no', 'n']
```

Example:

```text
response = "yes"
```

Result:

```text
True
```

---

# 18. Range Checking

Python allows clean range comparisons.

```python
if 65 <= temperature <= 75:
    print("Comfortable temperature")
```

This means:

```text
temperature >= 65
AND
temperature <= 75
```

---

# 19. Debugging Common Errors

## Wrong Data Type

Wrong:

```python
temperature = input("Enter temperature: ")

if temperature > 80:
    print("Hot")
```

Correct:

```python
temperature = float(input("Enter temperature: "))
```

---

## Missing Colon

Wrong:

```python
if temperature > 80
```

Correct:

```python
if temperature > 80:
```

---

## Wrong Indentation

Wrong:

```python
if temperature > 80:
print("Hot")
```

Correct:

```python
if temperature > 80:
    print("Hot")
```

---

## Using `=` Instead of `==`

Wrong:

```python
if temperature = 80:
```

Correct:

```python
if temperature == 80:
```

`=` assigns a value.

`==` compares two values.

---

# 20. Unreachable Conditions

Incorrect logic:

```python
if temperature > 100:
    print("Extremely hot")

elif temperature > 90:
    print("Very hot")

elif temperature > 100:
    print("Hot")
```

The last condition will never execute because values above `100` are already handled by the first condition.

Correct ordering and logical structure are important in conditional programming.

---

# Main Program Flow

```text
User Input
     ↓
Type Conversion
     ↓
Condition Checking
     ↓
if / elif / else
     ↓
Logical Operators
     ↓
Nested Decisions
     ↓
Validation
     ↓
Final Output
```

---

# Real-World Applications

The concepts in this lab can be used in:

* Login and authentication systems
* Student grading systems
* Weather applications
* Banking applications
* E-commerce websites
* User eligibility checks
* Data validation systems
* Recommendation systems
* Automation scripts
* Data analysis workflows

---

# Key Concepts Learned

```text
if
    → Run code when condition is True

if-else
    → Handle True and False conditions

if-elif-else
    → Handle multiple conditions

and
    → All conditions must be True

or
    → At least one condition must be True

not
    → Reverse the condition

Nested if
    → Decision inside another decision

try-except
    → Handle invalid input

while
    → Repeat code

continue
    → Skip and retry

return
    → Return a value from a function
```

---

# Technologies Used

* Python 3
* PyCharm
* Python Standard Library

---

# Learning Outcome

After completing this lab, I gained a better understanding of how Python programs make decisions based on user input and changing conditions.

I also learned how multiple conditions can be combined to create more intelligent and interactive programs.

The main programming pattern practiced in this lab was:

```text
Input
  ↓
Evaluate
  ↓
Decision
  ↓
Action
  ↓
Output
```

This provides a strong foundation for future Python topics such as loops, functions, data structures, automation, and data science.

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

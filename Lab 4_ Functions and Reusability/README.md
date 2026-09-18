# Lab 4: Functions and Reusability

## Overview

This lab focuses on **functions in Python** and how they help create reusable, organized, and maintainable code.

Instead of repeating the same code multiple times, functions allow a task to be written once and reused whenever needed.

The lab uses a **temperature conversion system** to demonstrate function concepts such as parameters, return values, multiple return values, input validation, loops, and reusable program structure.

---

## Objectives

By completing this lab, I learned how to:

* Create custom functions using `def`
* Pass values to functions using parameters
* Return results using `return`
* Return multiple values from a function
* Use functions inside loops
* Apply the DRY principle
* Validate function inputs
* Handle invalid data using `try-except`
* Organize programs into smaller reusable components
* Use basic logging and file output

---

# 1. Creating a Basic Function

A function is created using the `def` keyword.

```python id="35ap4y"
def greet_user():
    print("Welcome to Python!")
```

The function is executed by calling it:

```python id="ifv9j8"
greet_user()
```

### Concept

```text id="7p8yen"
Define Function
      ↓
Call Function
      ↓
Execute Code
```

Functions help prevent repeated code.

---

# 2. Function Parameters

Parameters allow data to be passed into a function.

```python id="t9lci8"
def celsius_to_fahrenheit(celsius):
    fahrenheit = (celsius * 9/5) + 32
    return fahrenheit
```

Here:

```text id="p8k6ta"
celsius = parameter
```

Function call:

```python id="etqh2v"
result = celsius_to_fahrenheit(25)
```

Here:

```text id="oxax4e"
25 = argument
```

---

# 3. Returning Values

The `return` statement sends the calculated result back from the function.

```python id="7nnoxq"
def add(a, b):
    result = a + b
    return result
```

Usage:

```python id="01g0v1"
answer = add(10, 5)

print(answer)
```

Output:

```text id="7ofvpt"
15
```

The lab uses this same concept in temperature conversion functions.

---

# 4. Multiple Parameters

A function can accept more than one input.

```python id="aoz50g"
def universal_temperature_converter(
    temperature,
    from_scale,
    to_scale
):
```

The three parameters represent:

```text id="c2q1rp"
temperature
from_scale
to_scale
```

Example:

```python id="78we0s"
universal_temperature_converter(32, "F", "C")
```

This means:

```text id="0j51mu"
Convert 32°F to Celsius
```

---

# 5. Multiple Return Values

Python functions can return more than one value.

```python id="0wacms"
def calculate(a, b):

    addition = a + b
    subtraction = a - b

    return addition, subtraction
```

Usage:

```python id="snc9nd"
add, subtract = calculate(10, 5)
```

Results:

```text id="859nl4"
add = 15
subtract = 5
```

The lab also returns multiple temperature conversions and status messages from functions.

---

# 6. Universal Temperature Converter

The main converter can work with:

* Celsius
* Fahrenheit
* Kelvin

Basic workflow:

```text id="9t0muq"
Input Temperature
      ↓
Convert to Celsius
      ↓
Validate Value
      ↓
Convert to Target Scale
      ↓
Return Result
```

Example logic:

```python id="dunswd"
if from_scale == "C":
    celsius = temperature

elif from_scale == "F":
    celsius = (temperature - 32) * 5/9

elif from_scale == "K":
    celsius = temperature - 273.15
```

Then Celsius is converted to the required target scale.

---

# 7. Input Validation

The lab validates user input before performing calculations.

```python id="g6tr7l"
try:
    temperature = float(temperature)

except ValueError:
    return None, "Invalid temperature value"
```

### Why?

If the user enters:

```text id="hpca5y"
hello
```

instead of a number, the program does not crash.

It returns an error message instead.

---

# 8. Using `None`

`None` represents the absence of a valid result.

Example:

```python id="y5e7d2"
return None, "Invalid temperature"
```

The program can check:

```python id="ywqbbm"
if result is not None:
    print(result)
else:
    print("Conversion failed")
```

---

# 9. String Methods

The lab uses:

```python id="f7fdcr"
from_scale = from_scale.upper()
to_scale = to_scale.upper()
```

This converts:

```text id="lmg74l"
c → C
f → F
k → K
```

Another useful method is:

```python id="z93lck"
.strip()
```

which removes extra spaces from user input.

---

# 10. Functions with Conditional Logic

Functions can contain `if`, `elif`, and `else`.

```python id="22tvip"
def check_score(score):

    if score >= 80:
        return "A"

    elif score >= 60:
        return "B"

    else:
        return "Fail"
```

This combines Lab 2 control flow with reusable functions.

---

# 11. Functions Inside Loops

A function can be applied repeatedly to multiple values.

```python id="yypw9k"
temperatures = [0, 25, 50, 100]

for temp in temperatures:

    result = celsius_to_fahrenheit(temp)

    print(result)
```

This is useful for **batch processing**.

The lab uses functions inside loops to process temperature lists efficiently.

---

# 12. Lists and `.append()`

The lab stores processed results inside lists.

```python id="752yg2"
results = []

results.append(10)
results.append(20)
```

Result:

```python id="2ig1hz"
[10, 20]
```

This allows multiple converted values to be collected for later use.

---

# 13. `while True`

Interactive programs use:

```python id="h47pyq"
while True:
```

This keeps the program running until the user chooses to exit.

Example:

```python id="bczh8z"
while True:

    choice = input("Enter command: ")

    if choice == "exit":
        break
```

This is useful for menu-driven applications.

---

# 14. Lambda Functions

The lab also introduces small anonymous functions using `lambda`.

```python id="cf67z0"
square = lambda x: x ** 2
```

Usage:

```python id="yqyx9m"
print(square(5))
```

Output:

```text id="xfss86"
25
```

In the lab, lambda functions are stored inside a dictionary to represent different conversion options.

---

# 15. File Logging

The lab also demonstrates saving conversion activity into a file.

```python id="v8dgxz"
with open("conversion_log.txt", "a") as file:

    file.write("Conversion completed\n")
```

`"a"` means **append mode**, which adds new information without deleting old content.

The lab uses this pattern to record temperature conversions.

---

# 16. `round()`

The `round()` function limits decimal places.

```python id="48ql2j"
value = 3.141592

print(round(value, 2))
```

Output:

```text id="s97qol"
3.14
```

The lab uses this to return cleaner temperature values.

---

# 17. Main Program Entry Point

The lab uses:

```python id="lw77kg"
if __name__ == "__main__":
    main_converter_loop()
```

This means:

> Run the main program only when this Python file is executed directly.

It helps organize larger Python programs properly.

---

# DRY Principle

DRY means:

```text id="sbcpdh"
Don't Repeat Yourself
```

Instead of repeating:

```python id="jhzqvl"
result1 = (25 * 9/5) + 32
result2 = (30 * 9/5) + 32
result3 = (40 * 9/5) + 32
```

Create one function:

```python id="yp4y5c"
def convert(celsius):
    return (celsius * 9/5) + 32
```

Then reuse it:

```python id="31t56d"
convert(25)
convert(30)
convert(40)
```

This makes code:

* Cleaner
* Shorter
* Easier to debug
* Easier to maintain

---

# Main Concepts Learned

```text id="zx6czn"
def
   → Create function

parameter
   → Input for function

argument
   → Actual value passed

return
   → Send result back

multiple return
   → Return multiple values

function call
   → Execute function

try / except
   → Handle invalid input

function + loop
   → Process many values

lambda
   → Small anonymous function

DRY
   → Avoid repeating code
```

---

# Practical Applications

Functions are used in almost every real-world Python project.

Examples include:

* Data cleaning
* Data analysis
* Temperature monitoring
* Automation scripts
* Input validation
* File processing
* API processing
* Calculators
* Business applications
* Scientific calculations

---

# Technologies Used

* Python 3
* PyCharm
* Python Standard Library
* `datetime`
* Basic file handling

---

# Learning Outcome

After completing this lab, I learned how to organize Python code into reusable functions instead of writing repetitive code.

The main workflow practiced was:

```text id="jrqdb6"
Input
  ↓
Pass to Function
  ↓
Process Data
  ↓
Validate
  ↓
Return Result
  ↓
Reuse Function
```

Functions are an important foundation for **data science, automation, APIs, file processing, and larger Python applications**.

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

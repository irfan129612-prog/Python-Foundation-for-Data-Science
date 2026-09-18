# Lab 8: Exception Handling and Logging

## Overview

This lab focuses on **Exception Handling and Logging in Python**.

Real-world applications can face many problems such as:

* Missing files
* Invalid user input
* Permission errors
* Invalid JSON data
* Unexpected runtime errors

Instead of allowing the program to crash, Python provides exception handling tools that allow errors to be detected and handled properly.

The lab also introduces **logging**, which records important program events, warnings, and errors for debugging and monitoring.

---

## Objectives

By completing this lab, I learned how to:

* Handle runtime errors using `try` and `except`
* Handle specific exceptions
* Use `finally` for cleanup operations
* Work safely with files
* Handle invalid JSON data
* Validate data before processing
* Use Python's `logging` module
* Create log files
* Use different logging levels
* Build more reliable Python applications

---

# 1. What is an Exception?

An exception is an error that occurs while a program is running.

Example:

```python id="jtc8zm"
number = int("hello")
```

Python cannot convert:

```text id="283kwi"
"hello"
```

into an integer.

Therefore, it raises an error:

```text id="vxn85c"
ValueError
```

Without exception handling, the program may stop.

---

# 2. Basic `try-except`

The basic structure is:

```python id="60dvjk"
try:

    number = int(input("Enter a number: "))

except ValueError:

    print("Invalid number")
```

### Concept

```text id="4hrzj4"
try
 ↓
Run risky code
 ↓
Error?
 ↓
Yes → except handles it
No  → continue normally
```

---

# 3. Why Exception Handling Matters

Without exception handling:

```python id="0308gf"
file = open("missing.txt")
```

If the file does not exist:

```text id="a7cwdz"
Program crashes
```

With exception handling:

```python id="p8ea32"
try:

    file = open("missing.txt")

except FileNotFoundError:

    print("File not found")
```

Now the program handles the problem gracefully.

The lab uses this same approach for file operations.

---

# 4. Handling Specific Exceptions

Different problems produce different exception types.

## `FileNotFoundError`

File does not exist.

```python id="1ivur5"
except FileNotFoundError:
    print("File not found")
```

---

## `PermissionError`

Program does not have permission to access a file.

```python id="m30h78"
except PermissionError:
    print("Permission denied")
```

---

## `ValueError`

A value cannot be converted or processed correctly.

```python id="mvdvmm"
except ValueError:
    print("Invalid value")
```

---

## `UnicodeDecodeError`

Python cannot correctly decode file contents.

```python id="1r5ymn"
except UnicodeDecodeError:
    print("Unable to decode file")
```

The lab demonstrates several specific file-related exceptions instead of using only one generic error handler.

---

# 5. Catching Unexpected Errors

A general exception handler can catch other unexpected problems.

```python id="t1siyn"
try:
    # risky code

except Exception as e:
    print("Unexpected error:", e)
```

Here:

```text id="cc7795"
e
```

contains information about the error.

Example:

```python id="mfk88a"
except Exception as e:
    print(type(e).__name__)
    print(e)
```

This can help during debugging.

---

# 6. `finally`

The `finally` block always executes.

```python id="hxd8te"
try:

    file = open("data.txt")

except FileNotFoundError:

    print("File not found")

finally:

    print("Operation completed")
```

Even if an error occurs:

```text id="34gwsg"
finally
```

will still execute.

Typical use:

```text id="6pstuu"
Close file
Release resource
Cleanup
```

The lab uses `finally` to ensure file resources are properly cleaned up.

---

# 7. Using `with open()` for Safer File Handling

A better way to handle files is:

```python id="qohjtw"
with open("data.txt", "r") as file:

    content = file.read()
```

`with open()` automatically closes the file.

Combined with exception handling:

```python id="s6jkct"
try:

    with open("data.txt", "r") as file:

        content = file.read()

except FileNotFoundError:

    print("File not found")
```

The lab uses context managers to improve file safety and cleanup.

---

# 8. JSON Exception Handling

JSON files can contain invalid syntax.

Example:

```json id="7cv4pn"
{
    "name": "Irfan",
    "age": 30,
}
```

Python may raise:

```text id="otf95q"
JSONDecodeError
```

Safe handling:

```python id="chjwqc"
import json

try:

    with open("data.json", "r") as file:
        data = json.load(file)

except json.JSONDecodeError:

    print("Invalid JSON format")
```

The lab specifically handles malformed JSON using `json.JSONDecodeError`.

---

# 9. Data Validation

Exception handling becomes even stronger when data is validated before processing.

Example:

```python id="vykpuq"
data = {
    "name": "Ali",
    "age": 25
}

if "name" not in data:
    raise ValueError("Name is required")
```

This means the program checks whether expected data is present.

The lab also validates required JSON fields and data types before processing.

---

# 10. `raise`

Sometimes we intentionally create an exception.

```python id="ocqyqt"
age = -5

if age < 0:

    raise ValueError("Age cannot be negative")
```

`raise` means:

> This situation is invalid, so create an error.

This is useful for validation.

---

# 11. What is Logging?

Logging means recording information about what a program is doing.

Instead of only:

```python id="05orcb"
print("File processed")
```

we can write:

```python id="gqvfl7"
logger.info("File processed")
```

Logging provides a structured history of application activity.

---

# 12. Importing Logging

Python provides a built-in module:

```python id="qe70jc"
import logging
```

No external installation is required.

---

# 13. Basic Logging Configuration

Example:

```python id="xw3oc7"
import logging

logging.basicConfig(
    level=logging.DEBUG
)
```

This configures the logging system.

The lab configures logging with timestamps, logger names, severity levels, file output and console output.

---

# 14. Creating a Logger

```python id="0l1gtb"
logger = logging.getLogger(__name__)
```

Now the logger can record different types of messages.

---

# 15. Logging Levels

Python logging uses different severity levels.

## DEBUG

Detailed information useful during development.

```python id="pfycn9"
logger.debug("File exists")
```

---

## INFO

Normal application activity.

```python id="n7ftqf"
logger.info("File processed successfully")
```

---

## WARNING

Something unusual happened, but the program can continue.

```python id="tbfkq6"
logger.warning("JSON file is empty")
```

---

## ERROR

An operation failed.

```python id="5vdtfg"
logger.error("File not found")
```

---

## CRITICAL

A serious error occurred.

```python id="nt5g0x"
logger.critical("Unexpected system failure")
```

### Severity order

```text id="66hnbk"
DEBUG
  ↓
INFO
  ↓
WARNING
  ↓
ERROR
  ↓
CRITICAL
```

The lab uses all of these logging patterns while processing files and JSON data.

---

# 16. Logging to a File

Logs can be saved permanently.

Example:

```python id="scdz5g"
logging.FileHandler(
    "application.log"
)
```

This creates:

```text id="1lhd2i"
application.log
```

A log file may contain:

```text id="vx6kx2"
INFO - File processing started
DEBUG - File exists
ERROR - Invalid JSON
INFO - Processing finished
```

The lab configures both file and console handlers.

---

# 17. Logging vs `print()`

### `print()`

```python id="wl0tgo"
print("File loaded")
```

Useful for simple output.

But normally disappears after the program finishes.

### Logging

```python id="z7zqvt"
logger.info("File loaded")
```

Can include:

```text id="hj42q4"
Date
Time
Severity
Module
Message
```

and can be saved in a file.

---

# 18. File Processing with Logging

Example workflow:

```python id="ojli13"
logger.info("Starting file processing")

try:

    with open("data.json", "r") as file:

        data = json.load(file)

    logger.info("File processed successfully")

except FileNotFoundError:

    logger.error("File not found")

except json.JSONDecodeError:

    logger.error("Invalid JSON")

finally:

    logger.info("Processing finished")
```

This combines:

```text id="tpfph4"
Exception Handling
+
File Handling
+
JSON
+
Logging
```

---

# 19. Batch Processing

Logging becomes especially useful when many files are processed.

Concept:

```text id="3a5dpw"
File 1 → Success
File 2 → Error
File 3 → Success
File 4 → Error
```

At the end:

```text id="p9j0cf"
Successful: 2
Failed: 2
```

The lab includes batch JSON processing and tracks successful and failed files using logging.

---

# 20. Main Exception Handling Flow

```text id="dr8cje"
Risky Operation
      ↓
     try
      ↓
   Error?
   /    \
 No      Yes
 ↓        ↓
Continue except
          ↓
      Handle Error
          ↓
        finally
```

---

# Main Concepts to Remember

```text id="5h4gn6"
try
→ Run risky code

except
→ Handle error

finally
→ Always execute

raise
→ Create an exception intentionally

FileNotFoundError
→ File missing

PermissionError
→ Access denied

ValueError
→ Invalid value

JSONDecodeError
→ Invalid JSON

Exception as e
→ Get error information

logging
→ Record program activity
```

---

# Logging Cheat Sheet

```text id="yv3kwa"
logger.debug()
→ Development details

logger.info()
→ Normal activity

logger.warning()
→ Possible problem

logger.error()
→ Operation failed

logger.critical()
→ Serious failure
```

---

# Practical Applications

Exception handling and logging are useful in:

* Data pipelines
* Automation scripts
* API applications
* Data Science projects
* File processing
* ETL workflows
* Web applications
* System administration
* Cybersecurity tools
* Production applications

Without proper exception handling, one bad file or invalid value can stop an entire workflow.

Logging helps identify:

```text id="6mg04o"
What happened?
When did it happen?
Where did it happen?
What error occurred?
```

---

# Technologies Used

* Python 3
* PyCharm
* Python `logging` module
* Python `json` module
* File Handling
* Exception Handling

---

# Learning Outcome

After completing this lab, I learned how to create Python programs that can continue working even when unexpected problems occur.

The overall workflow is:

```text id="ibvzzm"
Input / File
     ↓
Validation
     ↓
try
     ↓
Processing
     ↓
Error?
 ↓        ↓
No       Yes
 ↓        ↓
Success  except
           ↓
       Log Error
           ↓
        finally
```

These concepts make Python applications:

* More reliable
* Easier to debug
* Easier to maintain
* More suitable for real-world use

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

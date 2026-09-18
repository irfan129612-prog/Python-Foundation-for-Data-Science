# Lab 7: Working with JSON Files

## Overview

This lab focuses on working with **JSON (JavaScript Object Notation)** using Python.

JSON is a lightweight and structured format commonly used for:

* APIs
* Web applications
* Configuration files
* Data exchange
* Data storage

The main goal of this lab was to learn how Python can:

```text
Read JSON
    ↓
Convert JSON to Python
    ↓
Access Required Data
    ↓
Modify / Process Data
    ↓
Convert Python Data to JSON
    ↓
Save JSON File
```

---

## Objectives

By completing this lab, I learned how to:

* Understand JSON structure
* Read JSON files using Python
* Convert JSON data into Python dictionaries and lists
* Access nested JSON data
* Convert Python dictionaries into JSON
* Save Python data into JSON files
* Format JSON for better readability
* Handle invalid JSON files
* Use JSON in practical data-processing applications

---

# 1. What is JSON?

JSON stands for:

```text
JavaScript Object Notation
```

It is a text-based format used to store and exchange structured data.

Example:

```json
{
    "name": "Irfan",
    "age": 30,
    "skills": [
        "Python",
        "Data Science"
    ]
}
```

JSON is human-readable and widely used by APIs and modern applications.

---

# 2. JSON Structure

JSON mainly contains **key-value pairs**.

```json
{
    "name": "Irfan",
    "age": 30
}
```

Here:

```text
"name" → key
"Irfan" → value

"age" → key
30 → value
```

JSON objects use:

```text
{ }
```

JSON arrays use:

```text
[ ]
```

---

# 3. JSON and Python Data Types

JSON structures closely match Python structures.

```text
JSON Object     → Python Dictionary
JSON Array      → Python List
JSON String     → Python str
JSON Number     → Python int / float
JSON true       → Python True
JSON false      → Python False
JSON null       → Python None
```

This makes JSON easy to work with in Python.

---

# 4. Importing the JSON Module

Python provides a built-in `json` module.

```python
import json
```

No additional installation is required.

---

# 5. Reading a JSON File

A JSON file can be opened using `with open()`.

```python
import json

with open("data.json", "r") as file:
    data = json.load(file)
```

The important part is:

```python
json.load(file)
```

It converts:

```text
JSON File
    ↓
Python Dictionary / List
```

The lab uses this same method to load JSON files into Python.

---

# 6. Accessing JSON Data

Suppose JSON data becomes:

```python
data = {
    "name": "Irfan",
    "age": 30,
    "city": "Mansehra"
}
```

Access values using keys:

```python
print(data["name"])
```

Output:

```text
Irfan
```

Another example:

```python
print(data["age"])
```

Output:

```text
30
```

---

# 7. Nested JSON

Real-world JSON often contains data inside other data.

Example:

```python
data = {
    "student": {
        "name": "Ali",
        "marks": {
            "Python": 90,
            "Math": 85
        }
    }
}
```

To access Python marks:

```python
print(
    data["student"]["marks"]["Python"]
)
```

Output:

```text
90
```

Concept:

```text
data
 ↓
student
 ↓
marks
 ↓
Python
 ↓
90
```

The lab includes nested objects and arrays such as student courses and contact information.

---

# 8. JSON Arrays / Python Lists

JSON can contain lists.

```json
{
    "skills": [
        "Python",
        "SQL",
        "Power BI"
    ]
}
```

After loading into Python:

```python
skills = data["skills"]
```

Access first skill:

```python
print(skills[0])
```

Output:

```text
Python
```

Loop through data:

```python
for skill in data["skills"]:
    print(skill)
```

---

# 9. Using `.get()`

Instead of:

```python
data["name"]
```

we can use:

```python
data.get("name")
```

`.get()` is useful because it can avoid a `KeyError` when a key does not exist.

Example:

```python
city = data.get("city", "Unknown")
```

If `city` is unavailable:

```text
Unknown
```

will be returned.

---

# 10. Converting Python Dictionary to JSON String

Suppose:

```python
student = {
    "name": "Irfan",
    "score": 90
}
```

Convert it to JSON:

```python
json_data = json.dumps(student)
```

Concept:

```text
Python Dictionary
       ↓
json.dumps()
       ↓
JSON String
```

The lab uses `json.dumps()` to convert Python dictionary data into JSON strings.

---

# 11. Pretty Printing JSON

JSON can be formatted using:

```python
json.dumps(data, indent=4)
```

Instead of:

```json
{"name":"Irfan","age":30}
```

it becomes:

```json
{
    "name": "Irfan",
    "age": 30
}
```

`indent=4` makes JSON easier for humans to read.

---

# 12. Writing JSON to a File

Python data can be saved as JSON.

```python
import json

data = {
    "name": "Irfan",
    "course": "Python"
}

with open("data.json", "w") as file:

    json.dump(
        data,
        file,
        indent=4
    )
```

Concept:

```text
Python Dictionary
       ↓
json.dump()
       ↓
JSON File
```

The lab writes Python dictionary data into JSON files using this pattern.

---

# 13. `json.load()` vs `json.loads()`

These look similar but are different.

### `json.load()`

Used with a **file**.

```python
data = json.load(file)
```

```text
JSON File → Python
```

### `json.loads()`

Used with a **JSON string**.

```python
data = json.loads(json_string)
```

```text
JSON String → Python
```

---

# 14. `json.dump()` vs `json.dumps()`

### `json.dump()`

Writes Python data directly into a JSON file.

```python
json.dump(data, file)
```

```text
Python → JSON File
```

### `json.dumps()`

Creates a JSON string.

```python
json_string = json.dumps(data)
```

```text
Python → JSON String
```

---

# 15. Easy Way to Remember

```text
LOAD
JSON → Python

DUMP
Python → JSON
```

And:

```text
load()  → File
loads() → String

dump()  → File
dumps() → String
```

The extra:

```text
s
```

can be remembered as:

```text
s = string
```

---

# 16. Handling Missing JSON Files

```python
try:

    with open("data.json", "r") as file:
        data = json.load(file)

except FileNotFoundError:

    print("JSON file not found")
```

This prevents the program from crashing when the file does not exist.

---

# 17. Handling Invalid JSON

JSON must follow correct syntax.

Incorrect:

```json
{
    "name": "Irfan",
    "age": 30,
}
```

The extra comma may cause an error.

Python can handle it using:

```python
try:

    data = json.load(file)

except json.JSONDecodeError:

    print("Invalid JSON format")
```

The lab specifically handles malformed JSON using `json.JSONDecodeError`.

---

# 18. Looping Through JSON Data

Suppose:

```python
data = {
    "students": [
        {"name": "Ali", "score": 80},
        {"name": "Sara", "score": 90}
    ]
}
```

We can process every student:

```python
for student in data["students"]:

    print(student["name"])
    print(student["score"])
```

This combines:

```text
JSON
+
Dictionary
+
List
+
Loop
```

---

# 19. Reading Nested Data Safely

Instead of directly writing:

```python
data["company"]["address"]["city"]
```

a safer method can be:

```python
city = (
    data
    .get("company", {})
    .get("address", {})
    .get("city", "Unknown")
)
```

This reduces errors if some nested key does not exist.

---

# 20. JSON Data Processing Flow

A common real-world workflow is:

```text
JSON File / API
      ↓
json.load() / response.json()
      ↓
Python Dictionary
      ↓
Access Required Fields
      ↓
Clean / Analyze Data
      ↓
Modify Data
      ↓
json.dump()
      ↓
New JSON File
```

---

# JSON vs CSV

| JSON                 | CSV                      |
| -------------------- | ------------------------ |
| Key-value structure  | Rows and columns         |
| Supports nested data | Mainly tabular data      |
| Common in APIs       | Common in datasets       |
| Lists + dictionaries | Table structure          |
| More flexible        | Simpler for spreadsheets |

---

# Why JSON Matters for APIs

Most modern APIs return data in JSON format.

Example:

```text
Python
   ↓
API Request
   ↓
Server
   ↓
JSON Response
   ↓
Python Dictionary
```

This means Lab 7 directly prepares for **Lab 9: API Integration**.

---

# Main Functions to Remember

```text
import json
→ Use JSON tools

json.load()
→ JSON file to Python

json.loads()
→ JSON string to Python

json.dump()
→ Python to JSON file

json.dumps()
→ Python to JSON string

.get()
→ Safely access dictionary value

indent=4
→ Pretty formatting

JSONDecodeError
→ Invalid JSON error
```

---

# Practical Applications

JSON is commonly used in:

* REST APIs
* Web applications
* Mobile applications
* Configuration files
* Data exchange
* Automation
* Cloud services
* Data pipelines
* NoSQL databases
* Data Science workflows

The lab highlights JSON as an important format for APIs, configuration files, structured storage and analytics data exchange.

---

# Technologies Used

* Python 3
* PyCharm
* JSON
* Python `json` module
* Dictionaries
* Lists
* File Handling

---

# Learning Outcome

After completing this lab, I learned how to move structured data between JSON and Python.

The main workflow is:

```text
JSON
 ↓
Python Dictionary / List
 ↓
Process Data
 ↓
Python Dictionary / List
 ↓
JSON
```

This knowledge provides an important foundation for:

* API Integration
* Data Science
* Automation
* Web Development
* Data Engineering

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

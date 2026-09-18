# Lab 6: File Handling with TXT and CSV

## Overview

This lab focuses on **file handling in Python** using TXT and CSV files.

The main goal was to learn how Python can:

* Read external files
* Process and clean file data
* Convert text into structured data
* Calculate summary statistics
* Write processed results to new files
* Handle file-related errors safely

This lab introduces an important real-world data-processing workflow:

```text
File
 ↓
Read Data
 ↓
Clean / Parse
 ↓
Process
 ↓
Analyze
 ↓
Write Results
```

---

## Objectives

By completing this lab, I learned how to:

* Read text files line by line
* Use `with open()` for safe file handling
* Understand file modes such as `r`, `w`, and `a`
* Clean text using `.strip()`
* Split text into parts using `.split()`
* Process structured CSV data
* Use Python's built-in `csv` module
* Read CSV rows using `csv.DictReader`
* Convert CSV strings into numerical data
* Calculate totals, averages, minimums, and maximums
* Write new CSV files using `csv.DictWriter`
* Handle missing files and other errors

---

# 1. Opening Files in Python

Python uses the `open()` function to access files.

```python
file = open("data.txt", "r")
```

Here:

```text
data.txt → file name
"r"      → read mode
```

A better approach is using `with open()`:

```python
with open("data.txt", "r") as file:
    data = file.read()
```

The `with` statement automatically closes the file after the operation is completed.

---

# 2. File Modes

Python supports different file modes.

```text
r → Read
w → Write
a → Append
```

### Read Mode

```python
with open("data.txt", "r") as file:
    data = file.read()
```

Used to read an existing file.

### Write Mode

```python
with open("output.txt", "w") as file:
    file.write("Hello")
```

Used to create or overwrite a file.

### Append Mode

```python
with open("output.txt", "a") as file:
    file.write("New line")
```

Adds new content without removing existing data.

The lab uses these standard file operations and recommends context managers for safe file handling.

---

# 3. Reading a Text File Line by Line

A file can be processed one line at a time.

```python
with open("students.txt", "r") as file:

    for line in file:
        print(line)
```

This is useful when processing large files or structured text records.

The lab reads student information this way before extracting individual values.

---

# 4. Cleaning Text with `.strip()`

Lines read from a file may contain spaces or newline characters.

```python
line = "Irfan Ahmed\n"

clean_line = line.strip()
```

Result:

```text
Irfan Ahmed
```

The `.strip()` method removes unnecessary whitespace from the beginning and end of text.

---

# 5. Splitting Text with `.split()`

The `.split()` method divides text into separate parts.

Example:

```python
record = "Irfan - Python - A"

parts = record.split(" - ")
```

Result:

```python
["Irfan", "Python", "A"]
```

Individual values can then be accessed:

```python
name = parts[0]
course = parts[1]
grade = parts[2]
```

The lab uses this technique to convert text-file records into structured information.

---

# 6. Using `.replace()`

The `.replace()` method can remove or replace unwanted text.

```python
grade_text = "Grade: A"

grade = grade_text.replace("Grade: ", "")
```

Result:

```text
A
```

---

# 7. Converting Text Data into Dictionaries

After extracting values, they can be stored in dictionaries.

```python
student = {
    "name": "Irfan",
    "course": "Python",
    "grade": "A"
}
```

Multiple records can be stored inside a list:

```python
students = []

students.append(student)
```

This creates structured data that is easier to analyze.

The lab uses this approach when processing student records.

---

# 8. Error Handling for Files

A program may try to open a file that does not exist.

```python
try:

    with open("data.txt", "r") as file:
        print(file.read())

except FileNotFoundError:

    print("File not found")
```

This prevents the program from crashing.

The lab specifically handles `FileNotFoundError` and other file-processing exceptions.

---

# 9. Working with CSV Files

CSV stands for:

```text
Comma-Separated Values
```

Example:

```text
Name,Age,City
Irfan,30,Mansehra
Ali,25,Abbottabad
Ahmed,28,Peshawar
```

CSV files contain structured data in rows and columns.

The lab uses Python's built-in `csv` module to work with this format.

---

# 10. Importing the CSV Module

```python
import csv
```

The `csv` module provides tools for reading and writing CSV files.

---

# 11. `csv.DictReader()`

`DictReader()` reads each CSV row as a dictionary.

```python
import csv

with open("people.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

Example row:

```python
{
    "Name": "Irfan",
    "Age": "30",
    "City": "Mansehra"
}
```

Values can then be accessed by column name:

```python
print(row["Name"])
```

This is much easier than manually working with column indexes.

The lab uses `csv.DictReader()` to process sales data.

---

# 12. Converting CSV Values to Numbers

CSV values are usually read as strings.

For example:

```python
row["Quantity"]
```

may contain:

```text
"5"
```

To perform calculations:

```python
quantity = int(row["Quantity"])

price = float(row["Price"])
```

Then:

```python
total = quantity * price
```

The lab converts quantity and price data before calculating sales totals.

---

# 13. Calculating Statistics

After processing numerical data, Python can calculate basic statistics.

```python
values = [100, 200, 150, 300]
```

### Total

```python
sum(values)
```

### Count

```python
len(values)
```

### Average

```python
average = sum(values) / len(values)
```

### Minimum

```python
min(values)
```

### Maximum

```python
max(values)
```

The lab uses these techniques to calculate summary statistics from file data.

---

# 14. Writing CSV Files

Python can also create CSV files.

```python
import csv

with open("results.csv", "w", newline="") as file:

    writer = csv.DictWriter(
        file,
        fieldnames=["Name", "Score"]
    )

    writer.writeheader()

    writer.writerow({
        "Name": "Irfan",
        "Score": 90
    })
```

Output:

```text
Name,Score
Irfan,90
```

---

# 15. `fieldnames`

`fieldnames` define the CSV columns.

```python
fieldnames = [
    "Name",
    "Score",
    "City"
]
```

These become the header row of the CSV file.

---

# 16. `writeheader()`

```python
writer.writeheader()
```

Writes the CSV column names.

Example:

```text
Name,Score,City
```

---

# 17. `writerow()`

Writes one dictionary as one CSV row.

```python
writer.writerow({
    "Name": "Irfan",
    "Score": 90
})
```

For multiple rows:

```python
for student in students:
    writer.writerow(student)
```

The lab uses `csv.DictWriter()` and `writeheader()` when creating summary reports.

---

# TXT vs CSV

| TXT                             | CSV                            |
| ------------------------------- | ------------------------------ |
| Plain text                      | Structured rows and columns    |
| Manual parsing often required   | Easy to process using `csv`    |
| Useful for logs and simple data | Useful for datasets            |
| `.split()` often needed         | `DictReader()` handles columns |

---

# Main Data Processing Flow

```text
Input File
    ↓
Read File
    ↓
Clean Data
    ↓
Convert Data Types
    ↓
Store in Lists / Dictionaries
    ↓
Calculate Statistics
    ↓
Create Output File
```

---

# Important Functions and Methods

```text
open()
→ Open a file

with open()
→ Safely handle a file

.read()
→ Read file content

.strip()
→ Remove whitespace

.split()
→ Divide text into parts

.replace()
→ Replace/remove text

csv.DictReader()
→ CSV rows → dictionaries

int()
→ Convert to integer

float()
→ Convert to decimal number

sum()
→ Total

len()
→ Count

min()
→ Minimum

max()
→ Maximum

csv.DictWriter()
→ Write dictionary data to CSV

writeheader()
→ Write column names

writerow()
→ Write one row
```

---

# Practical Applications

File handling is useful for:

* Data analysis
* CSV datasets
* Student records
* Sales records
* Business reporting
* Log processing
* Data migration
* Automation
* Machine learning preprocessing
* Report generation

The lab highlights file handling as a foundation for data analysis, automation, business reporting, and later data-processing tasks.

---

# Technologies Used

* Python 3
* PyCharm
* TXT Files
* CSV Files
* Python `csv` module

---

# Learning Outcome

After completing this lab, I learned how Python can work with real external data instead of only values written directly inside a program.

The overall workflow was:

```text
Read
 ↓
Clean
 ↓
Parse
 ↓
Process
 ↓
Analyze
 ↓
Export
```

This provides an important foundation for future work with:

* Pandas
* Data Analysis
* Data Science
* APIs
* Automation
* Machine Learning datasets

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

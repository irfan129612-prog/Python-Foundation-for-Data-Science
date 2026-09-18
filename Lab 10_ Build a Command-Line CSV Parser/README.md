# Lab 10: Build a Command-Line CSV Parser

## Overview

This lab focuses on building a **Command-Line CSV Parser using Python**.

The project demonstrates how a Python script can accept commands from the terminal, read CSV data, filter records, calculate statistics, and display results without changing the code manually each time.

The overall workflow is:

```text
Terminal Command
      ↓
Read Arguments
      ↓
Load CSV File
      ↓
Filter Data
      ↓
Select Column
      ↓
Calculate Statistics
      ↓
Display Results
```

---

## Objectives

By completing this lab, I learned how to:

* Build a command-line Python application
* Use the `argparse` module
* Accept file names and options from the terminal
* Read CSV files
* Select specific columns
* Filter CSV rows
* Convert numerical data
* Calculate average, minimum, maximum, and count
* Handle missing or invalid data
* Organize code using functions
* Create a reusable CSV analysis tool

The lab specifically covers command-line argument parsing, CSV analysis, filtering, statistics, file handling, and reusable functions.

---

# 1. What is a Command-Line Application?

A command-line application is a program that runs from the terminal.

Normal Python script:

```bash
python csv_parser.py
```

A command-line tool can also receive options:

```bash
python csv_parser.py data.csv --column salary
```

Here:

```text
data.csv
→ Input file

--column salary
→ Analyze salary column
```

This makes the script flexible and reusable.

---

# 2. What is `argparse`?

Python provides the built-in:

```python
import argparse
```

module.

`argparse` allows the program to understand terminal arguments.

Example:

```bash
python csv_parser.py data.csv --column age
```

Python can understand:

```text
filename = data.csv
column = age
```

---

# 3. Creating an Argument Parser

Basic structure:

```python
import argparse

parser = argparse.ArgumentParser()
```

This creates the command-line parser.

---

# 4. Adding Arguments

Arguments are defined using:

```python
parser.add_argument()
```

Example:

```python
parser.add_argument(
    "filename",
    help="Path to CSV file"
)
```

Now the user must provide a filename.

Example:

```bash
python csv_parser.py sales.csv
```

---

# 5. Optional Arguments

The lab uses an option for selecting a column:

```python
parser.add_argument(
    "--column",
    "-c",
    required=True
)
```

Now both commands can represent the same option:

```bash
python csv_parser.py data.csv --column salary
```

or:

```bash
python csv_parser.py data.csv -c salary
```

The lab defines filename, column, filter, and display options through `argparse`.

---

# 6. Parsing Arguments

After defining arguments:

```python
args = parser.parse_args()
```

Now values can be accessed:

```python
print(args.filename)
print(args.column)
```

Concept:

```text
Terminal
   ↓
parse_args()
   ↓
Python Variables
```

---

# 7. Reading a CSV File

The tool then loads the CSV file.

```python
import csv

with open(filename, "r") as file:

    reader = csv.DictReader(file)

    data = list(reader)
```

Each row becomes a dictionary.

Example CSV:

```text
Name,Department,Salary
Ali,IT,50000
Sara,HR,45000
Ahmed,IT,60000
```

One row becomes:

```python
{
    "Name": "Ali",
    "Department": "IT",
    "Salary": "50000"
}
```

---

# 8. Selecting a Column

If the user runs:

```bash
python csv_parser.py employees.csv --column Salary
```

the program extracts:

```python
row["Salary"]
```

from every row.

Concept:

```text
CSV
 ↓
Salary Column
 ↓
50000
45000
60000
```

---

# 9. Converting Strings to Numbers

CSV values are usually read as strings.

Example:

```text
"50000"
```

For calculations:

```python
salary = float(row["Salary"])
```

Now mathematical operations are possible.

---

# 10. Calculating Statistics

The lab calculates statistics for numerical columns.

Suppose:

```python
values = [
    50000,
    45000,
    60000
]
```

## Count

```python
count = len(values)
```

## Minimum

```python
minimum = min(values)
```

## Maximum

```python
maximum = max(values)
```

## Average

```python
average = sum(values) / len(values)
```

Result:

```text
Count: 3
Minimum: 45000
Maximum: 60000
Average: 51666.67
```

---

# 11. Filtering CSV Rows

The program can also filter rows.

Example:

```bash
python csv_parser.py employees.csv \
--column Salary \
--filter Department IT
```

Meaning:

> Analyze only employees where Department is IT.

Basic logic:

```python
filtered_data = []

for row in data:

    if row["Department"] == "IT":

        filtered_data.append(row)
```

---

# 12. Case-Insensitive Filtering

The lab improves filtering using:

```python
row[filter_column].strip().lower()
```

and:

```python
filter_value.lower()
```

This allows:

```text
IT
it
It
```

to be treated similarly.

The lab's filter function compares normalized values before keeping matching rows.

---

# 13. `--filter`

The lab defines filtering using:

```python
parser.add_argument(
    "--filter",
    "-f",
    nargs=2
)
```

`nargs=2` means the option expects two values.

Example:

```bash
--filter Department IT
```

Two values:

```text
Department
IT
```

become:

```python
filter_column = "Department"
filter_value = "IT"
```

---

# 14. `--show-data`

The lab also provides:

```python
--show-data
```

Example:

```bash
python csv_parser.py data.csv \
--column Salary \
--show-data
```

This allows matching data rows to be displayed along with statistics.

It is defined using:

```python
action="store_true"
```

Meaning:

```text
Option present → True

Option absent → False
```

The lab uses `action='store_true'` for the show-data option.

---

# 15. Example Command

```bash
python csv_parser.py data.csv \
--column salary \
--filter department Engineering
```

The lab includes this same style of command-line usage.

Concept:

```text
data.csv
      ↓
Filter:
department = Engineering
      ↓
Select:
salary
      ↓
Calculate:
average / min / max
```

---

# 16. Creating Functions

Instead of writing everything in one block, the program is divided into functions.

Example:

```python
def read_csv_file(filename):
    pass
```

```python
def filter_rows(data, column, value):
    pass
```

```python
def calculate_statistics(data, column):
    pass
```

```python
def display_filtered_data(data):
    pass
```

This makes the program:

* Easier to understand
* Easier to test
* Easier to maintain
* More reusable

---

# 17. Main Function

The program combines all components inside:

```python
def main():
```

Basic flow:

```python
def main():

    parser = create_argument_parser()

    args = parser.parse_args()

    data = read_csv_file(args.filename)
```

The lab's `main()` function parses command-line arguments, loads the CSV, applies filters, and then calculates statistics.

---

# 18. `if __name__ == "__main__"`

The script can be started using:

```python
if __name__ == "__main__":
    main()
```

Meaning:

> Run `main()` when this Python file is executed directly.

This helps organize professional Python programs.

---

# 19. Handling Empty Files

The program checks:

```python
if not data:

    print("CSV file is empty")

    sys.exit(1)
```

This prevents calculations on empty data.

The lab performs this check before continuing with statistics.

---

# 20. `sys.exit()`

Python provides:

```python
import sys
```

Program can be stopped using:

```python
sys.exit(1)
```

Normally:

```text
0
→ successful completion

1
→ error / unsuccessful completion
```

This is useful for command-line tools.

---

# 21. Error Handling

Possible errors include:

```text
File does not exist
Wrong column name
Empty CSV
Non-numeric values
Invalid filter column
Permission problems
```

Safe code can use:

```python
try:

    with open(filename, "r") as file:
        ...

except FileNotFoundError:

    print("File not found")
```

This combines Lab 8's exception handling with the CSV tool.

---

# 22. Displaying Filtered Data

The lab creates formatted output using column headers.

Concept:

```text
Name            | Department      | Salary
------------------------------------------------
Ali             | IT              | 50000
Ahmed           | IT              | 60000
```

This makes terminal output easier to read.

The lab dynamically creates headers from dictionary keys when displaying filtered CSV data.

---

# 23. Complete Project Flow

```text
User Command
     ↓
argparse
     ↓
Get Filename
     ↓
Read CSV
     ↓
Validate Data
     ↓
Apply Filter
     ↓
Select Column
     ↓
Convert to Numbers
     ↓
Calculate Statistics
     ↓
Display Results
```

---

# Main Concepts to Remember

```text
argparse
→ Handle command-line arguments

ArgumentParser()
→ Create CLI parser

add_argument()
→ Define command options

parse_args()
→ Read supplied options

csv.DictReader()
→ CSV rows to dictionaries

filter
→ Select required rows

float()
→ Convert CSV values to numbers

sum()
→ Total

len()
→ Count

min()
→ Minimum

max()
→ Maximum

sys.exit()
→ Stop program
```

---

# Example Usage

### Analyze Salary

```bash
python csv_parser.py data.csv --column salary
```

### Analyze Age

```bash
python csv_parser.py data.csv --column age
```

### Filter by Department

```bash
python csv_parser.py data.csv \
--column salary \
--filter department Engineering
```

### Show Filtered Data

```bash
python csv_parser.py data.csv \
--column salary \
--filter department Engineering \
--show-data
```

---

# Concepts Combined from Previous Labs

Lab 10 combines almost everything learned earlier:

```text
Lab 1
Data Types
   +
Lab 2
Conditions
   +
Lab 3
Loops
   +
Lab 4
Functions
   +
Lab 6
CSV Files
   +
Lab 8
Exception Handling
   ↓
Command-Line CSV Parser
```

---

# Practical Applications

A command-line CSV parser can be used for:

* Data analysis
* Business reports
* Sales analysis
* Employee datasets
* Financial records
* Research datasets
* Log analysis
* Data cleaning
* Automation scripts
* Quick dataset exploration

---

# Technologies Used

* Python 3
* PyCharm
* CSV
* `csv`
* `argparse`
* `sys`
* Functions
* Exception Handling
* Command-Line Interface

---

# Learning Outcome

After completing this lab, I learned how to turn a normal Python script into a **reusable command-line data analysis tool**.

Instead of modifying the source code for every dataset, the user can control the program through terminal arguments.

The final workflow is:

```text
CSV Dataset
     ↓
Command-Line Tool
     ↓
Filter Data
     ↓
Select Column
     ↓
Analyze
     ↓
Statistics
     ↓
Readable Output
```

This provides a useful foundation for:

* Python Automation
* Data Analysis
* Data Science
* CLI Tools
* ETL Scripts
* Data Engineering

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

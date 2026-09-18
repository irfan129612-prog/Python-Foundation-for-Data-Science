# Lab 9: Automate Weather Data Retrieval with API

## Overview

This lab focuses on retrieving real-time weather data from an external service using a **REST API**.

The project demonstrates how Python can communicate with an online API, receive data in JSON format, extract useful information, handle possible errors, and display results in a readable format.

The main workflow is:

```text
Python Program
      ↓
Send API Request
      ↓
Weather Server
      ↓
Receive JSON Response
      ↓
Extract Required Data
      ↓
Display / Analyze Results
```

---

## Objectives

By completing this lab, I learned how to:

* Understand the basics of REST APIs
* Work with HTTP requests
* Use API keys
* Send GET requests using Python
* Work with the `requests` library
* Receive and process JSON responses
* Extract nested weather data
* Handle HTTP status codes
* Handle network and API errors
* Display weather information in tabular format
* Create reusable API-based Python functions

The lab specifically introduces REST APIs, HTTP requests, API keys, JSON parsing, error handling, and reusable weather retrieval scripts.

---

# 1. What is an API?

API stands for:

```text
Application Programming Interface
```

An API allows one application to communicate with another application.

Example:

```text
Python Program
      ↓
Weather API
      ↓
Weather Data
```

Instead of manually opening a weather website, Python can request the same data automatically.

---

# 2. What is a REST API?

A REST API allows applications to communicate over the internet using HTTP requests.

A client can request data from a server.

Example:

```text
Client
  ↓
Request
  ↓
Server
  ↓
Response
```

In this lab:

```text
Python
  ↓
OpenWeatherMap API
  ↓
Weather Data
```

The lab uses OpenWeatherMap as the weather-data service.

---

# 3. API Key

An API key is used to identify or authorize an application when accessing an API.

Concept:

```text
User / Application
       ↓
API Key
       ↓
API Service
```

The API key should be kept secure.

It should not be publicly exposed in a GitHub repository.

Example placeholder:

```python
API_KEY = "YOUR_API_KEY_HERE"
```

The lab instructs users to obtain an API key and keep it secure.

---

# 4. Installing the `requests` Library

Python uses the `requests` library to communicate with web APIs.

```bash
pip install requests
```

Import it using:

```python
import requests
```

The lab uses `requests` for HTTP communication with the weather service.

---

# 5. Sending a GET Request

A GET request asks a server to return information.

Example:

```python
response = requests.get(url)
```

Concept:

```text
requests.get()
      ↓
Send Request
      ↓
API Server
      ↓
Receive Response
```

---

# 6. Building the API URL

The weather API requires information such as:

* City
* API key
* Units

Example structure:

```python
url = f"{BASE_URL}?q={city_name}&appid={API_KEY}&units=metric"
```

Here:

```text
BASE_URL
→ API endpoint

q
→ city name

appid
→ API key

units=metric
→ Celsius units
```

---

# 7. HTTP Status Codes

The server returns a status code with every response.

Example:

```python
response.status_code
```

Important codes:

```text
200 → Request successful

401 → Unauthorized / invalid credentials

404 → Requested resource not found
```

Example:

```python
if response.status_code == 200:
    print("Success")
```

The lab checks different response codes when retrieving weather data.

---

# 8. Converting API Response to JSON

Most APIs return structured data in JSON format.

Python can convert the response using:

```python
data = response.json()
```

Concept:

```text
API Response
     ↓
JSON
     ↓
response.json()
     ↓
Python Dictionary
```

This connects directly with the JSON concepts learned in Lab 7.

---

# 9. Extracting Weather Data

API responses often contain nested dictionaries.

For example:

```python
temperature = weather_data["main"]["temp"]
```

Other fields may include:

```python
city = weather_data["name"]

country = weather_data["sys"]["country"]

humidity = weather_data["main"]["humidity"]

pressure = weather_data["main"]["pressure"]

wind_speed = weather_data["wind"]["speed"]
```

The lab extracts city, country, temperature, humidity, pressure, weather description, wind speed, visibility, and other values from nested JSON.

---

# 10. Creating a Reusable Weather Function

A reusable function can retrieve weather for different cities.

```python
def get_weather_data(city_name):

    url = f"{BASE_URL}?q={city_name}&appid={API_KEY}&units=metric"

    response = requests.get(url)

    if response.status_code == 200:
        return response.json()

    return None
```

Usage:

```python
weather = get_weather_data("London")
```

The same function can then be reused for:

```text
London
Karachi
Islamabad
Peshawar
Dubai
```

---

# 11. Error Handling

Internet-based programs can fail for many reasons.

Possible issues:

```text
No internet
Server unavailable
Wrong API key
City not found
Request timeout
Invalid JSON
```

Therefore, API requests should use `try-except`.

Example:

```python
try:

    response = requests.get(url)

except requests.exceptions.RequestException as e:

    print("Network error:", e)
```

The lab handles network errors and JSON parsing errors during API retrieval.

---

# 12. Timeout Handling

A request may take too long.

Example:

```python
response = requests.get(
    url,
    timeout=10
)
```

If the server does not respond within the expected time, Python can handle the timeout.

```python
except requests.exceptions.Timeout:

    print("Request timed out")
```

The lab includes timeout handling in the enhanced weather script.

---

# 13. Connection Error

If internet access fails:

```python
except requests.exceptions.ConnectionError:

    print("Connection failed")
```

This prevents the application from crashing.

---

# 14. Validating User Input

Before contacting the API, input can be checked.

Example:

```python
if not city_name.strip():

    print("City name required")
```

This prevents useless requests.

The lab also validates city names before sending API requests.

---

# 15. Processing Multiple Cities

A loop can retrieve weather for multiple locations.

```python
cities = [
    "London",
    "Islamabad",
    "Karachi"
]

for city in cities:

    weather = get_weather_data(city)
```

This combines concepts from previous labs:

```text
Lists
+
Loops
+
Functions
+
APIs
+
JSON
```

---

# 16. Displaying Data in a Table

The lab uses the `tabulate` library to display results in a readable table.

Install:

```bash
pip install tabulate
```

Import:

```python
from tabulate import tabulate
```

Concept:

```text
Raw Dictionary Data
        ↓
tabulate()
        ↓
Formatted Table
```

The lab installs and uses `tabulate` for formatted weather output.

---

# 17. Summary Statistics

Weather data from multiple cities can also be analyzed.

For example:

```python
temperatures = [
    data["Temperature (°C)"]
    for data in weather_data_list
]
```

Average:

```python
average = sum(temperatures) / len(temperatures)
```

Highest:

```python
max(temperatures)
```

Lowest:

```python
min(temperatures)
```

This combines API data retrieval with basic data analysis.

---

# 18. Exporting Weather Data

Retrieved weather data can also be written to a file.

Example:

```python
with open("weather_data.txt", "w") as file:

    file.write("Weather Data\n")
```

This combines:

```text
API
+
JSON
+
File Handling
```

The lab includes an export function for saving retrieved weather information.

---

# 19. Complete API Workflow

```text
City Name
   ↓
Validate Input
   ↓
Build API URL
   ↓
requests.get()
   ↓
HTTP Response
   ↓
Check Status Code
   ↓
response.json()
   ↓
Extract Required Fields
   ↓
Store / Analyze
   ↓
Display Table
   ↓
Export if Needed
```

---

# Main Concepts to Remember

```text
API
→ Service used by programs to communicate

REST API
→ Web-based API communication

API Key
→ Access / identification key

requests
→ Python HTTP library

requests.get()
→ Send GET request

response
→ Server's reply

status_code
→ Request result

response.json()
→ Convert JSON response to Python

timeout
→ Maximum wait time

JSON
→ Common API data format

tabulate
→ Display formatted tables
```

---

# Common Status Codes

```text
200
→ Success

401
→ Unauthorized / API key problem

404
→ Resource not found
```

---

# Error Handling Flow

```text
Send Request
     ↓
Success?
 /        \
Yes        No
 ↓          ↓
JSON     Handle Error
 ↓
Extract Data
 ↓
Display Result
```

---

# Practical Applications

API integration can be used for:

* Weather applications
* Agricultural monitoring
* Business dashboards
* Financial data
* Stock prices
* Currency exchange
* Maps
* Logistics systems
* Research automation
* Data collection
* Data Science pipelines

The lab specifically mentions weather monitoring, dashboards, automated research data collection, logistics, and application development as real-world uses.

---

# Technologies Used

* Python 3
* PyCharm
* REST API
* HTTP
* OpenWeatherMap API
* `requests`
* JSON
* `tabulate`
* Exception Handling
* Functions
* Lists and Dictionaries

---

# Learning Outcome

After completing this lab, I learned how Python can retrieve live data from an external online service and process that data automatically.

The project combines concepts from previous labs:

```text
Functions
   +
Loops
   +
Dictionaries
   +
JSON
   +
Exception Handling
   +
API Integration
```

The overall workflow is:

```text
External API
     ↓
Python Request
     ↓
JSON Data
     ↓
Extract
     ↓
Process
     ↓
Analyze
     ↓
Display / Export
```

This provides an important foundation for:

* Data Science
* Data Engineering
* Automation
* Web APIs
* AI Applications
* Real-Time Data Projects

---

## Author

**Irfan Ahmed**

Python Learning & Practical Lab Portfolio

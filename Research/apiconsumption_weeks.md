# API Consumption with restful API

## Introduction

API consumption with Python refers to the process of interacting with Application Programming Interfaces (APIs) using Python programming language. APIs allow different software systems to communicate and exchange data with each other. Python, with its simplicity and vast range of libraries, is commonly used for consuming APIs.

## Table of Content

1. Understanding the API 

2. Libraries
    1. Choosing a library
    2. Importing libraries

3. API requests and responses
    1. Making API requests
    2. Handling API responses

4. Authentication

## 1. Understanding the API 

Understanding the API is the foundational step before consuming it with Python or any other programming language. This involves studying the API documentation provided by the service or platform that offers the API. API documentation serves as a comprehensive guide to the API's functionality, endpoints, input parameters, output formats, authentication methods, error handling, and more.

Below is a list of some of things to look for in API documentation:

1. Endpoint

2. HTTP Methods

3. Parameters

4. Authentication

5. Error Handling

By thoroughly studying the API documentation, you gain a clear understanding of how to structure your Python code for making API requests, how to interpret the responses, and how to handle different scenarios effectively. This knowledge helps you build robust and efficient applications that interact seamlessly with the API and meet your specific needs.


## 2. Libraries

### Choosing a library

Python offers several libraries for making API requests, such as `requests`, `http.client`, and others. The `requests` library is a popular choice due to its simplicity and ease of use.

### Importing a library 

If you haven't already installed the required libraries, use pip, Python's package manager, to install them. For example, to install requests, you can use: pip install requests.

Example on how to import and use the `requests` library:

```jsx
import requests

# API endpoint and parameters
api_url = "https://api.example.com/data"
params = {"param1": "value1", "param2": "value2"}

# Sending a GET request with parameters
response = requests.get(api_url, params=params)

# Check if the request was successful (status code 200)
if response.status_code == 200:
    # Parse the JSON response
    data = response.json()
    # Process the data as needed
    print(data)
else:
    print(f"API request failed with status code: {response.status_code}")
```

## 3. API requests and responses

### Making API requests 

Use the chosen library to send HTTP requests to the API's endpoints. This typically involves constructing the request URL, adding any required headers or parameters, and specifying the HTTP method (GET, POST, PUT, DELETE, etc.).

Example:

```jsx

import requests

def get_random_advice():
    api_url = "https://api.adviceslip.com/advice"
    
    try:
        # Sending a GET request to the API
        response = requests.get(api_url)
        
        # Check if the request was successful (status code 200)
        if response.status_code == 200:
            # Parse the JSON response
            data = response.json()
            # Access the advice
            advice = data["slip"]["advice"]
            print(f"Random Advice: {advice}")
        else:
            print(f"API request failed with status code: {response.status_code}")
    except requests.RequestException as e:
        print(f"An error occured: {e})

```

### Handling API responses

After sending a request to the API using Python and the `requests` library, you will receive a response from the server. The API response contains the data you requested (if applicable) and additional information about the status of the request. Handling API responses involves extracting the relevant data from the response and interpreting the status code and other response details. Here's how you can handle API responses using `requests`:

1. Checking the Status Code:
The HTTP status code is a three-digit number that indicates the success or failure of the API request. It is included in the response object returned by requests. Common HTTP status codes include:

200: OK (Request succeeded)
201: Created (Request succeeded and a new resource was created)
204: No Content (Request succeeded, but there is no data to return)
400: Bad Request (The request was malformed or invalid)

2. Error Handling:
Always include error handling in your code to handle potential issues like network errors, invalid responses, or API errors. You can use Python's try and except blocks to catch exceptions and handle errors. 

Example: 

```jsx

import requests

# API endpoint URL
api_url = "https://api.example.com/data"

try:
    # Sending a GET request
    response = requests.get(api_url)

    # Check if the request was successful (status code 200)
    if response.status_code == 200:
        # Parse the JSON response
        data = response.json()
        # Access the data
        print(f"Name: {data['name']}")
        print(f"Age: {data['age']}")
        print(f"Email: {data['email']}")
    else:
        print(f"API request failed with status code: {response.status_code}")
except requests.RequestException as e:
    print(f"An error occurred: {e}")

```

## 4. Authentication

Authentication in API consumption refers to the process of verifying the identity of the user or application that is making the API request. APIs often require authentication to ensure that only authorized users can access certain resources or perform specific actions. Authentication is a crucial security measure that helps protect sensitive data and prevent unauthorized access to API endpoints.

There are various authentication methods used in API consumption, and the choice of method depends on the API provider's security requirements. Here are some common authentication methods used in API consumption:

1. API Key Authentication:
This involves passing an API key as a parameter or in the request headers. The API key is a unique identifier provided by the API provider to the client (user or application) when they register for API access. The API key acts as a secret token, and the API server validates it to authorize access.

Example:

```jsx

import requests

api_url = "https://api.example.com/data"
api_key = "YOUR_API_KEY"

headers = {"Authorization": f"Bearer {api_key}"}
response = requests.get(api_url, headers=headers)

```

2. OAuth (OAuth2) Authentication:
OAuth is a more secure and sophisticated authentication protocol used when APIs require access to specific user data on behalf of the user. OAuth allows users to grant limited access to their resources without sharing their actual credentials (username and password) with the API.
The OAuth process involves obtaining access tokens, which are temporary credentials that the API client uses to access resources. The client sends the access token in the request headers for each API call.

Example: 
```jsx
import requests
from requests_oauthlib import OAuth2Session

client_id = "YOUR_CLIENT_ID"
client_secret = "YOUR_CLIENT_SECRET"
authorization_base_url = "https://api.example.com/authorize"
token_url = "https://api.example.com/token"

oauth = OAuth2Session(client_id, redirect_uri="http://localhost:8000/callback")
authorization_url, state = oauth.authorization_url(authorization_base_url)

# Redirect the user to the authorization URL and retrieve the access token after user consent.
# Then use the access token in subsequent API requests.

```

## Conclusion

In conclusion, API consumption is a fundamental aspect of modern software development that empowers developers to build more powerful, interconnected, and adaptable applications. By leveraging APIs, developers can access a vast array of functionalities, data, and services, allowing them to focus on creating unique, value-added experiences for their users. APIs have become the backbone of web and mobile applications, enabling seamless integration with external resources and unlocking new possibilities in the world of software development.
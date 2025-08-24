# API Testing with Pythons requests module 

This repository contains Python script that test a simple endpoints of a local API, such as `/health`, `/signup`, `/login`,. The tests are performed using the `requests` library.

## Prerequisites

To run the tests, make sure you have the following installed:

- Python 3.x
- `requests` library

You can install the `requests` library using pip:

```shell
pip install requests

```
To run the tests, make sure you run the uvicorn server:

```shell
uvicorn main:app --reload
```

Fork Alejandros original repo create an own bransch in VS Code. Navigate to the backend folder and activate the virtual enviroment and add packages that`s needed. Create a own pythonfile in the backend folder for implement the code in scripts below. 



## Testing the API explanation of the tests 

1. Health Check
The test_api() function sends a GET request to the /health endpoint of the API to verify if the server is up and running. It will print the response status code and body.

2. Signup
The test_signup() function sends a POST request to the /signup endpoint to create a new user. It sends a username and password in the request body. It checks if the user is successfully created or if an error occurs (e.g., if the username is already registered).

3. Login
The test_login() function sends a POST request to the /login endpoint with the user's credentials. If successful, it returns an authentication token (access_token) which is required for further API requests.

4. Products 
def add_one_product(token) function sends a POST request to the /products endpoint with the Authorization token (Bearer token) for authorization . If successful, it returns a message that the product has been added.

## Database updates when test are running on the server 

When you run the server and ther user is already added you will get response that user already exist when you try to added that user in the system. Try to test with diffrent users to login to avoid 400 bad request response from the client server. 

## Sample Code 

```Py

import requests

# Base URL variable for your API (local development server that comes with Uvicorn) 
BASE_URL = "http://127.0.0.1:8000"

# User credentials variables for testing signup and login you can switch to other USERNAME/PASSWORD IF YOU WANT 

USERNAME = "HANNES"
PASSWORD = "KATTEN"

def test_api():
    """
    Test the /health endpoint to check if the server is running.
    Prints the response status code and body for debugging.
    """
    url = f"{BASE_URL}/health"
    response = requests.get(url)
    
    if response.status_code == 200:
        print(f"Test passed! Server is up and running. Status code: {response.status_code}")
        print(f"Response body: {response.text}")
    else:
        print(f"Test failed! Status code: {response.status_code}")

# Run the health check test will run when you run your pythonfile 
test_api()


def test_signup():
    """
    Test the /signup endpoint by creating a new user.
    Verifies if the user is created successfully or if an error occurs (e.g., username already exists).
    """
    signup_url = f"{BASE_URL}/signup"
    user_data = {
        "username": USERNAME,
        "password": PASSWORD
    }
    
    response = requests.post(signup_url, json=user_data)
    
    if response.status_code == 200:
        print(f"Signup successful. User created. Status code: {response.status_code}")
        print("Response:", response.json())
    elif response.status_code == 400:
        print(f"Signup failed. Username already registered. Error: {response.json()['detail']}")
        print(f"Status Code: {response.status_code}")
    else:
        print(f"Signup failed with unexpected status code: {response.status_code}")
        print(f"Response: {response.text}")

# Run the signup test will run when you run the pythonfile 
test_signup()


def test_login():
    """
    Test the /login endpoint to authenticate the user and retrieve the token.
    """
    login_url = f"{BASE_URL}/login"
    login_data = {
        "username": USERNAME,
        "password": PASSWORD
    }
    
    response = requests.post(login_url, data=login_data)
    
    if response.status_code == 200:
        print(f"Login successful. Status code: {response.status_code}")
        print("Response:", response.json())
        
        token = response.json().get("access_token")
        
        if token:
            print(f"Access Token: {token}")
            return token
        else:
            print("Login successful, but no token received.")
            return None
    else:
        print(f"Status code: {response.status_code}")
        print("Response:", response.json())
        

# Get the login token and run the test test_login
token = test_login()


```

## try to implement the test for endpoint {BASE_URL}/products 

```py

def add_one_product(token): # token is used and taken from the login_test above 

    """
    Test the /products endpoint by adding a new product.
    Uses the provided token for authorization in the Authorization header.
    """
    
    # Define the URL for the /products endpoint to add a new product
   
    
    # Prepare the product data to be sent in the request body

    product_data = {

         # Name of the product
         # Description of the product
    }
    
    # Prepare the headers with the Authorization token (Bearer token) for authorization

    headers = {
         # Token for authorization
         # Specify the content type as JSON
    }
    
    # Send a POST request to the /products endpoint with the product data and headers

    """
    Implement assertions here below for the post request 

    """
   
    # Check if the server responded with status code 200 (OK)
  
    # If successful, print the status code and the product details returned by the server

    # The response should include product details returned
    
    # If the request failed, print the status code and the error response from the server
        

```

5## How to run the tests ? 

Be in the backend folder where your own pythonfile with the requests are 

run following command. It´can be python3 instead of python for linux/macOS users 

```py 

python (filename of python)

python3 (filename of python)

```




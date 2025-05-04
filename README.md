# Educational Coding Assignment: Building a POST Endpoint with LiteLLM Integration

## 1. Overview of the assignment

In this assignment, you will design and implement a server-side POST endpoint that accepts user input in JSON format, processes the input through LiteLLM (a lightweight language model), and returns the generated response. This exercise aims to enhance your understanding of RESTful API development, handling JSON data, and integrating language models into web applications.

## 2. Learning objectives

- Understand how to create a POST API endpoint using a web framework (e.g., Flask, Express, FastAPI)
- Learn how to parse and validate JSON request data
- Integrate LiteLLM for text generation
- Handle responses and error cases appropriately
- Test API endpoints effectively

*(Note: The assignment does not specify a particular programming language or framework; adapt instructions accordingly.)*

## 3. Prerequisites and setup instructions

### Prerequisites

- Basic knowledge of Python (or your chosen language)
- Familiarity with RESTful API concepts
- Python 3.8+ installed on your system
- pip (Python package installer)

### Setup instructions

1. **Create a project directory:**

```bash
mkdir lite_llm_api
cd lite_llm_api
```

2. **Set up a virtual environment (optional but recommended):**

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install necessary packages:**

```bash
pip install fastapi uvicorn pydantic lite-llm
```

*(Note: Replace `lite-llm` with the actual package name if different.)*

4. **Create your main application file:**

```bash
touch main.py
```

## 4. Step-by-step guide to completing the assignment

### Step 1: Import necessary modules

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import lite_llm  # Replace with actual LiteLLM import if different
```

### Step 2: Define data models

```python
class UserInput(BaseModel):
    message: str
```

### Step 3: Initialize the FastAPI app and LiteLLM model

```python
app = FastAPI()

# Initialize LiteLLM model (assuming a simple load method)
llm_model = lite_llm.load_model()
```

### Step 4: Create the POST endpoint

```python
@app.post("/generate")
async def generate_response(user_input: UserInput):
    try:
        prompt = user_input.message
        # Generate response using LiteLLM
        response_text = llm_model.generate(prompt)
        return {"response": response_text}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))
```

### Step 5: Run the server

```bash
uvicorn main:app --reload
```

Your API will be accessible at `http://127.0.0.1:8000`.

## 5. Explanation of key concepts

- **POST Endpoint:** An API route that accepts data sent in the request body, typically used for creating or processing resources.
- **JSON Data Handling:** Using Pydantic models to parse and validate incoming JSON payloads.
- **LiteLLM Integration:** Loading and utilizing a lightweight language model to generate text based on user input.
- **Error Handling:** Using try-except blocks and HTTP exceptions to manage runtime errors gracefully.
- **Server Running:** Using Uvicorn to serve the FastAPI application with hot-reload enabled for development.

## 6. Testing instructions

### Using cURL

```bash
curl -X POST "http://127.0.0.1:8000/generate" -H "Content-Type: application/json" -d '{"message": "Hello, how are you?"}'
```

### Using Python requests

```python
import requests

url = "http://127.0.0.1:8000/generate"
payload = {"message": "Tell me a joke."}
response = requests.post(url, json=payload)
print(response.json())
```

### Validating responses

- Ensure the response contains a `"response"` key with generated text.
- Test with invalid data (e.g., missing `"message"`) to verify error handling.

## 7. Additional resources for further learning

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Pydantic Models](https://pydantic.dev/)
- [LiteLLM Documentation](https://lite-llm.readthedocs.io/) *(Replace with actual link if available)*
- [Building REST APIs with Python](https://realpython.com/api-integration-in-python/)
- [Understanding HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

---

**Happy coding!**  
Feel free to extend this assignment by adding features such as input validation, logging, or deploying your API to a cloud platform.
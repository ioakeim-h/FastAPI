A web page communicates with a FastAPI server by sending HTTP requests, and the server responds back with the appropriate data or action.

HTTP request methods are commonly associated with CRUD operations, with each operation using a specific HTTP verb:

| CRUD   | HTTP Request Method |
| ------ | ------------------- |
| Create | POST                |
| Read   | GET                 |
| Update | PUT                 |
| Delete | DELETE              |

In FastAPI, each CRUD operation corresponds to an endpoint, which is a URL path segment that handles a specific type of request.

## GET request 

A client attempts to retrieve information from the API when it makes a `GET` request

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/hello") # /hello is the endpoint
async def say_hello():
    return {"message": "Hello, World!!!"} # JSON

# Run methods:
# uvicorn myscript:app --reload
# fastapi dev myscript.py
# fastapi run myscript.py

```

`@app.get()` lets FastAPI know that at the path `"/hello"` we are going to be returning the `say_hello()` function. The endpoint is the URL, the function is what decides the response, and the `GET` request retrieves that response. A `GET` request is sent whenever a client asks a server for data from a specific URL. 

In the example above, the data are available via http://localhost:8000/hello. 
There are a few common ways to access it:
1. Browser: Simply enter the URL in the address bar
2. Command line: `curl http://localhost:8000/hello`
3. Python: `requests.get("http://localhost:8000/hello")`


## FastAPI Swagger UI

FastAPI Swagger UI is an automatic web interface created by FastAPI, accessible at the `/docs` endpoint. It lets you explore, test, and document your API endpoints.

* **Interactive docs** – Displays all endpoints with their methods (GET, POST, etc.), inputs, and outputs.
* **Try endpoints** – Send requests directly from the browser, including parameters or JSON, and view responses immediately.

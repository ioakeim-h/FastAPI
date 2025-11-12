A web page communicates with a FastAPI server by sending HTTP requests, and the server responds back with the appropriate data or action.

HTTP request methods are commonly associated with CRUD operations, with each operation using a specific HTTP verb:

| CRUD   | HTTP Request Method |
| ------ | ------------------- |
| Create | POST                |
| Read   | GET                 |
| Update | PUT                 |
| Delete | DELETE              |

In FastAPI, each CRUD operation corresponds to an endpoint, which is a URL path segment that handles a specific type of request.

##  Create a GET request 

A client attempts to retrieve information from the API when it makes a `GET` request. The data is available via the endpoint - http://localhost:8000/api-endpoint in the example below.

```python
from fastapi import FastAPI
import uvicorn

app = FastAPI()

@app.get("/api-endpoint")
async def api_endpoint():
    return {"message": "Hello, World!!!"}

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

The endpoint is the URL, the function is what decides the response, and a `GET` request retrieves that response. A `GET` request is sent whenever a client asks a server for data from a specific URL. There are a few common ways to do it:

1. Browser: Simply enter the endpoint URL in the address bar
2. Command line: `curl http://localhost:8000/api-endpoint`
3. Python: `requests.get("http://localhost:8000/api-endpoint")`
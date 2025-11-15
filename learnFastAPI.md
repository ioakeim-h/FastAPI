A web page communicates with a FastAPI server by sending HTTP requests, and the server responds back with the appropriate data or action.

HTTP request methods are commonly associated with CRUD operations, with each operation using a specific HTTP verb:

| CRUD   | HTTP Request Method |
| ------ | ------------------- |
| Create | POST                |
| Read   | GET                 |
| Update | PUT                 |
| Delete | DELETE              |

In FastAPI, each CRUD operation corresponds to an endpoint, which is a URL path segment that handles a specific type of request.

# Static Paths

## GET request 

A client attempts to retrieve information from the API when it makes a `GET` request

```python
from fastapi import FastAPI

# Data
BOOKS = [
    {'title': 'Title One', 'author': 'Author One', 'category': 'science'},
    {'title': 'Title Three', 'author': 'Author Three', 'category': 'history'},
    {'title': 'Title Four', 'author': 'Author Four', 'category': 'math'},
]

app = FastAPI()

@app.get("/books") # /books is the endpoint 
async def read_all_books():
    return BOOKS

# Run methods:
# uvicorn myscript:app --reload
# fastapi dev myscript.py
# fastapi run myscript.py

# Response:
#     [
#         {'title': 'Title One', 'author': 'Author One', 'category': 'science'},
#         {'title': 'Title Three', 'author': 'Author Three', 'category': 'history'},
#         {'title': 'Title Four', 'author': 'Author Four', 'category': 'math'},
#     ]
```

`@app.get()` lets FastAPI know that at the endpoint `"/books"` we are going to be returning the `read_all_books()` function. The endpoint is the path, the function is what decides the response, and the `GET` request retrieves that response. 

In the example above, the response is available at localhost, which often uses port 8000 by default, though the port can be changed.
http://localhost:8000/books

Common ways to access it:
1. Browser: Simply enter the URL in the address bar
2. Command line: `curl http://localhost:8000/books`
3. Python: `requests.get("http://localhost:8000/books")`



# Dynamic Path Parameters

A dynamic path parameter is a value that gets passed into the endpoint through the URL. Imagine a website where you can look up any book. Instead of creating a separate page for every book, you make one page that changes based on the book’s ID.

So instead of creating several static paths like:
- `/books/philokalia`
- `/books/life-of-st-antonios`
- `/books/way-of-a-pilgrim`

You make one dynamic path parameter: `/books/{book_title}`

The `{book_title}` part is a placeholder.
When someone visits `/books/philokalia`, the server takes `"philokalia"` and shows the information for that book.
When someone visits `/books/life-of-st-antonios`, it shows the information for that book.

```python
from fastapi import FastAPI

BOOKS = [
    {'title': 'Title One', 'author': 'Author One', 'category': 'science'},
    {'title': 'Title Three', 'author': 'Author Three', 'category': 'history'},
    {'title': 'Title Four', 'author': 'Author Four', 'category': 'math'},
]

app = FastAPI()

@app.get("/books/{book_title}") # /books is the endpoint, {book_title} is the path parameter 
async def read_all_books(book_title):
    for book in BOOKS:
        if book.get("title").lower() == book_title.lower():
            return book

# Request: curl "http://localhost:8000/books/Title%20One"
# Reponse: {'title': 'Title One', 'author': 'Author One', 'category': 'science'}
```

Notes: 
- Order matters when defining path parameters in FastAPI. If you have a dynamic route (one with a variable path parameter) before a static route (one with a fixed path), the dynamic route will match requests first, preventing the static route from ever being reached. As a general rule, add static APIs before dynamic.
- An API URL cannot have spaces - replace those with `%20`










## FastAPI Swagger UI

FastAPI Swagger UI is an automatic web interface created by FastAPI, accessible at the `/docs` endpoint. It lets you explore, test, and document your API endpoints.

* **Interactive docs** – Displays all endpoints with their methods (GET, POST, etc.), inputs, and outputs.
* **Try endpoints** – Send requests directly from the browser, including parameters or JSON, and view responses immediately.





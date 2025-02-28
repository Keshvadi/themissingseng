---
title: APIs
parent: Web Fundamental
nav_order: 86
layout: default
---

## APIs (Application Programming Interfaces)

An API, or Application Programming Interface, is a set of rules and specifications that allows different software applications to communicate with each other. Think of it as a contract that defines how one piece of software can request services or data from another. In web development, APIs are crucial for connecting front-end applications (running in the browser) to back-end services (running on servers).

---

### Key Concepts

- **Client:** The application that _makes_ a request to the API (e.g., a web browser, a mobile app, another server).
- **Server:** The application that _provides_ the API and responds to requests.
- **Request:** A message sent from the client to the server, asking for data or an action. Requests include:
  - **Method:** The HTTP method (verb) indicating the desired action (e.g., `GET`, `POST`, `PUT`, `DELETE`, `PATCH`).
  - **URL (Endpoint):** The specific address on the server where the resource or service is located.
  - **Headers:** Metadata about the request (e.g., content type, authentication tokens).
  - **Body (optional):** Data sent with the request (e.g., form data, JSON payload).
- **Response:** A message sent from the server back to the client, containing the result of the request. Responses include:
  - **Status Code:** A three-digit number indicating the success or failure of the request (e.g., `200 OK`, `404 Not Found`, `500 Internal Server Error`).
  - **Headers:** Metadata about the response (e.g., content type).
  - **Body (optional):** Data returned by the server (e.g., JSON data, HTML, XML).
- **Resource:** A piece of data or a service that can be accessed via the API (e.g., a user, a product, a list of blog posts).
- **Endpoint:** A specific URL where a resource or service can be accessed.
- **REST (Representational State Transfer):** A common architectural style for designing APIs, especially web APIs. RESTful APIs use standard HTTP methods to interact with resources, and they often use JSON for data exchange.

---

### Common HTTP Methods (Verbs)

- **`GET`:** Retrieves data from the server. `GET` requests should _not_ have side effects (they should be read-only).
- **`POST`:** Sends data to the server to create a _new_ resource. Often used for form submissions or creating new records in a database.
- **`PUT`:** Updates an _existing_ resource completely. The client sends the entire updated representation of the resource.
- **`PATCH`:** Updates an _existing_ resource partially. The client sends only the fields that need to be changed.
- **`DELETE`:** Deletes a resource.

---

### Example: Interacting with a RESTful API (using `fetch` in JavaScript)

Imagine a simple API for managing a list of books.

- **Get all books:**

  ```javascript
  fetch("/api/books") // GET request to /api/books
    .then((response) => response.json()) // Parse the JSON response
    .then((data) => console.log(data)); // Log the data (an array of books)
  ```

- **Get a specific book:**

  ```javascript
  fetch("/api/books/123") // GET request to /api/books/123 (book with ID 123)
    .then((response) => response.json())
    .then((data) => console.log(data));
  ```

- **Create a new book:**

  ```javascript
  fetch("/api/books", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      title: "My New Book",
      author: "John Doe",
      year: 2023,
    }),
  })
    .then((response) => response.json())
    .then((data) => console.log(data)); // Log the newly created book (including its ID)
  ```

- **Update a book:**

  ```javascript
  fetch("/api/books/123", {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      title: "Updated Title",
      author: "John Doe",
      year: 2024,
    }),
  })
    .then((response) => response.json())
    .then((data) => console.log(data));
  ```

- **Delete a book:**

  ```javascript
  fetch("/api/books/123", {
    method: "DELETE",
  }).then((response) => {
    if (response.ok) {
      console.log("Book deleted successfully");
    } else {
      console.error("Error deleting book");
    }
  });
  ```

- **Example JSON Response (for `GET /api/books`):**

  ```json
  [
    {
      "id": 1,
      "title": "The Hitchhiker's Guide to the Galaxy",
      "author": "Douglas Adams",
      "year": 1979
    },
    {
      "id": 2,
      "title": "Pride and Prejudice",
      "author": "Jane Austen",
      "year": 1813
    }
  ]
  ```

- **Example Status Codes:**

  - **2xx (Success):**
    - `200 OK`: The request was successful.
    - `201 Created`: A new resource was created (often returned by `POST` requests).
    - `204 No Content`: The request was successful, but there's no content to return (common for `DELETE` requests).
  - **4xx (Client Error):**
    - `400 Bad Request`: The request was malformed or invalid.
    - `401 Unauthorized`: Authentication is required, or the provided credentials are invalid.
    - `403 Forbidden`: The client is authenticated, but doesn't have permission to access the resource.
    - `404 Not Found`: The requested resource was not found.
    - `405 Method Not Allowed`: Request method is not supported for the requested resource.
  - **5xx (Server Error):**
    - `500 Internal Server Error`: A generic server error.
    - `502 Bad Gateway`: The server, while acting as a gateway, received an invalid response from another server.
    - `503 Service Unavailable`: The server is temporarily unavailable.

---

### API Documentation

Good API documentation is _essential_. It explains how to use the API, including:

- Available endpoints (URLs).
- Supported HTTP methods for each endpoint.
- Request parameters (including data types and whether they are required or optional).
- Expected request body format (for `POST`, `PUT`, `PATCH`).
- Possible response status codes and their meanings.
- Response body format (e.g., JSON schema).
- Authentication requirements.
- Examples.

Common formats for API documentation include:

- **Swagger/OpenAPI:** A widely used specification for describing RESTful APIs. Tools like Swagger UI can generate interactive documentation from an OpenAPI definition.
- **RAML (RESTful API Modeling Language):** Another specification for describing RESTful APIs.
- **API Blueprint:** A Markdown-based format for describing APIs.

## Well-documented APIs are much easier to use and integrate with.

---
title: Backend Basics
parent: Web Fundamental
nav_order: 85
layout: default
---

## Backend Basics

The backend of a web application is the part that users _don't_ see. It's the "server-side" of the application, responsible for handling data storage, logic, and communication with the frontend (the client-side, what users interact with in their browsers). Think of a restaurant: the frontend is the dining room, tables, and menu that customers see; the backend is the kitchen, chefs, and all the processes that happen behind the scenes to prepare and deliver the food.

---

### Core Concepts

- **Server:** A computer (or program) that provides services to other computers (clients) over a network. For web applications, the server responds to requests from web browsers (clients).
- **Database:** An organized collection of data. Web applications use databases to store user information, product details, content, and anything else that needs to be persistent. Common database types include:
  - **Relational Databases (SQL):** Data is organized into tables with rows and columns (e.g., PostgreSQL, MySQL, MariaDB, SQL Server, Oracle).
  - **NoSQL Databases:** Data is stored in various formats (document, key-value, graph, etc.), often more flexible than relational databases (e.g., MongoDB, Cassandra, Redis, DynamoDB).
- **API (Application Programming Interface):** A set of rules and specifications that define how different software components interact. In web development, APIs often use HTTP requests to exchange data (usually in JSON or XML format) between the client (frontend) and the server (backend).
- **HTTP Requests:** The fundamental way clients and servers communicate on the web. Common HTTP methods include:
  - **GET:** Retrieves data from the server (e.g., fetching a web page, getting a list of products).
  - **POST:** Sends data to the server to create or update a resource (e.g., submitting a form, creating a new user account).
  - **PUT:** Updates an entire existing resource.
  - **PATCH:** Partially updates an existing resource.
  - **DELETE:** Deletes a resource.
- **REST (Representational State Transfer):** An architectural style for designing networked applications. RESTful APIs use standard HTTP methods (GET, POST, PUT, DELETE) to interact with resources (represented by URLs). REST is a very common pattern for web APIs.
- **Authentication:** Verifying the identity of a user (e.g., using a username and password).
- **Authorization:** Determining what a user is allowed to do (e.g., restricting access to certain resources based on user roles).
- **Server-Side Languages:** Programming languages used to write backend logic. Popular choices include:
  - **Python** (with frameworks like Django, Flask)
  - **JavaScript** (with Node.js and frameworks like Express.js)
  - **Java** (with frameworks like Spring Boot)
  - **Ruby** (with Ruby on Rails)
  - **PHP** (with frameworks like Laravel, Symfony)
  - **Go**
  - **C#** (with .NET)
- **Frameworks:** Collections of pre-written code and tools that simplify backend development. Frameworks provide structure, common functionalities (like routing, database interaction, and templating), and security features.
- **Deployment:** The process of making your backend application available on a server so that users can access it. This often involves using cloud platforms (like AWS, Google Cloud, Azure) or containerization (Docker).
- **ORM:** Object-Relational Mapping (ORM) is a technique that lets you query and manipulate data from a database using an object-oriented paradigm.
- **MVC:** Model-View-Controller (MVC) is a software design pattern commonly used for developing user interfaces that divides the related program logic into three interconnected elements.

---

### Example: A Simple Backend Interaction

1.  **Client Request:** A user clicks a button on a website (the frontend) to view a list of products. The frontend sends an HTTP GET request to the backend API endpoint `/api/products`.
2.  **Server Processing:** The backend server receives the request.
3.  **Database Query:** The backend code (written in Python, Node.js, etc.) queries the database to retrieve the product data.
4.  **Response:** The server formats the product data (usually as JSON) and sends it back to the client in an HTTP response.
5.  **Client Rendering:** The frontend (JavaScript code) receives the JSON data and updates the web page to display the list of products.

---

### Basic Backend Tasks

- **Handling Requests:** Receiving and processing HTTP requests from the frontend.
- **Routing:** Mapping URLs to specific functions or handlers in your backend code.
- **Database Interaction:** Connecting to a database, querying data, inserting/updating/deleting data.
- **Business Logic:** Implementing the core logic of your application (e.g., validating user input, processing payments, sending emails).
- **Authentication and Authorization:** Securing your application and controlling user access.
- **API Development:** Creating and managing APIs for the frontend (or other applications) to interact with.
- **Error Handling:** Gracefully handling errors and providing informative responses.
- **Testing:** Writing automated tests to ensure the backend code works correctly.
- **Deployment** Deploying and make the application accessible.

This is a high-level overview of backend basics. Building a backend application involves learning a server-side language, a framework, database concepts, and API design principles. The next section (APIs) will go into more detail about APIs, which are a fundamental part of modern web development.

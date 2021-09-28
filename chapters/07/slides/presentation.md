class: dark middle

# Enterprise Web Development C&#35;
> Chapter 7 - The REST is still unwritten
---

### Chapter 7 - The REST is still unwritten
# Table of contents

TODO: complete ToC

---
name: what-rest
class: dark middle

# The REST is still unwritten
> What is REST?

---
### The REST is still unwritten
# What is REST?

- **R**epresentational **S**tate **T**ransfer
- introduced and defined in 2000 by Roy Fielding in his [doctoral dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)

<br />

> Representational State Transfer is inteded to evoke an image of how a well-designed Web application behaves: a network of web pages (a virtual state machine), where the user progresses through an application by selecting links (state transitions), resulting in the next page (representing the next state of the application) being transferred to the user and rendered for their use.

<p style="text-align:right;"><em>Roy Fielding</em></p>

---
### The REST is still unwritten
# What is REST?

- **architectural style** for designing networked applications
- nothing more but **using current features of the web**
  - 40y old matured and widely accepted HTTP protocol
  - standard and unified methods (POST, GET, PUT and DELETE)
  - stateless nature of HTTP
  - easy to use **U**niform **R**esource **I**dentifier
- leverages these features with some constraints: **7 principles**

---
### What is REST?
# Principle 1

> Everything is **Resource**

- fundamental concept of REST
- has
  - data
  - relationships to other resources
  - methods that operates against it to allow for accessing and manipulating the associated information

Examples:
- [www.hogent.be/image/logo.gif]() (Image resource)
- [www.hogent.be/students/1001]() (Dynamically pulled resource)
- [www.hogent.be/videos/v001]() (Video resource)
- [www.hogent.be/home.html]() (Static resource)

---
### What is REST?
# Principle 2

> Every resource is identified by a **Unique Identifier**

- **U**nifirm **R**esource **L**ocator identifies the online location of a resource
- directory structure-like URIs

Examples:
- Get customer details with name "Shiv": [www.hogent.be/Customers/Shiv]()
- Get customer details with name "Raju": [www.hogent.be/Customers/Raju]()
- Get orders for customer "Shiv": [www.hogent.be/Customers/Shiv/Orders]()
- Get orders for customer "Raju": [www.hogent.be/Customers/Raju/Orders]()

---
### What is REST?
# Principle 3

> Describe resource **functionality** with **HTTP methods**

.center[
| Method | Description                             |
| ------ | --------------------------------------- |
| GET    | retrieve a representation of a resource |
| POST   | create new resources and sub-resources  |
| PUT    | update existing resources               |
| PATCH  | partially update existing resources     |
| DELETE | delete existing resources               |
]

This ensures **uniform interfaces** accross multiple REST APIs

---
### Principle 3
# Examples (1/2)

- `/orders`:
  - GET: list all orders
  - POST: create a new order
  - PUT/DELETE: unused


- `/orders/{id}`:
  - GET: get order details
  - POST: add item
  - PUT: update order
  - DELETE: delete an order

---
### Principle 3
# Examples (2/2)

- `/customers/{id}/orders`:
  - GET: get orders for customer
  - POST: add order
  - PUT: unused
  - DELETE: cancel all customer orders

---
### What is REST?
# Principle 4

> Communication is done by **Representation**

- use some **media type**
  - often XML (`application/xml`)
  - or JSON (`application/json`)
- set the appropriate **HTTP headers**
  - `Accept`: what do you expect as input?
  - `Content-Type`: what are you returning?

---
### What is REST?
# Principle 5

> Responses: give **feedback** to help developers succeed

- helps using an API
- helps debugging errors
- use the correct **HTTP response code**
  - and provide some **message** in the body

---
### Principle 5
# HTTP status ranges in a nutshell

- `1xx`: hold on
- `2xx`: here you go
- `3xx`: go away
- `4xx`: you fucked up
- `5xx`: I fucked up

> <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes" target="_blank">Read about all HTTP status codes yourself</a>

---
### What is REST?
# Principle 6

> Be **stateless**

- every request is independent
- server does not need to remember previous requests and state

<br />
<img src="./images/REST-stateless.png" width="70%" class="center" />

---
### What is REST?
# Principle 7

> **Document** your API

- OpenAPI = specification
- Swagger = tools (for displaying OpenAPI specs, etc.)

<br />
<img src="./images/openapi-swagger.png" width="50%" class="center" />

---
### Principle 7
# OpenAPI

- **O**pen**A**PI **S**pecification (OAS)
- formerly known as Swagger
- YAML or JSON
- standard, programming language independent description of a REST API
- only specifies functionality
  - not which implementation
  - not what dataset
  - ...
- **OAS 3.0**: both people and machines can view, understand and interpret the functionality of a REST API
- from documentation the client code can be generated

---
### Principle 7
# swagger.json

```{json}
{
  "swagger":"2.0",
  "info":{
    "description":"This is a sample server Petstore server.  You can find out more about Swagger at [http://swagger.io](http://swagger.io) or on [irc.freenode.net, #swagger](http://swagger.io/irc/).  For this sample, you can use the api key `special-key` to test the authorization filters.",
    "version":"1.0.5",
    "title":"Swagger Petstore",
    "termsOfService":"http://swagger.io/terms/",
    "contact":{
      "email":"apiteam@swagger.io"
    }
  },
  "host":"petstore.swagger.io",
  "basePath":"/v2",
}
```

> <a href="https://petstore.swagger.io/v2/swagger.json" target="_blank">Take a look at a live example (you might need a JSON prettifier)</a>

---
### Principle 7
# Swagger UI

- to visualize and interact with the API's resources
- auto-generated from OAS

<img src="./images/swagger-ui.png" width="90%" class="center" />

---
### What is REST?
# Consumer

Who can consume a REST API?

- MVC application
- SPA application (Blazor, Angular, React, Vue...)
- The Swagger UI
- Postman app
- ...

---
### What is REST?
# Summary

- **not a standard**
- set of 6 **constraints** to call an API **RESTful**
  - Uniform interface
  - Client-server separated
  - Stateless
  - Cachable
  - Layered system
  - Code on demand (optional)

> <a href="https://restfulapi.net/rest-architectural-constraints/" target="_blank">Read more about it</a>

---
name: building-rest-api
class: dark middle

# The REST is still unwritten
> Building a REST API


---
class: dark middle

# The REST is still unwritten
> Input validation

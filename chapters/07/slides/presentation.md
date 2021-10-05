class: dark middle

# Enterprise Web Development C&#35;
> Chapter 7 - The REST is still unwritten
---

### Chapter 7 - The REST is still unwritten
# Table of contents

- [What is an API?](#api)
- [What is REST?](#rest)
- [HTTP methods and status ranges](#http)
- [Document your API](#documentation)
- [Building a REST API](#building-rest-api)
- [Input validation](#input-validation)
- [Summary](#summary)

---
name: building-rest-api
class: dark middle

# The REST is still unwritten
> Building a REST API


---
class: dark middle

# The REST is still unwritten
> Input validation

---
name: api
class: dark middle

# The REST is still unwritten
> What is an API?

---
### The REST is still unwritten
# What is an API?

* **A**pplication **P**rogramming **I**nterface
* approach to make software work with other software
* <=> User Interface: let's users work with software
* nowadays mostly in the context of the Web (HTTP)

---
name: rest
class: dark middle

# The REST is still unwritten
> What is REST?

---
### The REST is still unwritten
# What is REST?

- **R**epresentational **S**tate **T**ransfer, [°Roy Fielding in 2000](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
- **architectural style** for designing networked applications
- nothing more but **using current features of the web**
  - 40y old matured and widely accepted HTTP protocol
  - standard and unified methods (POST, GET, PUT and DELETE)
  - stateless nature of HTTP
  - easy to use **U**niform **R**esource **I**dentifier

---
### The REST is still unwritten
# What is REST?

- leverages these features with 5 constraints:
  - uniform interface
  - client-server
  - stateless
  - cachable
  - layered system

---
### What is REST?
# Uniform interface

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
# Uniform interface

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
# Uniform interface

> Communication is done by **Representation**

- use some **media type**
  - often JSON (`application/json`)
  - or XML (`application/xml`)
- set the appropriate **HTTP headers**
  - `Accept`: what do you expect as input?
  - `Content-Type`: what are you returning?

---
### What is REST?
# Client-Server

* client and server should be able to evolve independently
* client should be able to do all it needs with the available resource URI's

---
### What is REST?
# Stateless

- every request is independent
- server does not need to remember previous requests and state
- no sessions, no history...

<br />
<img src="./images/REST-stateless.png" width="70%" class="center" />

---
### What is REST?
# Cacheable

* all responses should be made cachable (if possible)
* good caching ensures the server scales better (less requests to process)
* and the client responds faster

---
### What is REST?
# Layered System

* REST allows to spread data and API over several servers
* example:
  * Server A: API
  * Server B: data storage
  * Server C: authentication
* big advantage: servers are able to scale independently

---
name: http
class: dark middle

# The REST is still unwritten
> HTTP methods and status ranges

---
### What is REST?
# HTTP methods

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
### What is REST?
# HTTP status ranges in a nutshell

- `1xx`: hold on
- `2xx`: here you go
- `3xx`: go away
- `4xx`: you fucked up
- `5xx`: I fucked up

> <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes" target="_blank">Read about all HTTP status codes yourself</a>

---
name: documentation
class: dark middle

# The REST is still unwritten
> Document your API

---
### The REST is still unwritten
# Document your API

- OpenAPI = specification
- Swagger = tools (for displaying OpenAPI specs, etc.)

<br />
<img src="./images/openapi-swagger.png" width="50%" class="center" />

---
### Document your API
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
### Document your API
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
### Document your API
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
name: building-rest-api
class: dark middle

# The REST is still unwritten
> Building a REST API


---
name: input-validation
class: dark middle

# The REST is still unwritten
> Input validation

---
name: summary
class: dark middle

# The REST is still unwritten
> Summary

---
### The REST is still unwritten
# Summary

- REST is **not a standard**
- set of **5 constraints** to call an API **RESTful**
  - Uniform interface
  - Client-server separated
  - Stateless
  - Cachable
  - Layered system

> <a href="https://restfulapi.net/rest-architectural-constraints/" target="_blank">Read more about it</a>

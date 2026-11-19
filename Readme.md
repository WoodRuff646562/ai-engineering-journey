# Day 02 – Postman API Practice

## Overview

This folder contains my Postman collections created while learning API fundamentals, HTTP methods, request/response handling, JSON data, and API authentication.

The goal was to understand how APIs work through practical exercises rather than only studying theory.

## Tools & Technologies

- **Postman** – API testing and debugging
- **JSON** – Data exchange format
- **HTTP** – Communication protocol
- **JSONPlaceholder** – Practice REST API
- **DummyJSON** – Authentication practice API

## Collection Structure

### 1. HTTP Methods Demo

Practised the fundamental HTTP methods using JSONPlaceholder.

| Method | Purpose | Exercise |
|---|---|---|
| GET | Retrieve data | Fetch users |
| POST | Create data | Create a user |
| PUT | Replace data | Update a user |
| PATCH | Partially update data | Modify user information |
| DELETE | Delete data | Delete a user |

**Base URL:** `https://jsonplaceholder.typicode.com`

### 2. HTTP Method Practice

A separate collection containing additional HTTP method exercises completed during the learning process.

Topics include:
- GET requests
- POST requests
- PATCH requests
- PUT requests

### 3. Authorization Demo

Practised API authentication using Bearer Tokens with DummyJSON.

**API endpoints:**

- Login: `POST https://dummyjson.com/auth/login`
- Protected profile: `GET https://dummyjson.com/auth/me`

Topics learned:
- Authentication and authorization
- Access tokens
- Refresh tokens
- Authorization headers
- Bearer Token authentication
- HTTP 401 Unauthorized responses

## Key Concepts Learned

- Difference between API requests and responses
- HTTP status codes (200, 201, 400, 401, 403, 404, 500)
- Request methods: GET, POST, PUT, PATCH and DELETE
- Headers, query parameters and request bodies
- JSON objects, arrays and nested data
- Path parameters vs. query parameters
- Authentication using Bearer Tokens
- Difference between authentication and authorization

## Important Notes

**JSONPlaceholder:** This is a practice API. POST, PUT, PATCH and DELETE demonstrate API responses but do not permanently modify the underlying data.

**Security:** Never commit real access tokens, refresh tokens, API keys or passwords to GitHub. Replace sensitive values with placeholders before exporting or committing collections.

## Learning Outcome

By completing these exercises, I gained practical experience with REST API testing, HTTP methods, JSON responses, request configuration and token-based authentication.

These fundamentals will support my next learning stages in Python, backend development and AI application engineering.

---

**Learning Journey:** AI Engineering Journey  
**Day:** 02  
**Status:** Completed
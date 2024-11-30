# Flask Authentication and User Management API

This project provides a robust authentication and user management system built with Flask. It includes JWT-based authentication, user role management, and admin-specific privileges for managing users. The project is designed to be a modular and extensible foundation for building secure web applications.

---

## Features

- **JWT Authentication**:
  - Access and refresh token handling.
  - Secure routes protected by JWT.
  - Custom error responses for invalid, expired, or missing tokens.

- **User Management**:
  - User registration with hashed passwords.
  - Login endpoint to issue tokens.
  - Fetch current user details via protected endpoints.
  - Admin-only access to list all users with pagination.

- **Role-Based Access Control**:
  - Claims-based permissions.
  - Assign admin privileges to specific users.

---
## Installation and Setup

### Prerequisites
- Python 3.8 or higher
- A supported database (e.g., SQLite, PostgreSQL, MySQL)

```
# Project Setup Guide

Follow these steps to set up and run the project:

---

## 1. Create and Activate a Virtual Environment

```bash
1. python -m venv venv
2. source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
3. pip install -r requirements.txt
4. export FLASK_APP=main.py  # On Windows $env:FLASK_APP = "main.py"
5. flask shell
  5.1 db
  5.2 from models import User
  5.3 db.create_all()
6. exit shell ctrl+z

7. python
  7.1 import secrets
  7.2 secrets.tokens_hex(12)

8. create .env file paste these variables

FLASK_SECRET_KEY={random text}
FLASK_DEBUG=True
FLASK_SQLALCHEMY_DATABASE_URI=sqlite:///db.sqlite3
FLASK_SQLALCHEMY_ECHO=True
FLASK_JWT_SECRET_KEY={generated at step 7.2}

9. Exit 

10. flask run

```


## Usage
  Use postman or any other HTTP request app
  - First register user with register api
  - Login with the user with login api
    - Copy the access token, this we will use as bearer token for rest of the steps.
  -  /users/all api is allowed for admins only, currently the username prince is considerd as admin.


### API Endpoints

#### **Authentication (`/auth`)**

1. **Register**:
   - **POST** `/auth/register`
   - **Body**:
     ```json
     {
       "username": "user1",
       "email": "user1@example.com",
       "password": "securepassword"
     }
     ```

2. **Login**:
   - **POST** `/auth/login`
   - **Body**:
     ```json
     {
       "username": "user1",
       "password": "securepassword"
     }
     ```

3. **Who Am I**:
   - **GET** `/auth/whoami`  
   - Requires access token.

4. **Refresh Token**:
   - **GET** `/auth/refresh`  
   - Requires refresh token.

---

#### **User Management (`/users`)**

1. **List Users (Admin Only)**:
   - **GET** `/users/all`
   - **Query Parameters**:
     - `page`: Page number (default: 1)
     - `per_page`: Items per page (default: 5)

---

### Dependencies

Key dependencies included in `requirements.txt`:

- **Flask**: Web framework.
- **Flask-JWT-Extended**: JWT-based authentication.
- **Flask-SQLAlchemy**: ORM for database interactions.
- **Marshmallow**: Data serialization and validation.

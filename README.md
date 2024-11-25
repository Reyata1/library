Sure! Below is a more specific and detailed version of the **`README.md`** file, tailored to the API routes, payloads, and database interactions based on the code provided.

---

# Library Management System API Documentation

This RESTful API is designed for managing users, books, authors, and their relationships within a library system. The API allows users to register, authenticate, and interact with books and authors in a MySQL database. It also supports handling book-author relationships.

## Table of Contents

- [Overview](#overview)
- [Setup Instructions](#setup-instructions)
- [API Endpoints](#api-endpoints)
  - [User Endpoints](#user-endpoints)
  - [Author Endpoints](#author-endpoints)
  - [Book Endpoints](#book-endpoints)
  - [Book-Author Relationship Endpoints](#book-author-relationship-endpoints)
- [Database Schema](#database-schema)
- [Technology Stack](#technology-stack)

---

## Overview

The API provides functionality for:

1. **User Registration and Authentication**: Allows users to register, log in, and authenticate using JWT tokens.
2. **CRUD Operations for Authors**: Enables the creation, retrieval, updating, and deletion of authors.
3. **CRUD Operations for Books**: Enables managing books in the system.
4. **Book-Author Relationships**: Manages the relationship between books and authors.

---

## Setup Instructions

### Prerequisites

- PHP 7.4 or higher
- MySQL
- Composer

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repository.git
   cd your-repository
   ```

2. Install project dependencies:
   ```bash
   composer install
   ```

3. Set up the MySQL database:
   - Create a database named `lib_db` in MySQL.
   - Use the provided SQL schema to create the necessary tables.

4. Run the PHP built-in server:
   ```bash
   php -S localhost:8080 -t public
   ```

5. The API is now accessible at `http://localhost:8080`.

---

## API Endpoints

### User Endpoints

#### **POST `/user/register`**

Registers a new user. 

**Request Body:**
```json
{
    "username": "Joshua C. Miranda",
    "password": "123"
}
```

**Response:**
- Success: 
  ```json
  {
    "status": "success",
    "data": null
  }
  ```
- Failure (Username already registered):
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Username is already registered!"
    }
  }
  ```

#### **POST `/user/auth`**

Authenticates a user and returns a JWT token.

**Request Body:**
```json
{
    "username": "Joshua C. Miranda",
    "password": "123"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "jwt_token_here",
    "data": null
  }
  ```
- Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Authentication Failed"
    }
  }
  ```

#### **GET `/user/show`**

Fetches a list of all users (requires JWT token for authorization).

**Headers:**
```json
{
  "Authorization": "{token}"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": [
    {
      "user_id": "4",
      "username": "Joshua Miranda"
    },
    {
      "user_id": "5",
      "username": "Joshua C. Miranda"
    }
    ]
  }
  ```

#### **PUT `/user/update`**

Updates user information (requires valid JWT token).

**Request Body:**
```json
{
  "token": "jwt_token_here",
  "user_id": "5",
  "username": "Joshua B Miranda",
  "password": "123"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": null
  }
  ```
- Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Invalid or expired token"
    }
  }
  ```

#### **DELETE `/user/delete`**

Deletes a user account (requires valid JWT token).

**Request Body:**
```json
{
  "token": "jwt_token_here",
  "user_id": "5"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "data": null
  }
  ```
- Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Invalid or expired token"
    }
  }
  ```

---

### Author Endpoints

#### **POST `/author/register`**

Creates a new author.

**Request Body:**
```json
  "token": "jwt_token_here",
  "name": "Miranda Joshua"
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "jwt_token_here",  
    "data": null
  }
  ```
- Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Author name already exist"
    }
  }
  ```

#### **GET `/author/show`**

Fetches a list of all authors.

**Headers:**
```json
{
  "Authorization": "{token}"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": [
    {
      "author_id": "6",
      "name": "Miranda Joshua"
    },
    {
      "author_id": "7",
      "name": "Miranda c Joshua"
    }
    ]
  }
  ```

#### **PUT `/author/update`**

Updates author details.

**Request Body:**
```json
{
  "token":"jwt_token_here",
  "author_id": "5",
  "name": "Miranda C. Joshua"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token":"jwt_token_here",
    "data": null
  }
  ```

#### **DELETE `/author/delete`**

Deletes an author by ID.

**Request Body:**
```json
{
  "token":"jwt_token_here",
  "author_id": 5
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": null
  }
  ```
  - Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Invalid or expired token"
    }
  }
  ```

---

### Book Endpoints

#### **POST `/book/register`**

Adds a new book.

**Request Body:**
```json
{
    "token": "new_jwt_token",
    "title": "Math",
    "author_id": "4"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": null
  }
  ```

#### **GET `/book/show`**

Fetches a list of all books.
**Headers:**
```json
{
  "Authorization": "{token}"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": [
    {
      "book_id": "2",
      "title": "Science",
      "author_id": "1"
    },
    {
      "book_id": "3",
      "title": "Math",
      "author_id": "4"
    }
    ]
  }
  ```

#### **PUT `/book/update`**

Updates a book's details.

**Request Body:**
```json
{
    "token": "new_jwt_token",
    "book_id": 6,
    "title": "History",
    "author_id": 4
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": null
  }
  ```

#### **DELETE `/book/delete`**

Deletes a book by ID.

**Request Body:**
```json
{
  "token": "new_jwt_token",
  "book_id": "6"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "data": null
  }
  ```
  - Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Invalid or expired token"
    }
  }
  ```
---

### Book-Author Relationship Endpoints

#### **POST `/book_author/register`**

Creates a relationship between a book and an author.

**Request Body:**
```json
{
    "token": "new_jwt_token",
    "book_id": 2,
    "author_id": 1
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": null
  }
  ```

#### **GET `/book_author/show`**

Fetches all book-author relationships.
**Headers:**
```json
{
  "Authorization": "{token}"
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "data": [
      {
        "token": "new_jwt_token",
        "collection_id": 1,
        "book_id": 2,
        "author_id": 1
      }
    ]
  }
  ```

#### **PUT `/book_author/update`**

Updates a book-author relationship.

**Request Body:**
```json
{
  "token": "new_jwt_token",
  "collection_id": 1,
  "book_id": 1,
  "author_id": 1
}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "token": "new_jwt_token",
    "data": null
  }
  ```

#### **DELETE `/book_author/delete`**

Deletes a book-author relationship.

**Request Body:**
```json
{
  "collection_id": "1"

}
```

**Response:**
- Success:
  ```json
  {
    "status": "success",
    "data": null
  }
  ```
  - Failure:
  ```json
  {
    "status": "fail",
    "data": {
      "title": "Invalid or expired token"
    }
  }
  ```
---

## Database Schema

- **users_tbl**
  - `user_id`: Primary Key
  - `username`: VARCHAR(255)
  - `password`: VARCHAR(255)

- **authors_tbl**
  - `author_id`: Primary Key
  - `name`: VARCHAR(255)
  - `bio`: TEXT

- **books_tbl**
  - `book_id`: Primary Key
  - `title`: VARCHAR(255)
  - `author_id`: Foreign Key (references `authors_tbl.author_id`)

- **books_authors**
  - `collection_id`: Primary Key
  - `book_id`: Foreign Key (references `books_tbl.book_id`)
  - `author_id`: Foreign Key (references `authors_tbl.author_id`)

---

## Technology Stack

- **Slim Framework** (PHP)
- **MySQL** for database
- **JWT** for authentication
- **Composer** for dependency management

---

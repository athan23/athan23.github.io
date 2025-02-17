---
layout: devcodex
title: Dev Codex
permalink: /devcodex/
---

> This page is dedicated to sharing powerful code snippets and essential programming concepts to help developers of all levels enhance their skills. Whether you're looking for quick fixes, best practices, or deep dives into complex topics, you'll find concise, practical, and insightful resources here.

# Table of Contents

- [Elasticsearch](#elasticsearch)
    - [SQL Comparison](#elasticsearch-sql-comparison)
- [JWT](#jwt)
- [Node](#node)
    - [JWT](#node-jwt)
- [SQL](#sql)
    - [User](#sql-user-table)

## Elasticsearch {#elasticsearch}

### SQL Comparison (elasticsearch-sql-comparison)
Comparison between RDBMS and Elasticsearch

| RDBMS     | Elasticsearch |
|-----------|---------------|
| Databases | Clusters      |
| Tables    | Indices       |
| Rows      | Documents     |
| Columns   | Fields        |

- **Clusters** group a set of indices
- An **Index** is a collection of documents
- A **document** is a set of fields
- **Fields** are key-value pairs that contain your data

## Go {#go}

## Java {#java}

## JWT {#jwt}
JSON Web Token [(RFC 7519)](https://tools.ietf.org/html/rfc7519) is a compact, URL-safe means of representing claims to be transferred between two parties.

Example:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

More information about [JWT](https://jwt.io/)

### Uses
1. Authorization
2. Information Exchange

### Structure
- Header
    - Typically consists of two parts
        - Token type (JWT in this case)
        - Signing Algorithm
- Payload
    - Contains claims (statements about an entity)
- Signature
    - Used to verify the message wasn't changed along the way
    - Depends on signing algorithm

```js
// Header
{
  "alg": "HS256",
  "typ": "JWT"
}

// Payload
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}

// Signature (the following is only applicable for HS256 algorithm)
// Use jwt.io debugger to check signatures for different algorithms
// Generate a 256 bit secret beforehand and store it somewhere safe
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  your-256-bit-secret
)
```

### Claims

Three types of claims
- Registered

    Not mandatory but recommended.

    Examples: **iss**(issuer), **exp**(expiration time), **sub**(subject).

- Public

    Can be defined at will. To avoid collision, use [defined claims](https://www.iana.org/assignments/jwt/jwt.xhtml) or define a URI that contains collision resistant namespace.

- Private

    Custom claims between producer and consumer. Not Registered and Public. Subject to collision.

More information about [claims](https://datatracker.ietf.org/doc/html/rfc7519#section-4).

## Node {#node}

### JWT {#node-jwt}

```js
// login
const token = jwt.sign({ userId: user.id }, process.env.JWT_SECRET_KEY, { expiresIn: '1h' });
res.status(200).json({ token });

// middleware
function verifyToken(req, res, next) {
  const token = req.header('Authorization');
  if (!token) return res.status(401).json({ error: 'Access denied' });
  try {
    // "Bearer <token>"
    const decoded = jwt.verify(token.split(' ')[1], process.env.JWT_SECRET);
    req.userId = decoded.userId;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
}

// router
router.get('/', verifyToken, function(req, res, next) {
  // do stuff
}
```

## Python {#python}

## Ruby {#ruby}

## SQL {#sql}

### User table {#sql-user-table}
```
CREATE TABLE user (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) NOT NULL,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

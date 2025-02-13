---
layout: codegems
title: CodeGems
permalink: /codegems/
---

Here, you'll find a curated collection of concise, powerful, and reusable code snippets designed to make your development process smoother and more efficient. Whether you're looking for quick solutions, best practices, or innovative coding techniques, this page serves as your go-to developer toolkit. Stay tuned for more snippets that simplify, automate, and enhance your coding experience!

#### Table of Contents
- [Node](#node)
    - [JWT](#node-jwt)
- [SQL](#sql)
    - [User](#sql-user-table)

## Go {#go}
## Java {#java}
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

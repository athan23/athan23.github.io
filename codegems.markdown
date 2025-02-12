---
layout: codegems
title: CodeGems
permalink: /codegems/
---

Here, you'll find a curated collection of concise, powerful, and reusable code snippets designed to make your development process smoother and more efficient. Whether you're looking for quick solutions, best practices, or innovative coding techniques, this page serves as your go-to developer toolkit. Stay tuned for more snippets that simplify, automate, and enhance your coding experience!

#### Table of Contents
- [SQL](#sql)

## Go {#go}
## Java {#java}
## Node {#node}
## Python {#python}
## Ruby {#ruby}
## SQL {#sql}
### User table
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

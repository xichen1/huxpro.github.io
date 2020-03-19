---
layout:     post
title:    "Note of Berkeley DB"
subtitle:   "finished note"
date:     2019-11-14
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

#### Levels of abstraction in a typical DBMS(database management system)

1. Data is stored in tables in conceptual schema.

##### Conceptual schema:

The conceptual schema describes the Database structure of the whole database for the community of users. This schema hides information about the physical storage structures and focuses on describing data types, entities, relationships, etc. And one database can only have one conceptual schema.



2. Use high level SQL commands (DDL or DML)

##### DDL:

Data Definition Language (DDL) is a standard for commands that define the different structures in a database. DDL statements create, modify, and remove database objects such as tables, indexes, and users. Common DDL statements are CREATE, ALTER, and DROP. 

##### DML:

A data manipulation language (DML) is a computer programming language used for adding (inserting), deleting, and modifying (updating) data in a database. Common DML statements are SELECT, INSERT, UPDATE.

3. Data is organized in files and indexes in physical schema
4. A DBMS uses suitable storage structure, index files and access paths to evaluate queries and return results.

##### Berkeley DB

It is an open source embedded database library that provides s simple function-call API for data access and management.

It supports many file structures and operations

###### The use of Berkeley DB:

1. Develop programs working with storage structures and indexes
2. Develop applications that don't need the full functionality of a DBMS and require high performance

###### Four file organizations supported in Berkeley DB

1. hash: Data is stored in an extended linear hash table. good for applications that need quick random-access
2. Btree: Data is stored in a sorted, balanced tree structure. Good for range-based searches
3. Queue: Data is stored in a queue as fixed-length records. Good for fast inserts at the tail of the queue. It also supports read/delete operation from the head of the queue. It provides record-level locking
4. Recnos: Data is stored in either fixed or variable-length records


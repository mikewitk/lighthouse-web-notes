# Relational Database Management System

A relational database is a type of database that organizes data into tables, and links them, based on defined relationships. These relationships enable you to retrieve and combine data from one or more tables with a single query.

## 1NF - 1st Normal Form

1NF is the step of **removing repetitive data across columns**

## 2NF - 2nd Normal Form

2NF is the step of **removing repetitive data across rows**

## Foreign Key

A column that is used to link two tables

## Primary Key

Same concept as Foreign Key, but in this case a primary key can be defined on more than one column

## Normalization

The process of remove repetition across columns and rows and then choosing meaningful primary keys to link the tables together.

# SQL - Structured Query Language

Entity: represent a thing that you want to track in a database. It will become a table in the database

Each "thing" inside this table is an entity instance (rows)

Attribute: represent the characteristics (columns)

Primary Key / Identifier: An attribute or group of attributes  that uniquely identifies an instance of the entity

Relationship: describes how one or more entities interact with each other

Cardinality: the count of instances that are allowed or are necessary between entity relationships

*******************************
## CLASS


Let's start creating a vocabulary (nouns not verbs)

* artist           -> entity
* album            -> entity
* genre            -> entity
* label
* payment
* playlist         -> entity
* song             -> entity
* song name
* song key
* track length
* user name

Artist: name, members (band), genre
Album: cover, songs, etc

The next step is to build an ERD (Entity Relationship Database)

Is a diagram that shows how the entities to be related to each other


| Artists | -------< | Albums |

1 artist can have many albums

(The key is to establish the rules while you are creating your Database Diagram)

Many-To-Many: it is better practice to break it into a One to Many + Many to One relationship
ex:

| Artists | >-----< | Genres |

| Artists | ------< | Genre by Artist | >---- | Genre |


*******************************

## Table JOINS with SQL

`Inner Join`:
* Produces only the set of records that match in both Table A and Table B.
* Does not have a side

`Full Outter Join`: produces the set of all records in Table A and Table B, with matching records from both sides where available. If there i no match, the missing side will contain null.

`Left Outer Join`: produces a complete set of records from Table A, with the matching records (where available) in Table B. If there is no match, the right side will contain null

* Outter Join have a side
* left_table LEFT JOIN right_table === left_table LEFT OUTER JOIN right_table
* tableA LEFT JOIN tableB === tableB RIGHT JOIN tableA

## Class - SQL from our Apps

> It all starts with the input

node lookup_people.js Paul

Where
* node = commando to execute the file
* lookup_people.js = file to be executed
* Paul = the input from the user

**Store Paul into a variable to be used inside your code**

```javascript
const famousPeople = process.argv[2];
```

> On your function file, you can define several functions and export all of them to be used on your main file

```javascript
module.exports = ( function () {

  // But to start querying, we need to connect to the DB

  const { Client } = require('pg')
  const client = new Client({
    user: 'vagrant',
    host: 'localhost',
    database: 'vagrant',
    password: 'labber'
  })
  client.connect()

  // Now the DB is connect we can start querying.

  function a (arg1, callback) {
    client.query(`` // query away. It is always good to test on the shell to check for the results
      , [arg1, other], (err, res) => {
        if (err) {
          //deal with your errors
        } else {
          callback (res.rows)
        }
      }
  }

  // You can define as much functions as you need

  // But at the end, you want to return an object of functions

  return {
    a: a,
    b: b,
    etc: etc
    }
})
```

This way, on our main file, we can call just the specific functions we need

```javascript
const bla = require ('fileName') //fileName and/or path to the functions file

bla.a( (result) => {}) // and here you can decide what you want to do with the result data


```

# KNEX

## Initializing the Library

Knex's PostgreSQL client allows you to set the initial search path for each connection automatically using an additional option "searchPath" as shown below

```javascript
var pg = require('knex')({
  client: 'pg',
  connection: process.env.PG_CONNECTION_STRING,
  searchPath: ['knex', 'public'],
});
```
*Initializing the library should normally only ever happen once in your application, as it creates a connection pool for the current database, you should use the instance returned from the initialize call throughout your library*

Specify the client for the particular favlour of SQL you are interested in:
```javascript
var pg = require('knex')({client: 'pg'});
knex('table').insert({a: 'b'}).returning('*').toString();
// "insert into "table" ("a") values ('b')"

pg('table').insert({a: 'b'}).returning('*').toString();
// "insert into "table" ("a") values ('b') returning *"
```

















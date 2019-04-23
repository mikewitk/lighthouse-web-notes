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




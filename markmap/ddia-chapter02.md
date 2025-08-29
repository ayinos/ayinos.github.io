# Chapter 02: Data Models and Query Languages.
## Introduction
- Data models are important
- Most applications are built by layering one data model over another
  - Real world -> Object/DS/APIs -> JSON/XML/RDBMS tables/Graph model ->  Bytes in memory/disk/network -> Electric currents/ Pulses of light etc.
- Each layer hides complexity of the layers below by providing a clean data model.

## Relational vs Document Model
### Intro
- Relational model 
  - Data is organized into relations (tables in SQL) 
  - Where each relation is an unordered collection of tuples (rows in SQL)
### The Birth of NoSQL
- NoSQL was a catchy twitter hashtag for a meetup on open source, distributed, non-relational dbs in 2009
- NoSQL is retroactively reinterpreted as Not Only SQL
- Driving forces behind the adoption of NoSQL DBs
  - Need for greater scalability than RDBMS can achieve including
    - large datasets or very high write throughput
  - Preference for free or open source software over commercial db products
  - Specialized query operations that are not well-supported by the relational model
  - Frustration with the restrictiveness of relational schemas and a desire for more dynamic & expressive data models
### The Object Relational Mismatch
### Many-to-One & Many-to-Many Relationships
### Are Document DBs repeating history
### Relational vs Document DBs

## Query Languages for Data
### Declarative Queries for the Web
### MapReduce Querying

## Graph-Like Data Models
### Property Graphs
### The Cypher Query Language
### Graph Queries in SQL
### Triple-Stores and SPARQL
### The Foundation: Datalog

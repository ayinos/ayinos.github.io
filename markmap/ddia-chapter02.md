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
- Common criticism of SQL data model 
  - Objects in the application code ----awkward translation layer----> relational db model of tables, rows & columns.
- ORM frameworks like ActiveRecord, Hibernate reduce the boilerplate code required by the translation layer but cannot completely hide the differences between the 2 models.
- 3 ways to represent one-to-many relationship from the user to positions, education, contact info etc. in a resume (LinkedIn profile) in a relational schema
  1. In traditional model, put _positions_, _education_ & _contact info_ in separate tables with a foreign key reference to the _users_ table. 
  2. Later versions of SQL added support for structured datatypes & XMl/JSON data, this allowed multi-values data to be stored within a single row, with support for querying & indexing inside the docs.
  3. Encode jobs, education, contact info as JSON/XML docs & store it on a text column in the db & let application interpret its structure & content. Typically, cannot use the db to query for values inside that encoded column.
- For a data structure like resume, which is mostly a self-contained document a JSON representation can be quite appropriate. Document-oriented dbs like MongoDB, CouchDB etc support this data model.
- The JSON representation has better locality than the multi-table schema. No need to perform multiple queries or messy multi-way joins. All relevant info is in one place & one query is sufficient.
### Many-to-One & Many-to-Many Relationships
- For data like region or industry storing IDs vs text string is a question of duplication.
- Advantage of using ID is that it has no meaning to humans and never needs to change, even if the info it identifies changes.
- If stored as text string this info needs to be duplicated and & all redundant copes need to be updated. This incurs write overheads & risks inconsistencies.
- Removing duplication in the key idea behind normalisation.
- Unfortunately normalising data requires many-to-one relationships, which do not fit nicely into the document model. In document dbs support for joins is often weak.
- If db does not support joins they need to be emulated in application code by making multiple queries to the db.
- Moreover, even if the initial version of an application fits well in a join-free document model data has a tendency of becoming more interconnected as features are added to applications. For example, Recommendations.
  - The recommendation is shown on the resume of the user who was recommended along with the photo of the user making the recommendation. 
  - If the recommender updates their photo any recommendation they have written need to reflect the new photo.
  - Hence, the recommendations should have a reference to the author's profile.
  - Needs many-to-many relationships.
### Are Document DBs repeating history
- The design of IBMs IMS (Information Management System) in 1970 used _hierarchical model_. It represented data as a tree of records nested within records, similar to JSON.
- Like document dbs, this worked well for one-to-many but made many-to-many difficult & did not support joins.
- Devs had to decide whether to duplicate (de-normalize) or manually resolve references.
- 2 prominent solutions proposed.
  1. Network Model (CODASYL)
     - Generalization of the hierarchical model.
     - In the tree structure of hierarchical model every record has exactly one parent, in network model each record could have multiple parents.
     - Links between records were not foreign keys but more like pointers
     - Only way to access a records was to follow a path from a root record along these chain of links. This was called an _access path_.
     - Simplest case would be like the traversal of a linked list, start at head and traverse until you find the record you are looking for.
     - But several paths could lead to the same record in case of many-to-many relationships. 
     - The application code had keep a track of the various relationships.
     - Code for querying & updating the db was complicated & inflexible.
     - If there was no path to the data you wanted, you could change the access paths but then devs had to go through a lot of handwritten db query code & rewrite it to handle new access paths. 
     - Hence, difficult to make changes to the applications data model. 
  2. Relational Model
     - By contrast, laid all data out in the open.
     - A relation (table) is simply a collection of tuples (rows).
     - Query optimizer automatically decides which parts of the query to execute in which order and which indexes to use. These choices are effectively the "access path" but big difference is they are ade automatically by the query optimiser not teh developer.
     - To query data in new ways, a new index could be added. Query optimizer automatically makes use of this index, rewriting queries is not needed.
     - Query optimizers are complicated & have consumed many years of R&D, but they need to be written once and all applications using that db can then benefit from it.
### Relational vs Document DBs
- In representing many-to-one & many-to-many relationships, relational & document dbs are not fundamentally different.
  - In both cases, the related item is referenced by a unique id called as a foreign key in the relational model and document reference in the document model.
  - Id is resolved at read time using joins or followup queries.
## Query Languages for Data
### Declarative Queries for the Web
### MapReduce Querying

## Graph-Like Data Models
### Property Graphs
### The Cypher Query Language
### Graph Queries in SQL
### Triple-Stores and SPARQL
### The Foundation: Datalog

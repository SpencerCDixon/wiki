# Database's 

When deciding on DB selection this is a great question to ask:

> What database or combination of databases best resolves your problem?

## Genres of DB's

#### Relational

* are set theory based systems
* implemented as two-dimensional tables with rows and columns
* query data using SQL (Structured Query Language)
* data values are typed (int, strings, dates, etc.)
* tables can join and morph tables into more complex tables due to their mathematical basis in set theory

#### Key/Value
* simplest genre
* essentially just a hash/map/dictionary
* a file system could be though of as K/V. (filename is key and content is the value)
* very performant but not as helpful when doing complex queries/aggregation

#### Columnar
* adding columns is quite inexpensive and done on a row-by-row basis
* good for big data needs

#### Document
* store documents (hash with a unique ID field with values that can be any type)
* can contain nested structures giving them high flexibility

#### Graph
* excel at dealing with highly interconnected data
* consists of nodes and relationships between nodes

---

#### Polyglot Persistence
Is the concept of using multiple DB solutions to create a system greater than
the sum of its parts.  Pick and choose different DB's to do what they do best.
Great example is using Redis for caching/pub-sub alongside a relational DB.

#### CRUD
Useful mnemonic for remembering data management operations: Create, Read,
Update, & Delete.

#### ACID

**A** - atomic; all ops succeed or none do
**C** - consistent; the data will always be in a good state, no inconsistent states
**I** - isolated; transactions don't interfere
**D** - durable; a committed transaction is save, even after a server crash

#### CAP Theorem

**C** - consistent; writes are atomic and requests retrieve the new value  
**A** - available; the db will always return a value as long as single server is running  
**P** - partition tolerant; system will function even if server communication is temporarily lost  

Essentially, at any given time you're able to have 2 of the 3 properties above.
When deciding on a DB you must figure out which of the 3 you're willing to give
up.  

Analogy to think about it: you're stranded on an island for 5 years with no
connection to the rest of the world.  You are _partitioned_ from the world.  A
boat comes by and asks you a question.  You're able to either respond to the
question and be _available_ or tell the sailor he needs to go home in order to
get the correct _consistent_ answer.  This is the CAP theorem.  You can be
consistent or available but never both.

DNS is perfect example of _eventual consistency_.  It takes time to propagate
the change to all nodes but a node will always be available.





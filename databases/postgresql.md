# Postgres

[Useful repo from Todd on common postgres
tasks](https://github.com/GoesToEleven/golang-web-dev/tree/master/044_postgres)

## Client

Has a server running on port `5432` by default and you can connect to it via the
client `psql`.

When using psql it uses a hash mark for admin users and dollar sign for regular
users.

```sh
$ psql book
book=# <-- admin user
book=$ <-- regular user
```

Piping a .sql file into your db:

```sh
$ cat ./path-to-file.sql | psql <dbname>
```

OR

```sh
$ psql <dbname> < ./path-to-file.sql
```

Get list of tables

```sh
$ psql book
book=$ \d
```

Get list details about a specific table
```sh
book=$ \d categories
```

## Adding Extensions

1. Enter your db
2. Create extensions

```
psql <dbname>

CREATE EXTENSION <extensionName> or "<extension-name>";
```

## Data Types

* `text` - string of any length
* `varchar(#)` - string of variable length up to #
* `char(#)` - string of exactly # characters

## Creating

```sql
CREATE TABLE cities (
  name text NOT NULL,
  postal_code varchar(9) CHECK (postal_code <> ''),
  country_code char(2) REFERENCES countries,
  PRIMARY KEY (country_code, postal_code)
);
```

* The `<>` check confirms that no values are empty strings.
* Uses a compound primary key consisting of the country code and postal code

```sql
CREATE TABLE venues (
  venue_id SERIAL PRIMARY KEY,
  name varchar(255),
  street_address text,
  type char(7) CHECK ( type in ('public', 'private') ) DEFAULT 'public',
  postal_code varchar(9),
  country_code char(2),
  FOREIGN KEY (country_code, postal_code) 
    REFERENCES cities (country_code, postal_code) MATCH FULL
);
```

## Insertion
You can have postgres return columsn after insertion by ending the query with a
'RETURNING' statement

```sql
INSERT INTO venues (name, postal_code, country_code)
VALUES ('Voodoo Donuts', '97205', 'us') RETURNING venue_id;
```

This allows you to get the primary key of the inserted row without having to do
an additional query!

Sub-Select.  When inserting a new row that has a foreign key:
```sql
INSERT INTO events (titole, starts, ends, venue_id)
  VALUES ('Moby', '2012-02-06 21:00', '2012-02-06 23:00', (
    SELECT venue_id
    FROM venues
    WHERE name = 'Crystal Ballroom'
  )
);
```
Instead of querying to get the venue_id we use a sub select query to get the
venue_id for us and then use that as a value in the insertion clause.

## Indexing

Without an index postgres must read each row from disk to see if it matches the
query.  Indexes help prevent full table scans when performing a query.

Postgres will automatically create an index on the primary key.  Using the
UNIQUE keyword is another way to force an index on a table column.

To see all the indexes you can use the `\di` command inside psql.

## Querying
`SELECT venue_id FROM events GROUP BY venue_id;` is so common we can use
DISTINCT:  

`SELECT DISTINCT venue_id FROM events;`


## Window Functions

> allow you to use built-in aggregate functions without requiring eveyr single
> field to be grouped to a single row

## Transactions
These are the defensive perimeter around your data.  They ensure all queries are
successful otherwise rollback the data to what it was before.

Thus far, all the basic queries have been implicitly wrapped in a transaction.
It's important to use transactions when you don't want/can't have two tables out
of sync.  Classic example is credit/debit example:

```sql
BEGIN TRANSACTION;
  UPDATE account SET total=total+5000.0 WHERE account_ID=1337;
  UPDATE account SET total=total-5000.0 WHERE account_ID=2339;
END;
```

## Stored Procedures
Allow for huge perf advantages but couples you to using postgres.

To see what languages are allowed when making stored procedures:
```sh
$ createlang <dbname> --list
```

Example of stored procedure which saves a few queries:
```sql
CREATE OR REPLACE FUNCTION add_event(title text, starts timestamp, ends
timestamp, venue text, postal varchar(9), country char(2) )
RETURNS boolean AS $$
DECLARE
    did_insert boolean := false;
    found_count integer;
    the_venue_id integer;
BEGIN
  SELECT venue_id INTO the_venue_id
  FROM venues AS v
  WHERE v.postal_code=postal AND v.country_code=country AND v.name ILIKE venue
  LIMIT 1;

  IF the_venue_id IS NULL THEN
    INSERT INTO venues (name, postal_code, country_code)
    VALUES (venue, postal, country)
    RETURNING venue_id INTO the_venue_id;

    did_insert := true;
  END IF;

  RAISE NOTICE 'Venue found %', the_venue_id
  
  INSERT INTO events (title, starts, ends, venue_id)
  VALUES (title, starts, ends, the_venue_id);

  RETURn did_insert;
END;
$$ LANGUAGE plpgsql;
```

If we stored this func in `add_event.sql` we could add it to our DB like:
```sql
book=# \i add_event.sql
```

## Triggers
These allows us to execute a stored procedure whenever some event happens.

## Views
These are essentially 'virtual' tables.  You create a query and the prepend
necessary sql to create a view.  You're then able to treat that view like a
table and make further queries on it.  For example:

```sql
CREATE VIEW holidays AS
  SELECT event_id AS holiday_id, title AS name, starts AS date
  FROM events
  WHERE title LIKE '%Day%' AND venue_id IS NULL;
```

## Rules
A RULE is a way to alter the parsed query tree.  It allows you to define how SQL
should parse the AST.

SQL Query   
  --> Lexer   
  --> AST   
  --> RULES   
  --> Query Planner (optimizes disk ops)   
  --> Execution  


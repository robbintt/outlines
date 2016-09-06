
### Why SQLite?

Speaker: Dave Sawyer
Talk: Pycon 2016 Monday May 30 - SQLite gotchas and gimmes.
Talk URL: 


* Search/Sort Efficiently
* transactions with rollback
* safe format
* handle large datasets. 32/64 bit agnostic
* little/big endian agnostic
* concurrency.



#### Gotchas!

* Remember to commit your db changes (duh) => try/finally
* SQLite autocommits by default. Probably want to turn this off to control your commits.
* Close your cursor because writers have to wait for readers etc.



#### Gimmees!

* SQLite has a built in context manager!  Use with statement!
    ``` python
    with connection:
        connection.execute(MY_SQLITE_STATEMENT, (data,))
    ```

    ``` python
    # even better, generate the cursor in the with context.
    with closing(self.connection.cursor()) as cursor:
        cursor.execute(MY_SQLITE_STATEMENT, (data,))
    ```

* See the code from the talk for his class. It's very compact and general.
* WAL mode - SQLite 3.7. Write Ahead Logging. Lets you read and write at the same time.  It's like a delta and the writers write then the readers use the delta to read.
* sqlite3.version = python module version
* sqlite3.sqlite_version = gives sqlite installation version
* sqlite3 :memory: -- in-memory model and very fast obviously. No writes to disk.

##### SQLite isolation levels: deferred, immediate, exclusive.

Lets just implement deferred. The other two are easy and not totally necessary.


##### Questions:




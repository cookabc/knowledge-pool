## [What is Distributed SQL?](https://twitter.com/alexxubyte/status/1542531936706392064)

> What is Distributed SQL? Why do we need it? How does it work?
>
> Google Spanner popularized the term Distributed SQL database in 2012. Distributed SQL databases ๐๐ฎ๐ญ๐จ๐ฆ๐๐ญ๐ข๐๐๐ฅ๐ฅ๐ฒ ๐ซ๐๐ฉ๐ฅ๐ข๐๐๐ญ๐ ๐๐๐ญ๐ to multiple nodes and are ๐ฌ๐ญ๐ซ๐จ๐ง๐ ๐ฅ๐ฒ ๐๐จ๐ง๐ฌ๐ข๐ฌ๐ญ๐๐ง๐ญ.
> 
> ๐๐๐ฑ๐จ๐ฌ ๐จ๐ซ ๐๐๐๐ญ algorithms are commonly used to achieve consensus across multiple nodes.
>
> Examples of Distributed SQL databases: Google Spanner, Amazon Aurora, CockroachDB, YugabyteDB, TiDB, etc.
>
> Terms:
OLTP = Online transactional processing
OLAP = Online analytical processing
HTAP = Hybrid transaction/analytical processing
> 

![dis_sql](dis_sql.jpeg)

๐นThe life of an OLTP query (marked with ๐๐ฅ๐ฎ๐ sequence numbers):

Step 1. A client sends a MySQL query and the query is interpreted by TiDB, a stateless layer that interprets the MySQL protocol.

Step 2: TiDB requests data mapping/placement information from the PD.

Step 3: PD responds with data mapping/ placement instructions & timestamp.

Step 4: TiDB executes queries on TiKV servers (row-based storage)

Step 5, 6: Query results are sent back to the client

๐นThe life of a complex ๐๐๐๐ query: follow the ๐ฒ๐๐ฅ๐ฅ๐จ๐ฐ sequence numbers
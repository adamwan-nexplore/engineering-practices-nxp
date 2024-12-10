# Introduction to Query Performance <!-- omit in toc -->

## on PostgreSQL <!-- omit in toc -->

Table of Contents

- [What will cover](#what-will-cover)
- [Good Performance](#good-performance)
- [Principles](#principles)
- [Agenda](#agenda)
- [Configurations \& Tooling](#configurations--tooling)
- [Table Schemas](#table-schemas)
- [Queries](#queries)
  - [How does a database engine process queries](#how-does-a-database-engine-process-queries)
  - [Common mistakes](#common-mistakes)
  - [What should know](#what-should-know)
- [Indices](#indices)
  - [The Nature](#the-nature)
  - [EXPLAIN \& Query Plan](#explain--query-plan)
    - [How to READ Query Plan](#how-to-read-query-plan)
    - [The Concept](#the-concept)
    - [Index Types](#index-types)
    - [Micro-optimization](#micro-optimization)
- [Monitoring](#monitoring)
- [To be Extreme](#to-be-extreme)
  - [No code](#no-code)
  - [No Database queries](#no-database-queries)
- [Reference](#reference)

## What will cover

- Management Models

  - OLTP (Online Transaction Processing)
    - store and query the transactions
  - ~~OLAP (Online Analytical Processing)~~
    - report data, for planning and management

- Vendors
  - Postgres
  - ~~MySQL~~
  - ~~OracleDB~~
  - ~~SQL Server~~

## Good Performance

1. `Good Enough` Number of Concurrent Connections
2. No Always-Slow Queries
3. Minimal Randomly-Slow Queries

> It is IMPOSSIBLE to avoid Randomly-Slow Queries
>
> Not all factors we are able to control
>
> - networking
> - connection pools
> - read-write bottlenecks from storage

## Principles

1. Transactional queries should be FAST (<500ms)
2. Number of concurrently queries of the same sessions should be less than 5
3. Queries inside a transaction should be a constant in most cases
4. Locks that blocks other queries should be avoided (Especially `Table-level Locking`)

   - optimistic lock - concurrent read is allowed; write is not allowed
   - pessimistic lock - concurrent read nor write allowed

> Advanced Topic: [Locks, Latches, Enqueues and Mutex](https://minervadb.xyz/postgresql-locks-latches-enqueues-and-mutex "https://minervadb.xyz/postgresql-locks-latches-enqueues-and-mutex")

## Agenda

1. Configurations & Tooling
2. Table Schemas
3. Queries
4. Indices
5. Monitoring
6. To be Extreme

## Configurations & Tooling

- [PgBouncer](https://www.pgbouncer.org "https://www.pgbouncer.org")
  - Manage connection pool efficiently
  - Azure Flexible Server provides the integration of PgBounder as an [addon](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-pgbouncer "https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-pgbouncer")
- [PgTune](https://pgtune.leopard.in.ua "https://pgtune.leopard.in.ua")
  - Optimize Postgres configuration file according to the hardware specification
- [Performance Insights](https://learn.microsoft.com/en-us/azure/postgresql/single-server/concepts-query-performance-insight "https://learn.microsoft.com/en-us/azure/postgresql/single-server/concepts-query-performance-insight")

  - All query statistics are stored in schema `azure_sys` - check [here](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-identify-slow-queries "https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-identify-slow-queries")

  ```sql
  SELECT
      max(datname),
      query_id,
      query_sql_text,
      SUM(calls) total_calls,
      SUM(total_time) total_time,
      SUM(total_time) * 1.0 / SUM(calls) avg_time,
      SUM(rows) * 1.0 / SUM(calls)  avg_rows
  FROM query_store.qs_view q
  JOIN pg_database d ON q.db_id = d.oid
  GROUP BY query_id, query_sql_text
  ORDER BY avg_rows DESC
  LIMIT 10 -- change top N based on preferences;
  ```

> Reference is [here](https://techcommunity.microsoft.com/t5/azure-database-support-blog/how-to-get-the-query-text-of-azure-database-for-postgresql/ba-p/3233322 "https://techcommunity.microsoft.com/t5/azure-database-support-blog/how-to-get-the-query-text-of-azure-database-for-postgresql/ba-p/3233322")

## Table Schemas

- Normalization

  - design the schema so that any change of one field only affect one record

- De-normalization

  - store module key on tables under the module
  - store the number of sum / average result of certain table in its parent table

## Queries

### How does a database engine process queries

1. Whether the query plan has cached, if yes, use the query plan
   - What developers can do: Make sure the query plans can be re-used as much as possible
2. Analyze the query
   - What developers can do: Be avoid to write complicated queries
3. Decide the query plan (Relational Algebra)
   - The Execution Plan Optimizer of Postgres is `Cost-based`, NOT `Rule-based`
   - What developers can do: Design the queries that can use the indices
4. Execute
   - What developers can do: Do not fetch too much data per query

### Common mistakes

1. Include non-[DML (Data Manipulation Language)](https://en.wikipedia.org/wiki/Data_manipulation_language "https://en.wikipedia.org/wiki/Data_manipulation_language") in a single Transaction
   - Always-Slow Queries on itself, Randomly-Slow Queries
   - Include Queries are purely to fetch data
   - Include long running function calls NOT RELATED to database
     - send emails
     - send to service bus
     - communicate with external APIs
2. Get too many records from one query
   - Always-Slow queries on itself, Randomly-Slow Queries
   - growing tables
     - with `OR` and `UNION`
     - module tables without `limit`
3. [N+1 Queries](https://docs.sentry.io/product/issues/issue-details/performance-issues/n-one-queries "https://docs.sentry.io/product/issues/issue-details/performance-issues/n-one-queries")

   - Affect Concurrent Connections, Randomly-Slow Queries
   - while fetching data from the grand-children tables (companies -> projects -> records)

   ```sql
   SELECT id, "name" FROM classes WHERE school_code = 'LSC';
   -- | id     | name |
   -- | 200101 | 1A   |
   -- | 200102 | 1B   |
   -- | 200103 | 1C   |
   -- | 200104 | 1D   |
   -- | 200105 | 1E   |
   -- | 200106 | 1F   |
   -- ...
   SELECT id, "name" FROM students WHERE class_id = '200101';
   SELECT id, "name" FROM students WHERE class_id = '200102';
   SELECT id, "name" FROM students WHERE class_id = '200103';
   SELECT id, "name" FROM students WHERE class_id = '200104';
   SELECT id, "name" FROM students WHERE class_id = '200105';
   SELECT id, "name" FROM students WHERE class_id = '200106';
   -- ...
   ```

4. Store huge records (>500KB each)
   - Always-Slow Queries on itself, Randomly-Slow Queries
   - Unstructured JSON
     - no schema
     - schema with recursive nature
     - schema with dynamic keys
   - Store encoded images
   - Store binary data
5. Illegitimate Use of TEXT filter with `LIKE`
   - Always-Slow Queries on itself, Randomly-Slow Queries
   - prefix search is acceptable
   - infix search is slow
   - postfix search is slow

> [Optimizations with Full-Text Search in PostgreSQL](https://www.alibabacloud.com/blog/optimizations-with-full-text-search-in-postgresql_595339 "https://www.alibabacloud.com/blog/optimizations-with-full-text-search-in-postgresql_595339")

### What should know

0. [Query Plan](https://thoughtbot.com/blog/reading-an-explain-analyze-query-plan "https://thoughtbot.com/blog/reading-an-explain-analyze-query-plan")
1. Be avoid to query with complicated conditions that requires `Full Table Scan` on several tables
2. Be aware of queries on Critical Tables (User Table, `Modules` Tables)
3. For each query, indices should be used for tables > 1k records

## Indices

### The Nature

- Indices are a separate store that can help running the queries faster (no clustered indices support in PG)

- Good - Make some DDL queries faster while it makes a small portions of DDL queries slower
- Bad - Require more storage, DML queries slower

### EXPLAIN & Query Plan

- IF you are unsure how the query performs, try `EXPLAIN` or `EXPLAIN ANALYZE`

#### How to READ Query Plan

- [Scan Nodes](https://pganalyze.com/docs/explain/scan-nodes "https://pganalyze.com/docs/explain/scan-nodes")

> Learn more on `Recheck Cond` [[1]](https://stackoverflow.com/questions/50959814/what-does-recheck-cond-in-explain-result-mean "https://stackoverflow.com/questions/50959814/what-does-recheck-cond-in-explain-result-mean") [[2]](https://dba.stackexchange.com/questions/106264/recheck-cond-line-in-query-plans-with-a-bitmap-index-scan "https://dba.stackexchange.com/questions/106264/recheck-cond-line-in-query-plans-with-a-bitmap-index-scan")

#### The Concept

- Selectivity
- Cardinality

#### Index Types

- `B-tree` use by default - O(log n)
- `Hash Index` could be a good choice UNDER a few circumstances - O(1)
  - REQUIREMENT: Postgres Version > 11, not us
- `GIST & GIN` for JSON data

> Learn more on `Hash Index` [[1]](https://dba.stackexchange.com/questions/212685/how-is-it-possible-for-hash-index-not-to-be-faster-than-btree-for-equality-looku "https://dba.stackexchange.com/questions/212685/how-is-it-possible-for-hash-index-not-to-be-faster-than-btree-for-equality-looku") [[2]](https://www.cybertec-postgresql.com/en/postgresql-hash-index-performance "https://www.cybertec-postgresql.com/en/postgresql-hash-index-performance")

#### Micro-optimization

- Good for frequently used queries
- Partial Index
- Index on Expressions

```sql
-- Can only use inefficient PREFIX search
SELECT * FROM projects WHERE directory LIKE '00123>%';

-- Can use Index on Expressions, IF the length of SEARCH token is FIXED
SELECT * FROM projects WHERE SUBSTRING(directory, 0, 6) = '00123>';

CREATE INDEX IF NOT EXISTS project_directory_idx ON "projects"(SUBSTRING(directory, 0, 6));
```

## Monitoring

- Alerts on Database Server Resource Usage
- Alerts to slow queries

## To be Extreme

### [No code](https://github.com/kelseyhightower/nocode "https://github.com/kelseyhightower/nocode")

> No code is the best way to write secure and reliable applications. Write nothing; deploy nowhere.

### No Database queries

> No queries is the best way to make the database performing good.

- Query the replica
- Cache the result in application
- Do not store static configuration data
  - store in the services providing `strong consistency`
    - [S3](https://aws.amazon.com/tw/s3/consistency "https://aws.amazon.com/tw/s3/consistency")
    - [Blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/concurrency-manage "https://learn.microsoft.com/en-us/azure/storage/blobs/concurrency-manage")

> ~~No~~ Only necessary queries to Master Database is the best way to make the database performing good

## Reference

- [Awesome Postgres](https://github.com/dhamaniasad/awesome-postgres "https://github.com/dhamaniasad/awesome-postgres")
- [SQL Performance Explained](https://sql-performance-explained.com "https://sql-performance-explained.com")
- [Use the Index, Luke](https://use-the-index-luke.com "https://use-the-index-luke.com")
- [Percona PostgreSQL Blog](https://www.percona.com/blog/category/postgresql "https://www.percona.com/blog/category/postgresql")

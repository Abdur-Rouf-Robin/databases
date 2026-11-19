# Databases

Study notes for this card. Same shape as the JavaScript notes: a fact, the mechanism, code you can type, a spoken answer, then homework.

Read one concept out loud. Close the file. Type the example. Answer the question without looking.

A line the play button covered on the photo is filled in here as the usual concept for that number.

## 01 SQL basics

- SQL is the language of the tables. You say what you want, not the loop that finds it.

- SELECT chooses columns. FROM names the table. WHERE filters rows. ORDER BY sorts. LIMIT caps.
- INSERT, UPDATE, and DELETE change rows. Always have a WHERE on UPDATE and DELETE.
- NULL means unknown. NULL = NULL is not true. Use IS NULL.
- COUNT(*) counts rows. COUNT(column) skips nulls.

```sql
SELECT vessel, arrived_at
FROM port_calls
WHERE arrived_at IS NOT NULL
ORDER BY arrived_at DESC
LIMIT 20;
```

Question. What does a missing WHERE do on DELETE?

Say this. It deletes every row in the table. I write the WHERE first, or I run a SELECT with the same WHERE and count, then the DELETE.

Teach it. SQL is an order at a counter. You name the dish. You do not walk into the kitchen and point at plates.

The mistake. Thinking NULL equals empty string. They are different, and your unique constraints treat them differently.

On your CV. Every product of yours sits on PostgreSQL.

### homework

- Close the page and answer out loud: What does a missing WHERE do on DELETE?

## 02 Joins

- A join stitches rows from two tables using a key.

- INNER JOIN keeps only matches. A port call with no facts disappears from an inner join.
- LEFT JOIN keeps every left row, and the right side is NULL when nothing matches.
- A join condition belongs in ON. A filter on the right table in WHERE can turn a left join back into an inner join.
- Join on keys, not on names that happen to look alike.

```sql
SELECT p.vessel, f.kind
FROM port_calls p
LEFT JOIN statement_of_facts f ON f.port_call_id = p.id;
```

Question. Why did my left join lose rows?

Say this. The WHERE clause said f.kind = 'NOR', and unmatched rows have NULL kind, so they were removed. Put that filter in the ON, or accept that you now want an inner join.

Teach it. Inner join is friends who both showed up. Left join is the whole class, with a blank seat beside anyone who came alone.

The mistake. Joining on a non-unique column and silently multiplying rows.

On your CV. Prisma relations become joins. Know the SQL under findMany with include.

### homework

- Close the page and answer out loud: Why did my left join lose rows?

## 03 Normalization

- Normalization means each fact lives in one place, so an update cannot disagree with itself.

- First normal form: one value per cell, no lists packed into a column.
- Second: every non-key column depends on the whole key, not a piece of it.
- Third: a non-key column does not depend on another non-key column. The vessel's owner address belongs on the owner, not copied onto every port call.
- You denormalise on purpose for a read-heavy report, and you accept the extra update work.

```sql
port_calls(id, vessel_id, arrived_at)
vessels(id, name, owner_id)
owners(id, name, phone)
```

Question. When is a copy of a value allowed?

Say this. When it is a snapshot, such as the fee at the time of the tournament entry. The price list may change later. The invoice must not.

Teach it. One phone number lives in one address book. If you write it on every letter, one day the letters will disagree.

The mistake. A comma-separated list of roles in one column. You cannot index or constrain it honestly.

On your CV. Your Prisma relations are this idea.

### homework

- Close the page and answer out loud: When is a copy of a value allowed?

## 04 Indexing

- An index is a side structure that finds rows without reading the whole table.

- An index on the column in WHERE, JOIN, or ORDER BY can turn a scan into a lookup.
- A primary key and a unique column are indexes.
- The leftmost columns of a composite index are the ones the planner can use. An index on (a, b) helps WHERE a = ?, and WHERE a = ? AND b = ?. It does not help WHERE b = ? alone.
- Every index slows writes. Index the questions you actually ask.

```sql
CREATE INDEX port_calls_vessel_arrived ON port_calls (vessel_id, arrived_at DESC);
```

Question. Why is a query still slow after I added an index?

Say this. The condition might not match the index order, or a function wraps the column, such as WHERE lower(email) = ?, while the index is on email. Or the table is tiny and a scan is cheaper. EXPLAIN tells you.

Teach it. The index is the index at the back of a book. It is extra pages to maintain, and it saves you from reading every page.

The mistake. Indexing every column, then wondering why inserts are slow.

On your CV. Foreign keys on port_call_id and user lookups need indexes.

### homework

- Close the page and answer out loud: Why is a query still slow after I added an index?

## 05 B+ tree indexes

- The usual index in PostgreSQL is a B+ tree: a balanced tree whose leaves hold the keys in order.

- Finding one key is a short walk from root to leaf, about log n steps.
- The leaves are linked, so a range such as arrived_at between two dates is a walk along the leaves, not a second search per row.
- The tree stays balanced, so the depth does not become a linked list.
- Hash indexes answer equality only. A B+ tree also answers order and range, which is why it is the default.

```sql
WHERE arrived_at >= '2026-01-01' AND arrived_at < '2026-02-01'
-- a B+ tree can start at January and scan forward
```

Question. Why not a binary search on the table file?

Say this. Rows are not kept in key order on disk, and inserts would reshuffle the file. The B+ tree is the ordered structure beside the table.

Teach it. It is a phone book. You open it in the middle, then the quarter, and the names on one page are in order so you can read a range.

The mistake. Expecting an index to help LIKE '%rou%'. A leading wildcard cannot walk an ordered tree.

On your CV. Say B+ tree if they ask what Postgres builds for a normal CREATE INDEX.

### homework

- Close the page and answer out loud: Why not a binary search on the table file?

## 06 Transactions and ACID

- A transaction is a bracket around work that must succeed or fail as one.

- Atomic: all writes commit, or none do.
- Consistent: constraints hold at the end. A foreign key cannot point at nothing.
- Isolated: concurrent transactions do not see each other's half-finished work, up to the isolation level.
- Durable: after commit, a crash does not forget the row. Postgres writes the WAL, the write-ahead log, first.

```sql
BEGIN;
INSERT INTO port_calls (id, vessel_id) VALUES (1, 9);
INSERT INTO facts (port_call_id, kind) VALUES (1, 'NOR');
COMMIT;
```

Question. What is the WAL for?

Say this. The database appends the change to a log and can flush that log before it says commit. After a crash it replays the log. That is durability without rewriting the whole table on every insert.

Teach it. ACID is a receipt. Either the whole purchase is on it, or you are still in the shop.

The mistake. Two separate queries and calling that a transaction. Without BEGIN and COMMIT, or prisma.$transaction, each statement commits alone.

On your CV. Creating a port call and its first fact belongs in one transaction.

### homework

- Close the page and answer out loud: What is the WAL for?

## 07 Isolation levels

- Isolation is how much concurrent transactions can interfere.

- Read uncommitted can see another transaction's uncommitted rows. Postgres does not offer it in practice.
- Read committed, the Postgres default, sees only committed data, and each statement takes a fresh snapshot.
- Repeatable read keeps one snapshot for the whole transaction, so a second read sees the same rows.
- Serializable makes concurrent transactions behave as if they ran one by one. It may abort one of them, and you retry.

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

Question. What is a phantom?

Say this. You count the rows, someone else inserts a row that matches, and you count again and the number changed. Repeatable read in Postgres also avoids that phantom via snapshots. Serializable is the level that also catches more subtle write skew.

Teach it. Read committed is looking up each time you speak. Repeatable read is a photograph taken when you sat down.

The mistake. Assuming the default makes a read-then-write safe. Two operators can still both read a berth as free and both book it. Use a constraint or SELECT FOR UPDATE.

On your CV. Money and berth assignment are where you mention this.

### homework

- Close the page and answer out loud: What is a phantom?

## 08 Locks and MVCC

- Postgres does not overwrite a row in place for readers. It keeps versions. That is MVCC.

- An update writes a new version. A reader with an older snapshot still sees the old one. Readers do not block writers.
- A row lock, SELECT FOR UPDATE, makes a second transaction wait before it changes that row.
- Deadlock is two transactions each holding what the other wants. Postgres aborts one.
- A long transaction holds its snapshot and can block cleanup of old versions, which is why you do not keep a transaction open while you call Stripe.

```sql
SELECT * FROM berths WHERE id = 3 FOR UPDATE;
```

Question. Do readers block writers in Postgres?

Say this. No, not in the InnoDB-style way people fear. MVCC lets a reader see a snapshot. Writers block writers of the same row. A long transaction still causes trouble by keeping old row versions alive.

Teach it. MVCC is a notebook where you write a new line instead of scratching out the old one while someone is still reading it.

The mistake. Holding a transaction across a human click or an HTTP call to Stripe.

On your CV. Use a row lock when two operators might assign the same berth.

### homework

- Close the page and answer out loud: Do readers block writers in Postgres?

## 09 Query optimization

- Optimization starts by measuring the query, not by guessing an index.

- Find the slow statement in the log or in pg_stat_statements.
- Look at the plan. A sequential scan of a huge table with a selective filter is a candidate for an index.
- Select only the columns you need. A wide row is more I/O.
- A missing join condition is a nested loop disaster. Fix the SQL before you buy a bigger server.

```sql
EXPLAIN (ANALYZE, BUFFERS) SELECT * FROM facts WHERE port_call_id = 42;
```

Question. The table is small and EXPLAIN says seq scan. Is that wrong?

Say this. No. Reading three pages in order can be cheaper than walking an index. The planner is allowed to scan.

Teach it. Time the run before you rearrange the kitchen.

The mistake. Adding indexes at random, or SELECT * in a hot path.

On your CV. This is how you would defend a slow port-call screen.

### homework

- Close the page and answer out loud: The table is small and EXPLAIN says seq scan. Is that wrong?

## 10 EXPLAIN plans

- EXPLAIN shows the plan. EXPLAIN ANALYZE runs it and shows the real time.

- Seq Scan reads the table. Index Scan uses an index and then the row. Index Only Scan can answer from the index.
- A Nested Loop is fine for a few outer rows. A Hash Join builds a table in memory. A Merge Join wants both sides ordered.
- Rows is the estimate. Actual rows is the truth. A huge gap means bad statistics. ANALYZE the table.
- Cost is an internal unit, not milliseconds. Believe the actual time.

```sql
EXPLAIN ANALYZE SELECT ...
-- look at actual time and rows, not only the cost number
```

Question. What do you do when the estimate is a thousand rows and the actual is two?

Say this. The statistics are stale or the predicate is odd. Run ANALYZE. Then look again. I do not add an index until the plan and the real rows agree that a scan is the problem.

Teach it. The plan is the route on the map. ANALYZE is driving it with a stopwatch.

The mistake. Reading only the first line and ignoring a nested loop over a million rows.

On your CV. Practice one EXPLAIN on a facts-by-port-call query.

### homework

- Close the page and answer out loud: What do you do when the estimate is a thousand rows and the actual is two?

## 11 Stored procedures

- A stored procedure is code inside the database, in SQL or PL/pgSQL.

- It can run several statements in one round trip and one transaction.
- It is useful for a constraint that is awkward in the application, or a report that must be consistent.
- It is harder to test, review, and deploy than a TypeScript function in the repo.
- I keep laytime in TypeScript so the unit test does not need a database. I would use SQL for a set-based report.

```sql
CREATE FUNCTION active_calls() RETURNS bigint LANGUAGE sql AS
$$ SELECT count(*) FROM port_calls WHERE departed_at IS NULL $$;
```

Question. Why is laytime not a stored procedure?

Say this. I want the same function in tests without Postgres, and I want it in code review beside the API. The database still enforces the foreign keys and the unique ids.

Teach it. A procedure is a recipe locked in the kitchen. Useful, and easy to forget when the menu in git has changed.

The mistake. Hiding the business rule only in the database and also only in the app, so they drift.

On your CV. You can defend the choice to keep laytime in the shared package.

### homework

- Close the page and answer out loud: Why is laytime not a stored procedure?

## 12 Views and triggers

- A view is a saved SELECT. A trigger is code that runs when a row changes.

- A view does not store rows, unless it is materialized. A materialized view is a cache you refresh.
- A trigger can stamp updated_at, or stop an illegal change.
- A trigger that calls the network or sends mail will surprise you during a migration.
- Prefer a constraint when the rule is 'this column must be unique' or 'this key must exist'.

```sql
CREATE VIEW open_calls AS
SELECT * FROM port_calls WHERE departed_at IS NULL;
```

Question. Trigger or application code for updated_at?

Say this. A trigger or a database default is harder to forget. Application code misses the one path that used a raw query. For laytime money, I still want the tested TypeScript, not a hidden trigger.

Teach it. A view is a window with a particular curtain. A trigger is a bell on the door.

The mistake. A trigger that updates the same table and fires itself.

On your CV. You do not need one in the viva unless they ask. Know the difference.

### homework

- Close the page and answer out loud: Trigger or application code for updated_at?

## 13 SQL vs NoSQL

- SQL databases give you relations, transactions, and a strong schema. NoSQL is a family, not one product.

- Postgres is the default when the data is related and the writes must agree, which is vessels, users, and payments.
- A document store is comfortable when each item is a self-contained document and you mostly fetch it by id.
- Redis is not a document database. It is memory structures with optional persistence.
- You can use both. The database of record stays the one that has the transaction.

```
Postgres: users, port calls, payments
Redis: rate limits, queue
Mongo, if used: a flexible document, not the payment ledger
```

Question. You list MongoDB on your CV. When do you pick it?

Say this. When the shape varies and I load the whole document by id. I do not put the payment or the laytime ledger there. Those need transactions and constraints, so they stay in Postgres.

Teach it. SQL is a filing cabinet with labelled drawers that refuse a folder in the wrong drawer. A document store is a box that will hold whatever you drop in, and you must be the clerk.

The mistake. Using Mongo because the tutorial did, for data that is obviously relational.

On your CV. Your CV lists both PostgreSQL and MongoDB. Be ready for this question.

### homework

- Close the page and answer out loud: You list MongoDB on your CV. When do you pick it?

## 14 MongoDB

- MongoDB stores BSON documents in collections. A document is like a JSON object.

- You query with a filter object, not with SQL.
- An embedded array is a join you already did. It is good when you always read the parent and the children together, and the array stays small.
- A reference is an id in another collection. You join in the application, or with a lookup.
- Multi-document transactions exist. They are not a reason to treat Mongo as Postgres.

```javascript
db.videos.insertOne({ title: "Episode", captions: ["en", "bn"] })
db.videos.find({ title: "Episode" })
```

Question. Embed or reference?

Say this. Embed what has no life of its own and is bounded, such as a few captions on a video. Reference what is large, shared, or growing without a limit, such as every watch event.

Teach it. A document is one folder. Put the papers you always pull out together inside it. Do not put the whole archive in one folder.

The mistake. An unbounded array that grows forever inside one document.

On your CV. Say where you actually used it. Do not claim Anemi's main store is Mongo. Anemi's database on the CV is PostgreSQL.

### homework

- Close the page and answer out loud: Embed or reference?

## 15 Redis data types

- Redis is not only strings. The type is chosen for the operation.

- String: a cache value, a counter with INCR.
- Hash: a small object, such as a few fields of a session.
- List: a simple queue, left push and right pop.
- Set: unique members. A sorted set, ZSET, is a leaderboard, score then member.
- BullMQ uses Redis data structures. You usually do not hand-roll the queue on a list.

```
INCR login:ip
SET cache:port:42 "{...}" EX 30
ZADD board 1524 "player-a"
```

Question. How would you show a live leaderboard?

Say this. A sorted set. ZADD the new rating, ZREVRANGE the top 20. Bracket's source of truth is still Postgres. Redis can be the fast copy.

Teach it. Each type is a different tool in one toolbox. A counter is not a folder.

The mistake. Using Redis as the only copy of a payment.

On your CV. Rate limits are strings and INCR. Queues are BullMQ's own keys.

### homework

- Close the page and answer out loud: How would you show a live leaderboard?

## 16 Replication

- Replication copies the database to another server.

- Postgres streams the WAL to a standby.
- A standby can take read queries, and it can be promoted if the primary dies.
- Replication lag means the standby is a moment behind. A user who writes and then reads from the standby may not see the write.
- Replicas are not backups. A bad DELETE replicates.

```
primary --WAL--> standby
reads can go to the standby
writes go to the primary
```

Question. The user saved and the refresh is empty. What happened?

Say this. The write hit the primary and the read hit a lagging replica. Read-your-writes means the next read, for that user, goes to the primary, or you wait until the replica catches the WAL position.

Teach it. Replication is a second notebook being copied as you write. A backup is yesterday's notebook in another building.

The mistake. Sending a read of a just-written payment to a lagging replica and calling it a bug in Prisma.

On your CV. You can describe this even if production is still a single Postgres.

### homework

- Close the page and answer out loud: The user saved and the refresh is empty. What happened?

## 17 Sharding

- Sharding splits rows across servers by a key.

- Pick a key you always have, such as tournament id, so one tournament's matches stay together.
- A query that does not include the key must ask every shard, which is a scatter.
- Moving a key later is painful. Consistent hashing makes adding a server move less data, and it is still an operational project.
- Do this after one Postgres is actually too big. Not before.

```
shard = hash(tournamentId) % N
```

Question. What would you shard first in Bracket?

Say this. By tournament id, if one database could no longer hold the matches. Users who cross tournaments become a scatter, so I would not shard by user id if the hot path is one tournament.

Teach it. Sharding is several filing cabinets. If the label is wrong, you open all of them.

The mistake. Sharding before you have measured a single-node limit.

On your CV. A viva topic, not something you claim to operate today unless you have.

### homework

- Close the page and answer out loud: What would you shard first in Bracket?

## 18 Partitioning

- Partitioning splits one logical table into physical pieces inside one database.

- Range partitioning is common for time: one partition per month of facts.
- A query with the date can ignore the other months. That is partition pruning.
- A query without the date still touches every partition.
- It is simpler than sharding because it is still one server and one transaction model.

```sql
CREATE TABLE facts (...) PARTITION BY RANGE (at);
CREATE TABLE facts_2026_01 PARTITION OF facts
  FOR VALUES FROM ('2026-01-01') TO ('2026-02-01');
```

Question. Partition or shard?

Say this. Partition when one machine can hold the disk and you want to drop old months or prune scans. Shard when one machine cannot hold the write rate or the size.

Teach it. Partitions are drawers in one cabinet. Shards are cabinets in different rooms.

The mistake. Forgetting the partition key in the WHERE, then paying for every drawer.

On your CV. A facts table that grows forever is the example you give.

### homework

- Close the page and answer out loud: Partition or shard?

## 19 Connection pooling

- Opening a Postgres connection is expensive. A pool keeps a set of them open and lends them out.

- Each API process has a pool with a max, for example 10.
- If you run 20 Node processes, that is 200 connections, and Postgres will suffer. PgBouncer sits in front and multiplexes.
- A transaction-mode pooler does not allow a session feature to leak across clients. Do not hold a named prepared session state and expect it to stick.
- A leaked connection, one you never release, empties the pool and the API hangs.

```
DATABASE_URL with a pool size
PgBouncer in transaction mode in front of Postgres
```

Question. The API is fine and Postgres says too many connections. Why?

Say this. PM2 started many workers, and each has a pool. The product of workers times pool size is the real number. Lower the pool or put PgBouncer in front.

Teach it. The pool is a stack of ten borrowed pens. If everyone keeps a pen, the eleventh person waits forever.

The mistake. A pool of 100 per process because the default felt small.

On your CV. Docker Compose with one API container hides this. PM2 cluster mode reveals it.

### homework

- Close the page and answer out loud: The API is fine and Postgres says too many connections. Why?

## 20 Backups and recovery

- A backup you have not restored is a rumour.

- Postgres can take a base backup and archive the WAL, so you can restore to a point in time.
- pg_dump is a logical copy. It is simpler and slower to restore when the database is huge.
- Test a restore on another machine. Check the time it takes. That time is your downtime if the disk dies.
- Redis can snapshot. If Redis only holds rate limits and a queue, decide what you can lose. Do not be surprised.

```bash
pg_dump --format=custom --file=vms.dump vms
pg_restore --dbname=vms_test vms.dump
```

Question. What do you tell them about the recovery point?

Say this. How much data we can afford to lose, and how long we can be down. WAL archiving makes the loss window small. A nightly dump means up to a day. I name the number instead of saying we have backups.

Teach it. A backup is a spare key you have tried in the lock. A file you have never opened is not a spare key.

The mistake. Storing the dump on the same disk as the database.

On your CV. Be honest about what you have practised.

### homework

- Close the page and answer out loud: What do you tell them about the recovery point?

## Homework for the whole file

1. Read the twenty titles out loud with the file closed.
2. Pick three and write the example from memory.
3. Teach one concept to an empty chair in under a minute.

# Databases

## chapter 1 SQL basics

- SQL = the language of the tables. we say what we want, not the loop that finds it
- a table = rows and columns. a row is one thing. a column is one fact
- SELECT chooses columns. FROM names the table. WHERE filters rows
- ORDER BY sorts. LIMIT caps how many rows come back
- INSERT adds a row. UPDATE changes rows. DELETE removes rows
- UPDATE and DELETE without WHERE touch every row
- NULL = unknown. it is not zero and it is not an empty string
- NULL = NULL is not true. use IS NULL
- COUNT(*) counts rows. COUNT(column) skips nulls
- a primary key identifies the row. it is unique and not null
- a foreign key points at a primary key in another table
- Postgres is the database under VMS, Anemi, and Bracket
- Prisma writes this SQL for us. we still have to be able to read it

```sql
SELECT vessel, arrived_at
FROM port_calls
WHERE arrived_at IS NOT NULL
ORDER BY arrived_at DESC
LIMIT 20;
```

```sql
INSERT INTO port_calls (id, vessel, allowed_hours)
VALUES ('pc_12', 'Ocean Star', 72);

UPDATE port_calls
SET allowed_hours = 80
WHERE id = 'pc_12';

DELETE FROM port_calls
WHERE id = 'pc_12';
```

- write the WHERE first. run the SELECT with that WHERE and count, then the DELETE
- strings in SQL use single quotes. double quotes are for names, when we need them
- `SELECT *` is fine while we explore. a real query names the columns

- homework of chapter 1
```sql
-- 1a  the 20 newest port calls that have arrived
-- 1b  count port calls where departed_at IS NULL
-- 1c  update vessel for id pc_9 only
-- 1d  what happens if the WHERE is missing on that update
-- 1e  why NULL = '' is the wrong test
```

## chapter 2 Joins

- a join stitches rows from two tables using a key
- INNER JOIN keeps only matches. a port call with no facts disappears
- LEFT JOIN keeps every left row. the right side is NULL when nothing matches
- the join condition belongs in ON
- a filter on the right table in WHERE can turn a left join back into an inner join
- join on keys, not on names that happen to look alike
- a join on a non-unique column multiplies rows. one port call with 3 facts becomes 3 rows
- Prisma `include` becomes a join or a second query. know which, by reading the SQL log once

```sql
SELECT p.vessel, f.kind
FROM port_calls p
LEFT JOIN statement_of_facts f ON f.port_call_id = p.id;
```

```sql
-- this drops port calls that have no NOR fact
SELECT p.vessel, f.kind
FROM port_calls p
LEFT JOIN statement_of_facts f ON f.port_call_id = p.id
WHERE f.kind = 'NOR';

-- this keeps the port call and only attaches a NOR fact
SELECT p.vessel, f.kind
FROM port_calls p
LEFT JOIN statement_of_facts f
  ON f.port_call_id = p.id AND f.kind = 'NOR';
```

- alias `p` and `f` so the column names do not clash
- if the result has more rows than port calls, the join key was not unique

- homework of chapter 2
```sql
-- 2a  every match, and the tournament name, keeping a match even if the tournament row is missing
-- 2b  only matches that have a winner
-- 2c  move a filter from WHERE into ON and say which rows come back
```

## chapter 3 Normalization

- normalization = each fact lives in one place
- if the same fact is copied, an update can disagree with itself
- first normal form: one value per cell. no list packed into a column
- second: every non-key column depends on the whole key, not a piece of it
- third: a non-key column does not depend on another non-key column
- the vessel's owner address belongs on the owner, not copied onto every port call
- we denormalise on purpose for a read-heavy report, and we accept the extra update work
- a junction table is how two lists relate. a user has many roles, a role has many users

```sql
-- fact copied onto every call. a renamed owner must be edited on every row
-- port_calls(id, vessel, owner_name, owner_city)

-- fact in one place
-- owners(id, name, city)
-- port_calls(id, vessel, owner_id)
```

```sql
CREATE TABLE user_roles (
  user_id TEXT NOT NULL REFERENCES users(id),
  role_id TEXT NOT NULL REFERENCES roles(id),
  PRIMARY KEY (user_id, role_id)
);
```

- the primary key of user_roles is both columns. one user can have many roles. the pair cannot repeat
- a JSON list of role names inside the user row breaks first normal form. it is harder to ask "who has operator"

- homework of chapter 3
```sql
-- 3a  a match stores home_team_city. where should the city live
-- 3b  draw users, roles, and the junction table
-- 3c  name one report where copying a column would be a choice, not an accident
```

## chapter 4 Indexing and B+ trees

- an index = a side structure that finds rows without reading the whole table
- we index the columns in WHERE, JOIN, and ORDER BY
- a primary key already has an index
- a foreign key should have an index too, or the join and the delete of a parent get slow
- a B+ tree is what Postgres builds for a normal CREATE INDEX
- the tree keeps keys in order. a range such as `arrived_at > ...` can walk a slice of the leaves
- each leaf points at the table row
- a hash index only answers equality. we almost never ask for one
- an index is not free. every INSERT and UPDATE must maintain it
- a composite index (a, b) helps a query on a, and a query on a and b. it does not help a query on b alone
- leftmost prefix = that rule

```sql
CREATE INDEX port_calls_arrived_at_idx ON port_calls (arrived_at);

CREATE INDEX facts_call_kind_idx ON statement_of_facts (port_call_id, kind);
```

- the second index serves `WHERE port_call_id = ?` and `WHERE port_call_id = ? AND kind = ?`
- it does not serve `WHERE kind = ?` by itself
- if a query reads 30 percent of the table, Postgres may ignore the index and scan. that can be the right plan

- homework of chapter 4
```sql
-- 4a  index for WHERE tournament_id = ? ORDER BY starts_at
-- 4b  does an index on (starts_at, tournament_id) serve WHERE tournament_id = ? 
-- 4c  why a B+ tree can answer a range and a pure hash index cannot
```

## chapter 5 Transactions and ACID

- a transaction = several writes that commit together, or not at all
- atomic = all or nothing
- consistent = the rules still hold after the commit. foreign keys, checks, our own invariants
- isolated = one transaction does not see another transaction's half-finished work
- durable = after commit, a crash does not lose it. the WAL is flushed
- creating a port call and its first fact is one transaction. if the fact insert fails, the port call must not remain
- BEGIN starts it. COMMIT saves it. ROLLBACK undoes it
- Prisma `$transaction` is that block
- a transaction held open while we call Stripe or FFmpeg keeps locks. do the slow work outside

```sql
BEGIN;
INSERT INTO port_calls (id, vessel, allowed_hours) VALUES ('pc_13', 'North Wind', 72);
INSERT INTO statement_of_facts (id, port_call_id, kind) VALUES ('f_1', 'pc_13', 'NOR');
COMMIT;
```

```ts
await db.$transaction(async (tx) => {
  const call = await tx.portCall.create({ data: { vesselName, allowedHours } });
  await tx.statementOfFacts.create({ data: { portCallId: call.id, kind: "NOR" } });
  return call;
});
```

- two writes that must commit together on Bracket: the match result and the row that advances the winner
- autocommit is the default for a single statement. the moment we need two statements, we open a transaction

- homework of chapter 5
```sql
-- 5a  write the BEGIN / two inserts / COMMIT for a match result and the next match slot
-- 5b  say what ROLLBACK does if the second insert fails
-- 5c  why the FFmpeg encode is outside the transaction
```

## chapter 6 Isolation, locks, and MVCC

- isolation level = how much of other people's unfinished work we can see
- read committed = Postgres default. we see only committed rows. a row can change between two reads in our transaction
- repeatable read = rows we already read stay stable for our transaction
- serializable = the result is as if the transactions ran one by one. Postgres may abort us. we retry
- a lost update = two transactions read 10, both add 1, both write 11. one update vanished
- fix the lost update with one UPDATE that uses the old value, or with a lock
- a lock = the right to touch a row, held until commit
- SELECT ... FOR UPDATE locks the rows we intend to change
- MVCC = readers do not block writers. Postgres keeps old row versions
- a long transaction keeps old versions alive. that is why we do not hold one open during an encode
- deadlock = two transactions each hold a lock the other wants. Postgres kills one. we retry that one

```sql
UPDATE balances
SET cents = cents - 500
WHERE user_id = 'u_1' AND cents >= 500;
```

```sql
BEGIN;
SELECT id, winner FROM matches WHERE id = 'm_1' FOR UPDATE;
UPDATE matches SET winner = 'a' WHERE id = 'm_1';
COMMIT;
```

- the balance update does not read-then-write in the application. the check is in the same statement
- FOR UPDATE is for the case where we must read the row, decide in code, then write

- homework of chapter 6
```sql
-- 6a  two requests both read score 1 and both write score 2. what was lost
-- 6b  rewrite it as one UPDATE
-- 6c  which isolation level is the Postgres default
-- 6d  why a reader usually does not wait for a writer
```

## chapter 7 Query optimization and EXPLAIN

- optimization = making the same answer cheaper
- we measure before we add an index. a slow feeling is not a measurement
- EXPLAIN shows the plan. EXPLAIN ANALYZE runs it and adds real times
- Seq Scan = read the table. fine for a small table
- Index Scan = use an index, then fetch the rows
- Bitmap Index Scan = collect many index matches, then read the table in chunks
- Nested Loop = for each left row, look up the right row. good when the left side is small and the right side is indexed
- Hash Join = build a hash table of one side. good for larger joins
- rows in the plan are estimates. ANALYZE updates the statistics those estimates use
- a filter that hides behind a function, such as `WHERE lower(email) = ...`, may not use a plain index on email

```sql
EXPLAIN ANALYZE
SELECT p.vessel
FROM port_calls p
JOIN statement_of_facts f ON f.port_call_id = p.id
WHERE p.arrived_at > NOW() - INTERVAL '7 days';
```

- read it from the inside out. the first line is the total. the indented lines are the steps
- if the estimate says 10 rows and the actual says 100000, the statistics are stale or the predicate is odd. run ANALYZE
- an index that the plan never uses is a write cost with no read benefit. drop it after we are sure

- homework of chapter 7
```sql
-- 7a  EXPLAIN ANALYZE the join above
-- 7b  say what Seq Scan means
-- 7c  the plan estimates 20 rows and actually reads 200000. what do we run
-- 7d  why WHERE lower(vessel) = 'north wind' may ignore an index on vessel
```

## chapter 8 Procedures, views, and triggers

- a view = a saved SELECT. it does not store rows, unless it is materialized
- a materialized view is a cache we refresh
- a stored procedure or function = SQL saved in the database and called by name
- we use one for a rule that must hold no matter which application writes
- laytime money stays in the tested TypeScript. a hidden procedure is harder to test beside the other tests
- a trigger = a function that runs when a row is inserted, updated, or deleted
- a trigger can stamp updated_at
- a trigger that calls the network or sends mail will surprise us during a migration
- prefer a constraint when the rule is "this column is unique" or "this key must exist"
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_calls AS
SELECT id, vessel
FROM port_calls
WHERE departed_at IS NULL;
```

```sql
CREATE OR REPLACE FUNCTION set_updated_at()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- a view is read like a table. `SELECT * FROM open_calls`
- the function above is the body. the trigger that calls it is a separate CREATE TRIGGER
- for money, the TypeScript function and its unit test are the source of truth

- homework of chapter 8
```sql
-- 8a  a view of matches where winner IS NULL
-- 8b  why updated_at in a trigger is harder to forget than updated_at in one route
-- 8c  why laytime stays in TypeScript anyway
```

## chapter 9 SQL, NoSQL, MongoDB, and Redis types

- SQL databases give relations, transactions, and a schema. Postgres is the one we run
- NoSQL is a family, not one product
- a document store is comfortable when each item is one document we mostly fetch by id
- MongoDB stores BSON documents in collections
- a document can embed a list. that is handy for a thing we always load together, and awkward when we need to query inside the list
- we still need an index in MongoDB. a missing index is a collection scan
- Redis is not a document database. it is memory structures with optional persistence
- string = a value, or a counter with INCR
- hash = a small object. HSET, HGET
- list = a queue. LPUSH, RPOP
- set = unique members
- sorted set = members with a score. a leaderboard
- key expiry is the TTL. the rate-limit window is a TTL
- the database of record stays the one that has the transaction. that is Postgres

```js
// a document we always read whole
{
  _id: "match_1",
  home: "A",
  away: "B",
  games: [{ n: 1, home: 11, away: 7 }]
}
```

```ts
await redis.zadd("standings:t_1", 3, "player_a");
await redis.zrevrange("standings:t_1", 0, 9, "WITHSCORES");
```

- embedding games inside the match is fine until we ask "every game that ended 11-7" across tournaments
- a sorted set is a read model. the match result is still written in Postgres first

- homework of chapter 9
```ts
// 9a  which store holds the port call row, and why
// 9b  a Redis type for "these user ids are online"
// 9c  a Redis type for a leaderboard
// 9d  when embedding a list in MongoDB becomes the wrong shape
```

## chapter 10 Replication

- replication = a copy of the data on another server
- the primary takes writes. a replica replays them
- we use a replica to read, or to take over if the primary dies
- asynchronous = the primary commits, then the replica catches up. faster. the last commits can be missing if the primary dies
- synchronous = the primary waits until the replica has the commit. slower. the standby has the data
- replication is not a backup. a bad DELETE is copied to the replica
- lag = the replica is behind. a user who writes and then reads from the replica may not see the write
- read-your-writes = send that user to the primary for a moment, or read from the primary always for that screen

```sql
-- on the primary, Postgres streams the WAL
-- a replica is started with primary_conninfo and a slot
-- the application chooses where a query goes
```

```ts
// a fresh write is read from the primary
const created = await primary.portCall.create({ data });
const again = await primary.portCall.findUnique({ where: { id: created.id } });
```

- a report that can be a few seconds old can use the replica
- a balance or a laytime figure the user just saved is read from the primary

- homework of chapter 10
```ts
// 10a  what a replica does not protect us from
// 10b  async versus sync, in one line each
// 10c  the user saves a score and the next read is stale. which node did the read hit
```

## chapter 11 Sharding, partitioning, pooling, and backups

- sharding = rows split across servers by a key
- pick a key we always have. for Bracket that would be tournament id, so one tournament stays together
- a query without the key asks every shard. that is a scatter
- the three projects are not sharded. one Postgres is the design until it is actually too big
- partitioning = pieces of one logical table inside one database
- range partitioning is common for time. one partition per month of facts
- a query with the month in the WHERE can skip the other partitions
- a connection = a session to Postgres. each one costs memory
- the API must not open a connection per request and leave it
- a pool reuses connections. Prisma has a pool. PgBouncer is a pool in front of Postgres when many processes connect
- a backup = a copy we can restore. replication is not a backup
- a base backup plus the WAL lets us restore to a point in time
- we test a restore. a backup we have never restored is a hope
- store the backup off the same disk as the database

```sql
-- one table, one partition per month
CREATE TABLE facts (
  id TEXT NOT NULL,
  at TIMESTAMPTZ NOT NULL
) PARTITION BY RANGE (at);
```

```ts
// pool size is finite
// if every request waits on a connection, the symptom is timeouts, not a wrong answer
```

- shard = hash(tournamentId) % N is the picture. moving N later moves rows. that is an operations project, not a config tweak
- point-in-time recovery needs the base backup and every WAL segment after it. a missing segment stops the restore there

- homework of chapter 11
```sql
-- 11a  shard key for Bracket if one database could no longer hold the matches, and why not user id
-- 11b  partition key for a facts table that is always filtered by month
-- 11c  why a replica does not replace a backup
-- 11d  what we do with a backup before we trust it
```

## chapter 12 A worked schema

- this chapter puts the earlier chapters on one small schema
- a port call has many facts. the fact points back with a foreign key
- allowed_hours is an integer of hours. money is computed in TypeScript, not stored as the only copy without a way to recompute it
- the index matches the screen: open calls ordered by arrival

```sql
CREATE TABLE port_calls (
  id TEXT PRIMARY KEY,
  vessel TEXT NOT NULL,
  allowed_hours INTEGER NOT NULL CHECK (allowed_hours > 0),
  arrived_at TIMESTAMPTZ,
  departed_at TIMESTAMPTZ
);

CREATE TABLE statement_of_facts (
  id TEXT PRIMARY KEY,
  port_call_id TEXT NOT NULL REFERENCES port_calls(id),
  kind TEXT NOT NULL,
  at TIMESTAMPTZ NOT NULL
);

CREATE INDEX facts_by_call ON statement_of_facts (port_call_id);
CREATE INDEX calls_by_arrival ON port_calls (arrived_at);
```

```ts
await db.$transaction(async (tx) => {
  const call = await tx.portCall.create({
    data: { id: "pc_14", vesselName: "River Gate", allowedHours: 72 },
  });
  await tx.statementOfFacts.create({
    data: { portCallId: call.id, kind: "NOR", at: new Date() },
  });
  return call;
});
```

- the CHECK stops a zero allowance in the database, even if a second client skips Zod
- the foreign key stops a fact whose port call does not exist
- deleting a port call that still has facts fails until we decide ON DELETE CASCADE or we delete the facts first. cascade is a choice we write down, not a surprise

- homework of chapter 12
```sql
-- 12a  add matches(id, tournament_id, winner) and a foreign key to tournaments
-- 12b  the index for "matches in this tournament"
-- 12c  the transaction that sets the winner and inserts the next-round row
-- 12d  EXPLAIN a query that lists open port calls from the last 7 days
```

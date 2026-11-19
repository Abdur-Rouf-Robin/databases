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

- example 1. table port_calls
- one row id pc_12, vesselName = Ocean Star
- SELECT names the columns. FROM names port_calls. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, vesselName
FROM port_calls
WHERE id = 'pc_12';

INSERT INTO port_calls (id, vesselName)
VALUES ('pc_12', 'Ocean Star');

UPDATE port_calls
SET vesselName = 'Ocean Star'
WHERE id = 'pc_12';

DELETE FROM port_calls
WHERE id = 'pc_12';
```

- homework
```sql
-- 1a  select vesselName for pc_12
-- 1b  count rows where vesselName IS NULL
-- 1c  the DELETE above does not touch other ids
-- 1d  a missing WHERE would delete every row of port_calls
```

- example 2. table matches
- one row id m_1, home = Ada
- SELECT names the columns. FROM names matches. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, home
FROM matches
WHERE id = 'm_1';

INSERT INTO matches (id, home)
VALUES ('m_1', 'Ada');

UPDATE matches
SET home = 'Ada'
WHERE id = 'm_1';

DELETE FROM matches
WHERE id = 'm_1';
```

- homework
```sql
-- 2a  select home for m_1
-- 2b  count rows where home IS NULL
-- 2c  the DELETE above does not touch other ids
-- 2d  a missing WHERE would delete every row of matches
```

- example 3. table tournaments
- one row id t_9, name = Rajshahi Open
- SELECT names the columns. FROM names tournaments. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM tournaments
WHERE id = 't_9';

INSERT INTO tournaments (id, name)
VALUES ('t_9', 'Rajshahi Open');

UPDATE tournaments
SET name = 'Rajshahi Open'
WHERE id = 't_9';

DELETE FROM tournaments
WHERE id = 't_9';
```

- homework
```sql
-- 3a  select name for t_9
-- 3b  count rows where name IS NULL
-- 3c  the DELETE above does not touch other ids
-- 3d  a missing WHERE would delete every row of tournaments
```

- example 4. table videos
- one row id v_4, title = Episode 1
- SELECT names the columns. FROM names videos. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, title
FROM videos
WHERE id = 'v_4';

INSERT INTO videos (id, title)
VALUES ('v_4', 'Episode 1');

UPDATE videos
SET title = 'Episode 1'
WHERE id = 'v_4';

DELETE FROM videos
WHERE id = 'v_4';
```

- homework
```sql
-- 4a  select title for v_4
-- 4b  count rows where title IS NULL
-- 4c  the DELETE above does not touch other ids
-- 4d  a missing WHERE would delete every row of videos
```

- example 5. table facts
- one row id f_2, kind = NOR
- SELECT names the columns. FROM names facts. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, kind
FROM facts
WHERE id = 'f_2';

INSERT INTO facts (id, kind)
VALUES ('f_2', 'NOR');

UPDATE facts
SET kind = 'NOR'
WHERE id = 'f_2';

DELETE FROM facts
WHERE id = 'f_2';
```

- homework
```sql
-- 5a  select kind for f_2
-- 5b  count rows where kind IS NULL
-- 5c  the DELETE above does not touch other ids
-- 5d  a missing WHERE would delete every row of facts
```

- example 6. table users
- one row id u_3, email = a@example.com
- SELECT names the columns. FROM names users. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, email
FROM users
WHERE id = 'u_3';

INSERT INTO users (id, email)
VALUES ('u_3', 'a@example.com');

UPDATE users
SET email = 'a@example.com'
WHERE id = 'u_3';

DELETE FROM users
WHERE id = 'u_3';
```

- homework
```sql
-- 6a  select email for u_3
-- 6b  count rows where email IS NULL
-- 6c  the DELETE above does not touch other ids
-- 6d  a missing WHERE would delete every row of users
```

- example 7. table payments
- one row id pay_8, eventId = evt_1
- SELECT names the columns. FROM names payments. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, eventId
FROM payments
WHERE id = 'pay_8';

INSERT INTO payments (id, eventId)
VALUES ('pay_8', 'evt_1');

UPDATE payments
SET eventId = 'evt_1'
WHERE id = 'pay_8';

DELETE FROM payments
WHERE id = 'pay_8';
```

- homework
```sql
-- 7a  select eventId for pay_8
-- 7b  count rows where eventId IS NULL
-- 7c  the DELETE above does not touch other ids
-- 7d  a missing WHERE would delete every row of payments
```

- example 8. table rooms
- one row id room_2, sessionId = s_9
- SELECT names the columns. FROM names rooms. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, sessionId
FROM rooms
WHERE id = 'room_2';

INSERT INTO rooms (id, sessionId)
VALUES ('room_2', 's_9');

UPDATE rooms
SET sessionId = 's_9'
WHERE id = 'room_2';

DELETE FROM rooms
WHERE id = 'room_2';
```

- homework
```sql
-- 8a  select sessionId for room_2
-- 8b  count rows where sessionId IS NULL
-- 8c  the DELETE above does not touch other ids
-- 8d  a missing WHERE would delete every row of rooms
```

- example 9. table vessels
- one row id vs_7, name = North Wind
- SELECT names the columns. FROM names vessels. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM vessels
WHERE id = 'vs_7';

INSERT INTO vessels (id, name)
VALUES ('vs_7', 'North Wind');

UPDATE vessels
SET name = 'North Wind'
WHERE id = 'vs_7';

DELETE FROM vessels
WHERE id = 'vs_7';
```

- homework
```sql
-- 9a  select name for vs_7
-- 9b  count rows where name IS NULL
-- 9c  the DELETE above does not touch other ids
-- 9d  a missing WHERE would delete every row of vessels
```

- example 10. table scores
- one row id sc_3, points = 11
- SELECT names the columns. FROM names scores. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, points
FROM scores
WHERE id = 'sc_3';

INSERT INTO scores (id, points)
VALUES ('sc_3', '11');

UPDATE scores
SET points = '11'
WHERE id = 'sc_3';

DELETE FROM scores
WHERE id = 'sc_3';
```

- homework
```sql
-- 10a  select points for sc_3
-- 10b  count rows where points IS NULL
-- 10c  the DELETE above does not touch other ids
-- 10d  a missing WHERE would delete every row of scores
```

- example 11. table teams
- one row id tm_2, name = Blue
- SELECT names the columns. FROM names teams. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM teams
WHERE id = 'tm_2';

INSERT INTO teams (id, name)
VALUES ('tm_2', 'Blue');

UPDATE teams
SET name = 'Blue'
WHERE id = 'tm_2';

DELETE FROM teams
WHERE id = 'tm_2';
```

- homework
```sql
-- 11a  select name for tm_2
-- 11b  count rows where name IS NULL
-- 11c  the DELETE above does not touch other ids
-- 11d  a missing WHERE would delete every row of teams
```

- example 12. table uploads
- one row id up_6, key = videos/u_1/a.mp4
- SELECT names the columns. FROM names uploads. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, key
FROM uploads
WHERE id = 'up_6';

INSERT INTO uploads (id, key)
VALUES ('up_6', 'videos/u_1/a.mp4');

UPDATE uploads
SET key = 'videos/u_1/a.mp4'
WHERE id = 'up_6';

DELETE FROM uploads
WHERE id = 'up_6';
```

- homework
```sql
-- 12a  select key for up_6
-- 12b  count rows where key IS NULL
-- 12c  the DELETE above does not touch other ids
-- 12d  a missing WHERE would delete every row of uploads
```

- example 13. table standings
- one row id st_1, player = player_a
- SELECT names the columns. FROM names standings. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, player
FROM standings
WHERE id = 'st_1';

INSERT INTO standings (id, player)
VALUES ('st_1', 'player_a');

UPDATE standings
SET player = 'player_a'
WHERE id = 'st_1';

DELETE FROM standings
WHERE id = 'st_1';
```

- homework
```sql
-- 13a  select player for st_1
-- 13b  count rows where player IS NULL
-- 13c  the DELETE above does not touch other ids
-- 13d  a missing WHERE would delete every row of standings
```

- example 14. table notices
- one row id n_2, port = Chattogram
- SELECT names the columns. FROM names notices. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, port
FROM notices
WHERE id = 'n_2';

INSERT INTO notices (id, port)
VALUES ('n_2', 'Chattogram');

UPDATE notices
SET port = 'Chattogram'
WHERE id = 'n_2';

DELETE FROM notices
WHERE id = 'n_2';
```

- homework
```sql
-- 14a  select port for n_2
-- 14b  count rows where port IS NULL
-- 14c  the DELETE above does not touch other ids
-- 14d  a missing WHERE would delete every row of notices
```

- example 15. table brackets
- one row id b_3, round = semi
- SELECT names the columns. FROM names brackets. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, round
FROM brackets
WHERE id = 'b_3';

INSERT INTO brackets (id, round)
VALUES ('b_3', 'semi');

UPDATE brackets
SET round = 'semi'
WHERE id = 'b_3';

DELETE FROM brackets
WHERE id = 'b_3';
```

- homework
```sql
-- 15a  select round for b_3
-- 15b  count rows where round IS NULL
-- 15c  the DELETE above does not touch other ids
-- 15d  a missing WHERE would delete every row of brackets
```

- example 16. table sessions
- one row id se_1, userId = u_3
- SELECT names the columns. FROM names sessions. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, userId
FROM sessions
WHERE id = 'se_1';

INSERT INTO sessions (id, userId)
VALUES ('se_1', 'u_3');

UPDATE sessions
SET userId = 'u_3'
WHERE id = 'se_1';

DELETE FROM sessions
WHERE id = 'se_1';
```

- homework
```sql
-- 16a  select userId for se_1
-- 16b  count rows where userId IS NULL
-- 16c  the DELETE above does not touch other ids
-- 16d  a missing WHERE would delete every row of sessions
```

- example 17. table queues
- one row id q_1, name = laytime
- SELECT names the columns. FROM names queues. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM queues
WHERE id = 'q_1';

INSERT INTO queues (id, name)
VALUES ('q_1', 'laytime');

UPDATE queues
SET name = 'laytime'
WHERE id = 'q_1';

DELETE FROM queues
WHERE id = 'q_1';
```

- homework
```sql
-- 17a  select name for q_1
-- 17b  count rows where name IS NULL
-- 17c  the DELETE above does not touch other ids
-- 17d  a missing WHERE would delete every row of queues
```

- example 18. table roles
- one row id r_1, name = operator
- SELECT names the columns. FROM names roles. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM roles
WHERE id = 'r_1';

INSERT INTO roles (id, name)
VALUES ('r_1', 'operator');

UPDATE roles
SET name = 'operator'
WHERE id = 'r_1';

DELETE FROM roles
WHERE id = 'r_1';
```

- homework
```sql
-- 18a  select name for r_1
-- 18b  count rows where name IS NULL
-- 18c  the DELETE above does not touch other ids
-- 18d  a missing WHERE would delete every row of roles
```

- example 19. table port_calls
- one row id pc_12, vesselName = Ocean Star
- SELECT names the columns. FROM names port_calls. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, vesselName
FROM port_calls
WHERE id = 'pc_12';

INSERT INTO port_calls (id, vesselName)
VALUES ('pc_12', 'Ocean Star');

UPDATE port_calls
SET vesselName = 'Ocean Star'
WHERE id = 'pc_12';

DELETE FROM port_calls
WHERE id = 'pc_12';
```

- homework
```sql
-- 19a  select vesselName for pc_12
-- 19b  count rows where vesselName IS NULL
-- 19c  the DELETE above does not touch other ids
-- 19d  a missing WHERE would delete every row of port_calls
```

- example 20. table matches
- one row id m_1, home = Ada
- SELECT names the columns. FROM names matches. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, home
FROM matches
WHERE id = 'm_1';

INSERT INTO matches (id, home)
VALUES ('m_1', 'Ada');

UPDATE matches
SET home = 'Ada'
WHERE id = 'm_1';

DELETE FROM matches
WHERE id = 'm_1';
```

- homework
```sql
-- 20a  select home for m_1
-- 20b  count rows where home IS NULL
-- 20c  the DELETE above does not touch other ids
-- 20d  a missing WHERE would delete every row of matches
```

- example 21. table tournaments
- one row id t_9, name = Rajshahi Open
- SELECT names the columns. FROM names tournaments. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM tournaments
WHERE id = 't_9';

INSERT INTO tournaments (id, name)
VALUES ('t_9', 'Rajshahi Open');

UPDATE tournaments
SET name = 'Rajshahi Open'
WHERE id = 't_9';

DELETE FROM tournaments
WHERE id = 't_9';
```

- homework
```sql
-- 21a  select name for t_9
-- 21b  count rows where name IS NULL
-- 21c  the DELETE above does not touch other ids
-- 21d  a missing WHERE would delete every row of tournaments
```

- example 22. table videos
- one row id v_4, title = Episode 1
- SELECT names the columns. FROM names videos. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, title
FROM videos
WHERE id = 'v_4';

INSERT INTO videos (id, title)
VALUES ('v_4', 'Episode 1');

UPDATE videos
SET title = 'Episode 1'
WHERE id = 'v_4';

DELETE FROM videos
WHERE id = 'v_4';
```

- homework
```sql
-- 22a  select title for v_4
-- 22b  count rows where title IS NULL
-- 22c  the DELETE above does not touch other ids
-- 22d  a missing WHERE would delete every row of videos
```

- example 23. table facts
- one row id f_2, kind = NOR
- SELECT names the columns. FROM names facts. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, kind
FROM facts
WHERE id = 'f_2';

INSERT INTO facts (id, kind)
VALUES ('f_2', 'NOR');

UPDATE facts
SET kind = 'NOR'
WHERE id = 'f_2';

DELETE FROM facts
WHERE id = 'f_2';
```

- homework
```sql
-- 23a  select kind for f_2
-- 23b  count rows where kind IS NULL
-- 23c  the DELETE above does not touch other ids
-- 23d  a missing WHERE would delete every row of facts
```

- example 24. table users
- one row id u_3, email = a@example.com
- SELECT names the columns. FROM names users. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, email
FROM users
WHERE id = 'u_3';

INSERT INTO users (id, email)
VALUES ('u_3', 'a@example.com');

UPDATE users
SET email = 'a@example.com'
WHERE id = 'u_3';

DELETE FROM users
WHERE id = 'u_3';
```

- homework
```sql
-- 24a  select email for u_3
-- 24b  count rows where email IS NULL
-- 24c  the DELETE above does not touch other ids
-- 24d  a missing WHERE would delete every row of users
```

- example 25. table payments
- one row id pay_8, eventId = evt_1
- SELECT names the columns. FROM names payments. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, eventId
FROM payments
WHERE id = 'pay_8';

INSERT INTO payments (id, eventId)
VALUES ('pay_8', 'evt_1');

UPDATE payments
SET eventId = 'evt_1'
WHERE id = 'pay_8';

DELETE FROM payments
WHERE id = 'pay_8';
```

- homework
```sql
-- 25a  select eventId for pay_8
-- 25b  count rows where eventId IS NULL
-- 25c  the DELETE above does not touch other ids
-- 25d  a missing WHERE would delete every row of payments
```

- example 26. table rooms
- one row id room_2, sessionId = s_9
- SELECT names the columns. FROM names rooms. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, sessionId
FROM rooms
WHERE id = 'room_2';

INSERT INTO rooms (id, sessionId)
VALUES ('room_2', 's_9');

UPDATE rooms
SET sessionId = 's_9'
WHERE id = 'room_2';

DELETE FROM rooms
WHERE id = 'room_2';
```

- homework
```sql
-- 26a  select sessionId for room_2
-- 26b  count rows where sessionId IS NULL
-- 26c  the DELETE above does not touch other ids
-- 26d  a missing WHERE would delete every row of rooms
```

- example 27. table vessels
- one row id vs_7, name = North Wind
- SELECT names the columns. FROM names vessels. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM vessels
WHERE id = 'vs_7';

INSERT INTO vessels (id, name)
VALUES ('vs_7', 'North Wind');

UPDATE vessels
SET name = 'North Wind'
WHERE id = 'vs_7';

DELETE FROM vessels
WHERE id = 'vs_7';
```

- homework
```sql
-- 27a  select name for vs_7
-- 27b  count rows where name IS NULL
-- 27c  the DELETE above does not touch other ids
-- 27d  a missing WHERE would delete every row of vessels
```

- example 28. table scores
- one row id sc_3, points = 11
- SELECT names the columns. FROM names scores. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, points
FROM scores
WHERE id = 'sc_3';

INSERT INTO scores (id, points)
VALUES ('sc_3', '11');

UPDATE scores
SET points = '11'
WHERE id = 'sc_3';

DELETE FROM scores
WHERE id = 'sc_3';
```

- homework
```sql
-- 28a  select points for sc_3
-- 28b  count rows where points IS NULL
-- 28c  the DELETE above does not touch other ids
-- 28d  a missing WHERE would delete every row of scores
```

- example 29. table teams
- one row id tm_2, name = Blue
- SELECT names the columns. FROM names teams. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM teams
WHERE id = 'tm_2';

INSERT INTO teams (id, name)
VALUES ('tm_2', 'Blue');

UPDATE teams
SET name = 'Blue'
WHERE id = 'tm_2';

DELETE FROM teams
WHERE id = 'tm_2';
```

- homework
```sql
-- 29a  select name for tm_2
-- 29b  count rows where name IS NULL
-- 29c  the DELETE above does not touch other ids
-- 29d  a missing WHERE would delete every row of teams
```

- example 30. table uploads
- one row id up_6, key = videos/u_1/a.mp4
- SELECT names the columns. FROM names uploads. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, key
FROM uploads
WHERE id = 'up_6';

INSERT INTO uploads (id, key)
VALUES ('up_6', 'videos/u_1/a.mp4');

UPDATE uploads
SET key = 'videos/u_1/a.mp4'
WHERE id = 'up_6';

DELETE FROM uploads
WHERE id = 'up_6';
```

- homework
```sql
-- 30a  select key for up_6
-- 30b  count rows where key IS NULL
-- 30c  the DELETE above does not touch other ids
-- 30d  a missing WHERE would delete every row of uploads
```

- example 31. table standings
- one row id st_1, player = player_a
- SELECT names the columns. FROM names standings. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, player
FROM standings
WHERE id = 'st_1';

INSERT INTO standings (id, player)
VALUES ('st_1', 'player_a');

UPDATE standings
SET player = 'player_a'
WHERE id = 'st_1';

DELETE FROM standings
WHERE id = 'st_1';
```

- homework
```sql
-- 31a  select player for st_1
-- 31b  count rows where player IS NULL
-- 31c  the DELETE above does not touch other ids
-- 31d  a missing WHERE would delete every row of standings
```

- example 32. table notices
- one row id n_2, port = Chattogram
- SELECT names the columns. FROM names notices. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, port
FROM notices
WHERE id = 'n_2';

INSERT INTO notices (id, port)
VALUES ('n_2', 'Chattogram');

UPDATE notices
SET port = 'Chattogram'
WHERE id = 'n_2';

DELETE FROM notices
WHERE id = 'n_2';
```

- homework
```sql
-- 32a  select port for n_2
-- 32b  count rows where port IS NULL
-- 32c  the DELETE above does not touch other ids
-- 32d  a missing WHERE would delete every row of notices
```

- example 33. table brackets
- one row id b_3, round = semi
- SELECT names the columns. FROM names brackets. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, round
FROM brackets
WHERE id = 'b_3';

INSERT INTO brackets (id, round)
VALUES ('b_3', 'semi');

UPDATE brackets
SET round = 'semi'
WHERE id = 'b_3';

DELETE FROM brackets
WHERE id = 'b_3';
```

- homework
```sql
-- 33a  select round for b_3
-- 33b  count rows where round IS NULL
-- 33c  the DELETE above does not touch other ids
-- 33d  a missing WHERE would delete every row of brackets
```

- example 34. table sessions
- one row id se_1, userId = u_3
- SELECT names the columns. FROM names sessions. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, userId
FROM sessions
WHERE id = 'se_1';

INSERT INTO sessions (id, userId)
VALUES ('se_1', 'u_3');

UPDATE sessions
SET userId = 'u_3'
WHERE id = 'se_1';

DELETE FROM sessions
WHERE id = 'se_1';
```

- homework
```sql
-- 34a  select userId for se_1
-- 34b  count rows where userId IS NULL
-- 34c  the DELETE above does not touch other ids
-- 34d  a missing WHERE would delete every row of sessions
```

- example 35. table queues
- one row id q_1, name = laytime
- SELECT names the columns. FROM names queues. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM queues
WHERE id = 'q_1';

INSERT INTO queues (id, name)
VALUES ('q_1', 'laytime');

UPDATE queues
SET name = 'laytime'
WHERE id = 'q_1';

DELETE FROM queues
WHERE id = 'q_1';
```

- homework
```sql
-- 35a  select name for q_1
-- 35b  count rows where name IS NULL
-- 35c  the DELETE above does not touch other ids
-- 35d  a missing WHERE would delete every row of queues
```

- example 36. table roles
- one row id r_1, name = operator
- SELECT names the columns. FROM names roles. WHERE uses the id
- NULL is unknown. use IS NULL
- UPDATE and DELETE always have a WHERE

```sql
SELECT id, name
FROM roles
WHERE id = 'r_1';

INSERT INTO roles (id, name)
VALUES ('r_1', 'operator');

UPDATE roles
SET name = 'operator'
WHERE id = 'r_1';

DELETE FROM roles
WHERE id = 'r_1';
```

- homework
```sql
-- 36a  select name for r_1
-- 36b  count rows where name IS NULL
-- 36c  the DELETE above does not touch other ids
-- 36d  a missing WHERE would delete every row of roles
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

- example 1. join port_calls to its child
- INNER keeps matches only
- LEFT keeps every port_calls row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.vesselName
FROM port_calls p
LEFT JOIN port_calls_child c ON c.parent_id = p.id
WHERE p.id = 'pc_12';
```

- homework
```sql
-- 1a  left join for pc_12
-- 1b  inner join drops pc_12 when it has no child
-- 1c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 1d  join on the key, not on vesselName text
```

- example 2. join matches to its child
- INNER keeps matches only
- LEFT keeps every matches row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.home
FROM matches p
LEFT JOIN matches_child c ON c.parent_id = p.id
WHERE p.id = 'm_1';
```

- homework
```sql
-- 2a  left join for m_1
-- 2b  inner join drops m_1 when it has no child
-- 2c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 2d  join on the key, not on home text
```

- example 3. join tournaments to its child
- INNER keeps matches only
- LEFT keeps every tournaments row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.name
FROM tournaments p
LEFT JOIN tournaments_child c ON c.parent_id = p.id
WHERE p.id = 't_9';
```

- homework
```sql
-- 3a  left join for t_9
-- 3b  inner join drops t_9 when it has no child
-- 3c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 3d  join on the key, not on name text
```

- example 4. join videos to its child
- INNER keeps matches only
- LEFT keeps every videos row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.title
FROM videos p
LEFT JOIN videos_child c ON c.parent_id = p.id
WHERE p.id = 'v_4';
```

- homework
```sql
-- 4a  left join for v_4
-- 4b  inner join drops v_4 when it has no child
-- 4c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 4d  join on the key, not on title text
```

- example 5. join facts to its child
- INNER keeps matches only
- LEFT keeps every facts row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.kind
FROM facts p
LEFT JOIN facts_child c ON c.parent_id = p.id
WHERE p.id = 'f_2';
```

- homework
```sql
-- 5a  left join for f_2
-- 5b  inner join drops f_2 when it has no child
-- 5c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 5d  join on the key, not on kind text
```

- example 6. join users to its child
- INNER keeps matches only
- LEFT keeps every users row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.email
FROM users p
LEFT JOIN users_child c ON c.parent_id = p.id
WHERE p.id = 'u_3';
```

- homework
```sql
-- 6a  left join for u_3
-- 6b  inner join drops u_3 when it has no child
-- 6c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 6d  join on the key, not on email text
```

- example 7. join payments to its child
- INNER keeps matches only
- LEFT keeps every payments row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.eventId
FROM payments p
LEFT JOIN payments_child c ON c.parent_id = p.id
WHERE p.id = 'pay_8';
```

- homework
```sql
-- 7a  left join for pay_8
-- 7b  inner join drops pay_8 when it has no child
-- 7c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 7d  join on the key, not on eventId text
```

- example 8. join rooms to its child
- INNER keeps matches only
- LEFT keeps every rooms row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.sessionId
FROM rooms p
LEFT JOIN rooms_child c ON c.parent_id = p.id
WHERE p.id = 'room_2';
```

- homework
```sql
-- 8a  left join for room_2
-- 8b  inner join drops room_2 when it has no child
-- 8c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 8d  join on the key, not on sessionId text
```

- example 9. join vessels to its child
- INNER keeps matches only
- LEFT keeps every vessels row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.name
FROM vessels p
LEFT JOIN vessels_child c ON c.parent_id = p.id
WHERE p.id = 'vs_7';
```

- homework
```sql
-- 9a  left join for vs_7
-- 9b  inner join drops vs_7 when it has no child
-- 9c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 9d  join on the key, not on name text
```

- example 10. join scores to its child
- INNER keeps matches only
- LEFT keeps every scores row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.points
FROM scores p
LEFT JOIN scores_child c ON c.parent_id = p.id
WHERE p.id = 'sc_3';
```

- homework
```sql
-- 10a  left join for sc_3
-- 10b  inner join drops sc_3 when it has no child
-- 10c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 10d  join on the key, not on points text
```

- example 11. join teams to its child
- INNER keeps matches only
- LEFT keeps every teams row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.name
FROM teams p
LEFT JOIN teams_child c ON c.parent_id = p.id
WHERE p.id = 'tm_2';
```

- homework
```sql
-- 11a  left join for tm_2
-- 11b  inner join drops tm_2 when it has no child
-- 11c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 11d  join on the key, not on name text
```

- example 12. join uploads to its child
- INNER keeps matches only
- LEFT keeps every uploads row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.key
FROM uploads p
LEFT JOIN uploads_child c ON c.parent_id = p.id
WHERE p.id = 'up_6';
```

- homework
```sql
-- 12a  left join for up_6
-- 12b  inner join drops up_6 when it has no child
-- 12c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 12d  join on the key, not on key text
```

- example 13. join standings to its child
- INNER keeps matches only
- LEFT keeps every standings row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.player
FROM standings p
LEFT JOIN standings_child c ON c.parent_id = p.id
WHERE p.id = 'st_1';
```

- homework
```sql
-- 13a  left join for st_1
-- 13b  inner join drops st_1 when it has no child
-- 13c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 13d  join on the key, not on player text
```

- example 14. join notices to its child
- INNER keeps matches only
- LEFT keeps every notices row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.port
FROM notices p
LEFT JOIN notices_child c ON c.parent_id = p.id
WHERE p.id = 'n_2';
```

- homework
```sql
-- 14a  left join for n_2
-- 14b  inner join drops n_2 when it has no child
-- 14c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 14d  join on the key, not on port text
```

- example 15. join brackets to its child
- INNER keeps matches only
- LEFT keeps every brackets row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.round
FROM brackets p
LEFT JOIN brackets_child c ON c.parent_id = p.id
WHERE p.id = 'b_3';
```

- homework
```sql
-- 15a  left join for b_3
-- 15b  inner join drops b_3 when it has no child
-- 15c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 15d  join on the key, not on round text
```

- example 16. join sessions to its child
- INNER keeps matches only
- LEFT keeps every sessions row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.userId
FROM sessions p
LEFT JOIN sessions_child c ON c.parent_id = p.id
WHERE p.id = 'se_1';
```

- homework
```sql
-- 16a  left join for se_1
-- 16b  inner join drops se_1 when it has no child
-- 16c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 16d  join on the key, not on userId text
```

- example 17. join queues to its child
- INNER keeps matches only
- LEFT keeps every queues row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.name
FROM queues p
LEFT JOIN queues_child c ON c.parent_id = p.id
WHERE p.id = 'q_1';
```

- homework
```sql
-- 17a  left join for q_1
-- 17b  inner join drops q_1 when it has no child
-- 17c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 17d  join on the key, not on name text
```

- example 18. join roles to its child
- INNER keeps matches only
- LEFT keeps every roles row. the child is NULL when there is none
- the kind filter belongs in ON if we still want childless parents

```sql
SELECT p.id, c.name
FROM roles p
LEFT JOIN roles_child c ON c.parent_id = p.id
WHERE p.id = 'r_1';
```

- homework
```sql
-- 18a  left join for r_1
-- 18b  inner join drops r_1 when it has no child
-- 18c  moving c.kind = 'NOR' into WHERE can drop the parent
-- 18d  join on the key, not on name text
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

- example 1. one fact, one place, for Ocean Star
- copying vesselName onto every child means a rename edits many rows
- the parent holds vesselName. the child holds the parent id pc_12
- a junction table is two ids and a primary key of both

```sql
-- bad: vesselName copied on every child row
-- good:
-- parents(id, vesselName)
-- children(id, parent_id)

INSERT INTO parents (id, vesselName) VALUES ('pc_12', 'Ocean Star');
```

- homework
```sql
-- 1a  where Ocean Star is stored once
-- 1b  the child column is parent_id, not a copy of vesselName
-- 1c  user_roles primary key is (user_id, role_id)
-- 1d  first normal form: one value in the cell, not a list
```

- example 2. one fact, one place, for Ada
- copying home onto every child means a rename edits many rows
- the parent holds home. the child holds the parent id m_1
- a junction table is two ids and a primary key of both

```sql
-- bad: home copied on every child row
-- good:
-- parents(id, home)
-- children(id, parent_id)

INSERT INTO parents (id, home) VALUES ('m_1', 'Ada');
```

- homework
```sql
-- 2a  where Ada is stored once
-- 2b  the child column is parent_id, not a copy of home
-- 2c  user_roles primary key is (user_id, role_id)
-- 2d  first normal form: one value in the cell, not a list
```

- example 3. one fact, one place, for Rajshahi Open
- copying name onto every child means a rename edits many rows
- the parent holds name. the child holds the parent id t_9
- a junction table is two ids and a primary key of both

```sql
-- bad: name copied on every child row
-- good:
-- parents(id, name)
-- children(id, parent_id)

INSERT INTO parents (id, name) VALUES ('t_9', 'Rajshahi Open');
```

- homework
```sql
-- 3a  where Rajshahi Open is stored once
-- 3b  the child column is parent_id, not a copy of name
-- 3c  user_roles primary key is (user_id, role_id)
-- 3d  first normal form: one value in the cell, not a list
```

- example 4. one fact, one place, for Episode 1
- copying title onto every child means a rename edits many rows
- the parent holds title. the child holds the parent id v_4
- a junction table is two ids and a primary key of both

```sql
-- bad: title copied on every child row
-- good:
-- parents(id, title)
-- children(id, parent_id)

INSERT INTO parents (id, title) VALUES ('v_4', 'Episode 1');
```

- homework
```sql
-- 4a  where Episode 1 is stored once
-- 4b  the child column is parent_id, not a copy of title
-- 4c  user_roles primary key is (user_id, role_id)
-- 4d  first normal form: one value in the cell, not a list
```

- example 5. one fact, one place, for NOR
- copying kind onto every child means a rename edits many rows
- the parent holds kind. the child holds the parent id f_2
- a junction table is two ids and a primary key of both

```sql
-- bad: kind copied on every child row
-- good:
-- parents(id, kind)
-- children(id, parent_id)

INSERT INTO parents (id, kind) VALUES ('f_2', 'NOR');
```

- homework
```sql
-- 5a  where NOR is stored once
-- 5b  the child column is parent_id, not a copy of kind
-- 5c  user_roles primary key is (user_id, role_id)
-- 5d  first normal form: one value in the cell, not a list
```

- example 6. one fact, one place, for a@example.com
- copying email onto every child means a rename edits many rows
- the parent holds email. the child holds the parent id u_3
- a junction table is two ids and a primary key of both

```sql
-- bad: email copied on every child row
-- good:
-- parents(id, email)
-- children(id, parent_id)

INSERT INTO parents (id, email) VALUES ('u_3', 'a@example.com');
```

- homework
```sql
-- 6a  where a@example.com is stored once
-- 6b  the child column is parent_id, not a copy of email
-- 6c  user_roles primary key is (user_id, role_id)
-- 6d  first normal form: one value in the cell, not a list
```

- example 7. one fact, one place, for evt_1
- copying eventId onto every child means a rename edits many rows
- the parent holds eventId. the child holds the parent id pay_8
- a junction table is two ids and a primary key of both

```sql
-- bad: eventId copied on every child row
-- good:
-- parents(id, eventId)
-- children(id, parent_id)

INSERT INTO parents (id, eventId) VALUES ('pay_8', 'evt_1');
```

- homework
```sql
-- 7a  where evt_1 is stored once
-- 7b  the child column is parent_id, not a copy of eventId
-- 7c  user_roles primary key is (user_id, role_id)
-- 7d  first normal form: one value in the cell, not a list
```

- example 8. one fact, one place, for s_9
- copying sessionId onto every child means a rename edits many rows
- the parent holds sessionId. the child holds the parent id room_2
- a junction table is two ids and a primary key of both

```sql
-- bad: sessionId copied on every child row
-- good:
-- parents(id, sessionId)
-- children(id, parent_id)

INSERT INTO parents (id, sessionId) VALUES ('room_2', 's_9');
```

- homework
```sql
-- 8a  where s_9 is stored once
-- 8b  the child column is parent_id, not a copy of sessionId
-- 8c  user_roles primary key is (user_id, role_id)
-- 8d  first normal form: one value in the cell, not a list
```

- example 9. one fact, one place, for North Wind
- copying name onto every child means a rename edits many rows
- the parent holds name. the child holds the parent id vs_7
- a junction table is two ids and a primary key of both

```sql
-- bad: name copied on every child row
-- good:
-- parents(id, name)
-- children(id, parent_id)

INSERT INTO parents (id, name) VALUES ('vs_7', 'North Wind');
```

- homework
```sql
-- 9a  where North Wind is stored once
-- 9b  the child column is parent_id, not a copy of name
-- 9c  user_roles primary key is (user_id, role_id)
-- 9d  first normal form: one value in the cell, not a list
```

- example 10. one fact, one place, for 11
- copying points onto every child means a rename edits many rows
- the parent holds points. the child holds the parent id sc_3
- a junction table is two ids and a primary key of both

```sql
-- bad: points copied on every child row
-- good:
-- parents(id, points)
-- children(id, parent_id)

INSERT INTO parents (id, points) VALUES ('sc_3', '11');
```

- homework
```sql
-- 10a  where 11 is stored once
-- 10b  the child column is parent_id, not a copy of points
-- 10c  user_roles primary key is (user_id, role_id)
-- 10d  first normal form: one value in the cell, not a list
```

- example 11. one fact, one place, for Blue
- copying name onto every child means a rename edits many rows
- the parent holds name. the child holds the parent id tm_2
- a junction table is two ids and a primary key of both

```sql
-- bad: name copied on every child row
-- good:
-- parents(id, name)
-- children(id, parent_id)

INSERT INTO parents (id, name) VALUES ('tm_2', 'Blue');
```

- homework
```sql
-- 11a  where Blue is stored once
-- 11b  the child column is parent_id, not a copy of name
-- 11c  user_roles primary key is (user_id, role_id)
-- 11d  first normal form: one value in the cell, not a list
```

- example 12. one fact, one place, for videos/u_1/a.mp4
- copying key onto every child means a rename edits many rows
- the parent holds key. the child holds the parent id up_6
- a junction table is two ids and a primary key of both

```sql
-- bad: key copied on every child row
-- good:
-- parents(id, key)
-- children(id, parent_id)

INSERT INTO parents (id, key) VALUES ('up_6', 'videos/u_1/a.mp4');
```

- homework
```sql
-- 12a  where videos/u_1/a.mp4 is stored once
-- 12b  the child column is parent_id, not a copy of key
-- 12c  user_roles primary key is (user_id, role_id)
-- 12d  first normal form: one value in the cell, not a list
```

- example 13. one fact, one place, for player_a
- copying player onto every child means a rename edits many rows
- the parent holds player. the child holds the parent id st_1
- a junction table is two ids and a primary key of both

```sql
-- bad: player copied on every child row
-- good:
-- parents(id, player)
-- children(id, parent_id)

INSERT INTO parents (id, player) VALUES ('st_1', 'player_a');
```

- homework
```sql
-- 13a  where player_a is stored once
-- 13b  the child column is parent_id, not a copy of player
-- 13c  user_roles primary key is (user_id, role_id)
-- 13d  first normal form: one value in the cell, not a list
```

- example 14. one fact, one place, for Chattogram
- copying port onto every child means a rename edits many rows
- the parent holds port. the child holds the parent id n_2
- a junction table is two ids and a primary key of both

```sql
-- bad: port copied on every child row
-- good:
-- parents(id, port)
-- children(id, parent_id)

INSERT INTO parents (id, port) VALUES ('n_2', 'Chattogram');
```

- homework
```sql
-- 14a  where Chattogram is stored once
-- 14b  the child column is parent_id, not a copy of port
-- 14c  user_roles primary key is (user_id, role_id)
-- 14d  first normal form: one value in the cell, not a list
```

- example 15. one fact, one place, for semi
- copying round onto every child means a rename edits many rows
- the parent holds round. the child holds the parent id b_3
- a junction table is two ids and a primary key of both

```sql
-- bad: round copied on every child row
-- good:
-- parents(id, round)
-- children(id, parent_id)

INSERT INTO parents (id, round) VALUES ('b_3', 'semi');
```

- homework
```sql
-- 15a  where semi is stored once
-- 15b  the child column is parent_id, not a copy of round
-- 15c  user_roles primary key is (user_id, role_id)
-- 15d  first normal form: one value in the cell, not a list
```

- example 16. one fact, one place, for u_3
- copying userId onto every child means a rename edits many rows
- the parent holds userId. the child holds the parent id se_1
- a junction table is two ids and a primary key of both

```sql
-- bad: userId copied on every child row
-- good:
-- parents(id, userId)
-- children(id, parent_id)

INSERT INTO parents (id, userId) VALUES ('se_1', 'u_3');
```

- homework
```sql
-- 16a  where u_3 is stored once
-- 16b  the child column is parent_id, not a copy of userId
-- 16c  user_roles primary key is (user_id, role_id)
-- 16d  first normal form: one value in the cell, not a list
```

- example 17. one fact, one place, for laytime
- copying name onto every child means a rename edits many rows
- the parent holds name. the child holds the parent id q_1
- a junction table is two ids and a primary key of both

```sql
-- bad: name copied on every child row
-- good:
-- parents(id, name)
-- children(id, parent_id)

INSERT INTO parents (id, name) VALUES ('q_1', 'laytime');
```

- homework
```sql
-- 17a  where laytime is stored once
-- 17b  the child column is parent_id, not a copy of name
-- 17c  user_roles primary key is (user_id, role_id)
-- 17d  first normal form: one value in the cell, not a list
```

- example 18. one fact, one place, for operator
- copying name onto every child means a rename edits many rows
- the parent holds name. the child holds the parent id r_1
- a junction table is two ids and a primary key of both

```sql
-- bad: name copied on every child row
-- good:
-- parents(id, name)
-- children(id, parent_id)

INSERT INTO parents (id, name) VALUES ('r_1', 'operator');
```

- homework
```sql
-- 18a  where operator is stored once
-- 18b  the child column is parent_id, not a copy of name
-- 18c  user_roles primary key is (user_id, role_id)
-- 18d  first normal form: one value in the cell, not a list
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

- example 1. index for port_calls(vesselName) and for (pc_12 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX port_calls_vesselName_idx ON port_calls (vesselName);
CREATE INDEX port_calls_parent_kind_idx ON port_calls (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 1a  index the column we filter for pc_12
-- 1b  B+ tree, not a hash index, for a range on vesselName
-- 1c  an unused index still costs writes
-- 1d  leftmost prefix of (parent_id, kind)
```

- example 2. index for matches(home) and for (m_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX matches_home_idx ON matches (home);
CREATE INDEX matches_parent_kind_idx ON matches (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 2a  index the column we filter for m_1
-- 2b  B+ tree, not a hash index, for a range on home
-- 2c  an unused index still costs writes
-- 2d  leftmost prefix of (parent_id, kind)
```

- example 3. index for tournaments(name) and for (t_9 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX tournaments_name_idx ON tournaments (name);
CREATE INDEX tournaments_parent_kind_idx ON tournaments (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 3a  index the column we filter for t_9
-- 3b  B+ tree, not a hash index, for a range on name
-- 3c  an unused index still costs writes
-- 3d  leftmost prefix of (parent_id, kind)
```

- example 4. index for videos(title) and for (v_4 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX videos_title_idx ON videos (title);
CREATE INDEX videos_parent_kind_idx ON videos (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 4a  index the column we filter for v_4
-- 4b  B+ tree, not a hash index, for a range on title
-- 4c  an unused index still costs writes
-- 4d  leftmost prefix of (parent_id, kind)
```

- example 5. index for facts(kind) and for (f_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX facts_kind_idx ON facts (kind);
CREATE INDEX facts_parent_kind_idx ON facts (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 5a  index the column we filter for f_2
-- 5b  B+ tree, not a hash index, for a range on kind
-- 5c  an unused index still costs writes
-- 5d  leftmost prefix of (parent_id, kind)
```

- example 6. index for users(email) and for (u_3 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX users_email_idx ON users (email);
CREATE INDEX users_parent_kind_idx ON users (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 6a  index the column we filter for u_3
-- 6b  B+ tree, not a hash index, for a range on email
-- 6c  an unused index still costs writes
-- 6d  leftmost prefix of (parent_id, kind)
```

- example 7. index for payments(eventId) and for (pay_8 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX payments_eventId_idx ON payments (eventId);
CREATE INDEX payments_parent_kind_idx ON payments (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 7a  index the column we filter for pay_8
-- 7b  B+ tree, not a hash index, for a range on eventId
-- 7c  an unused index still costs writes
-- 7d  leftmost prefix of (parent_id, kind)
```

- example 8. index for rooms(sessionId) and for (room_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX rooms_sessionId_idx ON rooms (sessionId);
CREATE INDEX rooms_parent_kind_idx ON rooms (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 8a  index the column we filter for room_2
-- 8b  B+ tree, not a hash index, for a range on sessionId
-- 8c  an unused index still costs writes
-- 8d  leftmost prefix of (parent_id, kind)
```

- example 9. index for vessels(name) and for (vs_7 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX vessels_name_idx ON vessels (name);
CREATE INDEX vessels_parent_kind_idx ON vessels (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 9a  index the column we filter for vs_7
-- 9b  B+ tree, not a hash index, for a range on name
-- 9c  an unused index still costs writes
-- 9d  leftmost prefix of (parent_id, kind)
```

- example 10. index for scores(points) and for (sc_3 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX scores_points_idx ON scores (points);
CREATE INDEX scores_parent_kind_idx ON scores (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 10a  index the column we filter for sc_3
-- 10b  B+ tree, not a hash index, for a range on points
-- 10c  an unused index still costs writes
-- 10d  leftmost prefix of (parent_id, kind)
```

- example 11. index for teams(name) and for (tm_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX teams_name_idx ON teams (name);
CREATE INDEX teams_parent_kind_idx ON teams (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 11a  index the column we filter for tm_2
-- 11b  B+ tree, not a hash index, for a range on name
-- 11c  an unused index still costs writes
-- 11d  leftmost prefix of (parent_id, kind)
```

- example 12. index for uploads(key) and for (up_6 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX uploads_key_idx ON uploads (key);
CREATE INDEX uploads_parent_kind_idx ON uploads (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 12a  index the column we filter for up_6
-- 12b  B+ tree, not a hash index, for a range on key
-- 12c  an unused index still costs writes
-- 12d  leftmost prefix of (parent_id, kind)
```

- example 13. index for standings(player) and for (st_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX standings_player_idx ON standings (player);
CREATE INDEX standings_parent_kind_idx ON standings (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 13a  index the column we filter for st_1
-- 13b  B+ tree, not a hash index, for a range on player
-- 13c  an unused index still costs writes
-- 13d  leftmost prefix of (parent_id, kind)
```

- example 14. index for notices(port) and for (n_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX notices_port_idx ON notices (port);
CREATE INDEX notices_parent_kind_idx ON notices (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 14a  index the column we filter for n_2
-- 14b  B+ tree, not a hash index, for a range on port
-- 14c  an unused index still costs writes
-- 14d  leftmost prefix of (parent_id, kind)
```

- example 15. index for brackets(round) and for (b_3 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX brackets_round_idx ON brackets (round);
CREATE INDEX brackets_parent_kind_idx ON brackets (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 15a  index the column we filter for b_3
-- 15b  B+ tree, not a hash index, for a range on round
-- 15c  an unused index still costs writes
-- 15d  leftmost prefix of (parent_id, kind)
```

- example 16. index for sessions(userId) and for (se_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX sessions_userId_idx ON sessions (userId);
CREATE INDEX sessions_parent_kind_idx ON sessions (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 16a  index the column we filter for se_1
-- 16b  B+ tree, not a hash index, for a range on userId
-- 16c  an unused index still costs writes
-- 16d  leftmost prefix of (parent_id, kind)
```

- example 17. index for queues(name) and for (q_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX queues_name_idx ON queues (name);
CREATE INDEX queues_parent_kind_idx ON queues (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 17a  index the column we filter for q_1
-- 17b  B+ tree, not a hash index, for a range on name
-- 17c  an unused index still costs writes
-- 17d  leftmost prefix of (parent_id, kind)
```

- example 18. index for roles(name) and for (r_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX roles_name_idx ON roles (name);
CREATE INDEX roles_parent_kind_idx ON roles (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 18a  index the column we filter for r_1
-- 18b  B+ tree, not a hash index, for a range on name
-- 18c  an unused index still costs writes
-- 18d  leftmost prefix of (parent_id, kind)
```

- example 19. index for port_calls(vesselName) and for (pc_12 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX port_calls_vesselName_idx ON port_calls (vesselName);
CREATE INDEX port_calls_parent_kind_idx ON port_calls (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 19a  index the column we filter for pc_12
-- 19b  B+ tree, not a hash index, for a range on vesselName
-- 19c  an unused index still costs writes
-- 19d  leftmost prefix of (parent_id, kind)
```

- example 20. index for matches(home) and for (m_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX matches_home_idx ON matches (home);
CREATE INDEX matches_parent_kind_idx ON matches (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 20a  index the column we filter for m_1
-- 20b  B+ tree, not a hash index, for a range on home
-- 20c  an unused index still costs writes
-- 20d  leftmost prefix of (parent_id, kind)
```

- example 21. index for tournaments(name) and for (t_9 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX tournaments_name_idx ON tournaments (name);
CREATE INDEX tournaments_parent_kind_idx ON tournaments (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 21a  index the column we filter for t_9
-- 21b  B+ tree, not a hash index, for a range on name
-- 21c  an unused index still costs writes
-- 21d  leftmost prefix of (parent_id, kind)
```

- example 22. index for videos(title) and for (v_4 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX videos_title_idx ON videos (title);
CREATE INDEX videos_parent_kind_idx ON videos (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 22a  index the column we filter for v_4
-- 22b  B+ tree, not a hash index, for a range on title
-- 22c  an unused index still costs writes
-- 22d  leftmost prefix of (parent_id, kind)
```

- example 23. index for facts(kind) and for (f_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX facts_kind_idx ON facts (kind);
CREATE INDEX facts_parent_kind_idx ON facts (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 23a  index the column we filter for f_2
-- 23b  B+ tree, not a hash index, for a range on kind
-- 23c  an unused index still costs writes
-- 23d  leftmost prefix of (parent_id, kind)
```

- example 24. index for users(email) and for (u_3 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX users_email_idx ON users (email);
CREATE INDEX users_parent_kind_idx ON users (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 24a  index the column we filter for u_3
-- 24b  B+ tree, not a hash index, for a range on email
-- 24c  an unused index still costs writes
-- 24d  leftmost prefix of (parent_id, kind)
```

- example 25. index for payments(eventId) and for (pay_8 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX payments_eventId_idx ON payments (eventId);
CREATE INDEX payments_parent_kind_idx ON payments (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 25a  index the column we filter for pay_8
-- 25b  B+ tree, not a hash index, for a range on eventId
-- 25c  an unused index still costs writes
-- 25d  leftmost prefix of (parent_id, kind)
```

- example 26. index for rooms(sessionId) and for (room_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX rooms_sessionId_idx ON rooms (sessionId);
CREATE INDEX rooms_parent_kind_idx ON rooms (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 26a  index the column we filter for room_2
-- 26b  B+ tree, not a hash index, for a range on sessionId
-- 26c  an unused index still costs writes
-- 26d  leftmost prefix of (parent_id, kind)
```

- example 27. index for vessels(name) and for (vs_7 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX vessels_name_idx ON vessels (name);
CREATE INDEX vessels_parent_kind_idx ON vessels (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 27a  index the column we filter for vs_7
-- 27b  B+ tree, not a hash index, for a range on name
-- 27c  an unused index still costs writes
-- 27d  leftmost prefix of (parent_id, kind)
```

- example 28. index for scores(points) and for (sc_3 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX scores_points_idx ON scores (points);
CREATE INDEX scores_parent_kind_idx ON scores (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 28a  index the column we filter for sc_3
-- 28b  B+ tree, not a hash index, for a range on points
-- 28c  an unused index still costs writes
-- 28d  leftmost prefix of (parent_id, kind)
```

- example 29. index for teams(name) and for (tm_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX teams_name_idx ON teams (name);
CREATE INDEX teams_parent_kind_idx ON teams (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 29a  index the column we filter for tm_2
-- 29b  B+ tree, not a hash index, for a range on name
-- 29c  an unused index still costs writes
-- 29d  leftmost prefix of (parent_id, kind)
```

- example 30. index for uploads(key) and for (up_6 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX uploads_key_idx ON uploads (key);
CREATE INDEX uploads_parent_kind_idx ON uploads (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 30a  index the column we filter for up_6
-- 30b  B+ tree, not a hash index, for a range on key
-- 30c  an unused index still costs writes
-- 30d  leftmost prefix of (parent_id, kind)
```

- example 31. index for standings(player) and for (st_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX standings_player_idx ON standings (player);
CREATE INDEX standings_parent_kind_idx ON standings (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 31a  index the column we filter for st_1
-- 31b  B+ tree, not a hash index, for a range on player
-- 31c  an unused index still costs writes
-- 31d  leftmost prefix of (parent_id, kind)
```

- example 32. index for notices(port) and for (n_2 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX notices_port_idx ON notices (port);
CREATE INDEX notices_parent_kind_idx ON notices (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 32a  index the column we filter for n_2
-- 32b  B+ tree, not a hash index, for a range on port
-- 32c  an unused index still costs writes
-- 32d  leftmost prefix of (parent_id, kind)
```

- example 33. index for brackets(round) and for (b_3 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX brackets_round_idx ON brackets (round);
CREATE INDEX brackets_parent_kind_idx ON brackets (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 33a  index the column we filter for b_3
-- 33b  B+ tree, not a hash index, for a range on round
-- 33c  an unused index still costs writes
-- 33d  leftmost prefix of (parent_id, kind)
```

- example 34. index for sessions(userId) and for (se_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX sessions_userId_idx ON sessions (userId);
CREATE INDEX sessions_parent_kind_idx ON sessions (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 34a  index the column we filter for se_1
-- 34b  B+ tree, not a hash index, for a range on userId
-- 34c  an unused index still costs writes
-- 34d  leftmost prefix of (parent_id, kind)
```

- example 35. index for queues(name) and for (q_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX queues_name_idx ON queues (name);
CREATE INDEX queues_parent_kind_idx ON queues (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 35a  index the column we filter for q_1
-- 35b  B+ tree, not a hash index, for a range on name
-- 35c  an unused index still costs writes
-- 35d  leftmost prefix of (parent_id, kind)
```

- example 36. index for roles(name) and for (r_1 lookup)
- a normal CREATE INDEX in Postgres is a B+ tree
- the tree answers equality and a range
- composite (parent_id, kind) serves the left prefix
- every insert maintains the index

```sql
CREATE INDEX roles_name_idx ON roles (name);
CREATE INDEX roles_parent_kind_idx ON roles (parent_id, kind);
-- serves parent_id, and parent_id + kind
-- does not serve kind alone
```

- homework
```sql
-- 36a  index the column we filter for r_1
-- 36b  B+ tree, not a hash index, for a range on name
-- 36c  an unused index still costs writes
-- 36d  leftmost prefix of (parent_id, kind)
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

- example 1. one transaction for pc_12 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO port_calls (id, vesselName) VALUES ('pc_12', 'Ocean Star');
INSERT INTO port_calls_child (id, parent_id) VALUES ('pc_12_c', 'pc_12');
COMMIT;
```

- homework
```sql
-- 1a  if the second insert fails, pc_12 is rolled back
-- 1b  durable means a crash after COMMIT keeps Ocean Star
-- 1c  do not hold this transaction open during ffmpeg
-- 1d  Prisma $transaction is the same bracket
```

- example 2. one transaction for m_1 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO matches (id, home) VALUES ('m_1', 'Ada');
INSERT INTO matches_child (id, parent_id) VALUES ('m_1_c', 'm_1');
COMMIT;
```

- homework
```sql
-- 2a  if the second insert fails, m_1 is rolled back
-- 2b  durable means a crash after COMMIT keeps Ada
-- 2c  do not hold this transaction open during ffmpeg
-- 2d  Prisma $transaction is the same bracket
```

- example 3. one transaction for t_9 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO tournaments (id, name) VALUES ('t_9', 'Rajshahi Open');
INSERT INTO tournaments_child (id, parent_id) VALUES ('t_9_c', 't_9');
COMMIT;
```

- homework
```sql
-- 3a  if the second insert fails, t_9 is rolled back
-- 3b  durable means a crash after COMMIT keeps Rajshahi Open
-- 3c  do not hold this transaction open during ffmpeg
-- 3d  Prisma $transaction is the same bracket
```

- example 4. one transaction for v_4 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO videos (id, title) VALUES ('v_4', 'Episode 1');
INSERT INTO videos_child (id, parent_id) VALUES ('v_4_c', 'v_4');
COMMIT;
```

- homework
```sql
-- 4a  if the second insert fails, v_4 is rolled back
-- 4b  durable means a crash after COMMIT keeps Episode 1
-- 4c  do not hold this transaction open during ffmpeg
-- 4d  Prisma $transaction is the same bracket
```

- example 5. one transaction for f_2 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO facts (id, kind) VALUES ('f_2', 'NOR');
INSERT INTO facts_child (id, parent_id) VALUES ('f_2_c', 'f_2');
COMMIT;
```

- homework
```sql
-- 5a  if the second insert fails, f_2 is rolled back
-- 5b  durable means a crash after COMMIT keeps NOR
-- 5c  do not hold this transaction open during ffmpeg
-- 5d  Prisma $transaction is the same bracket
```

- example 6. one transaction for u_3 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO users (id, email) VALUES ('u_3', 'a@example.com');
INSERT INTO users_child (id, parent_id) VALUES ('u_3_c', 'u_3');
COMMIT;
```

- homework
```sql
-- 6a  if the second insert fails, u_3 is rolled back
-- 6b  durable means a crash after COMMIT keeps a@example.com
-- 6c  do not hold this transaction open during ffmpeg
-- 6d  Prisma $transaction is the same bracket
```

- example 7. one transaction for pay_8 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO payments (id, eventId) VALUES ('pay_8', 'evt_1');
INSERT INTO payments_child (id, parent_id) VALUES ('pay_8_c', 'pay_8');
COMMIT;
```

- homework
```sql
-- 7a  if the second insert fails, pay_8 is rolled back
-- 7b  durable means a crash after COMMIT keeps evt_1
-- 7c  do not hold this transaction open during ffmpeg
-- 7d  Prisma $transaction is the same bracket
```

- example 8. one transaction for room_2 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO rooms (id, sessionId) VALUES ('room_2', 's_9');
INSERT INTO rooms_child (id, parent_id) VALUES ('room_2_c', 'room_2');
COMMIT;
```

- homework
```sql
-- 8a  if the second insert fails, room_2 is rolled back
-- 8b  durable means a crash after COMMIT keeps s_9
-- 8c  do not hold this transaction open during ffmpeg
-- 8d  Prisma $transaction is the same bracket
```

- example 9. one transaction for vs_7 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO vessels (id, name) VALUES ('vs_7', 'North Wind');
INSERT INTO vessels_child (id, parent_id) VALUES ('vs_7_c', 'vs_7');
COMMIT;
```

- homework
```sql
-- 9a  if the second insert fails, vs_7 is rolled back
-- 9b  durable means a crash after COMMIT keeps North Wind
-- 9c  do not hold this transaction open during ffmpeg
-- 9d  Prisma $transaction is the same bracket
```

- example 10. one transaction for sc_3 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO scores (id, points) VALUES ('sc_3', '11');
INSERT INTO scores_child (id, parent_id) VALUES ('sc_3_c', 'sc_3');
COMMIT;
```

- homework
```sql
-- 10a  if the second insert fails, sc_3 is rolled back
-- 10b  durable means a crash after COMMIT keeps 11
-- 10c  do not hold this transaction open during ffmpeg
-- 10d  Prisma $transaction is the same bracket
```

- example 11. one transaction for tm_2 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO teams (id, name) VALUES ('tm_2', 'Blue');
INSERT INTO teams_child (id, parent_id) VALUES ('tm_2_c', 'tm_2');
COMMIT;
```

- homework
```sql
-- 11a  if the second insert fails, tm_2 is rolled back
-- 11b  durable means a crash after COMMIT keeps Blue
-- 11c  do not hold this transaction open during ffmpeg
-- 11d  Prisma $transaction is the same bracket
```

- example 12. one transaction for up_6 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO uploads (id, key) VALUES ('up_6', 'videos/u_1/a.mp4');
INSERT INTO uploads_child (id, parent_id) VALUES ('up_6_c', 'up_6');
COMMIT;
```

- homework
```sql
-- 12a  if the second insert fails, up_6 is rolled back
-- 12b  durable means a crash after COMMIT keeps videos/u_1/a.mp4
-- 12c  do not hold this transaction open during ffmpeg
-- 12d  Prisma $transaction is the same bracket
```

- example 13. one transaction for st_1 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO standings (id, player) VALUES ('st_1', 'player_a');
INSERT INTO standings_child (id, parent_id) VALUES ('st_1_c', 'st_1');
COMMIT;
```

- homework
```sql
-- 13a  if the second insert fails, st_1 is rolled back
-- 13b  durable means a crash after COMMIT keeps player_a
-- 13c  do not hold this transaction open during ffmpeg
-- 13d  Prisma $transaction is the same bracket
```

- example 14. one transaction for n_2 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO notices (id, port) VALUES ('n_2', 'Chattogram');
INSERT INTO notices_child (id, parent_id) VALUES ('n_2_c', 'n_2');
COMMIT;
```

- homework
```sql
-- 14a  if the second insert fails, n_2 is rolled back
-- 14b  durable means a crash after COMMIT keeps Chattogram
-- 14c  do not hold this transaction open during ffmpeg
-- 14d  Prisma $transaction is the same bracket
```

- example 15. one transaction for b_3 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO brackets (id, round) VALUES ('b_3', 'semi');
INSERT INTO brackets_child (id, parent_id) VALUES ('b_3_c', 'b_3');
COMMIT;
```

- homework
```sql
-- 15a  if the second insert fails, b_3 is rolled back
-- 15b  durable means a crash after COMMIT keeps semi
-- 15c  do not hold this transaction open during ffmpeg
-- 15d  Prisma $transaction is the same bracket
```

- example 16. one transaction for se_1 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO sessions (id, userId) VALUES ('se_1', 'u_3');
INSERT INTO sessions_child (id, parent_id) VALUES ('se_1_c', 'se_1');
COMMIT;
```

- homework
```sql
-- 16a  if the second insert fails, se_1 is rolled back
-- 16b  durable means a crash after COMMIT keeps u_3
-- 16c  do not hold this transaction open during ffmpeg
-- 16d  Prisma $transaction is the same bracket
```

- example 17. one transaction for q_1 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO queues (id, name) VALUES ('q_1', 'laytime');
INSERT INTO queues_child (id, parent_id) VALUES ('q_1_c', 'q_1');
COMMIT;
```

- homework
```sql
-- 17a  if the second insert fails, q_1 is rolled back
-- 17b  durable means a crash after COMMIT keeps laytime
-- 17c  do not hold this transaction open during ffmpeg
-- 17d  Prisma $transaction is the same bracket
```

- example 18. one transaction for r_1 and its first child
- atomic: both inserts commit, or neither does
- BEGIN, the two inserts, COMMIT
- a slow encode stays outside this block

```sql
BEGIN;
INSERT INTO roles (id, name) VALUES ('r_1', 'operator');
INSERT INTO roles_child (id, parent_id) VALUES ('r_1_c', 'r_1');
COMMIT;
```

- homework
```sql
-- 18a  if the second insert fails, r_1 is rolled back
-- 18b  durable means a crash after COMMIT keeps operator
-- 18c  do not hold this transaction open during ffmpeg
-- 18d  Prisma $transaction is the same bracket
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

- example 1. one UPDATE for a counter related to pc_12
- two reads of 72 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'pc_12';

BEGIN;
SELECT id FROM port_calls WHERE id = 'pc_12' FOR UPDATE;
UPDATE port_calls SET vesselName = 'Ocean Star' WHERE id = 'pc_12';
COMMIT;
```

- homework
```sql
-- 1a  lost update if both read 72 and both write 72+1
-- 1b  the single UPDATE above
-- 1c  default isolation is read committed
-- 1d  lock pc_12 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 2. one UPDATE for a counter related to m_1
- two reads of 3 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'm_1';

BEGIN;
SELECT id FROM matches WHERE id = 'm_1' FOR UPDATE;
UPDATE matches SET home = 'Ada' WHERE id = 'm_1';
COMMIT;
```

- homework
```sql
-- 2a  lost update if both read 3 and both write 3+1
-- 2b  the single UPDATE above
-- 2c  default isolation is read committed
-- 2d  lock m_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 3. one UPDATE for a counter related to t_9
- two reads of 16 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 't_9';

BEGIN;
SELECT id FROM tournaments WHERE id = 't_9' FOR UPDATE;
UPDATE tournaments SET name = 'Rajshahi Open' WHERE id = 't_9';
COMMIT;
```

- homework
```sql
-- 3a  lost update if both read 16 and both write 16+1
-- 3b  the single UPDATE above
-- 3c  default isolation is read committed
-- 3d  lock t_9 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 4. one UPDATE for a counter related to v_4
- two reads of 6 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'v_4';

BEGIN;
SELECT id FROM videos WHERE id = 'v_4' FOR UPDATE;
UPDATE videos SET title = 'Episode 1' WHERE id = 'v_4';
COMMIT;
```

- homework
```sql
-- 4a  lost update if both read 6 and both write 6+1
-- 4b  the single UPDATE above
-- 4c  default isolation is read committed
-- 4d  lock v_4 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 5. one UPDATE for a counter related to f_2
- two reads of 1 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'f_2';

BEGIN;
SELECT id FROM facts WHERE id = 'f_2' FOR UPDATE;
UPDATE facts SET kind = 'NOR' WHERE id = 'f_2';
COMMIT;
```

- homework
```sql
-- 5a  lost update if both read 1 and both write 1+1
-- 5b  the single UPDATE above
-- 5c  default isolation is read committed
-- 5d  lock f_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 6. one UPDATE for a counter related to u_3
- two reads of 1 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'u_3';

BEGIN;
SELECT id FROM users WHERE id = 'u_3' FOR UPDATE;
UPDATE users SET email = 'a@example.com' WHERE id = 'u_3';
COMMIT;
```

- homework
```sql
-- 6a  lost update if both read 1 and both write 1+1
-- 6b  the single UPDATE above
-- 6c  default isolation is read committed
-- 6d  lock u_3 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 7. one UPDATE for a counter related to pay_8
- two reads of 15000 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'pay_8';

BEGIN;
SELECT id FROM payments WHERE id = 'pay_8' FOR UPDATE;
UPDATE payments SET eventId = 'evt_1' WHERE id = 'pay_8';
COMMIT;
```

- homework
```sql
-- 7a  lost update if both read 15000 and both write 15000+1
-- 7b  the single UPDATE above
-- 7c  default isolation is read committed
-- 7d  lock pay_8 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 8. one UPDATE for a counter related to room_2
- two reads of 12 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'room_2';

BEGIN;
SELECT id FROM rooms WHERE id = 'room_2' FOR UPDATE;
UPDATE rooms SET sessionId = 's_9' WHERE id = 'room_2';
COMMIT;
```

- homework
```sql
-- 8a  lost update if both read 12 and both write 12+1
-- 8b  the single UPDATE above
-- 8c  default isolation is read committed
-- 8d  lock room_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 9. one UPDATE for a counter related to vs_7
- two reads of 48 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'vs_7';

BEGIN;
SELECT id FROM vessels WHERE id = 'vs_7' FOR UPDATE;
UPDATE vessels SET name = 'North Wind' WHERE id = 'vs_7';
COMMIT;
```

- homework
```sql
-- 9a  lost update if both read 48 and both write 48+1
-- 9b  the single UPDATE above
-- 9c  default isolation is read committed
-- 9d  lock vs_7 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 10. one UPDATE for a counter related to sc_3
- two reads of 11 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'sc_3';

BEGIN;
SELECT id FROM scores WHERE id = 'sc_3' FOR UPDATE;
UPDATE scores SET points = '11' WHERE id = 'sc_3';
COMMIT;
```

- homework
```sql
-- 10a  lost update if both read 11 and both write 11+1
-- 10b  the single UPDATE above
-- 10c  default isolation is read committed
-- 10d  lock sc_3 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 11. one UPDATE for a counter related to tm_2
- two reads of 2 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'tm_2';

BEGIN;
SELECT id FROM teams WHERE id = 'tm_2' FOR UPDATE;
UPDATE teams SET name = 'Blue' WHERE id = 'tm_2';
COMMIT;
```

- homework
```sql
-- 11a  lost update if both read 2 and both write 2+1
-- 11b  the single UPDATE above
-- 11c  default isolation is read committed
-- 11d  lock tm_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 12. one UPDATE for a counter related to up_6
- two reads of 200 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'up_6';

BEGIN;
SELECT id FROM uploads WHERE id = 'up_6' FOR UPDATE;
UPDATE uploads SET key = 'videos/u_1/a.mp4' WHERE id = 'up_6';
COMMIT;
```

- homework
```sql
-- 12a  lost update if both read 200 and both write 200+1
-- 12b  the single UPDATE above
-- 12c  default isolation is read committed
-- 12d  lock up_6 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 13. one UPDATE for a counter related to st_1
- two reads of 1500 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'st_1';

BEGIN;
SELECT id FROM standings WHERE id = 'st_1' FOR UPDATE;
UPDATE standings SET player = 'player_a' WHERE id = 'st_1';
COMMIT;
```

- homework
```sql
-- 13a  lost update if both read 1500 and both write 1500+1
-- 13b  the single UPDATE above
-- 13c  default isolation is read committed
-- 13d  lock st_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 14. one UPDATE for a counter related to n_2
- two reads of 24 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'n_2';

BEGIN;
SELECT id FROM notices WHERE id = 'n_2' FOR UPDATE;
UPDATE notices SET port = 'Chattogram' WHERE id = 'n_2';
COMMIT;
```

- homework
```sql
-- 14a  lost update if both read 24 and both write 24+1
-- 14b  the single UPDATE above
-- 14c  default isolation is read committed
-- 14d  lock n_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 15. one UPDATE for a counter related to b_3
- two reads of 4 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'b_3';

BEGIN;
SELECT id FROM brackets WHERE id = 'b_3' FOR UPDATE;
UPDATE brackets SET round = 'semi' WHERE id = 'b_3';
COMMIT;
```

- homework
```sql
-- 15a  lost update if both read 4 and both write 4+1
-- 15b  the single UPDATE above
-- 15c  default isolation is read committed
-- 15d  lock b_3 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 16. one UPDATE for a counter related to se_1
- two reads of 15 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'se_1';

BEGIN;
SELECT id FROM sessions WHERE id = 'se_1' FOR UPDATE;
UPDATE sessions SET userId = 'u_3' WHERE id = 'se_1';
COMMIT;
```

- homework
```sql
-- 16a  lost update if both read 15 and both write 15+1
-- 16b  the single UPDATE above
-- 16c  default isolation is read committed
-- 16d  lock se_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 17. one UPDATE for a counter related to q_1
- two reads of 10 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'q_1';

BEGIN;
SELECT id FROM queues WHERE id = 'q_1' FOR UPDATE;
UPDATE queues SET name = 'laytime' WHERE id = 'q_1';
COMMIT;
```

- homework
```sql
-- 17a  lost update if both read 10 and both write 10+1
-- 17b  the single UPDATE above
-- 17c  default isolation is read committed
-- 17d  lock q_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 18. one UPDATE for a counter related to r_1
- two reads of 2 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'r_1';

BEGIN;
SELECT id FROM roles WHERE id = 'r_1' FOR UPDATE;
UPDATE roles SET name = 'operator' WHERE id = 'r_1';
COMMIT;
```

- homework
```sql
-- 18a  lost update if both read 2 and both write 2+1
-- 18b  the single UPDATE above
-- 18c  default isolation is read committed
-- 18d  lock r_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 19. one UPDATE for a counter related to pc_12
- two reads of 72 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'pc_12';

BEGIN;
SELECT id FROM port_calls WHERE id = 'pc_12' FOR UPDATE;
UPDATE port_calls SET vesselName = 'Ocean Star' WHERE id = 'pc_12';
COMMIT;
```

- homework
```sql
-- 19a  lost update if both read 72 and both write 72+1
-- 19b  the single UPDATE above
-- 19c  default isolation is read committed
-- 19d  lock pc_12 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 20. one UPDATE for a counter related to m_1
- two reads of 3 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'm_1';

BEGIN;
SELECT id FROM matches WHERE id = 'm_1' FOR UPDATE;
UPDATE matches SET home = 'Ada' WHERE id = 'm_1';
COMMIT;
```

- homework
```sql
-- 20a  lost update if both read 3 and both write 3+1
-- 20b  the single UPDATE above
-- 20c  default isolation is read committed
-- 20d  lock m_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 21. one UPDATE for a counter related to t_9
- two reads of 16 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 't_9';

BEGIN;
SELECT id FROM tournaments WHERE id = 't_9' FOR UPDATE;
UPDATE tournaments SET name = 'Rajshahi Open' WHERE id = 't_9';
COMMIT;
```

- homework
```sql
-- 21a  lost update if both read 16 and both write 16+1
-- 21b  the single UPDATE above
-- 21c  default isolation is read committed
-- 21d  lock t_9 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 22. one UPDATE for a counter related to v_4
- two reads of 6 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'v_4';

BEGIN;
SELECT id FROM videos WHERE id = 'v_4' FOR UPDATE;
UPDATE videos SET title = 'Episode 1' WHERE id = 'v_4';
COMMIT;
```

- homework
```sql
-- 22a  lost update if both read 6 and both write 6+1
-- 22b  the single UPDATE above
-- 22c  default isolation is read committed
-- 22d  lock v_4 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 23. one UPDATE for a counter related to f_2
- two reads of 1 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'f_2';

BEGIN;
SELECT id FROM facts WHERE id = 'f_2' FOR UPDATE;
UPDATE facts SET kind = 'NOR' WHERE id = 'f_2';
COMMIT;
```

- homework
```sql
-- 23a  lost update if both read 1 and both write 1+1
-- 23b  the single UPDATE above
-- 23c  default isolation is read committed
-- 23d  lock f_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 24. one UPDATE for a counter related to u_3
- two reads of 1 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'u_3';

BEGIN;
SELECT id FROM users WHERE id = 'u_3' FOR UPDATE;
UPDATE users SET email = 'a@example.com' WHERE id = 'u_3';
COMMIT;
```

- homework
```sql
-- 24a  lost update if both read 1 and both write 1+1
-- 24b  the single UPDATE above
-- 24c  default isolation is read committed
-- 24d  lock u_3 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 25. one UPDATE for a counter related to pay_8
- two reads of 15000 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'pay_8';

BEGIN;
SELECT id FROM payments WHERE id = 'pay_8' FOR UPDATE;
UPDATE payments SET eventId = 'evt_1' WHERE id = 'pay_8';
COMMIT;
```

- homework
```sql
-- 25a  lost update if both read 15000 and both write 15000+1
-- 25b  the single UPDATE above
-- 25c  default isolation is read committed
-- 25d  lock pay_8 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 26. one UPDATE for a counter related to room_2
- two reads of 12 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'room_2';

BEGIN;
SELECT id FROM rooms WHERE id = 'room_2' FOR UPDATE;
UPDATE rooms SET sessionId = 's_9' WHERE id = 'room_2';
COMMIT;
```

- homework
```sql
-- 26a  lost update if both read 12 and both write 12+1
-- 26b  the single UPDATE above
-- 26c  default isolation is read committed
-- 26d  lock room_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 27. one UPDATE for a counter related to vs_7
- two reads of 48 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'vs_7';

BEGIN;
SELECT id FROM vessels WHERE id = 'vs_7' FOR UPDATE;
UPDATE vessels SET name = 'North Wind' WHERE id = 'vs_7';
COMMIT;
```

- homework
```sql
-- 27a  lost update if both read 48 and both write 48+1
-- 27b  the single UPDATE above
-- 27c  default isolation is read committed
-- 27d  lock vs_7 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 28. one UPDATE for a counter related to sc_3
- two reads of 11 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'sc_3';

BEGIN;
SELECT id FROM scores WHERE id = 'sc_3' FOR UPDATE;
UPDATE scores SET points = '11' WHERE id = 'sc_3';
COMMIT;
```

- homework
```sql
-- 28a  lost update if both read 11 and both write 11+1
-- 28b  the single UPDATE above
-- 28c  default isolation is read committed
-- 28d  lock sc_3 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 29. one UPDATE for a counter related to tm_2
- two reads of 2 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'tm_2';

BEGIN;
SELECT id FROM teams WHERE id = 'tm_2' FOR UPDATE;
UPDATE teams SET name = 'Blue' WHERE id = 'tm_2';
COMMIT;
```

- homework
```sql
-- 29a  lost update if both read 2 and both write 2+1
-- 29b  the single UPDATE above
-- 29c  default isolation is read committed
-- 29d  lock tm_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 30. one UPDATE for a counter related to up_6
- two reads of 200 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'up_6';

BEGIN;
SELECT id FROM uploads WHERE id = 'up_6' FOR UPDATE;
UPDATE uploads SET key = 'videos/u_1/a.mp4' WHERE id = 'up_6';
COMMIT;
```

- homework
```sql
-- 30a  lost update if both read 200 and both write 200+1
-- 30b  the single UPDATE above
-- 30c  default isolation is read committed
-- 30d  lock up_6 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 31. one UPDATE for a counter related to st_1
- two reads of 1500 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'st_1';

BEGIN;
SELECT id FROM standings WHERE id = 'st_1' FOR UPDATE;
UPDATE standings SET player = 'player_a' WHERE id = 'st_1';
COMMIT;
```

- homework
```sql
-- 31a  lost update if both read 1500 and both write 1500+1
-- 31b  the single UPDATE above
-- 31c  default isolation is read committed
-- 31d  lock st_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 32. one UPDATE for a counter related to n_2
- two reads of 24 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'n_2';

BEGIN;
SELECT id FROM notices WHERE id = 'n_2' FOR UPDATE;
UPDATE notices SET port = 'Chattogram' WHERE id = 'n_2';
COMMIT;
```

- homework
```sql
-- 32a  lost update if both read 24 and both write 24+1
-- 32b  the single UPDATE above
-- 32c  default isolation is read committed
-- 32d  lock n_2 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 33. one UPDATE for a counter related to b_3
- two reads of 4 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'b_3';

BEGIN;
SELECT id FROM brackets WHERE id = 'b_3' FOR UPDATE;
UPDATE brackets SET round = 'semi' WHERE id = 'b_3';
COMMIT;
```

- homework
```sql
-- 33a  lost update if both read 4 and both write 4+1
-- 33b  the single UPDATE above
-- 33c  default isolation is read committed
-- 33d  lock b_3 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 34. one UPDATE for a counter related to se_1
- two reads of 15 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'se_1';

BEGIN;
SELECT id FROM sessions WHERE id = 'se_1' FOR UPDATE;
UPDATE sessions SET userId = 'u_3' WHERE id = 'se_1';
COMMIT;
```

- homework
```sql
-- 34a  lost update if both read 15 and both write 15+1
-- 34b  the single UPDATE above
-- 34c  default isolation is read committed
-- 34d  lock se_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 35. one UPDATE for a counter related to q_1
- two reads of 10 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'q_1';

BEGIN;
SELECT id FROM queues WHERE id = 'q_1' FOR UPDATE;
UPDATE queues SET name = 'laytime' WHERE id = 'q_1';
COMMIT;
```

- homework
```sql
-- 35a  lost update if both read 10 and both write 10+1
-- 35b  the single UPDATE above
-- 35c  default isolation is read committed
-- 35d  lock q_1 before the matching row, always in id order, to avoid a deadlock cycle
```

- example 36. one UPDATE for a counter related to r_1
- two reads of 2 then two writes can lose an increment
- the fix is SET n = n + 1 in one statement
- read committed is the Postgres default
- FOR UPDATE when we must read, decide, then write
- MVCC lets a reader proceed without waiting for the writer

```sql
UPDATE counters
SET n = n + 1
WHERE id = 'r_1';

BEGIN;
SELECT id FROM roles WHERE id = 'r_1' FOR UPDATE;
UPDATE roles SET name = 'operator' WHERE id = 'r_1';
COMMIT;
```

- homework
```sql
-- 36a  lost update if both read 2 and both write 2+1
-- 36b  the single UPDATE above
-- 36c  default isolation is read committed
-- 36d  lock r_1 before the matching row, always in id order, to avoid a deadlock cycle
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

- example 1. EXPLAIN for pc_12
- Seq Scan reads the table. fine when port_calls is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(vesselName), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, vesselName
FROM port_calls
WHERE id = 'pc_12';
```

- homework
```sql
-- 1a  read the plan from the inside out
-- 1b  estimate 10 rows, actual 100000, run ANALYZE
-- 1c  WHERE lower(vesselName) = 'ocean star' may not use an index on vesselName
-- 1d  an index the plan never uses is a write cost
```

- example 2. EXPLAIN for m_1
- Seq Scan reads the table. fine when matches is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(home), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, home
FROM matches
WHERE id = 'm_1';
```

- homework
```sql
-- 2a  read the plan from the inside out
-- 2b  estimate 10 rows, actual 100000, run ANALYZE
-- 2c  WHERE lower(home) = 'ada' may not use an index on home
-- 2d  an index the plan never uses is a write cost
```

- example 3. EXPLAIN for t_9
- Seq Scan reads the table. fine when tournaments is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(name), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, name
FROM tournaments
WHERE id = 't_9';
```

- homework
```sql
-- 3a  read the plan from the inside out
-- 3b  estimate 10 rows, actual 100000, run ANALYZE
-- 3c  WHERE lower(name) = 'rajshahi open' may not use an index on name
-- 3d  an index the plan never uses is a write cost
```

- example 4. EXPLAIN for v_4
- Seq Scan reads the table. fine when videos is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(title), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, title
FROM videos
WHERE id = 'v_4';
```

- homework
```sql
-- 4a  read the plan from the inside out
-- 4b  estimate 10 rows, actual 100000, run ANALYZE
-- 4c  WHERE lower(title) = 'episode 1' may not use an index on title
-- 4d  an index the plan never uses is a write cost
```

- example 5. EXPLAIN for f_2
- Seq Scan reads the table. fine when facts is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(kind), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, kind
FROM facts
WHERE id = 'f_2';
```

- homework
```sql
-- 5a  read the plan from the inside out
-- 5b  estimate 10 rows, actual 100000, run ANALYZE
-- 5c  WHERE lower(kind) = 'nor' may not use an index on kind
-- 5d  an index the plan never uses is a write cost
```

- example 6. EXPLAIN for u_3
- Seq Scan reads the table. fine when users is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(email), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, email
FROM users
WHERE id = 'u_3';
```

- homework
```sql
-- 6a  read the plan from the inside out
-- 6b  estimate 10 rows, actual 100000, run ANALYZE
-- 6c  WHERE lower(email) = 'a@example.com' may not use an index on email
-- 6d  an index the plan never uses is a write cost
```

- example 7. EXPLAIN for pay_8
- Seq Scan reads the table. fine when payments is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(eventId), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, eventId
FROM payments
WHERE id = 'pay_8';
```

- homework
```sql
-- 7a  read the plan from the inside out
-- 7b  estimate 10 rows, actual 100000, run ANALYZE
-- 7c  WHERE lower(eventId) = 'evt_1' may not use an index on eventId
-- 7d  an index the plan never uses is a write cost
```

- example 8. EXPLAIN for room_2
- Seq Scan reads the table. fine when rooms is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(sessionId), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, sessionId
FROM rooms
WHERE id = 'room_2';
```

- homework
```sql
-- 8a  read the plan from the inside out
-- 8b  estimate 10 rows, actual 100000, run ANALYZE
-- 8c  WHERE lower(sessionId) = 's_9' may not use an index on sessionId
-- 8d  an index the plan never uses is a write cost
```

- example 9. EXPLAIN for vs_7
- Seq Scan reads the table. fine when vessels is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(name), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, name
FROM vessels
WHERE id = 'vs_7';
```

- homework
```sql
-- 9a  read the plan from the inside out
-- 9b  estimate 10 rows, actual 100000, run ANALYZE
-- 9c  WHERE lower(name) = 'north wind' may not use an index on name
-- 9d  an index the plan never uses is a write cost
```

- example 10. EXPLAIN for sc_3
- Seq Scan reads the table. fine when scores is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(points), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, points
FROM scores
WHERE id = 'sc_3';
```

- homework
```sql
-- 10a  read the plan from the inside out
-- 10b  estimate 10 rows, actual 100000, run ANALYZE
-- 10c  WHERE lower(points) = '11' may not use an index on points
-- 10d  an index the plan never uses is a write cost
```

- example 11. EXPLAIN for tm_2
- Seq Scan reads the table. fine when teams is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(name), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, name
FROM teams
WHERE id = 'tm_2';
```

- homework
```sql
-- 11a  read the plan from the inside out
-- 11b  estimate 10 rows, actual 100000, run ANALYZE
-- 11c  WHERE lower(name) = 'blue' may not use an index on name
-- 11d  an index the plan never uses is a write cost
```

- example 12. EXPLAIN for up_6
- Seq Scan reads the table. fine when uploads is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(key), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, key
FROM uploads
WHERE id = 'up_6';
```

- homework
```sql
-- 12a  read the plan from the inside out
-- 12b  estimate 10 rows, actual 100000, run ANALYZE
-- 12c  WHERE lower(key) = 'videos/u_1/a.mp4' may not use an index on key
-- 12d  an index the plan never uses is a write cost
```

- example 13. EXPLAIN for st_1
- Seq Scan reads the table. fine when standings is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(player), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, player
FROM standings
WHERE id = 'st_1';
```

- homework
```sql
-- 13a  read the plan from the inside out
-- 13b  estimate 10 rows, actual 100000, run ANALYZE
-- 13c  WHERE lower(player) = 'player_a' may not use an index on player
-- 13d  an index the plan never uses is a write cost
```

- example 14. EXPLAIN for n_2
- Seq Scan reads the table. fine when notices is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(port), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, port
FROM notices
WHERE id = 'n_2';
```

- homework
```sql
-- 14a  read the plan from the inside out
-- 14b  estimate 10 rows, actual 100000, run ANALYZE
-- 14c  WHERE lower(port) = 'chattogram' may not use an index on port
-- 14d  an index the plan never uses is a write cost
```

- example 15. EXPLAIN for b_3
- Seq Scan reads the table. fine when brackets is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(round), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, round
FROM brackets
WHERE id = 'b_3';
```

- homework
```sql
-- 15a  read the plan from the inside out
-- 15b  estimate 10 rows, actual 100000, run ANALYZE
-- 15c  WHERE lower(round) = 'semi' may not use an index on round
-- 15d  an index the plan never uses is a write cost
```

- example 16. EXPLAIN for se_1
- Seq Scan reads the table. fine when sessions is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(userId), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, userId
FROM sessions
WHERE id = 'se_1';
```

- homework
```sql
-- 16a  read the plan from the inside out
-- 16b  estimate 10 rows, actual 100000, run ANALYZE
-- 16c  WHERE lower(userId) = 'u_3' may not use an index on userId
-- 16d  an index the plan never uses is a write cost
```

- example 17. EXPLAIN for q_1
- Seq Scan reads the table. fine when queues is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(name), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, name
FROM queues
WHERE id = 'q_1';
```

- homework
```sql
-- 17a  read the plan from the inside out
-- 17b  estimate 10 rows, actual 100000, run ANALYZE
-- 17c  WHERE lower(name) = 'laytime' may not use an index on name
-- 17d  an index the plan never uses is a write cost
```

- example 18. EXPLAIN for r_1
- Seq Scan reads the table. fine when roles is small
- Index Scan uses the index then fetches the row
- estimates come from statistics. ANALYZE refreshes them
- a wrapped column, lower(name), may ignore a plain index

```sql
EXPLAIN ANALYZE
SELECT id, name
FROM roles
WHERE id = 'r_1';
```

- homework
```sql
-- 18a  read the plan from the inside out
-- 18b  estimate 10 rows, actual 100000, run ANALYZE
-- 18c  WHERE lower(name) = 'operator' may not use an index on name
-- 18d  an index the plan never uses is a write cost
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

- example 1. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on port_calls
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_port_calls AS
SELECT id, vesselName FROM port_calls WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_port_calls()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 1a  select from open_port_calls where id = 'pc_12'
-- 1b  the view is not a second copy of the bytes
-- 1c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 1d  laytime money still has a unit test in TypeScript
```

- example 2. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on matches
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_matches AS
SELECT id, home FROM matches WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_matches()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 2a  select from open_matches where id = 'm_1'
-- 2b  the view is not a second copy of the bytes
-- 2c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 2d  laytime money still has a unit test in TypeScript
```

- example 3. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on tournaments
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_tournaments AS
SELECT id, name FROM tournaments WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_tournaments()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 3a  select from open_tournaments where id = 't_9'
-- 3b  the view is not a second copy of the bytes
-- 3c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 3d  laytime money still has a unit test in TypeScript
```

- example 4. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on videos
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_videos AS
SELECT id, title FROM videos WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_videos()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 4a  select from open_videos where id = 'v_4'
-- 4b  the view is not a second copy of the bytes
-- 4c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 4d  laytime money still has a unit test in TypeScript
```

- example 5. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on facts
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_facts AS
SELECT id, kind FROM facts WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_facts()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 5a  select from open_facts where id = 'f_2'
-- 5b  the view is not a second copy of the bytes
-- 5c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 5d  laytime money still has a unit test in TypeScript
```

- example 6. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on users
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_users AS
SELECT id, email FROM users WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_users()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 6a  select from open_users where id = 'u_3'
-- 6b  the view is not a second copy of the bytes
-- 6c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 6d  laytime money still has a unit test in TypeScript
```

- example 7. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on payments
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_payments AS
SELECT id, eventId FROM payments WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_payments()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 7a  select from open_payments where id = 'pay_8'
-- 7b  the view is not a second copy of the bytes
-- 7c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 7d  laytime money still has a unit test in TypeScript
```

- example 8. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on rooms
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_rooms AS
SELECT id, sessionId FROM rooms WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_rooms()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 8a  select from open_rooms where id = 'room_2'
-- 8b  the view is not a second copy of the bytes
-- 8c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 8d  laytime money still has a unit test in TypeScript
```

- example 9. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on vessels
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_vessels AS
SELECT id, name FROM vessels WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_vessels()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 9a  select from open_vessels where id = 'vs_7'
-- 9b  the view is not a second copy of the bytes
-- 9c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 9d  laytime money still has a unit test in TypeScript
```

- example 10. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on scores
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_scores AS
SELECT id, points FROM scores WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_scores()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 10a  select from open_scores where id = 'sc_3'
-- 10b  the view is not a second copy of the bytes
-- 10c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 10d  laytime money still has a unit test in TypeScript
```

- example 11. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on teams
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_teams AS
SELECT id, name FROM teams WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_teams()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 11a  select from open_teams where id = 'tm_2'
-- 11b  the view is not a second copy of the bytes
-- 11c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 11d  laytime money still has a unit test in TypeScript
```

- example 12. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on uploads
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_uploads AS
SELECT id, key FROM uploads WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_uploads()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 12a  select from open_uploads where id = 'up_6'
-- 12b  the view is not a second copy of the bytes
-- 12c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 12d  laytime money still has a unit test in TypeScript
```

- example 13. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on standings
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_standings AS
SELECT id, player FROM standings WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_standings()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 13a  select from open_standings where id = 'st_1'
-- 13b  the view is not a second copy of the bytes
-- 13c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 13d  laytime money still has a unit test in TypeScript
```

- example 14. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on notices
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_notices AS
SELECT id, port FROM notices WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_notices()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 14a  select from open_notices where id = 'n_2'
-- 14b  the view is not a second copy of the bytes
-- 14c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 14d  laytime money still has a unit test in TypeScript
```

- example 15. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on brackets
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_brackets AS
SELECT id, round FROM brackets WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_brackets()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 15a  select from open_brackets where id = 'b_3'
-- 15b  the view is not a second copy of the bytes
-- 15c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 15d  laytime money still has a unit test in TypeScript
```

- example 16. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on sessions
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_sessions AS
SELECT id, userId FROM sessions WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_sessions()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 16a  select from open_sessions where id = 'se_1'
-- 16b  the view is not a second copy of the bytes
-- 16c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 16d  laytime money still has a unit test in TypeScript
```

- example 17. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on queues
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_queues AS
SELECT id, name FROM queues WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_queues()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 17a  select from open_queues where id = 'q_1'
-- 17b  the view is not a second copy of the bytes
-- 17c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 17d  laytime money still has a unit test in TypeScript
```

- example 18. a view of open rows and a trigger that stamps time
- the view stores no rows
- the trigger sets updated_at on roles
- money stays in the tested TypeScript function, not only in a hidden procedure
- a trigger that updates the same table can fire itself

```sql
CREATE VIEW open_roles AS
SELECT id, name FROM roles WHERE closed_at IS NULL;

CREATE OR REPLACE FUNCTION touch_roles()
RETURNS trigger AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- homework
```sql
-- 18a  select from open_roles where id = 'r_1'
-- 18b  the view is not a second copy of the bytes
-- 18c  updated_at is easy to forget in one route and hard to forget in a trigger
-- 18d  laytime money still has a unit test in TypeScript
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

- example 1. document and Redis types beside the SQL row pc_12
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("port_calls:pc_12", "vesselName", "Ocean Star");
await redis.sadd("online", "pc_12");
await redis.zadd("standings:pc_12", 72, "Ocean Star");
await redis.expire("port_calls:pc_12", 60);
```

- homework
```ts
// 1a  HSET field vesselName value Ocean Star
// 1b  a set for online ids, here pc_12
// 1c  a sorted set score 72
// 1d  Postgres still holds the real row
```

- example 2. document and Redis types beside the SQL row m_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("matches:m_1", "home", "Ada");
await redis.sadd("online", "m_1");
await redis.zadd("standings:m_1", 3, "Ada");
await redis.expire("matches:m_1", 60);
```

- homework
```ts
// 2a  HSET field home value Ada
// 2b  a set for online ids, here m_1
// 2c  a sorted set score 3
// 2d  Postgres still holds the real row
```

- example 3. document and Redis types beside the SQL row t_9
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("tournaments:t_9", "name", "Rajshahi Open");
await redis.sadd("online", "t_9");
await redis.zadd("standings:t_9", 16, "Rajshahi Open");
await redis.expire("tournaments:t_9", 60);
```

- homework
```ts
// 3a  HSET field name value Rajshahi Open
// 3b  a set for online ids, here t_9
// 3c  a sorted set score 16
// 3d  Postgres still holds the real row
```

- example 4. document and Redis types beside the SQL row v_4
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("videos:v_4", "title", "Episode 1");
await redis.sadd("online", "v_4");
await redis.zadd("standings:v_4", 6, "Episode 1");
await redis.expire("videos:v_4", 60);
```

- homework
```ts
// 4a  HSET field title value Episode 1
// 4b  a set for online ids, here v_4
// 4c  a sorted set score 6
// 4d  Postgres still holds the real row
```

- example 5. document and Redis types beside the SQL row f_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("facts:f_2", "kind", "NOR");
await redis.sadd("online", "f_2");
await redis.zadd("standings:f_2", 1, "NOR");
await redis.expire("facts:f_2", 60);
```

- homework
```ts
// 5a  HSET field kind value NOR
// 5b  a set for online ids, here f_2
// 5c  a sorted set score 1
// 5d  Postgres still holds the real row
```

- example 6. document and Redis types beside the SQL row u_3
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("users:u_3", "email", "a@example.com");
await redis.sadd("online", "u_3");
await redis.zadd("standings:u_3", 1, "a@example.com");
await redis.expire("users:u_3", 60);
```

- homework
```ts
// 6a  HSET field email value a@example.com
// 6b  a set for online ids, here u_3
// 6c  a sorted set score 1
// 6d  Postgres still holds the real row
```

- example 7. document and Redis types beside the SQL row pay_8
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("payments:pay_8", "eventId", "evt_1");
await redis.sadd("online", "pay_8");
await redis.zadd("standings:pay_8", 15000, "evt_1");
await redis.expire("payments:pay_8", 60);
```

- homework
```ts
// 7a  HSET field eventId value evt_1
// 7b  a set for online ids, here pay_8
// 7c  a sorted set score 15000
// 7d  Postgres still holds the real row
```

- example 8. document and Redis types beside the SQL row room_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("rooms:room_2", "sessionId", "s_9");
await redis.sadd("online", "room_2");
await redis.zadd("standings:room_2", 12, "s_9");
await redis.expire("rooms:room_2", 60);
```

- homework
```ts
// 8a  HSET field sessionId value s_9
// 8b  a set for online ids, here room_2
// 8c  a sorted set score 12
// 8d  Postgres still holds the real row
```

- example 9. document and Redis types beside the SQL row vs_7
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("vessels:vs_7", "name", "North Wind");
await redis.sadd("online", "vs_7");
await redis.zadd("standings:vs_7", 48, "North Wind");
await redis.expire("vessels:vs_7", 60);
```

- homework
```ts
// 9a  HSET field name value North Wind
// 9b  a set for online ids, here vs_7
// 9c  a sorted set score 48
// 9d  Postgres still holds the real row
```

- example 10. document and Redis types beside the SQL row sc_3
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("scores:sc_3", "points", "11");
await redis.sadd("online", "sc_3");
await redis.zadd("standings:sc_3", 11, "11");
await redis.expire("scores:sc_3", 60);
```

- homework
```ts
// 10a  HSET field points value 11
// 10b  a set for online ids, here sc_3
// 10c  a sorted set score 11
// 10d  Postgres still holds the real row
```

- example 11. document and Redis types beside the SQL row tm_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("teams:tm_2", "name", "Blue");
await redis.sadd("online", "tm_2");
await redis.zadd("standings:tm_2", 2, "Blue");
await redis.expire("teams:tm_2", 60);
```

- homework
```ts
// 11a  HSET field name value Blue
// 11b  a set for online ids, here tm_2
// 11c  a sorted set score 2
// 11d  Postgres still holds the real row
```

- example 12. document and Redis types beside the SQL row up_6
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("uploads:up_6", "key", "videos/u_1/a.mp4");
await redis.sadd("online", "up_6");
await redis.zadd("standings:up_6", 200, "videos/u_1/a.mp4");
await redis.expire("uploads:up_6", 60);
```

- homework
```ts
// 12a  HSET field key value videos/u_1/a.mp4
// 12b  a set for online ids, here up_6
// 12c  a sorted set score 200
// 12d  Postgres still holds the real row
```

- example 13. document and Redis types beside the SQL row st_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("standings:st_1", "player", "player_a");
await redis.sadd("online", "st_1");
await redis.zadd("standings:st_1", 1500, "player_a");
await redis.expire("standings:st_1", 60);
```

- homework
```ts
// 13a  HSET field player value player_a
// 13b  a set for online ids, here st_1
// 13c  a sorted set score 1500
// 13d  Postgres still holds the real row
```

- example 14. document and Redis types beside the SQL row n_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("notices:n_2", "port", "Chattogram");
await redis.sadd("online", "n_2");
await redis.zadd("standings:n_2", 24, "Chattogram");
await redis.expire("notices:n_2", 60);
```

- homework
```ts
// 14a  HSET field port value Chattogram
// 14b  a set for online ids, here n_2
// 14c  a sorted set score 24
// 14d  Postgres still holds the real row
```

- example 15. document and Redis types beside the SQL row b_3
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("brackets:b_3", "round", "semi");
await redis.sadd("online", "b_3");
await redis.zadd("standings:b_3", 4, "semi");
await redis.expire("brackets:b_3", 60);
```

- homework
```ts
// 15a  HSET field round value semi
// 15b  a set for online ids, here b_3
// 15c  a sorted set score 4
// 15d  Postgres still holds the real row
```

- example 16. document and Redis types beside the SQL row se_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("sessions:se_1", "userId", "u_3");
await redis.sadd("online", "se_1");
await redis.zadd("standings:se_1", 15, "u_3");
await redis.expire("sessions:se_1", 60);
```

- homework
```ts
// 16a  HSET field userId value u_3
// 16b  a set for online ids, here se_1
// 16c  a sorted set score 15
// 16d  Postgres still holds the real row
```

- example 17. document and Redis types beside the SQL row q_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("queues:q_1", "name", "laytime");
await redis.sadd("online", "q_1");
await redis.zadd("standings:q_1", 10, "laytime");
await redis.expire("queues:q_1", 60);
```

- homework
```ts
// 17a  HSET field name value laytime
// 17b  a set for online ids, here q_1
// 17c  a sorted set score 10
// 17d  Postgres still holds the real row
```

- example 18. document and Redis types beside the SQL row r_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("roles:r_1", "name", "operator");
await redis.sadd("online", "r_1");
await redis.zadd("standings:r_1", 2, "operator");
await redis.expire("roles:r_1", 60);
```

- homework
```ts
// 18a  HSET field name value operator
// 18b  a set for online ids, here r_1
// 18c  a sorted set score 2
// 18d  Postgres still holds the real row
```

- example 19. document and Redis types beside the SQL row pc_12
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("port_calls:pc_12", "vesselName", "Ocean Star");
await redis.sadd("online", "pc_12");
await redis.zadd("standings:pc_12", 72, "Ocean Star");
await redis.expire("port_calls:pc_12", 60);
```

- homework
```ts
// 19a  HSET field vesselName value Ocean Star
// 19b  a set for online ids, here pc_12
// 19c  a sorted set score 72
// 19d  Postgres still holds the real row
```

- example 20. document and Redis types beside the SQL row m_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("matches:m_1", "home", "Ada");
await redis.sadd("online", "m_1");
await redis.zadd("standings:m_1", 3, "Ada");
await redis.expire("matches:m_1", 60);
```

- homework
```ts
// 20a  HSET field home value Ada
// 20b  a set for online ids, here m_1
// 20c  a sorted set score 3
// 20d  Postgres still holds the real row
```

- example 21. document and Redis types beside the SQL row t_9
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("tournaments:t_9", "name", "Rajshahi Open");
await redis.sadd("online", "t_9");
await redis.zadd("standings:t_9", 16, "Rajshahi Open");
await redis.expire("tournaments:t_9", 60);
```

- homework
```ts
// 21a  HSET field name value Rajshahi Open
// 21b  a set for online ids, here t_9
// 21c  a sorted set score 16
// 21d  Postgres still holds the real row
```

- example 22. document and Redis types beside the SQL row v_4
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("videos:v_4", "title", "Episode 1");
await redis.sadd("online", "v_4");
await redis.zadd("standings:v_4", 6, "Episode 1");
await redis.expire("videos:v_4", 60);
```

- homework
```ts
// 22a  HSET field title value Episode 1
// 22b  a set for online ids, here v_4
// 22c  a sorted set score 6
// 22d  Postgres still holds the real row
```

- example 23. document and Redis types beside the SQL row f_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("facts:f_2", "kind", "NOR");
await redis.sadd("online", "f_2");
await redis.zadd("standings:f_2", 1, "NOR");
await redis.expire("facts:f_2", 60);
```

- homework
```ts
// 23a  HSET field kind value NOR
// 23b  a set for online ids, here f_2
// 23c  a sorted set score 1
// 23d  Postgres still holds the real row
```

- example 24. document and Redis types beside the SQL row u_3
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("users:u_3", "email", "a@example.com");
await redis.sadd("online", "u_3");
await redis.zadd("standings:u_3", 1, "a@example.com");
await redis.expire("users:u_3", 60);
```

- homework
```ts
// 24a  HSET field email value a@example.com
// 24b  a set for online ids, here u_3
// 24c  a sorted set score 1
// 24d  Postgres still holds the real row
```

- example 25. document and Redis types beside the SQL row pay_8
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("payments:pay_8", "eventId", "evt_1");
await redis.sadd("online", "pay_8");
await redis.zadd("standings:pay_8", 15000, "evt_1");
await redis.expire("payments:pay_8", 60);
```

- homework
```ts
// 25a  HSET field eventId value evt_1
// 25b  a set for online ids, here pay_8
// 25c  a sorted set score 15000
// 25d  Postgres still holds the real row
```

- example 26. document and Redis types beside the SQL row room_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("rooms:room_2", "sessionId", "s_9");
await redis.sadd("online", "room_2");
await redis.zadd("standings:room_2", 12, "s_9");
await redis.expire("rooms:room_2", 60);
```

- homework
```ts
// 26a  HSET field sessionId value s_9
// 26b  a set for online ids, here room_2
// 26c  a sorted set score 12
// 26d  Postgres still holds the real row
```

- example 27. document and Redis types beside the SQL row vs_7
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("vessels:vs_7", "name", "North Wind");
await redis.sadd("online", "vs_7");
await redis.zadd("standings:vs_7", 48, "North Wind");
await redis.expire("vessels:vs_7", 60);
```

- homework
```ts
// 27a  HSET field name value North Wind
// 27b  a set for online ids, here vs_7
// 27c  a sorted set score 48
// 27d  Postgres still holds the real row
```

- example 28. document and Redis types beside the SQL row sc_3
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("scores:sc_3", "points", "11");
await redis.sadd("online", "sc_3");
await redis.zadd("standings:sc_3", 11, "11");
await redis.expire("scores:sc_3", 60);
```

- homework
```ts
// 28a  HSET field points value 11
// 28b  a set for online ids, here sc_3
// 28c  a sorted set score 11
// 28d  Postgres still holds the real row
```

- example 29. document and Redis types beside the SQL row tm_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("teams:tm_2", "name", "Blue");
await redis.sadd("online", "tm_2");
await redis.zadd("standings:tm_2", 2, "Blue");
await redis.expire("teams:tm_2", 60);
```

- homework
```ts
// 29a  HSET field name value Blue
// 29b  a set for online ids, here tm_2
// 29c  a sorted set score 2
// 29d  Postgres still holds the real row
```

- example 30. document and Redis types beside the SQL row up_6
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("uploads:up_6", "key", "videos/u_1/a.mp4");
await redis.sadd("online", "up_6");
await redis.zadd("standings:up_6", 200, "videos/u_1/a.mp4");
await redis.expire("uploads:up_6", 60);
```

- homework
```ts
// 30a  HSET field key value videos/u_1/a.mp4
// 30b  a set for online ids, here up_6
// 30c  a sorted set score 200
// 30d  Postgres still holds the real row
```

- example 31. document and Redis types beside the SQL row st_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("standings:st_1", "player", "player_a");
await redis.sadd("online", "st_1");
await redis.zadd("standings:st_1", 1500, "player_a");
await redis.expire("standings:st_1", 60);
```

- homework
```ts
// 31a  HSET field player value player_a
// 31b  a set for online ids, here st_1
// 31c  a sorted set score 1500
// 31d  Postgres still holds the real row
```

- example 32. document and Redis types beside the SQL row n_2
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("notices:n_2", "port", "Chattogram");
await redis.sadd("online", "n_2");
await redis.zadd("standings:n_2", 24, "Chattogram");
await redis.expire("notices:n_2", 60);
```

- homework
```ts
// 32a  HSET field port value Chattogram
// 32b  a set for online ids, here n_2
// 32c  a sorted set score 24
// 32d  Postgres still holds the real row
```

- example 33. document and Redis types beside the SQL row b_3
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("brackets:b_3", "round", "semi");
await redis.sadd("online", "b_3");
await redis.zadd("standings:b_3", 4, "semi");
await redis.expire("brackets:b_3", 60);
```

- homework
```ts
// 33a  HSET field round value semi
// 33b  a set for online ids, here b_3
// 33c  a sorted set score 4
// 33d  Postgres still holds the real row
```

- example 34. document and Redis types beside the SQL row se_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("sessions:se_1", "userId", "u_3");
await redis.sadd("online", "se_1");
await redis.zadd("standings:se_1", 15, "u_3");
await redis.expire("sessions:se_1", 60);
```

- homework
```ts
// 34a  HSET field userId value u_3
// 34b  a set for online ids, here se_1
// 34c  a sorted set score 15
// 34d  Postgres still holds the real row
```

- example 35. document and Redis types beside the SQL row q_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("queues:q_1", "name", "laytime");
await redis.sadd("online", "q_1");
await redis.zadd("standings:q_1", 10, "laytime");
await redis.expire("queues:q_1", 60);
```

- homework
```ts
// 35a  HSET field name value laytime
// 35b  a set for online ids, here q_1
// 35c  a sorted set score 10
// 35d  Postgres still holds the real row
```

- example 36. document and Redis types beside the SQL row r_1
- Postgres remains the database of record
- a document embeds a list we always load together
- Redis string, hash, list, set, sorted set
- ZADD is a leaderboard. the match result is still written in Postgres first

```ts
await redis.hset("roles:r_1", "name", "operator");
await redis.sadd("online", "r_1");
await redis.zadd("standings:r_1", 2, "operator");
await redis.expire("roles:r_1", 60);
```

- homework
```ts
// 36a  HSET field name value operator
// 36b  a set for online ids, here r_1
// 36c  a sorted set score 2
// 36d  Postgres still holds the real row
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

- example 1. primary and replica for pc_12
- the primary takes the write of Ocean Star
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "pc_12", vesselName: "Ocean Star" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 1a  write pc_12 on the primary
// 1b  the following read of pc_12 also uses the primary
// 1c  a report that can be a few seconds old may use the replica
// 1d  a mistaken DELETE of pc_12 is replicated. take a backup as well
```

- example 2. primary and replica for m_1
- the primary takes the write of Ada
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "m_1", home: "Ada" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 2a  write m_1 on the primary
// 2b  the following read of m_1 also uses the primary
// 2c  a report that can be a few seconds old may use the replica
// 2d  a mistaken DELETE of m_1 is replicated. take a backup as well
```

- example 3. primary and replica for t_9
- the primary takes the write of Rajshahi Open
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "t_9", name: "Rajshahi Open" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 3a  write t_9 on the primary
// 3b  the following read of t_9 also uses the primary
// 3c  a report that can be a few seconds old may use the replica
// 3d  a mistaken DELETE of t_9 is replicated. take a backup as well
```

- example 4. primary and replica for v_4
- the primary takes the write of Episode 1
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "v_4", title: "Episode 1" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 4a  write v_4 on the primary
// 4b  the following read of v_4 also uses the primary
// 4c  a report that can be a few seconds old may use the replica
// 4d  a mistaken DELETE of v_4 is replicated. take a backup as well
```

- example 5. primary and replica for f_2
- the primary takes the write of NOR
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "f_2", kind: "NOR" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 5a  write f_2 on the primary
// 5b  the following read of f_2 also uses the primary
// 5c  a report that can be a few seconds old may use the replica
// 5d  a mistaken DELETE of f_2 is replicated. take a backup as well
```

- example 6. primary and replica for u_3
- the primary takes the write of a@example.com
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "u_3", email: "a@example.com" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 6a  write u_3 on the primary
// 6b  the following read of u_3 also uses the primary
// 6c  a report that can be a few seconds old may use the replica
// 6d  a mistaken DELETE of u_3 is replicated. take a backup as well
```

- example 7. primary and replica for pay_8
- the primary takes the write of evt_1
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "pay_8", eventId: "evt_1" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 7a  write pay_8 on the primary
// 7b  the following read of pay_8 also uses the primary
// 7c  a report that can be a few seconds old may use the replica
// 7d  a mistaken DELETE of pay_8 is replicated. take a backup as well
```

- example 8. primary and replica for room_2
- the primary takes the write of s_9
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "room_2", sessionId: "s_9" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 8a  write room_2 on the primary
// 8b  the following read of room_2 also uses the primary
// 8c  a report that can be a few seconds old may use the replica
// 8d  a mistaken DELETE of room_2 is replicated. take a backup as well
```

- example 9. primary and replica for vs_7
- the primary takes the write of North Wind
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "vs_7", name: "North Wind" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 9a  write vs_7 on the primary
// 9b  the following read of vs_7 also uses the primary
// 9c  a report that can be a few seconds old may use the replica
// 9d  a mistaken DELETE of vs_7 is replicated. take a backup as well
```

- example 10. primary and replica for sc_3
- the primary takes the write of 11
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "sc_3", points: "11" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 10a  write sc_3 on the primary
// 10b  the following read of sc_3 also uses the primary
// 10c  a report that can be a few seconds old may use the replica
// 10d  a mistaken DELETE of sc_3 is replicated. take a backup as well
```

- example 11. primary and replica for tm_2
- the primary takes the write of Blue
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "tm_2", name: "Blue" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 11a  write tm_2 on the primary
// 11b  the following read of tm_2 also uses the primary
// 11c  a report that can be a few seconds old may use the replica
// 11d  a mistaken DELETE of tm_2 is replicated. take a backup as well
```

- example 12. primary and replica for up_6
- the primary takes the write of videos/u_1/a.mp4
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "up_6", key: "videos/u_1/a.mp4" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 12a  write up_6 on the primary
// 12b  the following read of up_6 also uses the primary
// 12c  a report that can be a few seconds old may use the replica
// 12d  a mistaken DELETE of up_6 is replicated. take a backup as well
```

- example 13. primary and replica for st_1
- the primary takes the write of player_a
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "st_1", player: "player_a" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 13a  write st_1 on the primary
// 13b  the following read of st_1 also uses the primary
// 13c  a report that can be a few seconds old may use the replica
// 13d  a mistaken DELETE of st_1 is replicated. take a backup as well
```

- example 14. primary and replica for n_2
- the primary takes the write of Chattogram
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "n_2", port: "Chattogram" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 14a  write n_2 on the primary
// 14b  the following read of n_2 also uses the primary
// 14c  a report that can be a few seconds old may use the replica
// 14d  a mistaken DELETE of n_2 is replicated. take a backup as well
```

- example 15. primary and replica for b_3
- the primary takes the write of semi
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "b_3", round: "semi" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 15a  write b_3 on the primary
// 15b  the following read of b_3 also uses the primary
// 15c  a report that can be a few seconds old may use the replica
// 15d  a mistaken DELETE of b_3 is replicated. take a backup as well
```

- example 16. primary and replica for se_1
- the primary takes the write of u_3
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "se_1", userId: "u_3" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 16a  write se_1 on the primary
// 16b  the following read of se_1 also uses the primary
// 16c  a report that can be a few seconds old may use the replica
// 16d  a mistaken DELETE of se_1 is replicated. take a backup as well
```

- example 17. primary and replica for q_1
- the primary takes the write of laytime
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "q_1", name: "laytime" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 17a  write q_1 on the primary
// 17b  the following read of q_1 also uses the primary
// 17c  a report that can be a few seconds old may use the replica
// 17d  a mistaken DELETE of q_1 is replicated. take a backup as well
```

- example 18. primary and replica for r_1
- the primary takes the write of operator
- an async replica can be behind. a read right after the write uses the primary
- a replica copies a bad DELETE too. it is not a backup
- sync commit waits for the standby. async returns sooner

```ts
const created = await primary.item.create({
  data: { id: "r_1", name: "operator" },
});
const again = await primary.item.findUnique({ where: { id: created.id } });
```

- homework
```ts
// 18a  write r_1 on the primary
// 18b  the following read of r_1 also uses the primary
// 18c  a report that can be a few seconds old may use the replica
// 18d  a mistaken DELETE of r_1 is replicated. take a backup as well
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

- example 1. partition, pool, backup, around port_calls
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for port_calls facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 1a  shard key would be a tournament id, not a random vesselName
-- 1b  pc_12 lives on one shard if we ever shard, and only after one node is too big
-- 1c  a backup we have never restored is untested
-- 1d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 2. partition, pool, backup, around matches
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for matches facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 2a  shard key would be a tournament id, not a random home
-- 2b  m_1 lives on one shard if we ever shard, and only after one node is too big
-- 2c  a backup we have never restored is untested
-- 2d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 3. partition, pool, backup, around tournaments
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for tournaments facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 3a  shard key would be a tournament id, not a random name
-- 3b  t_9 lives on one shard if we ever shard, and only after one node is too big
-- 3c  a backup we have never restored is untested
-- 3d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 4. partition, pool, backup, around videos
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for videos facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 4a  shard key would be a tournament id, not a random title
-- 4b  v_4 lives on one shard if we ever shard, and only after one node is too big
-- 4c  a backup we have never restored is untested
-- 4d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 5. partition, pool, backup, around facts
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for facts facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 5a  shard key would be a tournament id, not a random kind
-- 5b  f_2 lives on one shard if we ever shard, and only after one node is too big
-- 5c  a backup we have never restored is untested
-- 5d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 6. partition, pool, backup, around users
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for users facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 6a  shard key would be a tournament id, not a random email
-- 6b  u_3 lives on one shard if we ever shard, and only after one node is too big
-- 6c  a backup we have never restored is untested
-- 6d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 7. partition, pool, backup, around payments
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for payments facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 7a  shard key would be a tournament id, not a random eventId
-- 7b  pay_8 lives on one shard if we ever shard, and only after one node is too big
-- 7c  a backup we have never restored is untested
-- 7d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 8. partition, pool, backup, around rooms
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for rooms facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 8a  shard key would be a tournament id, not a random sessionId
-- 8b  room_2 lives on one shard if we ever shard, and only after one node is too big
-- 8c  a backup we have never restored is untested
-- 8d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 9. partition, pool, backup, around vessels
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for vessels facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 9a  shard key would be a tournament id, not a random name
-- 9b  vs_7 lives on one shard if we ever shard, and only after one node is too big
-- 9c  a backup we have never restored is untested
-- 9d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 10. partition, pool, backup, around scores
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for scores facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 10a  shard key would be a tournament id, not a random points
-- 10b  sc_3 lives on one shard if we ever shard, and only after one node is too big
-- 10c  a backup we have never restored is untested
-- 10d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 11. partition, pool, backup, around teams
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for teams facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 11a  shard key would be a tournament id, not a random name
-- 11b  tm_2 lives on one shard if we ever shard, and only after one node is too big
-- 11c  a backup we have never restored is untested
-- 11d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 12. partition, pool, backup, around uploads
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for uploads facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 12a  shard key would be a tournament id, not a random key
-- 12b  up_6 lives on one shard if we ever shard, and only after one node is too big
-- 12c  a backup we have never restored is untested
-- 12d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 13. partition, pool, backup, around standings
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for standings facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 13a  shard key would be a tournament id, not a random player
-- 13b  st_1 lives on one shard if we ever shard, and only after one node is too big
-- 13c  a backup we have never restored is untested
-- 13d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 14. partition, pool, backup, around notices
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for notices facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 14a  shard key would be a tournament id, not a random port
-- 14b  n_2 lives on one shard if we ever shard, and only after one node is too big
-- 14c  a backup we have never restored is untested
-- 14d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 15. partition, pool, backup, around brackets
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for brackets facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 15a  shard key would be a tournament id, not a random round
-- 15b  b_3 lives on one shard if we ever shard, and only after one node is too big
-- 15c  a backup we have never restored is untested
-- 15d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 16. partition, pool, backup, around sessions
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for sessions facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 16a  shard key would be a tournament id, not a random userId
-- 16b  se_1 lives on one shard if we ever shard, and only after one node is too big
-- 16c  a backup we have never restored is untested
-- 16d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 17. partition, pool, backup, around queues
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for queues facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 17a  shard key would be a tournament id, not a random name
-- 17b  q_1 lives on one shard if we ever shard, and only after one node is too big
-- 17c  a backup we have never restored is untested
-- 17d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 18. partition, pool, backup, around roles
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for roles facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 18a  shard key would be a tournament id, not a random name
-- 18b  r_1 lives on one shard if we ever shard, and only after one node is too big
-- 18c  a backup we have never restored is untested
-- 18d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 19. partition, pool, backup, around port_calls
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for port_calls facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 19a  shard key would be a tournament id, not a random vesselName
-- 19b  pc_12 lives on one shard if we ever shard, and only after one node is too big
-- 19c  a backup we have never restored is untested
-- 19d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 20. partition, pool, backup, around matches
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for matches facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 20a  shard key would be a tournament id, not a random home
-- 20b  m_1 lives on one shard if we ever shard, and only after one node is too big
-- 20c  a backup we have never restored is untested
-- 20d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 21. partition, pool, backup, around tournaments
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for tournaments facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 21a  shard key would be a tournament id, not a random name
-- 21b  t_9 lives on one shard if we ever shard, and only after one node is too big
-- 21c  a backup we have never restored is untested
-- 21d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 22. partition, pool, backup, around videos
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for videos facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 22a  shard key would be a tournament id, not a random title
-- 22b  v_4 lives on one shard if we ever shard, and only after one node is too big
-- 22c  a backup we have never restored is untested
-- 22d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 23. partition, pool, backup, around facts
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for facts facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 23a  shard key would be a tournament id, not a random kind
-- 23b  f_2 lives on one shard if we ever shard, and only after one node is too big
-- 23c  a backup we have never restored is untested
-- 23d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 24. partition, pool, backup, around users
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for users facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 24a  shard key would be a tournament id, not a random email
-- 24b  u_3 lives on one shard if we ever shard, and only after one node is too big
-- 24c  a backup we have never restored is untested
-- 24d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 25. partition, pool, backup, around payments
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for payments facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 25a  shard key would be a tournament id, not a random eventId
-- 25b  pay_8 lives on one shard if we ever shard, and only after one node is too big
-- 25c  a backup we have never restored is untested
-- 25d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 26. partition, pool, backup, around rooms
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for rooms facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 26a  shard key would be a tournament id, not a random sessionId
-- 26b  room_2 lives on one shard if we ever shard, and only after one node is too big
-- 26c  a backup we have never restored is untested
-- 26d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 27. partition, pool, backup, around vessels
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for vessels facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 27a  shard key would be a tournament id, not a random name
-- 27b  vs_7 lives on one shard if we ever shard, and only after one node is too big
-- 27c  a backup we have never restored is untested
-- 27d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 28. partition, pool, backup, around scores
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for scores facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 28a  shard key would be a tournament id, not a random points
-- 28b  sc_3 lives on one shard if we ever shard, and only after one node is too big
-- 28c  a backup we have never restored is untested
-- 28d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 29. partition, pool, backup, around teams
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for teams facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 29a  shard key would be a tournament id, not a random name
-- 29b  tm_2 lives on one shard if we ever shard, and only after one node is too big
-- 29c  a backup we have never restored is untested
-- 29d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 30. partition, pool, backup, around uploads
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for uploads facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 30a  shard key would be a tournament id, not a random key
-- 30b  up_6 lives on one shard if we ever shard, and only after one node is too big
-- 30c  a backup we have never restored is untested
-- 30d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 31. partition, pool, backup, around standings
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for standings facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 31a  shard key would be a tournament id, not a random player
-- 31b  st_1 lives on one shard if we ever shard, and only after one node is too big
-- 31c  a backup we have never restored is untested
-- 31d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 32. partition, pool, backup, around notices
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for notices facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 32a  shard key would be a tournament id, not a random port
-- 32b  n_2 lives on one shard if we ever shard, and only after one node is too big
-- 32c  a backup we have never restored is untested
-- 32d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 33. partition, pool, backup, around brackets
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for brackets facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 33a  shard key would be a tournament id, not a random round
-- 33b  b_3 lives on one shard if we ever shard, and only after one node is too big
-- 33c  a backup we have never restored is untested
-- 33d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 34. partition, pool, backup, around sessions
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for sessions facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 34a  shard key would be a tournament id, not a random userId
-- 34b  se_1 lives on one shard if we ever shard, and only after one node is too big
-- 34c  a backup we have never restored is untested
-- 34d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 35. partition, pool, backup, around queues
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for queues facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 35a  shard key would be a tournament id, not a random name
-- 35b  q_1 lives on one shard if we ever shard, and only after one node is too big
-- 35c  a backup we have never restored is untested
-- 35d  PgBouncer or the Prisma pool sits in front of Postgres
```

- example 36. partition, pool, backup, around roles
- these projects are not sharded. one Postgres until it is actually too big
- a partition by month skips other months
- the pool reuses connections. one connection per forgotten request exhausts it
- a backup is a copy we can restore. test the restore
- point in time needs the base backup and the WAL after it

```sql
-- partition key for roles facts: the month of at
-- pool: a finite set of connections shared by the API
-- backup: base + WAL, stored off the same disk
```

- homework
```sql
-- 36a  shard key would be a tournament id, not a random name
-- 36b  r_1 lives on one shard if we ever shard, and only after one node is too big
-- 36c  a backup we have never restored is untested
-- 36d  PgBouncer or the Prisma pool sits in front of Postgres
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

- example 1. schema row pc_12 / Ocean Star
- primary key, not null, check on a positive number
- foreign key from the child to pc_12
- index for the screen that lists by the filter column

```sql
CREATE TABLE port_calls (
  id TEXT PRIMARY KEY,
  vesselName TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO port_calls (id, vesselName, n) VALUES ('pc_12', 'Ocean Star', 72);
```

- homework
```sql
-- 1a  insert pc_12
-- 1b  the CHECK rejects n = 0
-- 1c  a child row with a missing parent fails the foreign key
-- 1d  EXPLAIN the select by id
```

- example 2. schema row m_1 / Ada
- primary key, not null, check on a positive number
- foreign key from the child to m_1
- index for the screen that lists by the filter column

```sql
CREATE TABLE matches (
  id TEXT PRIMARY KEY,
  home TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO matches (id, home, n) VALUES ('m_1', 'Ada', 3);
```

- homework
```sql
-- 2a  insert m_1
-- 2b  the CHECK rejects n = 0
-- 2c  a child row with a missing parent fails the foreign key
-- 2d  EXPLAIN the select by id
```

- example 3. schema row t_9 / Rajshahi Open
- primary key, not null, check on a positive number
- foreign key from the child to t_9
- index for the screen that lists by the filter column

```sql
CREATE TABLE tournaments (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO tournaments (id, name, n) VALUES ('t_9', 'Rajshahi Open', 16);
```

- homework
```sql
-- 3a  insert t_9
-- 3b  the CHECK rejects n = 0
-- 3c  a child row with a missing parent fails the foreign key
-- 3d  EXPLAIN the select by id
```

- example 4. schema row v_4 / Episode 1
- primary key, not null, check on a positive number
- foreign key from the child to v_4
- index for the screen that lists by the filter column

```sql
CREATE TABLE videos (
  id TEXT PRIMARY KEY,
  title TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO videos (id, title, n) VALUES ('v_4', 'Episode 1', 6);
```

- homework
```sql
-- 4a  insert v_4
-- 4b  the CHECK rejects n = 0
-- 4c  a child row with a missing parent fails the foreign key
-- 4d  EXPLAIN the select by id
```

- example 5. schema row f_2 / NOR
- primary key, not null, check on a positive number
- foreign key from the child to f_2
- index for the screen that lists by the filter column

```sql
CREATE TABLE facts (
  id TEXT PRIMARY KEY,
  kind TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO facts (id, kind, n) VALUES ('f_2', 'NOR', 1);
```

- homework
```sql
-- 5a  insert f_2
-- 5b  the CHECK rejects n = 0
-- 5c  a child row with a missing parent fails the foreign key
-- 5d  EXPLAIN the select by id
```

- example 6. schema row u_3 / a@example.com
- primary key, not null, check on a positive number
- foreign key from the child to u_3
- index for the screen that lists by the filter column

```sql
CREATE TABLE users (
  id TEXT PRIMARY KEY,
  email TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO users (id, email, n) VALUES ('u_3', 'a@example.com', 1);
```

- homework
```sql
-- 6a  insert u_3
-- 6b  the CHECK rejects n = 0
-- 6c  a child row with a missing parent fails the foreign key
-- 6d  EXPLAIN the select by id
```

- example 7. schema row pay_8 / evt_1
- primary key, not null, check on a positive number
- foreign key from the child to pay_8
- index for the screen that lists by the filter column

```sql
CREATE TABLE payments (
  id TEXT PRIMARY KEY,
  eventId TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO payments (id, eventId, n) VALUES ('pay_8', 'evt_1', 15000);
```

- homework
```sql
-- 7a  insert pay_8
-- 7b  the CHECK rejects n = 0
-- 7c  a child row with a missing parent fails the foreign key
-- 7d  EXPLAIN the select by id
```

- example 8. schema row room_2 / s_9
- primary key, not null, check on a positive number
- foreign key from the child to room_2
- index for the screen that lists by the filter column

```sql
CREATE TABLE rooms (
  id TEXT PRIMARY KEY,
  sessionId TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO rooms (id, sessionId, n) VALUES ('room_2', 's_9', 12);
```

- homework
```sql
-- 8a  insert room_2
-- 8b  the CHECK rejects n = 0
-- 8c  a child row with a missing parent fails the foreign key
-- 8d  EXPLAIN the select by id
```

- example 9. schema row vs_7 / North Wind
- primary key, not null, check on a positive number
- foreign key from the child to vs_7
- index for the screen that lists by the filter column

```sql
CREATE TABLE vessels (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO vessels (id, name, n) VALUES ('vs_7', 'North Wind', 48);
```

- homework
```sql
-- 9a  insert vs_7
-- 9b  the CHECK rejects n = 0
-- 9c  a child row with a missing parent fails the foreign key
-- 9d  EXPLAIN the select by id
```

- example 10. schema row sc_3 / 11
- primary key, not null, check on a positive number
- foreign key from the child to sc_3
- index for the screen that lists by the filter column

```sql
CREATE TABLE scores (
  id TEXT PRIMARY KEY,
  points TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO scores (id, points, n) VALUES ('sc_3', '11', 11);
```

- homework
```sql
-- 10a  insert sc_3
-- 10b  the CHECK rejects n = 0
-- 10c  a child row with a missing parent fails the foreign key
-- 10d  EXPLAIN the select by id
```

- example 11. schema row tm_2 / Blue
- primary key, not null, check on a positive number
- foreign key from the child to tm_2
- index for the screen that lists by the filter column

```sql
CREATE TABLE teams (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO teams (id, name, n) VALUES ('tm_2', 'Blue', 2);
```

- homework
```sql
-- 11a  insert tm_2
-- 11b  the CHECK rejects n = 0
-- 11c  a child row with a missing parent fails the foreign key
-- 11d  EXPLAIN the select by id
```

- example 12. schema row up_6 / videos/u_1/a.mp4
- primary key, not null, check on a positive number
- foreign key from the child to up_6
- index for the screen that lists by the filter column

```sql
CREATE TABLE uploads (
  id TEXT PRIMARY KEY,
  key TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO uploads (id, key, n) VALUES ('up_6', 'videos/u_1/a.mp4', 200);
```

- homework
```sql
-- 12a  insert up_6
-- 12b  the CHECK rejects n = 0
-- 12c  a child row with a missing parent fails the foreign key
-- 12d  EXPLAIN the select by id
```

- example 13. schema row st_1 / player_a
- primary key, not null, check on a positive number
- foreign key from the child to st_1
- index for the screen that lists by the filter column

```sql
CREATE TABLE standings (
  id TEXT PRIMARY KEY,
  player TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO standings (id, player, n) VALUES ('st_1', 'player_a', 1500);
```

- homework
```sql
-- 13a  insert st_1
-- 13b  the CHECK rejects n = 0
-- 13c  a child row with a missing parent fails the foreign key
-- 13d  EXPLAIN the select by id
```

- example 14. schema row n_2 / Chattogram
- primary key, not null, check on a positive number
- foreign key from the child to n_2
- index for the screen that lists by the filter column

```sql
CREATE TABLE notices (
  id TEXT PRIMARY KEY,
  port TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO notices (id, port, n) VALUES ('n_2', 'Chattogram', 24);
```

- homework
```sql
-- 14a  insert n_2
-- 14b  the CHECK rejects n = 0
-- 14c  a child row with a missing parent fails the foreign key
-- 14d  EXPLAIN the select by id
```

- example 15. schema row b_3 / semi
- primary key, not null, check on a positive number
- foreign key from the child to b_3
- index for the screen that lists by the filter column

```sql
CREATE TABLE brackets (
  id TEXT PRIMARY KEY,
  round TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO brackets (id, round, n) VALUES ('b_3', 'semi', 4);
```

- homework
```sql
-- 15a  insert b_3
-- 15b  the CHECK rejects n = 0
-- 15c  a child row with a missing parent fails the foreign key
-- 15d  EXPLAIN the select by id
```

- example 16. schema row se_1 / u_3
- primary key, not null, check on a positive number
- foreign key from the child to se_1
- index for the screen that lists by the filter column

```sql
CREATE TABLE sessions (
  id TEXT PRIMARY KEY,
  userId TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO sessions (id, userId, n) VALUES ('se_1', 'u_3', 15);
```

- homework
```sql
-- 16a  insert se_1
-- 16b  the CHECK rejects n = 0
-- 16c  a child row with a missing parent fails the foreign key
-- 16d  EXPLAIN the select by id
```

- example 17. schema row q_1 / laytime
- primary key, not null, check on a positive number
- foreign key from the child to q_1
- index for the screen that lists by the filter column

```sql
CREATE TABLE queues (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO queues (id, name, n) VALUES ('q_1', 'laytime', 10);
```

- homework
```sql
-- 17a  insert q_1
-- 17b  the CHECK rejects n = 0
-- 17c  a child row with a missing parent fails the foreign key
-- 17d  EXPLAIN the select by id
```

- example 18. schema row r_1 / operator
- primary key, not null, check on a positive number
- foreign key from the child to r_1
- index for the screen that lists by the filter column

```sql
CREATE TABLE roles (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  n INTEGER NOT NULL CHECK (n > 0)
);
INSERT INTO roles (id, name, n) VALUES ('r_1', 'operator', 2);
```

- homework
```sql
-- 18a  insert r_1
-- 18b  the CHECK rejects n = 0
-- 18c  a child row with a missing parent fails the foreign key
-- 18d  EXPLAIN the select by id
```

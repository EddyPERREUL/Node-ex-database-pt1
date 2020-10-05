1.
postgres=> CREATE DATABASE db_1;
CREATE DATABASE

postgres=# \c db_1
You are now connected to database "db_1" as user "postgres".

db_1=# INSERT INTO users (name, password, email) VALUES ('alice','123', 'alice@mail.com'), ('bob','456', 'bob@mail.co
m'), ('charlie', '789', 'charlie@mail.com');
INSERT 0 3

db_1=# SELECT * FROM users;
 id |  name   | password |      email
----+---------+----------+------------------
  1 | alice   | 123      | alice@mail.com
  2 | bob     | 456      | bob@mail.com
  3 | charlie | 789      | charlie@mail.com
(3 rows)
___________________________________________________________

2. 
db_1=# INSERT INTO users (name, password) VALUES ('dan', 101112), ('eve', 131415), ('faythe', 161718);
INSERT 0 3
db_1=# SELECT * FROM users;
 id |  name   | password |      email
----+---------+----------+------------------
  1 | alice   | 123      | alice@mail.com
  2 | bob     | 456      | bob@mail.com
  3 | charlie | 789      | charlie@mail.com
  4 | dan     | 101112   |
  5 | eve     | 131415   |
  6 | faythe  | 161718   |
(6 rows)

____________________________________________________________

3.
db_1=#  SELECT * FROM users WHERE length(password)>3;
 id |  name  | password | email
----+--------+----------+-------
  4 | dan    | 101112   |
  5 | eve    | 131415   |
  6 | faythe | 161718   |
(3 rows)

______________________________________________________________

4.
db_1=# ALTER TABLE users ADD COLUMN bio TEXT DEFAULT 'Hello, World!';
ALTER TABLE
db_1=# SELECT * FROM users;
 id |  name   | password |      email       |      bio
----+---------+----------+------------------+---------------
  1 | alice   | 123      | alice@mail.com   | Hello, World!
  2 | bob     | 456      | bob@mail.com     | Hello, World!
  3 | charlie | 789      | charlie@mail.com | Hello, World!
  4 | dan     | 101112   |                  | Hello, World!
  5 | eve     | 131415   |                  | Hello, World!
  6 | faythe  | 161718   |                  | Hello, World!
(6 rows)

________________________________________________________________

5.
db_1=# UPDATE users SET bio = 'hello,i am '||(name);
UPDATE 6
db_1=# SELECT * FROM users;
 id |  name   | password |      email       |        bio
----+---------+----------+------------------+--------------------
  1 | alice   | 123      | alice@mail.com   | hello,i am alice
  2 | bob     | 456      | bob@mail.com     | hello,i am bob
  3 | charlie | 789      | charlie@mail.com | hello,i am charlie
  4 | dan     | 101112   |                  | hello,i am dan
  5 | eve     | 131415   |                  | hello,i am eve
  6 | faythe  | 161718   |                  | hello,i am faythe
(6 rows)

_______________________________________________________________

6.
db_1=# SELECT * FROM users ORDER BY id DESC LIMIT 2;
 id |  name  | password | email |        bio
----+--------+----------+-------+-------------------
  6 | faythe | 161718   |       | hello,i am faythe
  5 | eve    | 131415   |       | hello,i am eve
(2 rows)

_______________________________________________________________

7.
db_1=# SELECT * FROM users WHERE id%2=1;
 id |  name   | password |      email       |        bio
----+---------+----------+------------------+--------------------
  1 | alice   | 123      | alice@mail.com   | hello,i am alice
  3 | charlie | 789      | charlie@mail.com | hello,i am charlie
  5 | eve     | 131415   |                  | hello,i am eve
(3 rows)

________________________________________________________________

8.
db_1=# DELETE FROM users WHERE id%2=0;
DELETE 3
db_1=# SELECT * FROM users;
 id |  name   | password |      email       |        bio
----+---------+----------+------------------+--------------------
  1 | alice   | 123      | alice@mail.com   | hello,i am alice
  3 | charlie | 789      | charlie@mail.com | hello,i am charlie
  5 | eve     | 131415   |                  | hello,i am eve
(3 rows)

_______________________________________________________________

9.
db_1=# DROP TABLE users;
DROP TABLE
postgres=# DROP DATABASE db_1;
DROP DATABASE


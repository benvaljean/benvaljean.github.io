---
layout: post 
title: SQL Examples
---

To join the table films with the table distributors:

    SELECT f.title, f.did, d.name, f.date_prod, f.kind
        FROM distributors d, films f
        WHERE f.did = d.did

           title       | did |     name     | date_prod  |   kind
    -------------------+-----+--------------+------------+----------
     The Third Man     | 101 | British Lion | 1949-12-23 | Drama
     The African Queen | 101 | British Lion | 1951-08-11 | Romantic
     ...

To sum the column len of all films and group the results by kind: SELECT
kind, sum(len) AS total FROM films GROUP BY kind;

       kind   | total
    ----------+-------
     Action   | 07:34
     Comedy   | 02:58
     Drama    | 14:28
     Musical  | 06:42
     Romantic | 04:38

To sum the column len of all films, group the results by kind and show
those group totals that are less than 5 hours:

    SELECT kind, sum(len) AS total
        FROM films
        GROUP BY kind
        HAVING sum(len) < interval '5 hours';

       kind   | total
    ----------+-------
     Comedy   | 02:58
     Romantic | 04:38

The following two examples are identical ways of sorting the individual
results according to the contents of the second column (name):

    SELECT * FROM distributors ORDER BY name;
    SELECT * FROM distributors ORDER BY 2;

     did |       name
    -----+------------------
     109 | 20th Century Fox
     110 | Bavaria Atelier
     101 | British Lion
     107 | Columbia
     102 | Jean Luc Godard
     113 | Luso films
     104 | Mosfilm
     103 | Paramount
     106 | Toho
     105 | United Artists
     111 | Walt Disney
     112 | Warner Bros.
     108 | Westward

The next example shows how to obtain the union of the tables
distributors and actors, restricting the results to those that begin
with the letter W in each table. Only distinct rows are wanted, so the
key word ALL is omitted.

    distributors:               actors:
     did |     name              id |     name
    -----+--------------        ----+----------------
     108 | Westward               1 | Woody Allen
     111 | Walt Disney            2 | Warren Beatty
     112 | Warner Bros.           3 | Walter Matthau
     ...                         ...

    SELECT distributors.name
        FROM distributors
        WHERE distributors.name LIKE 'W%'
    UNION
    SELECT actors.name
        FROM actors
        WHERE actors.name LIKE 'W%';

          name
    ----------------
     Walt Disney
     Walter Matthau
     Warner Bros.
     Warren Beatty
     Westward
     Woody Allen

This example shows how to use a function in the FROM clause, both with
and without a column definition list:

    CREATE FUNCTION distributors(int) RETURNS SETOF distributors AS $$
        SELECT * FROM distributors WHERE did = $1;
    $$ LANGUAGE SQL;

    SELECT * FROM distributors(111);
     did |    name
    -----+-------------
     111 | Walt Disney

    CREATE FUNCTION distributors_2(int) RETURNS SETOF record AS $$
        SELECT * FROM distributors WHERE did = $1;
    $$ LANGUAGE SQL;

    SELECT * FROM distributors_2(111) AS (f1 int, f2 text);
     f1  |     f2
    -----+-------------
     111 | Walt Disney

Taken from
<http://www.postgresql.org/docs/8.3/static/sql-select.html#SQL-FOR-UPDATE-SHARE>

#### Count records on multiple conditions and show weekly results

    select date_trunc('week',start),sum(case when blah is not null then 1 else 0 end) as blah_exists, count(*) as total from cust where user like 'pr/%' and start >='2012-01-01' group by 1 order by 1 asc;

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
[Category:MySQL](Category:MySQL "wikilink")

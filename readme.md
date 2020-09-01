SQL DataBases

Structured Query Language - 1970s

*reading data from a database is known as "querying"

BEST PRACTICE - capital letters, but not necessary

CHEATSHEET: https://github.com/treehouse/cheatsheets/blob/master/sql_basics/cheatsheet.md


-SQL-			-NoSQL- 	db's
________________________________________________
MySQL			MongoDB
PostgreSQL		CouchBase
Microsoft SQL		Redis
Oracle
SQLite


DATA 	V 	SCHEMA
info		how it's organized


------[Types of Data]---------------------------------------

Text Type Examples
-	TEXT
-	VARCHAR

Numeric Type Examples
-	INT
-	INTEGER

Date Type Examples
-	DATETIME
-	DATE
-	TIMESTAMP

++++++++++++ - KEYWORDS - +++++++++++++++++++++++++++++++++++++

SELECT * FROM <table name>;

S -when you want to write a query, retrieve info from table
* -bring info in all the tables columns back
; -like a question at the end of sentence, query OVER

EX)))

SELECT * FROM books;

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

ONE data

SELECT email FROM patrons;
SELECT first_name FROM patrons;

TWO data

SELECT first_name, email FROM patrons;
SELECT email, first_name FROM patrons;


=========+ AS +=================================================


SELECT title AS Title, first_published AS "First Published" FROM books;

*returns the column title as "Title" instead
*returns the column first_published as First Published
**have to use "" because 2 words
*** different rules for different databases "

=======CONDITIONALS--==--==--==--==--==--==--==--==--==--==--==--
=-=-=-=-=-=-=-=-=-=-=-=-= WHERE clause =-=-=-=-=-=-=-=-=-=-=-=-=-=

SELECT <columns> FROM <table> WHERE <condition>;

EX)

SELECT title, author FROM books WHERE first_published = 1997;

Equality / Inequality Values ------------------------------------
= != 
*CASE SeNsItIvE*

Relational Values / Relational Operators-------------------------

< less than
<= less than or equal to
> greater than
>= greater than or equal to

-------=----MULTIPLE CONDITIONS---------=---------=------=----=
===============================================================

SELECT title FROM books WHERE author = "J.K. Rowling" AND first_published < 2000;

AND	-all
OR	-either

---EXAMPLES-----

EX)

SELECT * FROM loans WHERE loaned_on < "2015-12-13";
answers "What are all the loans tht happened before December 13th, 2015?"

*Dates before now are considered LESS than dates after now

=+========+=======+ IN +========+========++=======+========++=======
----------------------------------for iterating----------------------------

SELECT <columns> FROM <table> WHERE <columns> IN (<value 1>, <value 2>, <value..>);

EX)

SELECT first_name, email FROM patrons WHERE library_id IN ("MC1001", "MC1100", "MC1011");
to find the people with the libary ID's (MCs)

** ADD in NOT before the IN to get the opposite

EX)

SELECT first_name, email FROM patrons WHERE library_id NOT IN ("MC1001", "MC1100", "MC1011");

=+========+=======+ BETWEEN +========+========++=====+======++=======
=================for ranges=============================================

SELECT <columns> FROM <table> WHERE <column> BETWEEN <minimum> AND <maximum>;

*lower value MUST be first



------------FINDING PATTERNS------------------------------------------------
------------------using details---------------------------------------------

LIKE

SELECT <columns> FROM <table> WHERE <column> LIKE <pattern>;
% is the wildcard, place it where you want it to guess, 
can place before AND after

EX)
SELECT title FROM books WHERE title LIKE "Harry Potter%Fire";
SELECT title FROM movies WHERE title LIKE "Alien%";
SELECT * FROM contacts WHERE first_name LIKE "%drew";
SELECT * FROM books WHERE title LIKE "%Brief History%";

PostgreSQL Specific Keywords
LIKE in PostgreSQL is case-sensitive. To case-insensitive searches do ILIKE.

SELECT * FROM contacts WHERE first_name ILIKE "%drew";

-----------FILTERING OUT-----------------------------------------------------
---------------OR finding missing information--------------------------------

SELECT * FROM loans WHERE return_by > "2015-12-18" AND returned_on IS NULL;
-people who haven't returned their books 
SELECT * FROM loans WHERE return_by > "2015-12-18" AND returned_on IS NOT NULL;
-people who have returned their books

===========QUERY from TWO TABLES=================================================
=====2===============================2===========================================

SELECT * FROM <table1>, <table2>
WHERE <table1>.<table1 column> = <table2>.<table2 column>
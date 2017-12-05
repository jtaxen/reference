HOW TO USE SQLITE
================

Open database:
=============
sqlite3 <db-name>

Show tables:
===========
.table

Show column names:
=================
pragma table_info(<table>);

Nice output:
============
.header on
.mode column

Select something:
================
select <column> in <table> where <condition 1> and <condition 2>;

Delete something:
================
delete from <table> where <condition>;

Copy a row from one db to another:
=================================
1.) Open db A.
2.) query:
attach database 'db B' as 'alias B';
3.) List attached db:s:
.database
4.) copy data from one table to another:
insert into <table A> select * from <alias B>.<table B> where <conditions>;


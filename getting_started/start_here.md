
Once you've created a free PythonAnywhere account, you can choose to start one of two consoles.

Ignoring the first row of consoles, we see there is a list called "other". These contain the tools that
we will be using to do our work. First, start by opening a MySQL console by clicking its blue link.

Once the console has finished loading, start asking MySQL to tell you a little more about itself.

Type in the following command:

    show databases;
	
Your output should roughly match this:
	
	+--------------------+       
	| Database           |
	+--------------------+            
	| information_schema |                           
	| USERNAME$default   |
	+--------------------+
	
    2 rows in set (0.09 sec)

These are the databases available to you. Continue with this command:

    show tables;
	
And the output:
	
	Empty set (0.00 sec)

Hopefully this isn't too suprpising. We haven't done anything yet. However, databases come with plenty of data already in them. 
There are tables of data that describe the database, and we'll look at that on in a moment by switching to it.

    mysql> use information_schema;
	
	Reading table information for completion of table and column names
	You can turn off this feature to get a quicker startup with -A
	
	Database changed
	
From now on I won't specify what your ouput should be. I will just print out the entire session of input/output. 
If you're having an error, it may be because you copy and pasted everything into the browser? Don't copy and paste the `mysql>` part. 

Actually, don't copy and paste *anything*. That's [no way to learn][Always_Type_Code] how to code! Type everything out yourself.

[Always_Type_Code]: http://www.shockoe.com/blog/typingcodeout/
	
Anyway, we are now looking at a new set of tables. Let's try that last operation again.

	mysql> show tables;
	+---------------------------------------+
	| Tables_in_information_schema          |
	+---------------------------------------+
	| CHARACTER_SETS                        |
	| COLLATIONS                            |
	| COLLATION_CHARACTER_SET_APPLICABILITY |
	| COLUMNS                               |
	| COLUMN_PRIVILEGES                     |
	| ENGINES                               |
	| EVENTS                                |
	| FILES                                 |
	| GLOBAL_STATUS                         |
	| GLOBAL_VARIABLES                      |
	| KEY_COLUMN_USAGE                      |
	| PARTITIONS                            |
	| PLUGINS                               |
	| PROCESSLIST                           |
	| PROFILING                             |
	| REFERENTIAL_CONSTRAINTS               |
	| ROUTINES                              |
	| SCHEMATA                              |
	| SCHEMA_PRIVILEGES                     |
	| SESSION_STATUS                        |
	| SESSION_VARIABLES                     |
	| STATISTICS                            |
	| TABLES                                |
	| TABLE_CONSTRAINTS                     |
	| TABLE_PRIVILEGES                      |
	| TRIGGERS                              |
	| USER_PRIVILEGES                       |
	| VIEWS                                 |
	| INNODB_CMP_RESET                      |
	| INNODB_TRX                            |
	| INNODB_CMPMEM_RESET                   |
	| INNODB_LOCK_WAITS                     |
	| INNODB_CMPMEM                         |
	| INNODB_CMP                            |
	| INNODB_LOCKS                          |
	+---------------------------------------+
	35 rows in set (0.00 sec)

The names of these tables are a little esoteric, but they are clear. Each of these tables contains what they advertise.

Let's have a closer look. Try to view everything in the `CHARACTER_SETS` table.

    mysql> SELECT * FROM CHARACTER_SETS;

Do you recognize any of these? There is one there that is very important to learn about. Here's some [additional reading][Additional_Reading], if you're interested.
[Additional_Reading]: http://en.wikipedia.org/wiki/UTF-8

To continue, let's try a new table.

    mysql> SELECT * FROM TABLES;
	...[way to much information]...
	35 rows in the set (0.09 sec)
	
That time we got a little scrolling action going on. Plus, there's all kinds of stacking and indenting issues happening because of how the output wrapped itself on new lines.

Let's try that again. Scroll up to the top of your output, and read the column names. There should be two distinct rows of columns, that look something like this:

	+---------------+--------------------+---------------------------------------+-------------+--------+---------+------------+------------+----------------+-------------+-----------------+--------------+-----------+----------------+-----
	----------------+---------------------+------------+-----------------+----------+-----------------+---------------+
	| TABLE_CATALOG | TABLE_SCHEMA       | TABLE_NAME                            | TABLE_TYPE  | ENGINE | VERSION | ROW_FORMAT | TABLE_ROWS | AVG_ROW_LENGTH | DATA_LENGTH | MAX_DATA_LENGTH | INDEX_LENGTH | DATA_FREE | AUTO_INCREMENT | CREA
	TE_TIME         | UPDATE_TIME         | CHECK_TIME | TABLE_COLLATION | CHECKSUM | CREATE_OPTIONS  | TABLE_COMMENT |
	+---------------+--------------------+---------------------------------------+-------------+--------+---------+------------+------------+----------------+-------------+-----------------+--------------+-----------+----------------+-----
	----------------+---------------------+------------+-----------------+----------+-----------------+---------------+
	
Pretty ugly? Notice that instead of one row of column names, we have two. This is because of wrapping. 
Just try to focus on the top left-most column name: `TABLE_CATALOG`. That's the first column name.
The next column names are `TABLE_SCHEMA` (the database the table lives in), `TABLE_TYPE`, and others.

Let's try to get just some of the more important information, and cut down on all this visual noise.

    mysql> SELECT TABLE_NAME FROM TABLES;
	+---------------------------------------+
	| TABLE_NAME                            |
	+---------------------------------------+
	| CHARACTER_SETS                        |
	| COLLATIONS                            |
	| COLLATION_CHARACTER_SET_APPLICABILITY |
	| COLUMNS                               |
	| COLUMN_PRIVILEGES                     |
	| ENGINES                               |
	| EVENTS                                |
	| FILES                                 |
	| GLOBAL_STATUS                         |
	| GLOBAL_VARIABLES                      |
	| KEY_COLUMN_USAGE                      |
	| PARTITIONS                            |
	| PLUGINS                               |
	| PROCESSLIST                           |
	| PROFILING                             |
	| REFERENTIAL_CONSTRAINTS               |
	| ROUTINES                              |
	| SCHEMATA                              |
	| SCHEMA_PRIVILEGES                     |
	| SESSION_STATUS                        |
	| SESSION_VARIABLES                     |
	| STATISTICS                            |
	| TABLES                                |
	| TABLE_CONSTRAINTS                     |
	| TABLE_PRIVILEGES                      |
	| TRIGGERS                              |
	| USER_PRIVILEGES                       |
	| VIEWS                                 |
	| INNODB_CMP_RESET                      |
	| INNODB_TRX                            |
	| INNODB_CMPMEM_RESET                   |
	| INNODB_LOCK_WAITS                     |
	| INNODB_CMPMEM                         |
	| INNODB_CMP                            |
	| INNODB_LOCKS                          |
	+---------------------------------------+
	35 rows in set (0.10 sec)	
	
Look familiar? Yes, that's equivilent to `show tables` for the whole database. Like I said, this is a database of information about the database.

Let's try getting data from two columns.

	mysql> SELECT TABLE_NAME, TABLE_COLLATION FROM TABLES;
	+---------------------------------------+-----------------+
	| TABLE_NAME                            | TABLE_COLLATION |
	+---------------------------------------+-----------------+
	| CHARACTER_SETS                        | utf8_general_ci |
	| COLLATIONS                            | utf8_general_ci |
	| COLLATION_CHARACTER_SET_APPLICABILITY | utf8_general_ci |
	| COLUMNS                               | utf8_general_ci |
	| COLUMN_PRIVILEGES                     | utf8_general_ci |
	| ENGINES                               | utf8_general_ci |
	| EVENTS                                | utf8_general_ci |
	| FILES                                 | utf8_general_ci |
	| GLOBAL_STATUS                         | utf8_general_ci |
	| GLOBAL_VARIABLES                      | utf8_general_ci |
	| KEY_COLUMN_USAGE                      | utf8_general_ci |
	| PARTITIONS                            | utf8_general_ci |
	| PLUGINS                               | utf8_general_ci |
	| PROCESSLIST                           | utf8_general_ci |
	| PROFILING                             | utf8_general_ci |
	| REFERENTIAL_CONSTRAINTS               | utf8_general_ci |
	| ROUTINES                              | utf8_general_ci |
	| SCHEMATA                              | utf8_general_ci |
	| SCHEMA_PRIVILEGES                     | utf8_general_ci |
	| SESSION_STATUS                        | utf8_general_ci |
	| SESSION_VARIABLES                     | utf8_general_ci |
	| STATISTICS                            | utf8_general_ci |
	| TABLES                                | utf8_general_ci |
	| TABLE_CONSTRAINTS                     | utf8_general_ci |
	| TABLE_PRIVILEGES                      | utf8_general_ci |
	| TRIGGERS                              | utf8_general_ci |
	| USER_PRIVILEGES                       | utf8_general_ci |
	| VIEWS                                 | utf8_general_ci |
	| INNODB_CMP_RESET                      | utf8_general_ci |
	| INNODB_TRX                            | utf8_general_ci |
	| INNODB_CMPMEM_RESET                   | utf8_general_ci |
	| INNODB_LOCK_WAITS                     | utf8_general_ci |
	| INNODB_CMPMEM                         | utf8_general_ci |
	| INNODB_CMP                            | utf8_general_ci |
	| INNODB_LOCKS                          | utf8_general_ci |
	+---------------------------------------+-----------------+
	35 rows in set (0.09 sec)
	
If you decided to read that link I posted earlier about character sets, take note. The MySQL developers chose utf8 for a reason. You should too.

In the future, you may find that `SELECT *` queries are just horrid ways of finding out information about tables, but it's easy when the data set is small.
So, how do you know if a table has 10 rows in it, or 10 million rows?

    mysql> SELECT COUNT(*) FROM COLUMNS;
	+----------+
	| COUNT(*) |
	+----------+
	|      359 |
	+----------+
	1 row in set (0.10 sec)
	
If you want to see what things look like anyway, here's a good way to do that:

	mysql> SELECT * FROM COLUMNS LIMIT 10;
	+---------------+--------------------+----------------+----------------------+------------------+----------------+-------------+-----------+--------------------------+------------------------+-------------------+---------------+-------
	-------------+-----------------+-------------+------------+-------+------------+----------------+
	| TABLE_CATALOG | TABLE_SCHEMA       | TABLE_NAME     | COLUMN_NAME          | ORDINAL_POSITION | COLUMN_DEFAULT | IS_NULLABLE | DATA_TYPE | CHARACTER_MAXIMUM_LENGTH | CHARACTER_OCTET_LENGTH | NUMERIC_PRECISION | NUMERIC_SCALE | CHARAC
	TER_SET_NAME | COLLATION_NAME  | COLUMN_TYPE | COLUMN_KEY | EXTRA | PRIVILEGES | COLUMN_COMMENT |
	+---------------+--------------------+----------------+----------------------+------------------+----------------+-------------+-----------+--------------------------+------------------------+-------------------+---------------+-------
	-------------+-----------------+-------------+------------+-------+------------+----------------+
	| NULL          | information_schema | CHARACTER_SETS | CHARACTER_SET_NAME   |                1 |                | NO          | varchar   |                       32 |                     96 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(32) |            |       | select     |                |
	| NULL          | information_schema | CHARACTER_SETS | DEFAULT_COLLATE_NAME |                2 |                | NO          | varchar   |                       32 |                     96 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(32) |            |       | select     |                |
	| NULL          | information_schema | CHARACTER_SETS | DESCRIPTION          |                3 |                | NO          | varchar   |                       60 |                    180 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(60) |            |       | select     |                |
	| NULL          | information_schema | CHARACTER_SETS | MAXLEN               |                4 | 0              | NO          | bigint    |                     NULL |                   NULL |                19 |             0 | NULL
				 | NULL            | bigint(3)   |            |       | select     |                |
	| NULL          | information_schema | COLLATIONS     | COLLATION_NAME       |                1 |                | NO          | varchar   |                       32 |                     96 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(32) |            |       | select     |                |
	| NULL          | information_schema | COLLATIONS     | CHARACTER_SET_NAME   |                2 |                | NO          | varchar   |                       32 |                     96 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(32) |            |       | select     |                |
	| NULL          | information_schema | COLLATIONS     | ID                   |                3 | 0              | NO          | bigint    |                     NULL |                   NULL |                19 |             0 | NULL
				 | NULL            | bigint(11)  |            |       | select     |                |
	| NULL          | information_schema | COLLATIONS     | IS_DEFAULT           |                4 |                | NO          | varchar   |                        3 |                      9 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(3)  |            |       | select     |                |
	| NULL          | information_schema | COLLATIONS     | IS_COMPILED          |                5 |                | NO          | varchar   |                        3 |                      9 |              NULL |          NULL | utf8
				 | utf8_general_ci | varchar(3)  |            |       | select     |                |
	| NULL          | information_schema | COLLATIONS     | SORTLEN              |                6 | 0              | NO          | bigint    |                     NULL |                   NULL |                19 |             0 | NULL
				 | NULL            | bigint(3)   |            |       | select     |                |
	+---------------+--------------------+----------------+----------------------+------------------+----------------+-------------+-----------+--------------------------+------------------------+-------------------+---------------+-------
	-------------+-----------------+-------------+------------+-------+------------+----------------+
	10 rows in set (0.10 sec)
	
Eh. Not so good. At least we know now that `SELECT *` isn't always the best approach. We should ask for specific columns in the database to limit this sort of thing.
But...how do we know which columns to ask for? Ah. Here is a good place to introduce yet another great `SHOW` statement.

    mysql> SHOW COLUMNS FROM COLUMNS;
	+--------------------------+---------------------+------+-----+---------+-------+
	| Field                    | Type                | Null | Key | Default | Extra |
	+--------------------------+---------------------+------+-----+---------+-------+
	| TABLE_CATALOG            | varchar(512)        | YES  |     | NULL    |       |
	| TABLE_SCHEMA             | varchar(64)         | NO   |     |         |       |
	| TABLE_NAME               | varchar(64)         | NO   |     |         |       |
	| COLUMN_NAME              | varchar(64)         | NO   |     |         |       |
	| ORDINAL_POSITION         | bigint(21) unsigned | NO   |     | 0       |       |
	| COLUMN_DEFAULT           | longtext            | YES  |     | NULL    |       |
	| IS_NULLABLE              | varchar(3)          | NO   |     |         |       |
	| DATA_TYPE                | varchar(64)         | NO   |     |         |       |
	| CHARACTER_MAXIMUM_LENGTH | bigint(21) unsigned | YES  |     | NULL    |       |
	| CHARACTER_OCTET_LENGTH   | bigint(21) unsigned | YES  |     | NULL    |       |
	| NUMERIC_PRECISION        | bigint(21) unsigned | YES  |     | NULL    |       |
	| NUMERIC_SCALE            | bigint(21) unsigned | YES  |     | NULL    |       |
	| CHARACTER_SET_NAME       | varchar(32)         | YES  |     | NULL    |       |
	| COLLATION_NAME           | varchar(32)         | YES  |     | NULL    |       |
	| COLUMN_TYPE              | longtext            | NO   |     | NULL    |       |
	| COLUMN_KEY               | varchar(3)          | NO   |     |         |       |
	| EXTRA                    | varchar(27)         | NO   |     |         |       |
	| PRIVILEGES               | varchar(80)         | NO   |     |         |       |
	| COLUMN_COMMENT           | varchar(255)        | NO   |     |         |       |
	+--------------------------+---------------------+------+-----+---------+-------+
	19 rows in set (0.00 sec)
	
So there we have it. Exploring our database is easy with the built in `SHOW` statements for databases, tables in databases, and columns in tables.
And now we also know how to look at specific information without using `SELECT * FROM TABLE_NAME`. 

Just remember, in the real world there are many, many different ways to do things. 
This tutorial is meant only to show you how the `SHOW` statements work, and at the same time, introduce you to `SELECT` statements, as well as the `information_schema` database. 

The point is, don't do stuff like this, even though you can.

	mysql> SELECT TABLE_NAME, COLUMN_NAME, COLLATION_NAME FROM COLUMNS WHERE TABLE_NAME LIKE 'COLUMNS';
	+------------+--------------------------+-----------------+
	| TABLE_NAME | COLUMN_NAME              | COLLATION_NAME  |
	+------------+--------------------------+-----------------+
	| COLUMNS    | TABLE_CATALOG            | utf8_general_ci |
	| COLUMNS    | TABLE_SCHEMA             | utf8_general_ci |
	| COLUMNS    | TABLE_NAME               | utf8_general_ci |
	| COLUMNS    | COLUMN_NAME              | utf8_general_ci |
	| COLUMNS    | ORDINAL_POSITION         | NULL            |
	| COLUMNS    | COLUMN_DEFAULT           | utf8_general_ci |
	| COLUMNS    | IS_NULLABLE              | utf8_general_ci |
	| COLUMNS    | DATA_TYPE                | utf8_general_ci |
	| COLUMNS    | CHARACTER_MAXIMUM_LENGTH | NULL            |
	| COLUMNS    | CHARACTER_OCTET_LENGTH   | NULL            |
	| COLUMNS    | NUMERIC_PRECISION        | NULL            |
	| COLUMNS    | NUMERIC_SCALE            | NULL            |
	| COLUMNS    | CHARACTER_SET_NAME       | utf8_general_ci |
	| COLUMNS    | COLLATION_NAME           | utf8_general_ci |
	| COLUMNS    | COLUMN_TYPE              | utf8_general_ci |
	| COLUMNS    | COLUMN_KEY               | utf8_general_ci |
	| COLUMNS    | EXTRA                    | utf8_general_ci |
	| COLUMNS    | PRIVILEGES               | utf8_general_ci |
	| COLUMNS    | COLUMN_COMMENT           | utf8_general_ci |
	+------------+--------------------------+-----------------+
	19 rows in set (0.09 sec)
	
Just use the appropriate `SHOW` statement.

This is a good stopping point for right now.

Here is a link to the [next walkthrough][Next_Walkthrough].

[Next_Walkthrough]: https://github.com/Droogans/mysql_tutorial/blob/master/getting_started/using_git.md
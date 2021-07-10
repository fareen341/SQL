<b>COMMANDS IN MYSQL</b><br>
#DDL(data definition language): THIS DEALS WITH SCHEMA(STRUCTURE) MEANING (TABLES):<br><br>
1)create (to create view, function, triggers.....etc  )<br>
2)alter<br>
3)drop<br>
4)truncate<br>
5)rename<br>
6)comment<br>
<br>
1)create<br>
Syntax:<br>
<b>1)create (table,view,function) table_name,view_name,function_name;</b><br>
Example:
create table student(rollno int, name varchar(20), date int);
<pre>
MariaDB [testingdb]> create table dummy(
    -> id int
    -> );
Query OK, 0 rows affected (2.314 sec)


To see the table description use desc or describe followed by table name:
MariaDB [testingdb]> desc dummy;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| id    | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
1 row in set (0.102 sec)
</pre>

<b>2)alter table:</b>
i)to add new column:
<pre>
MariaDB [testingdb]> alter table dummy add name varchar(20);
Query OK, 0 rows affected (0.513 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [testingdb]> desc dummy;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.040 sec)
</pre>

ii)to modify column datatype:
<pre>
MariaDB [testingdb]> alter table dummy modify name int;
Query OK, 0 rows affected (1.395 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [testingdb]> desc dummy;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| id    | int(11) | YES  |     | NULL    |       |
| name  | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.014 sec)
</pre>

iii)to add gender column after id:
<pre>
MariaDB [testingdb]> alter table dummy add column gender char(1) after id;
Query OK, 0 rows affected (0.173 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [testingdb]> desc dummy;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int(11)     | YES  |     | NULL    |       |
| gender | char(1)     | YES  |     | NULL    |       |
| name   | varchar(20) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.032 sec)
</pre>

iv)to add column the very first:
<pre>
MariaDB [testingdb]> alter table dummy add column user_id int first;
Query OK, 0 rows affected (0.816 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [testingdb]> desc dummy;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| user_id | int(11)     | YES  |     | NULL    |       |
| id      | int(11)     | YES  |     | NULL    |       |
| gender  | char(1)     | YES  |     | NULL    |       |
| name    | varchar(20) | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.136 sec)
</pre>

v)to delete a column:
<pre>
MariaDB [testingdb]> alter table dummy drop column name;
Query OK, 0 rows affected (0.122 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

<b>3)drop: to drop the entire table with structure and record:</b>
<pre>
MariaDB [testingdb]> drop table dummy;
Query OK, 0 rows affected (1.185 sec)
</pre>

<b>4)truncate: this delete all data, and keep only structure, every space allocated for the data is removed</b>
<pre>
>truncate table dummy;
</pre>

<b>5)rename: to rename table name</b>
Note: table name is not case sensitive, but the records are case sensitive.
Example: table emp,EMP,Emp are all same , but record Fareen,FAREEN,fareen all are different.
<pre>
MariaDB [testingdb]> create table emp(id int);
Query OK, 0 rows affected (0.578 sec)

MariaDB [testingdb]> create table EMP(name varchar(20));
ERROR 1050 (42S01): Table 'emp' already exists
</pre>

<pre>
MariaDB [testingdb]> alter table emp rename to emp_info;
Query OK, 0 rows affected (0.832 sec)
</pre>

<b>6)comment</b>

<b>DML</b>
1)insert
2)update
3)delete

<b>1)insert</b>
Method 1:
<pre>
MariaDB [testingdb]> insert into customer values(1,'fareen');
Query OK, 1 row affected (0.094 sec)
</pre>
Method 2:
<pre>
MariaDB [testingdb]> insert into customer(id,name) values(2,'annu');
Query OK, 1 row affected (0.072 sec)
</pre>
To insert multiple records in one single command:
<pre>
MariaDB [testingdb]> insert into customer(id,name) values(3,'zoya'),(4,'sana');
Query OK, 2 rows affected (0.044 sec)
Records: 2  Duplicates: 0  Warnings: 0
</pre>

To copy the record of one table into another use the below command, but for this command to execute properly the structure of both the table must be same:
<pre>
MariaDB [testingdb]> insert into emp(select * from customer);
Query OK, 4 rows affected (0.118 sec)
Records: 4  Duplicates: 0  Warnings: 0
</pre>

<b>CONSTRAINTS</b>
1)primary key
2)foreign key
3)check
4)unique
5)not null
6)default

<b>1)primary key</b>
column level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int primary key
    -> );
Query OK, 0 rows affected (0.707 sec)
</pre>

table level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> primary key(id)
    -> );
Query OK, 0 rows affected (0.552 sec)
</pre>

multiple primary key on single table:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> user_id int,
    -> primary key(id,user_id)
    -> );
Query OK, 0 rows affected (1.423 sec)
</pre>

add existing table
<pre>
MariaDB [testingdb]> alter table emp add primary key(id,user_id);
Query OK, 0 rows affected (1.057 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

drop:
<pre>
MariaDB [testingdb]> alter table emp drop primary key;

we can't do >alter table emp drop primary key(id);   //invalid
</pre>

<b>2)Foreign key:</b><br>
mobile table

When deleting the record from student table it'll give error, but we can delete record from mobile table, Also id which is linked cannot be update<br>
<pre>
MariaDB [testingdb]> delete from student where id=2;<br>
ERROR 1451 (23000): Cannot delete or update a parent row: a foreign key constraint fails (`testingdb`.`mobile`,<br> CONSTRAINT `mobile_ibfk_1` FOREIGN KEY (`sid`) REFERENCES `student` (`id`))<br>
</pre>

To delete the data from student table we can achieve that using:<br>
But deleting the data from student table will also delete the data linked in mobile table.<br>
Example:if we delete id=1 record from student table it also must delete the id=1 linked record from mobile table as well<br>
Use command to achieve this use:<br>
<pre>
MariaDB [testingdb]> create table mobile(
    -> id int primary key auto_increment,
    -> sid int,mob varchar(40),
    -> foreign key(sid) references student(id) on delete cascade on update cascade);
Query OK, 0 rows affected (0.711 sec)
</pre>

<b>3)check</b>
row level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> age int check(age > 18)
    -> );
Query OK, 0 rows affected (0.350 sec)
</pre>

column level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> age int,
    -> check(age > 18)
    -> );
Query OK, 0 rows affected (0.567 sec)
</pre>

add on existing table:
<pre>
MariaDB [testingdb]> alter table emp add constraint chk check(age > 18);
Query OK, 0 rows affected (1.054 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

drop:
<pre>
MariaDB [testingdb]> alter table emp drop constraint chk;
Query OK, 0 rows affected (0.089 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

<b>4)unique</b>
row level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> subject varchar(10) unique
    -> );
Query OK, 0 rows affected (0.488 sec)


</pre>

table level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> subject varchar(10),
    -> constraint uk1 unique(subject)
    -> );
Query OK, 0 rows affected (0.253 sec)

OR 

MariaDB [testingdb]> create table emp(
    -> id int,
    -> subject varchar(10),
    -> unique(subject)
    -> );
Query OK, 0 rows affected (0.620 sec)
</pre>

add on existing table:
<pre>
MariaDB [testingdb]> alter table emp add constraint unk unique(subject);
Query OK, 0 rows affected (0.325 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

drop:
<pre>
MariaDB [testingdb]> alter table emp drop constraint unk;
Query OK, 0 rows affected (1.163 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

<b>6)not null</b>
on row level:
<pre>
MariaDB [testingdb]> create table emp(
    -> id int not null
    -> );
Query OK, 0 rows affected (0.526 sec)
</pre>

no table level for this one:

add on the existing table:
In MySQL, nullability is a part of the datatype, not a constraint. So:
<pre>
MariaDB [testingdb]> alter table emp modify id int not null;
Query OK, 0 rows affected (0.806 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

drop:
<pre>
MariaDB [testingdb]> alter table emp modify id int;
Query OK, 0 rows affected (0.789 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>


<b>7)default</b>
<pre>
MariaDB [testingdb]> create table emp(
    -> id int,
    -> loc varchar(20) default 'Mumbai'
    -> );
Query OK, 0 rows affected (0.286 sec)
</pre>

no table level for this:

add on existing table:
<pre>
MariaDB [testingdb]> alter table emp modify loc varchar(20) default 'Mumbai';
Query OK, 0 rows affected (0.137 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>

drop:
<pre>
MariaDB [testingdb]> alter table emp alter loc set default 'Mumbai';
Query OK, 0 rows affected (0.456 sec)
Records: 0  Duplicates: 0  Warnings: 0

OR

MariaDB [testingdb]> alter table emp alter loc drop default;
Query OK, 0 rows affected (0.055 sec)
Records: 0  Duplicates: 0  Warnings: 0
</pre>



Updating:
<pre>
MariaDB [testingdb]> update student
set id=4 where id=2;
Query OK, 1 row affected (0.168 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [testingdb]> select * from student;
+----+---------+------+
| id | name    | per  |
+----+---------+------+
|  1 | fareen  | 77.8 |
|  3 | sana    |   50 |
|  4 | anamika |   90 |
+----+---------+------+
3 rows in set (0.001 sec)

MariaDB [testingdb]> select * from mobile;
+----+------+-------------+
| id | sid  | mob         |
+----+------+-------------+
|  1 |    1 | 9876543210  |
|  2 |    4 | 83948674638 |
|  3 |    4 | 9486848390  |
+----+------+-------------+
3 rows in set (0.000 sec)
</pre>

Deleting:
<pre>
MariaDB [testingdb]> delete from student where id=4;
Query OK, 1 row affected (0.075 sec)

MariaDB [testingdb]> select * from student;
+----+--------+------+
| id | name   | per  |
+----+--------+------+
|  1 | fareen | 77.8 |
|  3 | sana   |   50 |
+----+--------+------+
2 rows in set (0.000 sec)

MariaDB [testingdb]> select * from mobile;
+----+------+------------+
| id | sid  | mob        |
+----+------+------------+
|  1 |    1 | 9876543210 |
+----+------+------------+
1 row in set (0.000 sec)
</pre>

<b>OPERATORS</b><br>
1)as operators : 'as' is used to give alias name.<br>
<pre>
MariaDB [testingdb]> select x as x_label,y as y_label from number;
+---------+---------+
| x_label | y_label |
+---------+---------+
|      10 |      20 |
|      40 |      58 |
|       3 |      56 |
+---------+---------+
3 rows in set (0.000 sec)
</pre>

2)Atrithmetic Operator(+,-,/,*,%):<br>
<pre>
MariaDB [testingdb]> select x,y, x+y as addition,x-y as subtraction, x*y as multiplication, x/y as division, x%y as modulus from number;
+------+------+----------+-------------+----------------+----------+---------+
| x    | y    | addition | subtraction | multiplication | division | modulus |
+------+------+----------+-------------+----------------+----------+---------+
|   10 |   20 |       30 |         -10 |            200 |   0.5000 |      10 |
|   40 |   58 |       98 |         -18 |           2320 |   0.6897 |      40 |
|    3 |   56 |       59 |         -53 |            168 |   0.0536 |       3 |
+------+------+----------+-------------+----------------+----------+---------+
3 rows in set (0.001 sec)
</pre>

It works without as keyword as well, but better to write as.<br>
<pre>
MariaDB [testingdb]> select x+y addition from number;
+----------+
| addition |
+----------+
|       30 |
|       98 |
|       59 |
+----------+
3 rows in set (0.001 sec)
</pre>

3)Comparision operator(<,>,<=,>=,=,==):<br>
for assigning value we use set operator just like we use in update query.<br>
Examples<br>
<pre>
MariaDB [testingdb]> select * from emp2;
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  1 | Fareen  | IT       |  50000 | 2018-09-02 |
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
|  3 | Roma    | Accounts |  60000 | 2020-03-02 |
+----+---------+----------+--------+------------+
3 rows in set (0.000 sec)

MariaDB [testingdb]> select * from emp2 where dept='IT';
+----+--------+------+--------+------------+
| id | name   | dept | salary | doj        |
+----+--------+------+--------+------------+
|  1 | Fareen | IT   |  50000 | 2018-09-02 |
+----+--------+------+--------+------------+
1 row in set (0.029 sec)

MariaDB [testingdb]> select * from emp2 where salary>50000;
+----+------+----------+--------+------------+
| id | name | dept     | salary | doj        |
+----+------+----------+--------+------------+
|  3 | Roma | Accounts |  60000 | 2020-03-02 |
+----+------+----------+--------+------------+
1 row in set (0.059 sec)

MariaDB [testingdb]> select * from emp2 where salary>=50000;
+----+--------+----------+--------+------------+
| id | name   | dept     | salary | doj        |
+----+--------+----------+--------+------------+
|  1 | Fareen | IT       |  50000 | 2018-09-02 |
|  3 | Roma   | Accounts |  60000 | 2020-03-02 |
+----+--------+----------+--------+------------+
2 rows in set (0.001 sec)

MariaDB [testingdb]> select * from emp2 where doj>='2021-07-05';
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
1 row in set (0.044 sec)
</pre>

4)Logical operator(and,or,not):
To check more than one condition at a time<br>
<u>and operator</u><br>
Example<br>
<pre>
MariaDB [testingdb]> select * from emp2 where salary>50000 and salary<70000;
+----+------+----------+--------+------------+
| id | name | dept     | salary | doj        |
+----+------+----------+--------+------------+
|  3 | Roma | Accounts |  60000 | 2020-03-02 |
+----+------+----------+--------+------------+
1 row in set (0.131 sec)
</pre>

<u>or operator</u><br>
Example<br>
<pre>
MariaDB [testingdb]> select * from emp2 where salary=30000 or salary=50000 or salary=34000;
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  1 | Fareen  | IT       |  50000 | 2018-09-02 |
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
2 rows in set (0.039 sec)
</pre>
This query is same as >select * from emp2 where salary IN(30000,50000,34000);

<u>not operator</u><br>
Example<br>
<pre>
</pre>

5)Instead or wtiting multiple or operator use IN & NOT IN<br>
Example<br>
<pre>
MariaDB [testingdb]> select * from emp2 where salary IN(50000,60000,70000);
+----+--------+----------+--------+------------+
| id | name   | dept     | salary | doj        |
+----+--------+----------+--------+------------+
|  1 | Fareen | IT       |  50000 | 2018-09-02 |
|  3 | Roma   | Accounts |  60000 | 2020-03-02 |
+----+--------+----------+--------+------------+
2 rows in set (0.049 sec)

MariaDB [testingdb]> select * from emp2 where salary NOT IN(50000,60000,70000);
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
1 row in set (0.001 sec)
</pre>

6)Between Operator:<br>
Example<br>
<pre>
MariaDB [testingdb]> select * from emp2 where salary between 30000 and 60000;
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  1 | Fareen  | IT       |  50000 | 2018-09-02 |
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
|  3 | Roma    | Accounts |  60000 | 2020-03-02 |
+----+---------+----------+--------+------------+
3 rows in set (0.001 sec)
</pre>
Here including 30000 and 60000.

7)NULL & NOT NULL<br>
Example:<br>
<pre>
MariaDB [testingdb]> select * from student where per is NULL;
+----+---------+------+
| id | name    | per  |
+----+---------+------+
|  6 | anamika | NULL |
|  7 | roma    | NULL |
+----+---------+------+
2 rows in set (0.147 sec)

MariaDB [testingdb]> select * from student where per is NOT NULL;
+----+--------+------+
| id | name   | per  |
+----+--------+------+
|  1 | fareen | 77.8 |
|  3 | sana   |   50 |
+----+--------+------+
2 rows in set (0.000 sec)
</pre>

8)Like operator:<br>
Example<br>
1)IT% - record which starts with IT.<br>
2)%IT - record which ends with IT.<br>
3)%IT% - record which has IT start or end or anywhere in between.<br>
4)_m% - record which has m in the second position, __m record which has m in the 3rd position, ___m which has m in the 4th position ...so on.<br>

<pre>
1)
MariaDB [testingdb]> select * from emp2 where name LIKE 'R%';
+----+------+----------+--------+------------+
| id | name | dept     | salary | doj        |
+----+------+----------+--------+------------+
|  3 | Roma | Accounts |  60000 | 2020-03-02 |
+----+------+----------+--------+------------+
1 row in set (0.142 sec)

MariaDB [testingdb]> select * from emp2 where name LIKE 'r%';
+----+------+----------+--------+------------+
| id | name | dept     | salary | doj        |
+----+------+----------+--------+------------+
|  3 | Roma | Accounts |  60000 | 2020-03-02 |
+----+------+----------+--------+------------+
1 row in set (0.001 sec)

2)
MariaDB [testingdb]> select * from emp2 where name LIKE '%ka';
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select * from emp2 where name LIKE '%KA';
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
1 row in set (0.001 sec)

3)
MariaDB [testingdb]> select * from emp2 where name LIKE '%mik%';
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
1 row in set (0.000 sec)

4)
MariaDB [testingdb]> select * from emp2 where name LIKE '__a%';
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
1 row in set (0.000 sec)
</pre>



<b>CLAUSES</b><br>
1)Order by clause: default is ascending order.<br>
to sort in descending order, use desc.<br>
Example<br>
<pre>
MariaDB [testingdb]> select * from emp2 order by salary;
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
|  1 | Fareen  | IT       |  50000 | 2018-09-02 |
|  3 | Roma    | Accounts |  60000 | 2020-03-02 |
+----+---------+----------+--------+------------+
3 rows in set (0.091 sec)

MariaDB [testingdb]> select * from emp2 order by salary desc;
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  3 | Roma    | Accounts |  60000 | 2020-03-02 |
|  1 | Fareen  | IT       |  50000 | 2018-09-02 |
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
3 rows in set (0.001 sec)
</pre>

2)Limit clause: to limit the number of records<br>
Example<br>
<pre>
MariaDB [testingdb]> select * from emp2 limit 2;
+----+---------+----------+--------+------------+
| id | name    | dept     | salary | doj        |
+----+---------+----------+--------+------------+
|  1 | Fareen  | IT       |  50000 | 2018-09-02 |
|  2 | Anamika | Accounts |  34000 | 2021-08-02 |
+----+---------+----------+--------+------------+
2 rows in set (0.001 sec)
</pre>


<b>FUNCTIONS</b>

<b>DISTINCT FUNCTION</b><br>
It won't allow the repeated records.
Example<br>
<pre>
MariaDB [testingdb]> select distinct(dept) as depts from emp2;
+----------+
| depts    |
+----------+
| IT       |
| Accounts |
+----------+
2 rows in set (0.042 sec)
</pre>


1)Concat function<br>
<pre>
MariaDB [testingdb]> select CONCAT('Good','-','Evening') as greeting;
+--------------+
| greeting     |
+--------------+
| Good-Evening |
+--------------+
1 row in set (0.060 sec)

MariaDB [testingdb]> select name,dept,CONCAT(name,'-',dept) as name_dept from emp2;
+---------+----------+------------------+
| name    | dept     | name_dept        |
+---------+----------+------------------+
| Fareen  | IT       | Fareen-IT        |
| Anamika | Accounts | Anamika-Accounts |
| Roma    | Accounts | Roma-Accounts    |
+---------+----------+------------------+
3 rows in set (0.000 sec)
</pre>

2)upper,lower function:<br>
<pre>
MariaDB [testingdb]> select UPPER('fareen');
+-----------------+
| UPPER('fareen') |
+-----------------+
| FAREEN          |
+-----------------+
1 row in set (0.128 sec)

MariaDB [testingdb]> select LOWER('FAREEN');
+-----------------+
| LOWER('FAREEN') |
+-----------------+
| fareen          |
+-----------------+
1 row in set (0.016 sec)

MariaDB [testingdb]> select name,dept,UPPER(name) as name_upper from emp2;
+---------+----------+------------+
| name    | dept     | name_upper |
+---------+----------+------------+
| Fareen  | IT       | FAREEN     |
| Anamika | Accounts | ANAMIKA    |
| Roma    | Accounts | ROMA       |
+---------+----------+------------+
3 rows in set (0.001 sec)
</pre>

3)Replace function<br>
select REPLACE(string, <br>
select_from given string, <br>
replace with another string)<br>
<pre>
MariaDB [testingdb]> select REPLACE("Good Morning","Morning",'Evening');
+---------------------------------------------+
| REPLACE("Good Morning","Morning",'Evening') |
+---------------------------------------------+
| Good Evening                                |
+---------------------------------------------+
1 row in set (0.001 sec)

MariaDB [testingdb]> select dept, REPLACE(dept,'IT','IT DEPARTMENT') as u_dept from emp2;
+----------+---------------+
| dept     | u_dept        |
+----------+---------------+
| IT       | IT DEPARTMENT |
| Accounts | Accounts      |
| Accounts | Accounts      |
+----------+---------------+
3 rows in set (0.000 sec)
</pre>

4)Substr()<br>
To get substring from the string<br>
SUBSTRING(string/column, <br>
start_pos, <br>
length)<br>
<pre>
MariaDB [testingdb]> select SUBSTR('ITVEDANT',2,4) as result;
+--------+
| result |
+--------+
| TVED   |
+--------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select SUBSTR(dept,2,4) as result from emp2;
+--------+
| result |
+--------+
| T      |
| ccou   |
| ccou   |
+--------+
3 rows in set (0.000 sec)
</pre>

5)length<br>
To get the length of the string<br>
<pre>
MariaDB [testingdb]> select LENGTH ('fareen') as result;
+--------+
| result |
+--------+
|      6 |
+--------+
1 row in set (0.107 sec)

MariaDB [testingdb]> select LENGTH (dept) as result from emp2;
+--------+
| result |
+--------+
|      2 |
|      8 |
|      8 |
+--------+
3 rows in set (0.000 sec)

</pre>

6)Math function:<br>
abs(), ceil(), floor(), round(), MOD(N2,N2), exp(), pow(), sqrt();<br>
<pre>
MariaDB [testingdb]> select abs(-4) as result;
+--------+
| result |
+--------+
|      4 |
+--------+
1 row in set (0.114 sec)

MariaDB [testingdb]> select ceil(19.9) as result;
+--------+
| result |
+--------+
|     20 |
+--------+
1 row in set (0.048 sec)

MariaDB [testingdb]> select floor(19.9) as result;
+--------+
| result |
+--------+
|     19 |
+--------+
1 row in set (0.011 sec)

MariaDB [testingdb]> select round(19.9) as result;
+--------+
| result |
+--------+
|     20 |
+--------+
1 row in set (0.028 sec)

MariaDB [testingdb]> select mod(19,9) as result;
+--------+
| result |
+--------+
|      1 |
+--------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select exp(2) as result;
+------------------+
| result           |
+------------------+
| 7.38905609893065 |
+------------------+
1 row in set (0.081 sec)

MariaDB [testingdb]> select pow(2,2) as result;
+--------+
| result |
+--------+
|      4 |
+--------+
1 row in set (0.002 sec)

MariaDB [testingdb]> select sqrt(2) as result;
+--------------------+
| result             |
+--------------------+
| 1.4142135623730951 |
+--------------------+
1 row in set (0.000 sec)
</pre>

<b>AGGREGATE FUNCTION</b><br>
1)count: counts the record except the NULL records.<br>
count(*) : counts everything including NULL records too.<br>
2)sum : return addition.<br>
3)avg : return average.<br>
4)min : return minimum<br> 
5)max : return maximin<br>

<pre>
MariaDB [testingdb]> select COUNT(name) as total_records from emp2;
+---------------+
| total_records |
+---------------+
|             3 |
+---------------+
1 row in set (0.128 sec)

MariaDB [testingdb]> select SUM(salary) as total_records from emp2;
+---------------+
| total_records |
+---------------+
|        144000 |
+---------------+
1 row in set (0.035 sec)

MariaDB [testingdb]> select AVG(salary) as total_records from emp2;
+---------------+
| total_records |
+---------------+
|         48000 |
+---------------+
1 row in set (0.001 sec)

MariaDB [testingdb]> select MIN(salary) as total_records from emp2;
+---------------+
| total_records |
+---------------+
|         34000 |
+---------------+
1 row in set (0.039 sec)

MariaDB [testingdb]> select MAX(salary) as total_records from emp2;
+---------------+
| total_records |
+---------------+
|         60000 |
+---------------+
1 row in set (0.001 sec)

</pre>


<b>DATE</b><br>
curdate()<br>
now()<br>
sysdate()<br>
lastday()<br>
datediff() : it gives total number of days.<br>


<pre>
MariaDB [testingdb]> select curdate() as date;
+------------+
| date       |
+------------+
| 2021-07-06 |
+------------+
1 row in set (0.026 sec)

MariaDB [testingdb]> select now() as date_time;
+---------------------+
| date_time           |
+---------------------+
| 2021-07-06 20:39:23 |
+---------------------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select sysdate() as sys_date_time;
+---------------------+
| sys_date_time       |
+---------------------+
| 2021-07-06 20:39:42 |
+---------------------+
1 row in set (0.086 sec)
</pre>

Example:<br>
<pre>
MariaDB [testingdb]> create table emp3(name varchar(20), purchase_datetime datetime);
Query OK, 0 rows affected (1.098 sec)

MariaDB [testingdb]> insert into emp3(name, purchase_datetime) values("fareen",now());
Query OK, 1 row affected (0.063 sec)

MariaDB [testingdb]> select * from emp3;
+--------+---------------------+
| name   | purchase_datetime   |
+--------+---------------------+
| fareen | 2021-07-06 20:45:43 |
+--------+---------------------+
1 row in set (0.001 sec)

MariaDB [testingdb]> insert into emp3(name, purchase_datetime) values("fareen",curdate());
Query OK, 1 row affected (0.110 sec)

MariaDB [testingdb]> select * from emp3;
+--------+---------------------+
| name   | purchase_datetime   |
+--------+---------------------+
| fareen | 2021-07-06 20:45:43 |
| fareen | 2021-07-06 00:00:00 |
+--------+---------------------+
2 rows in set (0.001 sec)

MariaDB [testingdb]> select last_day('2021-05-02') as last_date;
+------------+
| last_date  |
+------------+
| 2021-05-31 |
+------------+
1 row in set (0.040 sec)

MariaDB [testingdb]> select last_day(curdate()) as last_date;
+------------+
| last_date  |
+------------+
| 2021-07-31 |
+------------+
1 row in set (0.001 sec)
//last date of this month is 31st.

MariaDB [testingdb]> select datediff('2021-07-02','2020-08-04') as diff;
+------+
| diff |
+------+
|  332 |
+------+
1 row in set (0.057 sec)
</pre>

EXTRACT YEAR, MONTH, DAY, HOUR<br>
<pre>
MariaDB [testingdb]> select year('2021-07-06') as year;
+------+
| year |
+------+
| 2021 |
+------+
1 row in set (0.001 sec)

MariaDB [testingdb]> select year(now()) as year;
+------+
| year |
+------+
| 2021 |
+------+
1 row in set (0.001 sec)

MariaDB [testingdb]> select month(now()) as year;
+------+
| year |
+------+
|    7 |
+------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select day(now()) as year;
+------+
| year |
+------+
|    6 |
+------+
1 row in set (0.001 sec)

MariaDB [testingdb]> select hour(now()) as year;
+------+
| year |
+------+
|   20 |
+------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select minute(now()) as year;
+------+
| year |
+------+
|   59 |
+------+
1 row in set (0.000 sec)

MariaDB [testingdb]> select second(now()) as year;
+------+
| year |
+------+
|    5 |
+------+
1 row in set (0.001 sec)
</pre>

CHANGING THE DATE FORMAT<br>
use function:<br>
date_format(date,format);<br>
%j - day
%M - month in full words(as in September)<br>
%d - date<br>
%Y - year(in fout digit)<br>
%y - year(only last two digit)<br>
Example<br>
<pre>
MariaDB [testingdb]> select date_format('2021-07-06','%d %M %Y') as new_format;
+--------------+
| new_format   |
+--------------+
| 06 July 2021 |
+--------------+
1 row in set (0.104 sec)

MariaDB [testingdb]> select date_format('2021-07-06','%d-%M-%Y') as new_format;
+--------------+
| new_format   |
+--------------+
| 06-July-2021 |
+--------------+
1 row in set (0.011 sec)
</pre>

<b>GROUP BY vs HAVING CLAUSE</b>
GROUP BY<br>
Example: to group the employee by dept.<br>
It automatically sort in ascending, to do in descending use >select * from emp group by dept desc;<br>
<pre>
MariaDB [emptbl]> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | ename  | job       | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
14 rows in set (0.000 sec)

MariaDB [emptbl]> select job,count(empno) as total_emp from emp group by job;
+-----------+-----------+
| job       | total_emp |
+-----------+-----------+
| ANALYST   |         2 |
| CLERK     |         4 |
| MANAGER   |         3 |
| PRESIDENT |         1 |
| SALESMAN  |         4 |
+-----------+-----------+
5 rows in set (0.001 sec)

MariaDB [emptbl]> select job,count(empno) as total_emp from emp group by job having count(empno)>3;
+----------+-----------+
| job      | total_emp |
+----------+-----------+
| CLERK    |         4 |
| SALESMAN |         4 |
+----------+-----------+
2 rows in set (0.001 sec)

where clause is not allowed with group by:
MariaDB [emptbl]> select job,count(empno) as total_emp from emp group by job where count(empno)>3;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'where count(empno)>3' at line 1

</pre>
<b>SUB-QURIES</b>
Sub-queries execute from inner to outer except correlated query.
1)Single row sub-query: which is returning the single record/row/tuple.<br>
2)Multi-row sub-query: which is returning the multiplt row.
Example<br>

<pre>
1)

Question 1)Find the name of the employee having the highest salary in the table<br>
MariaDB [emptbl]> select * from emp where sal=(select max(sal) from emp);
+-------+-------+-----------+------+------------+---------+------+--------+
| empno | ename | job       | mgr  | hiredate   | sal     | comm | deptno |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
+-------+-------+-----------+------+------------+---------+------+--------+
1 row in set (0.001 sec)

Question 2)Find bunch of salary exculding highest salary.
MariaDB [emptbl]> select max(sal) from emp where sal!=(select max(sal) from emp);
+----------+
| max(sal) |
+----------+
|  3000.00 |
+----------+
1 row in set (0.001 sec)

Here :
step one is :
MariaDB [emptbl]> select max(sal) from emp;
+----------+
| max(sal) |
+----------+
|  5000.00 |
+----------+
1 row in set (0.000 sec)

step two is :
select max(sal) from emp where sal!=(select max(sal) from emp);

MariaDB [emptbl]> select * from emp where sal=(select max(sal) from emp where sal!=(select max(sal) from emp));
+-------+-------+---------+------+------------+---------+------+--------+
| empno | ename | job     | mgr  | hiredate   | sal     | comm | deptno |
+-------+-------+---------+------+------------+---------+------+--------+
|  7788 | SCOTT | ANALYST | 7566 | 1982-12-09 | 3000.00 | NULL |     20 |
|  7902 | FORD  | ANALYST | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+-------+---------+------+------------+---------+------+--------+
2 rows in set (0.037 sec)

QUESTION 3: Find the emp having salary less than avg salary 
MariaDB [emptbl]> select * from emp where sal<(select avg(sal) from emp);
+-------+--------+----------+------+------------+---------+---------+--------+
| empno | ename  | job      | mgr  | hiredate   | sal     | comm    | deptno |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK    | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7934 | MILLER | CLERK    | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+----------+------+------------+---------+---------+--------+
8 rows in set (0.014 sec)

MariaDB [emptbl]> select avg(sal) from emp;
+-------------+
| avg(sal)    |
+-------------+
| 2073.214286 |
+-------------+
1 row in set (0.001 sec)

2)Multiple 
MariaDB [emptbl]> select job,avg(sal) from emp group by job;
+-----------+-------------+
| job       | avg(sal)    |
+-----------+-------------+
| ANALYST   | 3000.000000 |
| CLERK     | 1037.500000 |
| MANAGER   | 2758.333333 |
| PRESIDENT | 5000.000000 |
| SALESMAN  | 1400.000000 |
+-----------+-------------+
5 rows in set (0.044 sec)

MariaDB [emptbl]> select * from emp where sal IN (select avg(sal) from emp group by job);
+-------+-------+-----------+------+------------+---------+------+--------+
| empno | ename | job       | mgr  | hiredate   | sal     | comm | deptno |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7788 | SCOTT | ANALYST   | 7566 | 1982-12-09 | 3000.00 | NULL |     20 |
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
|  7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+-------+-----------+------+------------+---------+------+--------+
3 rows in set (0.169 sec)
</pre>


<b>ANY & ALL</b><br>
![anyandall](https://user-images.githubusercontent.com/59610617/124790817-1f065180-df69-11eb-99ca-cc6d0af8a104.png)

<pre>

</pre>




<b>ER</b><br>
1)ONE to ONE<br>
![onetoone](https://user-images.githubusercontent.com/59610617/124769672-481de680-df57-11eb-9703-34a9687e81b4.png)

2)ON TO MANY
![onetomany](https://user-images.githubusercontent.com/59610617/124769707-510eb800-df57-11eb-8d4c-87bbb9991ffb.png)

3)Many to One

4)Many to Many
![manytomany](https://user-images.githubusercontent.com/59610617/124769864-756a9480-df57-11eb-801c-b04ec0ada21c.png)

<b>JOINS</b><br>
Need of joins:<br>
If we need to fetch the information or data between two or more table, we use join.<br>
Two or more tables can be joined if:<br>
1)There should be a common column between tables with name and datatype.<br>
2)If different names, then at least they should same in datatype.<br>
JOIN=cartesion product + condition<br>

<pre>
EMP AND DEPT TABLE:
MariaDB [emptbl]> select * from customer;
+-----+--------+--------+----------+
| eid | name   | salary | location |
+-----+--------+--------+----------+
|   1 | Mac    |  30000 | Mumbai   |
|   2 | Fareen |  20000 | Boston   |
|   3 | Roma   |  50000 | NULL     |
|   4 | Giya   |  70000 | Boston   |
+-----+--------+--------+----------+
4 rows in set (0.001 sec)

MariaDB [emptbl]> select * from dept_location;
+-----+--------+-------+
| eid | deptid | loc   |
+-----+--------+-------+
|   1 | D1     | Thane |
|   2 | D2     | USA   |
|   3 | NULL   | China |
+-----+--------+-------+
3 rows in set (0.001 sec)
</pre>

1)Cross join<br>
syntax: r X x<br>
example:select * from emp CROSS JOIN dept;<br>
<pre>
MariaDB [emptbl]> select * from customer CROSS JOIN dept_location;
+-----+--------+--------+----------+-----+--------+-------+
| eid | name   | salary | location | eid | deptid | loc   |
+-----+--------+--------+----------+-----+--------+-------+
|   1 | Mac    |  30000 | Mumbai   |   1 | D1     | Thane |
|   1 | Mac    |  30000 | Mumbai   |   2 | D2     | USA   |
|   1 | Mac    |  30000 | Mumbai   |   3 | NULL   | China |
|   2 | Fareen |  20000 | Boston   |   1 | D1     | Thane |
|   2 | Fareen |  20000 | Boston   |   2 | D2     | USA   |
|   2 | Fareen |  20000 | Boston   |   3 | NULL   | China |
|   3 | Roma   |  50000 | NULL     |   1 | D1     | Thane |
|   3 | Roma   |  50000 | NULL     |   2 | D2     | USA   |
|   3 | Roma   |  50000 | NULL     |   3 | NULL   | China |
|   4 | Giya   |  70000 | Boston   |   1 | D1     | Thane |
|   4 | Giya   |  70000 | Boston   |   2 | D2     | USA   |
|   4 | Giya   |  70000 | Boston   |   3 | NULL   | China |
+-----+--------+--------+----------+-----+--------+-------+
12 rows in set (0.001 sec)
</pre>

2)Inner join: this gives rows from both the table that satisfy the given condition.<br>
<pre>
emp.eid=dept.eid
select * from emp,dept where emp.eid=dept.eid;
select * from emp INNER JOIN dept on(emp.eid=dept.eid);
select * from emp INNER JOIN dept using(eid);
select * from emp INNER JOIN dept using(eid) where salary>6000;
select * from emp INNER JOIN dept using(eid) orderby salary;

MariaDB [emptbl]> select * from customer,dept_location where customer.eid=dept_location.eid;
+-----+--------+--------+----------+-----+--------+-------+
| eid | name   | salary | location | eid | deptid | loc   |
+-----+--------+--------+----------+-----+--------+-------+
|   1 | Mac    |  30000 | Mumbai   |   1 | D1     | Thane |
|   2 | Fareen |  20000 | Boston   |   2 | D2     | USA   |
|   3 | Roma   |  50000 | NULL     |   3 | NULL   | China |
+-----+--------+--------+----------+-----+--------+-------+
3 rows in set (0.002 sec)

MariaDB [emptbl]> select * from customer INNER JOIN dept_location on(customer.eid=dept_location.eid);
+-----+--------+--------+----------+-----+--------+-------+
| eid | name   | salary | location | eid | deptid | loc   |
+-----+--------+--------+----------+-----+--------+-------+
|   1 | Mac    |  30000 | Mumbai   |   1 | D1     | Thane |
|   2 | Fareen |  20000 | Boston   |   2 | D2     | USA   |
|   3 | Roma   |  50000 | NULL     |   3 | NULL   | China |
+-----+--------+--------+----------+-----+--------+-------+
3 rows in set (0.001 sec)

MariaDB [emptbl]> select * from customer INNER JOIN dept_location using(eid) order by salary;
+-----+--------+--------+----------+--------+-------+
| eid | name   | salary | location | deptid | loc   |
+-----+--------+--------+----------+--------+-------+
|   2 | Fareen |  20000 | Boston   | D2     | USA   |
|   1 | Mac    |  30000 | Mumbai   | D1     | Thane |
|   3 | Roma   |  50000 | NULL     | NULL   | China |
+-----+--------+--------+----------+--------+-------+
3 rows in set (0.107 sec)


Question 1)Check where emp assigned with dept. Chcek its city and loc are same or not
MariaDB [emptbl]> select * from customer INNER JOIN dept_location on(customer.eid=dept_location.eid) and location=loc;
Empty set (0.045 sec)
</pre>


2)Left join: this join also give all rows from both the table that satisfy the given condn and along with that it gives all the rows from left of the table that is not satisfying the given condn.<br>
<pre>
here customer become left table dept_location become the right tbl.

MariaDB [emptbl]> select * from customer LEFT JOIN dept_location on(customer.eid=dept_location.eid);
+-----+--------+--------+----------+------+--------+-------+
| eid | name   | salary | location | eid  | deptid | loc   |
+-----+--------+--------+----------+------+--------+-------+
|   1 | Mac    |  30000 | Mumbai   |    1 | D1     | Thane |
|   2 | Fareen |  20000 | Boston   |    2 | D2     | USA   |
|   3 | Roma   |  50000 | NULL     |    3 | NULL   | China |
|   4 | Giya   |  70000 | Boston   | NULL | NULL   | NULL  |
+-----+--------+--------+----------+------+--------+-------+
4 rows in set (0.015 sec)

On reverse:
MariaDB [emptbl]> select * from dept_location LEFT JOIN customer on(customer.eid=dept_location.eid);
+-----+--------+-------+------+--------+--------+----------+
| eid | deptid | loc   | eid  | name   | salary | location |
+-----+--------+-------+------+--------+--------+----------+
|   1 | D1     | Thane |    1 | Mac    |  30000 | Mumbai   |
|   2 | D2     | USA   |    2 | Fareen |  20000 | Boston   |
|   3 | NULL   | China |    3 | Roma   |  50000 | NULL     |
+-----+--------+-------+------+--------+--------+----------+
3 rows in set (0.001 sec)
</pre>

3)Right join<br>
<pre>
MariaDB [emptbl]> select * from dept_location RIGHT JOIN customer on(customer.eid=dept_location.eid);
+------+--------+-------+-----+--------+--------+----------+
| eid  | deptid | loc   | eid | name   | salary | location |
+------+--------+-------+-----+--------+--------+----------+
|    1 | D1     | Thane |   1 | Mac    |  30000 | Mumbai   |
|    2 | D2     | USA   |   2 | Fareen |  20000 | Boston   |
|    3 | NULL   | China |   3 | Roma   |  50000 | NULL     |
| NULL | NULL   | NULL  |   4 | Giya   |  70000 | Boston   |
+------+--------+-------+-----+--------+--------+----------+
4 rows in set (0.001 sec)
</pre>

Removing ambiguity<br>
<pre>
MariaDB [emptbl]> select eid,name from customer INNER JOIN dept_location on(customer.eid=dept_location.eid);
ERROR 1052 (23000): Column 'eid' in field list is ambiguous
MariaDB [emptbl]> select customer.eid,name from customer INNER JOIN dept_location on(customer.eid=dept_location.eid);
+-----+--------+
| eid | name   |
+-----+--------+
|   1 | Mac    |
|   2 | Fareen |
|   3 | Roma   |
+-----+--------+
3 rows in set (0.013 sec)
</pre>

Table aliasing <br>
<pre>
MariaDB [emptbl]> select c.eid,name from customer c INNER JOIN dept_location d on(c.eid=d.eid);
+-----+--------+
| eid | name   |
+-----+--------+
|   1 | Mac    |
|   2 | Fareen |
|   3 | Roma   |
+-----+--------+
3 rows in set (0.002 sec)
</pre>





























































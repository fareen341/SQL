<b>COMMANDS IN MYSQL</b><br>
Primary Key:
student table

Foreign key:<br>
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

Updating:
<pre>
MariaDB [testingdb]> update student set id=4 where id=2;
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

<b>DISTINCT FUNCTION</b><br>
It won't allow the repeated records.
Exammple<br>
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



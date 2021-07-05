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



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



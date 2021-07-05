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


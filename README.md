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



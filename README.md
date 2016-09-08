Objective: To implement various Data Contraints on the schema values.

Theory: The SQL DATA CONSTRAINTS are an integrity which defines some conditions that restricts the column to remain true while inserting or updating or deleting data in the column. Constraints can be specified when the table created first with CREATE TABLE statement or at the time of modification of structure of an existing table with ALTER TABLE statement.

NOT NULL: This constraint confirms that a column cannot store NULL value.
UNIQUE: This constraint ensures that each rows for a column must have different value.
PRIMARY KEY: This constraint is a combination of  a NOT NULL constraint and a UNIQUE constraint. This constraint ensures that the specific column or combination of two or more columns for a table have an unique identity which helps to find a particular record in a table more easily and quickly.
CHECK: A check constraint ensures that  the value stored in a column meets a specific condition.
DEFAULT: This constraint provides a default value when specified none for this column.
FOREIGN KEY: A foreign key constraint is used to ensure the referential integrity of the data. in one table to match values in another table.


Question 1: Alter table to make phone no. column unique.

SQL> alter table empcsa1 modify phnno constraint Phn_Uniq unique;

Table altered.

Question 2: Ensure that Dname column does not have NULL value.

SQL> alter table dept  modify dname constraint Ntnl_dname not null;

Table altered.

Question 3: Set Default value of Designation as ‘Clerk’.

SQL> alter table empcsa1 modify designation default 'Clerk';

Table altered.

Question 4: The value of Salary must be greater than 5000.

SQL> alter table empcsa1 add constraint Chk_salary check(salary>5000);

Table altered.

Question 5: Drop Foreign Key Constraint.

SQL> alter table empcsa1 drop constraint Fgn_dno;

Table altered.

Question 6: Commission column can accept NULL values.

SQL> alter table empcsa1 modify commission number(7,3) default(0.00);

Table altered.

Question 7: Ensure that commission column must not be NULL.

SQL> alter table emp_csa1 modify commission number(7,3) not null;

Table altered.

Question 8: Drop Check and Default Constraints.

SQL> alter table empcsa1 drop constraint Chk_salary;

Table altered.	

Question 9: Delete a tuple from Dept table which is being replaced by Emp.

SQL> alter table empcsa1 add constraint Fgn_dno foreign key(Dno) references Dept(Dnumber) on delete cascade;

Table altered.

SQL> delete from dept where dnumber=10;

1 row deleted.



Errors:

1. SQL> delete from dept where dnumber=14;
delete from dept where dnumber=14
*
ERROR at line 1:
ORA-02292: integrity constraint (CSUSER5.FGN_DNO) violated - child record
found
	
ERROR at line 1:
ORA-02298: cannot validate (CSUSER5.FGN_DNO) - parent keys not found
	
Explanation: Data from Parent table cannot be deleted simply, if any child table has a foreign key referencing to the Parent table’s primary key. This is known as Referential Integrity Constraint. Hence, ON CASCASDE DELETE can be used to delete such values, which will also delete corresponding entries in child table.

2. SQL> alter table empcsa1 drop default;
alter table empcsa1 drop default 
                       *
ERROR at line 1:
ORA-00905: missing keyword

3. SQL> alter table empcsa1 add salary constraint Chk_salary check(salary>5000);
alter table empcsa1 add salary constraint Chk_salary check(salary>5000)
			      *
ERROR at line 1:
ORA-02263: need to specify the datatype for this column

Explanation: To apply CHECK constraint, name of the column is given inside the parenthesis with the condition, it is not specified outside it.

4. SQL> alter table empcsa1  modify designation constraint Def_designation default 'Clerk';
alter table empcsa1  modify designation constraint Def_designation default 'Clerk'
                                        *
ERROR at line 1:
ORA-02253: constraint specification not allowed here

5. SQL> alter table emp_csa1 modify commission number(7,3) not null;
alter table emp_csa1 modify commission number(7,3) not null
*
ERROR at line 1:
ORA-02296: cannot enable (CSUSER5.) - null values found
	
Explanation: As there are already null values present in the column, hence NULL constraint cannot be applied later. Either the tuples having null values should be deleted, all whole table has to be dropped.

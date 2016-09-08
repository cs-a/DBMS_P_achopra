heroku-postgres-40e986c1::PUCE=> create table employee (emp_name varchar(200),street varchar(100),city varchar(100));

heroku-postgres-40e986c1::PUCE=> create table ft_works (emp_name varchar(200),branch_name varchar(200),salary Integer);

insert into employee values ('Coyote','Toon','Hollywood');
insert into employee values ('Rabbit','Tunnel','Carrotville');
insert into employee values ('Smith','Revolver','Death Valley');
insert into employee values ('Williams','Seaview','Seattle');

insert into ft_works values ('Coyote','Mesa',1500);
insert into ft_works values ('Rabbit','Mesa',1300);
insert into ft_works values ('Gates','Redmond',5300);
insert into ft_works values ('Williams','Redmond',1500);

**JOIN**


CROSS JOIN

SQL: heroku-postgres-40e986c1::PUCE=> select * from employee,ft_works;
 emp_name |  street  |     city     | emp_name | branch_name | salary 
----------+----------+--------------+----------+-------------+--------
 Coyote   | Toon     | Hollywood    | Coyote   | Mesa        |   1500
 Coyote   | Toon     | Hollywood    | Rabbit   | Mesa        |   1300
 Coyote   | Toon     | Hollywood    | Gates    | Redmond     |   5300
 Coyote   | Toon     | Hollywood    | Williams | Redmond     |   1500
 Rabbit   | Tunnel   | Carrotville  | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel   | Carrotville  | Rabbit   | Mesa        |   1300
 Rabbit   | Tunnel   | Carrotville  | Gates    | Redmond     |   5300
 Rabbit   | Tunnel   | Carrotville  | Williams | Redmond     |   1500
 Smith    | Revolver | Death Valley | Coyote   | Mesa        |   1500
 Smith    | Revolver | Death Valley | Rabbit   | Mesa        |   1300
 Smith    | Revolver | Death Valley | Gates    | Redmond     |   5300
 Smith    | Revolver | Death Valley | Williams | Redmond     |   1500
 Williams | Seaview  | Seattle      | Coyote   | Mesa        |   1500
 Williams | Seaview  | Seattle      | Rabbit   | Mesa        |   1300
 Williams | Seaview  | Seattle      | Gates    | Redmond     |   5300
 Williams | Seaview  | Seattle      | Williams | Redmond     |   1500
(16 rows)


JOIN: heroku-postgres-40e986c1::PUCE=> select * from employee CROSS JOIN ft_works;

 emp_name |  street  |     city     | emp_name | branch_name | salary 
----------+----------+--------------+----------+-------------+--------
 Coyote   | Toon     | Hollywood    | Coyote   | Mesa        |   1500
 Coyote   | Toon     | Hollywood    | Rabbit   | Mesa        |   1300
 Coyote   | Toon     | Hollywood    | Gates    | Redmond     |   5300
 Coyote   | Toon     | Hollywood    | Williams | Redmond     |   1500
 Rabbit   | Tunnel   | Carrotville  | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel   | Carrotville  | Rabbit   | Mesa        |   1300
 Rabbit   | Tunnel   | Carrotville  | Gates    | Redmond     |   5300
 Rabbit   | Tunnel   | Carrotville  | Williams | Redmond     |   1500
 Smith    | Revolver | Death Valley | Coyote   | Mesa        |   1500
 Smith    | Revolver | Death Valley | Rabbit   | Mesa        |   1300
 Smith    | Revolver | Death Valley | Gates    | Redmond     |   5300
 Smith    | Revolver | Death Valley | Williams | Redmond     |   1500
 Williams | Seaview  | Seattle      | Coyote   | Mesa        |   1500
 Williams | Seaview  | Seattle      | Rabbit   | Mesa        |   1300
 Williams | Seaview  | Seattle      | Gates    | Redmond     |   5300
 Williams | Seaview  | Seattle      | Williams | Redmond     |   1500
(16 rows)

NATURAL JOIN

JOIN: heroku-postgres-40e986c1::PUCE=> select * from employee NATURAL JOIN ft_works;
 emp_name | street  |    city     | branch_name | salary 
----------+---------+-------------+-------------+--------
 Coyote   | Toon    | Hollywood   | Mesa        |   1500
 Rabbit   | Tunnel  | Carrotville | Mesa        |   1300
 Williams | Seaview | Seattle     | Redmond     |   1500
(3 rows)

SQL: heroku-postgres-40e986c1::PUCE=> select * from employee,ft_works where employee.emp_name=ft_works.emp_name;
 emp_name | street  |    city     | emp_name | branch_name | salary 
----------+---------+-------------+----------+-------------+--------
 Coyote   | Toon    | Hollywood   | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel  | Carrotville | Rabbit   | Mesa        |   1300
 Williams | Seaview | Seattle     | Williams | Redmond     |   1500
(3 rows)


INNER JOIN:

JOIN: heroku-postgres-40e986c1::PUCE=> select * from employee INNER JOIN ft_works ON employee.emp_name=ft_works.emp_name;
 emp_name | street  |    city     | emp_name | branch_name | salary 
----------+---------+-------------+----------+-------------+--------
 Coyote   | Toon    | Hollywood   | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel  | Carrotville | Rabbit   | Mesa        |   1300
 Williams | Seaview | Seattle     | Williams | Redmond     |   1500
(3 rows)

experiment:
heroku-postgres-40e986c1::PUCE=> select * from employee INNER JOIN ft_works ON ft_works.salary>1300 AND employee.emp_name=ft_works.emp_name;
 emp_name | street  |   city    | emp_name | branch_name | salary 
----------+---------+-----------+----------+-------------+--------
 Coyote   | Toon    | Hollywood | Coyote   | Mesa        |   1500
 Williams | Seaview | Seattle   | Williams | Redmond     |   1500
(2 rows)

LEFT OUTER JOIN :

JOIN: heroku-postgres-40e986c1::PUCE=> select * from employee LEFT OUTER JOIN ft_works
heroku-postgres-40e986c1::PUCE-> ON employee.emp_name=ft_works.emp_name;
 emp_name |  street  |     city     | emp_name | branch_name | salary 
----------+----------+--------------+----------+-------------+--------
 Coyote   | Toon     | Hollywood    | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel   | Carrotville  | Rabbit   | Mesa        |   1300
 Smith    | Revolver | Death Valley |          |             |       
 Williams | Seaview  | Seattle      | Williams | Redmond     |   1500
(4 rows)

RIGHT OUTER JOIN:

JOIN: heroku-postgres-40e986c1::PUCE=> select * from employee RIGHT OUTER JOIN ft_works
ON employee.emp_name=ft_works.emp_name;
 emp_name | street  |    city     | emp_name | branch_name | salary 
----------+---------+-------------+----------+-------------+--------
 Coyote   | Toon    | Hollywood   | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel  | Carrotville | Rabbit   | Mesa        |   1300
          |         |             | Gates    | Redmond     |   5300
 Williams | Seaview | Seattle     | Williams | Redmond     |   1500
(4 rows)

FULL OUTER JOIN:

heroku-postgres-40e986c1::PUCE=> select * from employee FULL OUTER JOIN ft_works
ON employee.emp_name=ft_works.emp_name;
 emp_name |  street  |     city     | emp_name | branch_name | salary 
----------+----------+--------------+----------+-------------+--------
 Coyote   | Toon     | Hollywood    | Coyote   | Mesa        |   1500
 Rabbit   | Tunnel   | Carrotville  | Rabbit   | Mesa        |   1300
 Smith    | Revolver | Death Valley |          |             |       
 Williams | Seaview  | Seattle      | Williams | Redmond     |   1500
          |          |              | Gates    | Redmond     |   5300
(5 rows)


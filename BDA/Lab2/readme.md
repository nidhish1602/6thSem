# Lab 2 (Cassandra)

## Create an employee information database 

```ruby 
cqlsh> create keyspace employee_info with
replication={'class':'SimpleStrategy','replication_factor':1};
```

```ruby 
cqlsh> use employee_info;
```

```ruby 
cqlsh:employee_info> create table employee_details(emp_id int,emp_name
                 ... text,designation text,doj timestamp,salary double,dept_name text,primary
                 ... key(emp_id,salary));

```

```ruby 
cqlsh:employee_info> begin batch
                 ... ... insert into
                 ... employee_details(emp_id,emp_name,designation,doj,salary,dept_name) values
                 ... (100,'tanya','manager','2020-09-11',30000,'testing')
                 ... insert into
                 ... employee_details(emp_id,emp_name,designation,doj,salary,dept_name) values
                 ... (111,'sakshi','associate','2020-06-11',25000,'development')
                 ... insert into
                 ... employee_details(emp_id,emp_name,designation,doj,salary,dept_name) values
                 ... (121,'hitesh','manager','2020-01-03',35000,'hr') 
                 ... apply batch;
```

```ruby 
cqlsh:employee_info> select * from employee_details;

 emp_id | salary | dept_name   | designation | doj                             | emp_name
--------+--------+-------------+-------------+---------------------------------+----------
    111 |  25000 | development |   associate | 2020-06-10 18:30:00.000000+0000 |   sakshi
    121 |  35000 |          hr |     manager | 2020-01-02 18:30:00.000000+0000 |   hitesh
    100 |  30000 |     testing |     manager | 2020-09-10 18:30:00.000000+0000 |    tanya

```

```ruby 
cqlsh:employee_info> update employee_details set emp_name='sharan' where emp_id=121 and salary=35000;
cqlsh:employee_info> select * from employee_details;

 emp_id | salary | dept_name   | designation | doj                             | emp_name
--------+--------+-------------+-------------+---------------------------------+----------
    111 |  25000 | development |   associate | 2020-06-10 18:30:00.000000+0000 |   sakshi
    121 |  35000 |          hr |     manager | 2020-01-02 18:30:00.000000+0000 |   sharan
    100 |  30000 |     testing |     manager | 2020-09-10 18:30:00.000000+0000 |    tanya

```

```ruby 
cqlsh:employee_info> alter table employee_details add project text;
cqlsh:employee_info> update employee_details set project='chat app' where
                 ... emp_id=111 and salary=25000;
cqlsh:employee_info> update employee_details set project='campusx' where
                 ... emp_id=121 and salary=35000;
cqlsh:employee_info> update employee_details set project='canteen app' where
                 ... emp_id=100 and salary=30000;
cqlsh:employee_info> select * from employee_details;

 emp_id | salary | dept_name   | designation | doj                             | emp_name | project
--------+--------+-------------+-------------+---------------------------------+----------+-------------
    111 |  25000 | development |   associate | 2020-06-10 18:30:00.000000+0000 |   sakshi |    chat app
    121 |  35000 |          hr |     manager | 2020-01-02 18:30:00.000000+0000 |   sharan |     campusx
    100 |  30000 |     testing |     manager | 2020-09-10 18:30:00.000000+0000 |    tanya | canteen app

```

```ruby 
cqlsh:employee_info> insert into employee_details(emp_id,emp_name,designation,doj,salary,dept_name)
                 ... values(113,'harsha','manager','2020-09-09',30000,'testing') using ttl 30;   
cqlsh:employee_info> select ttl(emp_name) from employee_details where
                 ... emp_id=113 and salary=30000;

 ttl(emp_name)
---------------
            23

```

```ruby 
cqlsh:employee_info> select * from employee_details;

 emp_id | salary | dept_name   | designation | doj                             | emp_name | project
--------+--------+-------------+-------------+---------------------------------+----------+-------------
    111 |  25000 | development |   associate | 2020-06-10 18:30:00.000000+0000 |   sakshi |    chat app
    113 |  30000 |     testing |     manager | 2020-09-08 18:30:00.000000+0000 |   harsha |        null
    121 |  35000 |          hr |     manager | 2020-01-02 18:30:00.000000+0000 |   sharan |     campusx
    100 |  30000 |     testing |     manager | 2020-09-10 18:30:00.000000+0000 |    tanya | canteen app

```

```ruby 
cqlsh:employee_info> select * from employee_details;

 emp_id | salary | dept_name   | designation | doj                             | emp_name | project
--------+--------+-------------+-------------+---------------------------------+----------+-------------
    111 |  25000 | development |   associate | 2020-06-10 18:30:00.000000+0000 |   sakshi |    chat app
    113 |  30000 |     testing |     manager | 2020-09-08 18:30:00.000000+0000 |   harsha |        null
    121 |  35000 |          hr |     manager | 2020-01-02 18:30:00.000000+0000 |   sharan |     campusx
    100 |  30000 |     testing |     manager | 2020-09-10 18:30:00.000000+0000 |    tanya | canteen app

```

```ruby 
cqlsh:employee_info> paging off;
Disabled Query paging.
cqlsh:employee_info> select * from employee_details where emp_id in
                 ... (111,121,100) order by salary;

 emp_id | salary | dept_name   | designation | doj                             | emp_name | project
--------+--------+-------------+-------------+---------------------------------+----------+-------------
    111 |  25000 | development |   associate | 2020-06-10 18:30:00.000000+0000 |   sakshi |    chat app
    100 |  30000 |     testing |     manager | 2020-09-10 18:30:00.000000+0000 |    tanya | canteen app
    121 |  35000 |          hr |     manager | 2020-01-02 18:30:00.000000+0000 |   sharan |     campusx

```
